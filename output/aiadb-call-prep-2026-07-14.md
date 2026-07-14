# AIADB Data Flow — Call Prep (14 Jul 26)

- **Notion page:** https://app.notion.com/p/39d7a5e7c4ee8137baf4ea419ce80e72

Compiled from the AIADB documents already in Notion (Elastic approach, MoM sudhir KT 08/07/26, AVI Setup for LLDS, Elasticsearch Architecture, Logstash, Low Latency Data) ahead of tonight's 8:00pm Elastic SME call.

## 1. Data Flow (end-to-end)

**Source (Kafka / files / DB / HTTP) → Logstash → Elasticsearch / LLDS / Vector DB → Kibana**

- **Source systems:** primarily Kafka topics; messages often serialized as Avro/JSON via a Schema Registry. Files, databases, and HTTP endpoints are also supported inputs.
- **Logstash** follows an **Input → Filter → Output** model:
  - *Input* — consumes from Kafka (or other sources); SSL-secured via keystore/truststore; consumer group IDs track offsets for reliable consumption.
  - *Filter* — lightweight enrichment/transformation (timestamps, field normalization, conditional logic) to standardize events before they're indexed.
  - *Output* — writes into Elasticsearch indices, SSL-secured; index naming aligned to the data domain/use case.
- **Batch ingestion path:** EDL (OSDS/Pyspark) → LLDS/Vector DB, using Logstash as the pipeline connector. DARE's role is onboarding these Logstash jobs.
- **Streaming ingestion path:** Apache Flink (batch + stream jobs), or Pyspark using the Elasticsearch Spark library.
- **Storage split (clarified 14 Jul by user):**
  - **LLDS** = fast-retrieval store for unstructured data (text blobs, documents) for real-time AIML use cases.
  - **"Vector DB" is not a separate product** — Elasticsearch itself is used as the vector database, via its native vector search (dense_vector fields + kNN) applied to AIML embeddings for semantic/similarity search (LLM/GenAI use cases).
  - So the same Elasticsearch cluster serves two query patterns: standard text/keyword search, and vector/kNN similarity search — not two separate systems.
- **Visualization/management:** Kibana — spaces, dashboards, index/data views, alerts, observability.

## 2. Ingestion Setup Steps (who owns what)

1. Create the Index for the AIML use case in Elasticsearch.
2. Create an AD group with Read/Write access to that index (owned by the Data Product Mgmt team, e.g. Chennu team).
3. Assign the AD group to the ES index (DARE / Elastic Admin does this).
4. Add individual/service accounts that run the ingestion job to that AD group (Data Product Mgmt team).
5. Set up the Logstash/Flink jobs and/or Pyspark jobs (Developer/Data Scientist does this; DARE assists with Pods/Spark setup in OSDS).
6. Deploy the Logstash/Flink jobs, or schedule Pyspark jobs via Autosys (PSG team).

## 3. Infrastructure (Vector DB)

| Env | Nodes | Breakdown |
|-----|-------|-----------|
| Dev | 7 | 1 kibana, 3 master, 1 ML, 2 hot |
| UAT | 9 | 1 kibana, 3 master, 1 ML, 4 hot |
| BCP | 17 | 2 kibana, 3 master, 4 ML, 8 hot |
| Prod | 17 | 2 kibana, 3 master, 4 ML, 8 hot |

Node roles: **Master** (cluster state, index create/delete), **Data** (store + index + search), **Ingest** (transforms inbound data), **ML** (model processing), **Coordinator** (delegates requests, merges search results).

## 4. Deployment Mechanics

- Managed via **UCD**: Import → Deploy → Activate (plus Stop/Start/Cleanup). Import must target the correct environment folder (Dev vs UAT) — configs are environment-specific.
- Logstash config files live at `/opt/apps/esrch/logstash/logstashPipelines/conf.d`, sourced from GitHub (`app-aiadb/aiadb-logstash-configApp`).
- Manual restart: `lsmanage {status|stop|start|restart}` for Logstash; `esmanage restart` for Elastic/Kibana nodes — must `su` to the aiadb service account first.
- **AVI (load balancer)** setup for new environments: create VIPs via the WMS Load Balancer request form (one for the app, one for Kibana), then engage the PE team for metadata.

## 5. Snapshot & Restore — ★ this week's active issue, covered in the 07/08 MoM ★

