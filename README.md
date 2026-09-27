<p align="center">
  <img src="docs/assets/banner.svg" alt="30 Days of Data & Software Engineering" width="100%">
</p>

One working system per day for 30 days, all built on the same synthetic e-commerce dataset, so each project can pick up where the previous ones left off: the pipeline from day 1 feeds the lakehouse on day 4, which feeds the API on day 6, which gets a cache on day 7, and so on until day 30 wires everything into one platform.

## Rules

1. Every number in a README comes from a benchmark or a real run committed under `results/`, with the hardware it ran on. If a change made no difference, the README says so.
2. Every project runs with one command, has tests, and has CI.
3. Each README explains the engineering decisions and trade-offs, not only the stack.
4. Limitations are written down.

## Progress

`1 / 31` (day 00 is setup)

| Day | Project | What it shows | Stack | Status |
|---:|---|---|---|---|
| 00 | [shopflow-datagen](https://github.com/silvano-moraes-de-souza/shopflow-datagen) · [de-project-template](https://github.com/silvano-moraes-de-souza/de-project-template) | Deterministic synthetic data, project template, benchmark harness | Python, NumPy, PyArrow | done |
| 01 | E-commerce Data Pipeline | Batch ETL, modeling, idempotent loads | Python, PostgreSQL, Docker | next |
| 02 | Data Quality Engine | Null rate, duplicates, outliers, schema drift, referential integrity | Python, Polars | |
| 03 | Incremental ETL / CDC | Watermarks, upserts, simulated CDC | Python, PostgreSQL | |
| 04 | Mini Lakehouse | Bronze, silver, gold; partitioning | Parquet, PyArrow, DuckDB | |
| 05 | SQL Performance Lab | Indexes and plans, measured with EXPLAIN ANALYZE | PostgreSQL | |
| 06 | Sales Analytics API | REST over the gold layer | FastAPI, DuckDB | |
| 07 | API Cache Layer | Cache-aside, TTL, invalidation, p50/p95 latency | Redis | |
| 08 | Pipeline Observability | Metrics, structured logs, dashboards | Prometheus, Grafana | |
| 09 | Pipeline Job Scheduler | DAGs, dependencies, run state | Python, PostgreSQL | |
| 10 | Pipeline Failure Simulator | Retries, backoff, reprocessing, recovery time | Python | |
| 11 | Data Alerting System | Threshold rules, alert deduplication | Python | |
| 12 | Data Contract Validator | Schemas, breaking-change detection in CI | Pydantic, JSON Schema | |
| 13 | Data Lineage Tracker | Source to transform to consumer | Python, networkx | |
| 14 | Mini Data Catalog | Dataset metadata, owners, search | FastAPI, Next.js | |
| 15 | Distributed Rate Limiter | Token bucket vs sliding window | Redis, Lua | |
| 16 | Distributed Task Queue | Workers, acks, throughput by worker count | Redis / RabbitMQ | |
| 17 | Event-Driven Order System | Idempotency, DLQ, correlation IDs | FastAPI, RabbitMQ, PostgreSQL | |
| 18 | API Gateway | Routing, auth, rate limiting | FastAPI, httpx | |
| 19 | Real-Time Analytics Dashboard | Streaming aggregation windows | RabbitMQ, DuckDB, Next.js | |
| 20 | Resilient Web Scraper | Retries, checkpoints, dedup, success rate | httpx, parsel | |
| 21 | Document Processing Pipeline | OCR, extraction, error queue | Tesseract, PyMuPDF | |
| 22 | CSV/Excel to Data Warehouse | Spreadsheet ingestion with validation | Python, DuckDB | |
| 23 | Financial Anomaly Detector | z-score, IQR, isolation forest, scored against injected anomalies | scikit-learn | |
| 24 | Financial Reconciliation Engine | Matching, divergences, audit trail | Python, SQL | |
| 25 | Product Recommendation Engine | Co-occurrence, offline precision@k | Python | |
| 26 | Local Search Engine | Inverted index, BM25 ranking | Python | |
| 27 | Mini Feature Store | Offline/online features, point-in-time joins | DuckDB, Redis | |
| 28 | Demand Forecasting Pipeline | Backtested time series forecasts | statsforecast | |
| 29 | ETL Benchmark Lab | Pandas vs Polars vs DuckDB, time and memory | Python | |
| 30 | Mini Data Engineering Platform | Everything above, wired together | Docker Compose | |

## How the projects connect

```mermaid
flowchart LR
    G[00 datagen] --> P01[01 pipeline]
    P01 --> P02[02 quality] --> P12[12 contracts] --> P13[13 lineage] --> P14[14 catalog]
    P01 --> P03[03 CDC] --> P04[04 lakehouse] --> P06[06 API] --> P07[07 cache] --> P15[15 rate limiter] --> P18[18 gateway]
    P04 --> P27[27 feature store] --> P28[28 forecasting]
    P01 --> P08[08 observability] --> P09[09 scheduler] --> P10[10 failure sim] --> P11[11 alerts]
    G --> P16[16 task queue] --> P17[17 event-driven] --> P19[19 real-time]
    P17 --> P24[24 reconciliation]
    P18 & P19 & P11 & P14 --> P30[30 platform]
```

## Shared building blocks

| Piece | What it gives every project |
|---|---|
| [shopflow-datagen](https://github.com/silvano-moraes-de-souza/shopflow-datagen) | The same customers, products, orders and payments at any scale, with an optional dirty mode that records exactly which problems it injected |
| [de-project-template](https://github.com/silvano-moraes-de-souza/de-project-template) | Layout, CI, Docker, benchmark harness and banner, created with one command |

## Author

Silvano Moraes de Souza · [GitHub](https://github.com/silvano-moraes-de-souza) · [Portfolio](https://silvanomsouza.vercel.app/)
