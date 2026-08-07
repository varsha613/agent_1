## Day Summary Header

- **Date:** 2026-08-07 (Friday)
- **Notion page:** https://app.notion.com/p/3b57a5e7c4ee81bda399fad90d9edad5
- **Work windows:** started 7:00 AM IST — earlier than usual, to compensate for hours lost 08/06 (user was away sick that day).
- **Status:** in progress

## Yesterday's Brief (06 Aug 26 — Thursday)

- User corrected 08/06 directly on Notion: Task 3 (Sudhir's cert renewal call) was **3.5h**, not the full 9.0h previously logged. Also did roles setup work and attended recurring meetings that day, hours not split out. Separately mentioned being "away sick" and losing hours on 08/06 — **this doesn't cleanly reconcile with the earlier 9.0h-day confirmation; flagged in `workdone/Aug-26.md` and the weekly sheet, not silently overwritten. Worth confirming 08/06's actual total when there's a moment.**
- **Carried over from 08/06's brain dump:** Deepak asked for a call for updates — **today, 08/07, 10:30 AM IST.**
- **Unconfirmed / rolled forward from 08/06:** Task 1 (roles setup + Deepak email — partially worked 08/06 per the brain dump, not fully closed), Task 2 (parallel-test working instance per 29 Jul MOM), Task 4 (workspace-call recap owed from 08/05).
- **New from today's brain dump:** Prathyusha's ad-hoc AIADB request — test two Logstash pipeline config scripts in UAT (`aiad_ao_event-idpfpcf-analytical.conf`, `aiadb_ao_depm-score-events.conf`), keep UAT index names identical to source, ping her when done so she can verify before production. User has already asked her for a story (Jira ticket).
- Standing lower-priority list still open: 2pm KT call, daily status update, AITAPA tracker update, subnet-error confirmation, Phase-2 review + Timothy McDonald, 07/21 Workspace-call confirmation, D001 Production Changes verification, image build statuses (r4.0.2, r4.0.2-1, Python 3.7), Rathiesh's notebook cross-check, GCP Cloud Spanner (BGNQ-2944), r4.0.2_mrm-2.0 prod release, Lukens Matthew email, Task 6 Elastic follow-up, Task 8 Leela email, both MOMs, BNKC-1642, AO Decision Model Prod work, EPLX KT, Jira Excel compilation.

## Today's Focus

Compensating for yesterday's reduced hours — started 7:00 AM IST. Priority order: (1) prep for Deepak's 10:30 AM call, (2) attend the call, (3) Prathyusha's AIADB UAT request, (4) workspace-call recap still owed, (5) rolled AITAPA items as time allows.

## Tasks (detailed, tabular)

| # | Task | Subtasks | AppID | Status |
|---|------|----------|-------|--------|
| 1 | Prep for Deepak's 10:30 AM call | 1) Finalize AITAPA RBAC roles review — confirm reader-persona GUID (`eab0b77e-...`) provenance, resolve old-principal (`11c8690c-...`) access question, get `terraform init && terraform plan` run if possible. 2) Prepare example pipeline run (Task 2 / 29 Jul MOM checklist): dataset, job, pipeline, package install — resume from the `AuthorizationFailed` datastore error. 3) Write a short, honest status summary for Deepak — resolved vs. still blocked, any decision needed from him. | AITAPA | Not started |
| 2 | Deepak's call — 10:30 AM IST | 1) Attend, walk through roles setup status. 2) Walk through example pipeline run / interim validation results. 3) Capture new action items / decisions from the call. | AITAPA | Not started |
| 3 | Prathyusha's ad-hoc — AIADB Logstash UAT | 1) Get the Jira story from Prathyusha (already requested). 2) Review both conf files: `aiad_ao_event-idpfpcf-analytical.conf`, `aiadb_ao_depm-score-events.conf`. 3) Deploy/test both pipelines in UAT — keep index names identical to source. 4) Verify pipeline behavior in UAT. 5) Ping Prathyusha once done, for her verification. 6) Proceed to production only after her sign-off. | AIADB | Not started |
| 4 | Workspace-call recap (owed from 08/05) | Give the recap so it can finally be logged. | AITAPA | Not started |
| 5 | Rolled forward (lower priority, as time allows) | 2pm KT call, daily status update, AITAPA tracker update, subnet-error confirmation, Phase-2 review + Timothy McDonald, 07/21 Workspace-call confirmation, D001 verification, image build statuses (r4.0.2, r4.0.2-1, Python 3.7), Rathiesh's notebook, GCP Cloud Spanner (BGNQ-2944), r4.0.2_mrm-2.0 prod release, Lukens Matthew email, Task 6 Elastic follow-up, Task 8 Leela email, both MOMs, BNKC-1642, AO Decision Model Prod work, EPLX KT, Jira Excel compilation. | Various | Not started |

## Progress Log

(One entry appended per check-in, newest last.)

### Day set up with detailed subtasks (direct from chat)

Pulled in updates from both the 08/06 and 08/07 Notion pages: 08/06's Task 3 hours corrected to 3.5h, roles+meetings work noted, Deepak's 10:30 AM call carried into today; 08/07's brain dump surfaced Prathyusha's Logstash UAT request and the roles/pipeline prep needed for Deepak's call. Built a detailed subtask breakdown per the user's request, starting 7:00 AM to compensate for yesterday's reduced hours (user was sick).

### Elastic — Kibana Dev Tools query to check UAT cluster CPU/heap during the 8/3 stress-test window

Context: the Search API Quota increase email thread (Mark Vanderflugt → ... → Kiran → Keshvam) needs confirmation of Elastic cluster CPU/memory usage during the 8/3 2–8pm ET performance test, before the API TPM quota goes from 2k→5k (prod target 8/14). User has Kibana + server access but no Stack Monitoring UI access in UAT — worked around it via Dev Tools console, which talks to the ES REST API directly and isn't gated by the same permission.

First attempt (`kibana-vdb-uat.wellsfargo.net`) hit a `400 parse_exception` — the `timestamp` field on `.monitoring-es-*` uses Elasticsearch's strict `date_time` format, which requires milliseconds; a bare `HH:mm:ssZ` fails even though it's valid ISO 8601. Corrected query (run in Dev Tools → Console):

```
GET .monitoring-es-*/_search
{
  "query": {
    "range": {
      "timestamp": {
        "gte": "2026-08-03T18:00:00.000Z",
        "lte": "2026-08-04T00:00:00.000Z"
      }
    }
  },
  "_source": ["source_node.name", "node_stats.process.cpu.percent", "node_stats.jvm.mem.heap_used_percent", "timestamp"],
  "size": 50
}
```

Note: `18:00:00.000Z`–`00:00:00.000Z` (UTC) = 8/3 2pm–8pm ET = 8/3 11:30pm–8/4 5:30am IST. `_source` trimmed to CPU/heap/node/timestamp; `size: 50` since the default (10) is too low across a 6-hour window with multiple nodes. Next: run against prod's equivalent once UAT results are in, then reply to Keshvam with the findings.

**Results (user ran it, pasted back):** only 7 of the returned docs had real `node_stats` — the rest (many duplicate `VDB_UAT_aiadb5662042247_mst2` entries) had only `timestamp`/`source_node.name`, because the query didn't filter by document `type`, so `.monitoring-es-*` returned a mix of `node_stats` docs and other monitoring doc types (shard/index stats) that don't carry CPU/heap. The 7 usable points, all around 19:37 UTC (~1:37pm ET, early in the window):

| Node | CPU % | Heap used % |
|---|---|---|
| ouvra99a0002_data1 | 1% | 8% |
| aiadba979042536_mst1 | 0% | 35% |
| ouvra96a0002_data4 | 1% | 57% |
| aiadba4b5042250_mst3 | 0% | 29% |
| ouvra97a0002_data3 | 0% | 10% |
| aiadbeffa042538_ml | 0% | 13% |
| ouvra98a0002_data2 | 1% | 31% |

CPU essentially idle everywhere, heap moderate (max 57%, nothing near a danger zone) — but this is one moment, not the full 6-hour window (`size: 50` with no sort just grabbed the first 50 docs ES returned, not a spread across 2pm–8pm ET; can't tell if there was a mid-test spike this sample missed).

**Follow-up query — aggregated max/avg per node across the full window** (what should actually go back to Mark/Keshvam, instead of a raw sample):

```
GET .monitoring-es-*/_search
{
  "size": 0,
  "query": {
    "bool": {
      "filter": [
        { "term": { "type": "node_stats" } },
        { "range": { "timestamp": { "gte": "2026-08-03T18:00:00.000Z", "lte": "2026-08-04T00:00:00.000Z" } } }
      ]
    }
  },
  "aggs": {
    "by_node": {
      "terms": { "field": "source_node.name", "size": 20 },
      "aggs": {
        "max_cpu": { "max": { "field": "node_stats.process.cpu.percent" } },
        "avg_cpu": { "avg": { "field": "node_stats.process.cpu.percent" } },
        "max_heap": { "max": { "field": "node_stats.jvm.mem.heap_used_percent" } },
        "avg_heap": { "avg": { "field": "node_stats.jvm.mem.heap_used_percent" } }
      }
    }
  }
}
```

If `source_node.name` errors on the `terms` agg (mapped as `text` not `keyword` in some monitoring templates), retry with `source_node.name.keyword`. Next: run this, then run the equivalent against prod, then reply to Keshvam with the max/avg table.

**Aggregation results (user ran it, pasted back) — ~2160 docs/node over the 6h window, so this one IS representative:**

| Node | Max CPU % | Avg CPU % | Max Heap % | Avg Heap % |
|---|---|---|---|---|
| ouvra99a0002_data1 | 50% | 1.77% | 67% | 37.2% |
| ouvra98a0002_data2 | 21% | 1.69% | 66% | 36.1% |
| aiadb5662042247_mst2 | 14% | 2.5% | 62% | 32.4% |
| ouvra96a0002_data4 | 5% | 0.19% | 66% | 36.5% |
| ouvra97a0002_data3 | 3% | 0.005% | 65% | 35.4% |
| aiadba4b5042250_mst3 | 1% | ~0% | 61% | 32.8% |
| aiadba979042536_mst1 | 0% | 0% | 60% | 29.1% |
| aiadbeffa042538_ml | 0% | 0% | 61% | 30.5% |

**Reading:** one data node (`ouvra99a0002_data1`) briefly spiked to 50% CPU, but its average stayed under 2% — a short burst, not sustained load. Everything else stayed low single digits. Heap tops out at 67% max, averaging 29–37% — comfortable margin before the 75–85% zone where JVM/GC pressure usually starts to matter. **Conclusion: UAT Elastic had ample headroom during the 8/3 stress test — nothing here blocks the TPM bump to 5k.** Matches Mark's existing assessment.

**Still open:** run the same aggregation against prod's equivalent cluster/index, then reply to Keshvam/Mark's thread with both results.

### Query walkthrough (user asked for a detailed explanation) + cluster-wide rollup + expanded 3-day/hourly query

**What the aggregation query does, piece by piece:**
- `GET .monitoring-es-*/_search` — hits every index matching `.monitoring-es-*`. Stack Monitoring writes a cluster-health snapshot (CPU, JVM heap, disk, etc.) every ~10s into one index per calendar day (e.g. `.monitoring-es-7-2026.08.03`); these are normal indices (just `.`-prefixed/hidden), so Dev Tools can query them directly with the plain Search API — that's what gets around not having the Stack Monitoring UI permission.
- `"size": 0` — skip returning raw documents, only return the aggregation results (cheaper, and we don't need ~17,000 individual docs).
- `"query": {"bool": {"filter": [...]}}` — decides which docs count: `{"term": {"type": "node_stats"}}` restricts to just the doc type that carries CPU/heap fields (the missing piece in the very first raw query, which is why half those results had no stats); `{"range": {"timestamp": {...}}}` is the time window.
- `"aggs": {"by_node": {"terms": {...}, "aggs": {...}}}` — like SQL `GROUP BY`: one bucket per distinct `source_node.name`, and inside each bucket, `max`/`avg` computed only over that node's docs. `doc_count: 2160` per node confirmed full 6-hour coverage (~one sample every 10s), unlike the first query's unsorted 50-doc sample.

**Cluster-wide rollup (across all 8 nodes, computed from the per-node table above):**

| Metric | Value | Node |
|---|---|---|
| Max CPU (cluster-wide) | 50% | ouvra99a0002_data1 (brief spike) |
| Avg CPU (cluster-wide) | ~0.77% | across all nodes/samples |
| Max Heap (cluster-wide) | 67% | ouvra99a0002_data1 |
| Avg Heap (cluster-wide) | ~33.7% | across all nodes/samples |

Worst single moment across the whole cluster: 50% CPU / 67% heap, briefly, on one node. Average load was under 1% CPU cluster-wide — healthy headroom.

**Expanded query — 3-day window (8/2–8/5), hourly buckets in ET** (to sanity-check the date/timezone assumption instead of trusting the fixed absolute UTC window):

```
GET .monitoring-es-*/_search
{
  "size": 0,
  "query": {
    "bool": {
      "filter": [
        { "term": { "type": "node_stats" } },
        { "range": { "timestamp": { "gte": "2026-08-02T00:00:00.000Z", "lte": "2026-08-05T00:00:00.000Z" } } }
      ]
    }
  },
  "aggs": {
    "over_time": {
      "date_histogram": {
        "field": "timestamp",
        "fixed_interval": "1h",
        "time_zone": "America/New_York"
      },
      "aggs": {
        "max_cpu": { "max": { "field": "node_stats.process.cpu.percent" } },
        "avg_cpu": { "avg": { "field": "node_stats.process.cpu.percent" } },
        "max_heap": { "max": { "field": "node_stats.jvm.mem.heap_used_percent" } },
        "avg_heap": { "avg": { "field": "node_stats.jvm.mem.heap_used_percent" } }
      }
    }
  }
}
```

`time_zone: "America/New_York"` on the `date_histogram` buckets by ET-local hour (handles EDT/EST automatically), so the output shows exactly which hour/date had the peak — confirms or disproves the 8/3 2–8pm ET assumption directly instead of relying on manual UTC conversion.

### `aggs` block, explained again more clearly (user asked for a re-explanation of the bucket/metric split)

**The `terms` aggregation (`by_node`) — grouping only, no math.** Think of ~17,000 matching `node_stats` documents as one pile. Each doc has `source_node.name` saying which server it came from. `terms: {"field": "source_node.name"}` sorts the pile into separate stacks, one per unique node name — 8 stacks for the 8 nodes in this cluster. That's the entire job of `terms`: splitting, not computing (the SQL `GROUP BY` equivalent).

**The nested `max`/`avg` aggregations — the actual math, run once per stack.** Because `max_cpu`/`avg_cpu`/`max_heap`/`avg_heap` are nested *inside* `by_node`'s `aggs`, Elasticsearch computes each one **separately for every stack**, not across the whole pile. Concretely, for the `ouvra99a0002_data1` stack (its 2160 docs, one reading every ~10s over 6h): `max_cpu` scans all 2160 CPU values in that stack only and keeps the highest (50); `avg_cpu` averages all 2160 in that stack only (1.77); same pattern for heap. Then it repeats independently for each of the other 7 stacks — `aiadba979042536_mst1`'s numbers are computed only from its own 2160 docs, never mixed with any other node's.

That's why the response's `buckets` array has 8 entries (one per node), each with its own `key` (node name), `doc_count`, and its own four numbers — nothing bleeds between nodes.

## Day Summary

*(written at wrap-up)*
