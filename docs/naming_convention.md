# Naming Conventions

This document defines naming conventions for a **Databricks Lakehouse** implementation following the **Medallion Architecture (Bronze / Silver / Gold)**.  
The goal is to ensure **consistency, clarity, lineage, and scalability** across all data assets.

---

## General Principles

- Use `snake_case` with lowercase letters and underscores (`_`).
- Use English for all object names.
- Prefer clear, descriptive names over abbreviations.
- Avoid SQL and Spark reserved keywords.
- Apply naming rules consistently across all layers.

---

## Table Naming Conventions

### Bronze Layer

The Bronze layer stores **raw, immutable data** ingested directly from source systems.

- Table names must start with the source system identifier.
- Table names must match the original source entity name.
- No renaming or business logic is applied.

**Examples**
- `crm_sales_details`
- `crm_cust_info`
- `erp_cust_az12`

---

### Silver Layer

The Silver layer stores **cleaned and standardized data**.

- Table names remain identical to Bronze to preserve lineage.
- Tables represent the same business entities with improved data quality.
- Deduplication, validation, and schema standardization occur here.

**Examples**
- `crm_sales_details`
- `crm_cust_info`
- `erp_cust_az12`

---

### Gold Layer

The Gold layer stores **business-ready, analytics-optimized data**.

- Table names must be business-oriented and source-agnostic.
- Tables follow dimensional modeling principles.

**Examples**
- `dim_customer`
- `dim_product`
- `fact_sales`
- `report_sales_monthly`

---

## Column Naming Conventions

### Surrogate Keys

- Surrogate keys are introduced only in the Gold layer.
- All surrogate keys must end with the suffix `_key`.

**Examples**
- `customer_key`
- `product_key`

---

### Technical Columns

Technical columns store system-generated metadata.

- All technical columns must start with the prefix `etl_`.
- These columns are not business attributes.

**Examples**
- `etl_load_timestamp`
- `etl_source_system`
- `etl_batch_id`
- `etl_is_current`

---

## Notebook & Job Naming Conventions

In Databricks, notebooks and jobs replace stored procedures.

### Notebook Naming

**Examples**
- `bronze_ingest_crm_sales_details`
- `silver_clean_crm_cust_info`
- `gold_build_fact_sales`

---

### Job Naming

**Examples**
- `job_bronze_ingestion`
- `job_silver_transformation`
- `job_gold_aggregation`

---

## Summary

These naming conventions support:
- Clear data lineage across Bronze, Silver, and Gold layers
- Databricks Lakehouse and ELT best practices
- Maintainable, scalable, and well-governed data pipelines
