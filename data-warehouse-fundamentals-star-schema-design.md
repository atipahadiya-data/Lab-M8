## Step 1: Fact vs Dimension Identification
**Order Amount**

    Type: Fact
    Reasoning: Numeric and measurable
    Analytics use: Summed or averaged to calculate revenue

**Quantity Sold**

    Type: Fact
    Reasoning: Numeric measure that varies per transaction
    Analytics use: Aggregated to analyze sales volume

**Customer**

    Type: Dimension
    Reasoning: Descriptive entity, not directly measurable
    Analytics use: Grouping/filtering sales by customer attributes

**Product**

    Type: Dimension
    Reasoning: Describes what was sold
    Analytics use: Analyze performance by product or category

**Date**

    Type: Dimension
    Reasoning: Time-based context for facts
    Analytics use: Time-series analysis, trends, period comparisons

**Region**

    Type: Dimension
    Reasoning: Descriptive geographic attribute
    Analytics use: Segment and compare performance by location

## Step 2: Fact Table Design
**fact_sales**
- sale_id (PK, surrogate key)
- customer_id (FK → dim_customer)
- product_id (FK → dim_product)
- date_id (FK → dim_date)
- region_id (FK → dim_region)
- order_amount (measure)
- quantity (measure)
- discount_amount (measure)
- profit_amount (measure)

## Step 3: Dimension Tables Design 
**dim_customer**
- customer_id (PK, surrogate)
- customer_name
- email
- segment
- registration_date
- city
- state
- country

**dim_product**
- product_id (PK, surrogate)
- product_name
- category
- subcategory
- brand
- unit_price
- unit_cost

**dim_date**
- date_id (PK, surrogate)
- date
- year
- quarter
- month
- week
- day_of_week
- is_holiday
- is_weekend

**dim_region**
- region_id (PK, surrogate)
- region_name
- country
- state
- city
- timezone

## Step 4: Star Schema Diagram

```mermaid
erDiagram
    FACT_SALES ||--|| DIM_CUSTOMER : "has"
    FACT_SALES ||--|| DIM_PRODUCT : "contains"
    FACT_SALES ||--|| DIM_DATE : "occurs on"
    FACT_SALES ||--|| DIM_REGION : "sold in"
    
    FACT_SALES {
        int sale_id PK
        int customer_id FK
        int product_id FK
        int date_id FK
        int region_id FK
        decimal order_amount
        int quantity
        decimal discount_amount
        decimal profit_amount
    }
    
    DIM_CUSTOMER {
        int customer_id PK
        string customer_name
        string email
        string segment
        date registration_date
    }
    
    DIM_PRODUCT {
        int product_id PK
        string product_name
        string category
        string brand
        decimal unit_price
    }
    
    DIM_DATE {
        int date_id PK
        date date
        int year
        int quarter
        int month
        string day_of_week
    }
    
    DIM_REGION {
        int region_id PK
        string region_name
        string country
        string state
    }


