# Dataset Storage and Organization Strategy

This document defines storage, zoning, schema, and ingestion strategies for different datasets to ensure scalability, governance, and reliable analytics.

---

## Dataset Analysis

### Application Logs
- **Characteristics:** High-volume, semi-structured, append-only
- **Usage Patterns:** Debugging, monitoring, root-cause analysis
- **Consumer Requirements:** Flexible querying, low-latency ingestion, long retention

### Daily Sales Summary
- **Characteristics:** Aggregated, structured, low volume
- **Usage Patterns:** Executive dashboards, BI reporting
- **Consumer Requirements:** Fast query performance, consistent schema

### Raw IoT Sensor Data
- **Characteristics:** Very high-volume, time-series, event-based
- **Usage Patterns:** Downstream processing, anomaly detection, ML
- **Consumer Requirements:** Scalable ingestion, replayability, immutability

### Customer Master Data
- **Characteristics:** Highly structured, slowly changing
- **Usage Patterns:** Enterprise-wide joins, reporting, analytics
- **Consumer Requirements:** Strong data quality, governance, consistency

### Marketing Campaign Results
- **Characteristics:** Semi-structured metrics, campaign-oriented
- **Usage Patterns:** Performance analysis, attribution
- **Consumer Requirements:** Clean, curated, analytics-ready data

### Ad-hoc Analyst Extracts
- **Characteristics:** Temporary, exploratory, inconsistent schemas
- **Usage Patterns:** One-off analysis and experimentation
- **Consumer Requirements:** Flexibility, isolation from production datasets

---

## Classification Table

| Dataset                    | Storage Type | Zone   | Schema Strategy  | Ingestion Type | Reasoning |
|----------------------------|--------------|--------|------------------|----------------|-----------|
| Application logs           | Data Lake    | Raw    | Schema-on-read   | Streaming      | High-volume, semi-structured data benefits from flexible schemas and scalable ingestion. |
| Daily sales summary        | Warehouse    | N/A    | Schema-on-write  | Batch          | Structured, aggregated data optimized for BI and reporting performance. |
| Raw IoT sensor data        | Data Lake    | Raw    | Schema-on-read   | Streaming      | Massive event streams require late schema binding and replay capability. |
| Customer master data       | Warehouse    | N/A    | Schema-on-write  | Batch          | Core business entity requiring strict schema enforcement and governance. |
| Marketing campaign results | Data Lake    | Gold   | Schema-on-write  | Batch          | Curated, trusted datasets designed for analytics and dashboard consumption. |
| Ad-hoc analyst extracts    | Data Lake    | Silver | Schema-on-read   | Batch          | Exploratory datasets need flexibility without impacting raw or curated data. |

---


---

## Review and Justification

### Consistency Check
- Raw, high-volume, or semi-structured datasets are stored in the **Data Lake (Raw zone)**.
- Curated and consumption-ready datasets are promoted to **Silver/Gold zones** or the **Warehouse**.
- Schema-on-write is used where data quality, performance, and trust are critical.

### Edge Case Considerations
- Application logs may be promoted to Silver if standardized metrics are derived.
- Marketing campaign results could move to a warehouse if heavily used for executive BI.
- Ad-hoc extracts should have lifecycle policies to avoid long-term clutter.

### Alternative Approaches
- A **Lakehouse architecture** could unify lake and warehouse while preserving zones.
- Near-real-time sales summaries could be streamed into the warehouse.
- Customer master data could also be exposed as a Gold dataset for ML feature reuse.

---