- **Objective:** set up Elasticsearch snapshot-and-restore via S3-compatible storage (HPOS) for VDB (Dev/UAT/Prod) and LLDS (Dev/UAT). Immediate driver: a pending production cutover change.
- **Current state:** LLDS has a snapshot repo but it's failing ("could not determine repository generation from root blobs", root cause not yet found). VDB has no snapshot/restore policy configured yet — starting from scratch in Dev.
- **Setup steps:** install Elastic S3 plugin → add keystore creds (S3 access/secret key) → apply cert-bypass JVM config + restart cluster → create the S3 snapshot repo (endpoint, bucket, base path) → verify reachability → configure SLM policy (daily 1:30am, all indices, 30-day retention) → test restore on one index → validate over multiple daily cycles.
- **Blockers:** 4 HPOS entitlements pending approval (ping Sanjeev once raised); bucket-creation permission missing (Tanya can help with S3 keys / new bucket); production team bundled VDB + LLDS cutover into one change ticket (ask is to split, LLDS first).
- **Status per Sudhir (14 Jul):** VDB snapshot HPOS integration + UAT sign-off is now done, documented in Confluence — good moment to confirm what changed vs. the MoM's plan and what's still outstanding for Prod.

## 6. Everything above section 5 is NOT from the MoM

The Logstash pipeline mechanics/troubleshooting, Elasticsearch architecture/terminology, AVI/load-balancer setup, the ingestion role-ownership breakdown, and the infrastructure node counts all come from separate KT/architecture docs (Elastic approach, Elasticsearch Architecture, Logstash, Low Latency Data) — not the MoM, which was scoped specifically to the snapshot/restore workstream.

---

## Questions to ask on tonight's call

### A. Daily / weekly / yearly common maintenance tasks
- **What daily checks/tasks does the team own for Elastic/LLDS beyond the new SLM snapshot job (cluster health, DLQ/queue monitoring, Logstash log review)?** *Why: the only daily task confirmed anywhere in the docs is the 1:30am SLM snapshot from the MoM — that's one project's output, not a standing ops checklist. Nothing documents what "normal daily support" looks like once onboarded.*
- **Is there a weekly cadence — index lifecycle management review, capacity/storage checks, patching windows?** *Why: none of the 6 docs mention a weekly rhythm at all, even though ILM and capacity management are standard Elastic operational concerns — unclear if it's informal/ad hoc or a defined process.*
- **Anything yearly — license renewal, major version upgrade cycle, DR/BCP snapshot-restore test, entitlement re-certification?** *Why: there's a dedicated 17-node BCP environment, which implies DR testing obligations, but no cadence or ownership is documented anywhere.*
- **For each of these, who owns it day-to-day vs. who DARE escalates to?** *Why: the docs show a fragmented ownership model (DARE, Data Product Mgmt/Chennu team, PSG for scheduling, PE for AVI) for initial setup — but not who's on the hook for ongoing maintenance once something's live.*

### B. Data-flow clarification (if still unclear)
(pulled directly from the Low Latency Data KT-prep doc, adjusted now that Elasticsearch = the vector DB)
- **What exactly is LLDS in our project — is it a custom store, and what's it backed by?** *Why: docs call it a "fast-retrieval store" but never name the underlying tech — need this to reason about failure modes.*
- **How does data flow end-to-end: Source → Logstash → Elasticsearch (LLDS + vector search)?** *Why: the docs give a high-level model but don't confirm it's exactly this sequence for AIADB specifically — needed to trace an issue to its actual hop.*
- **Which system is the source of truth — LLDS or Elasticsearch?** *Why: if the two ever disagree (a documented failure scenario — "data in LLDS but not in Elasticsearch"), you need to know which one to trust/recover from.*
- **What data goes through the standard text-search path vs. the vector/kNN path?** *Why: same cluster, two query patterns — need the actual routing/use-case split to debug correctly.*
- **When is vector/kNN search used vs. standard Elasticsearch text search?** *Why: rephrased from "VDB vs Elastic" now that they're the same engine — the real question is which query path a given use case takes.*
- **What's the expected latency (ms? seconds?), and what happens downstream if Elasticsearch is slow?** *Why: LLDS is explicitly a low-latency requirement for real-time AIML — need a concrete SLA number and the actual failure/fallback behavior if it's breached.*
