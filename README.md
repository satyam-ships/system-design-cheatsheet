# system-design-cheatsheet 🏗️

> A one-page-per-concept guide to system design: when to use it, trade-offs, and numbers to remember.

## A framework for any design question
1. **Clarify** requirements (functional, scale, latency, consistency).
2. **Estimate** load: QPS, storage, bandwidth.
3. **API + data model** first.
4. **High-level design**, then drill into bottlenecks.
5. **Trade-offs**: say what you gave up and why.

## Numbers worth memorizing
| Operation | Rough latency |
|---|---|
| L1 cache reference | ~1 ns |
| Main memory reference | ~100 ns |
| SSD random read | ~100 µs |
| Same-datacenter round trip | ~0.5 ms |
| Cross-continent round trip | ~100-150 ms |

Back-of-envelope: 1M requests/day ≈ 12 QPS. 100M/day ≈ 1,200 QPS average (plan for 2-3x peak).

## Building blocks
| Concept | Use when | Trade-off |
|---|---|---|
| Load balancer | Multiple stateless servers | Extra hop; health checks needed |
| Cache | Read-heavy, tolerates staleness | Invalidation complexity |
| CDN | Static/global content | Cost; cache purge delays |
| SQL | Relations, transactions | Vertical-scaling limits, sharding is hard |
| NoSQL (document/KV) | Flexible schema, horizontal scale | Weaker joins/transactions |
| Message queue | Decouple, absorb spikes | At-least-once → idempotency |
| Sharding | Data exceeds one node | Cross-shard queries, rebalancing |
| Replication | Availability, read scale | Replica lag |
| Rate limiter | Protect services | Distributed counters |

## CAP in one paragraph
During a network partition you choose consistency (reject some requests) or availability (serve possibly stale data). Without partitions you trade latency for consistency (PACELC).

## Classic designs to practice
URL shortener · rate limiter · chat system · news feed · notification service · file storage · ride matching · search autocomplete.

Next: roadmap in [backend-engineering-roadmap](https://github.com/satyam-ships/backend-engineering-roadmap). License: [MIT](LICENSE).
