# Schema Strategy & Processing Design – Summary

## Conceptual Understanding

### Schema-on-write
Schema is enforced **before data is stored**. Data must match a predefined structure during ingestion.

### Schema-on-read
Schema is applied **when data is queried or processed**. Raw data is stored without enforcement.

### Pros and Cons Comparison

| Approach | Pros | Cons |
|--------|------|------|
| Schema-on-write | High data quality, consistent reporting, governance-friendly | Less flexible, slower ingestion |
| Schema-on-read | Flexible, fast ingestion, supports schema evolution | Risk of inconsistency, requires strong governance |

---

## Scenario Evaluations

### IoT Streaming Data
- **Decision:** Schema-on-read  
- **Justification:** High volume, evolving structure, low-latency ingestion required

### Banking Transactions
- **Decision:** Schema-on-write  
- **Justification:** Regulatory compliance, accuracy, strict validation needed

### Clickstream Logs
- **Decision:** Schema-on-read  
- **Justification:** Semi-structured data, exploratory analytics use cases

### Daily Sales Reports
- **Decision:** Schema-on-write  
- **Justification:** Stable schema and consistent metrics required for reporting

---

## Batch vs Streaming Analysis

### Batch Processing
- **Schema Strategy:** Schema-on-write  
- **Reason:** Periodic processing allows strong validation and consistency

### Streaming Processing
- **Schema Strategy:** Schema-on-read (or light validation)  
- **Reason:** Prioritizes speed, flexibility, and schema evolution

### Strategy Differences
- Streaming favors flexibility and ingestion speed  
- Batch favors correctness and standardized outputs

---

## Design Reflection

### Where Flexibility Is Required
- Raw/Bronze zones  
- Exploratory analytics  
- Machine learning pipelines  

### Where Strict Control Is Mandatory
- Financial and regulatory data  
- Curated/Gold datasets  
- Business-critical reporting  

### Decision Principles
- Ingest fast, validate later when flexibility is needed  
- Enforce schema early for trusted, business-facing data  
