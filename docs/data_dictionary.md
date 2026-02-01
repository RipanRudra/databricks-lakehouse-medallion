# Data Catalog – Gold Layer

## Overview

The Gold Layer represents the **business-level data model** in the Databricks Lakehouse.  
It is designed to support **analytics, reporting, and BI use cases** and follows **dimensional modeling** principles.

The layer consists of:
- **Dimension tables** (descriptive business entities)
- **Fact tables** (measurable business events)

---

## 1. gold.dim_customers

**Purpose**  
Stores customer details enriched with demographic and geographic attributes.  
This table represents a **conformed customer dimension** used across analytical workloads.

### Columns

| Column Name     | Data Type | Description |
|-----------------|-----------|-------------|
| customer_key    | INT       | Surrogate key uniquely identifying each customer record in the dimension table. |
| customer_id     | INT       | Natural key representing the customer identifier from the source system. |
| customer_number | STRING    | Alphanumeric customer reference used for business tracking. |
| first_name      | STRING    | Customer first name. |
| last_name       | STRING    | Customer last name. |
| country         | STRING    | Country of residence for the customer (e.g., `Australia`). |
| marital_status  | STRING    | Marital status of the customer (e.g., `Married`, `Single`). |
| gender          | STRING    | Gender of the customer (e.g., `Male`, `Female`, `n/a`). |
| birthdate       | DATE      | Date of birth of the customer. |
| etl_load_timestamp | TIMESTAMP | Timestamp when the record was loaded into the Gold layer. |

---

## 2. gold.dim_products

**Purpose**  
Provides descriptive information about products and their classifications.  
This table acts as the **product dimension** for sales and inventory analytics.

### Columns

| Column Name           | Data Type | Description |
|----------------------|-----------|-------------|
| product_key          | INT       | Surrogate key uniquely identifying each product record. |
| product_id           | INT       | Natural product identifier from the source system. |
| product_number       | STRING    | Alphanumeric product code used for business reference. |
| product_name         | STRING    | Descriptive name of the product. |
| category_id          | STRING    | Identifier representing the product category. |
| category             | STRING    | High-level product category (e.g., `Bikes`, `Components`). |
| subcategory          | STRING    | Detailed product classification within a category. |
| maintenance_required | STRING    | Indicates whether maintenance is required (`Yes` / `No`). |
| cost                 | INT       | Base cost of the product in whole currency units. |
| product_line         | STRING    | Product line or series (e.g., `Road`, `Mountain`). |
| start_date           | DATE      | Date when the product became available. |
| etl_load_timestamp   | TIMESTAMP | Timestamp when the record was loaded into the Gold layer. |

---

## 3. gold.fact_sales

**Purpose**  
Stores **transactional sales data** at the order-line level.  
This fact table enables revenue, volume, and performance analysis.

### Columns

| Column Name      | Data Type | Description |
|------------------|-----------|-------------|
| order_number     | STRING    | Unique alphanumeric identifier for the sales order (e.g., `SO54496`). |
| product_key      | INT       | Surrogate key referencing `gold.dim_products`. |
| customer_key     | INT       | Surrogate key referencing `gold.dim_customers`. |
| order_date       | DATE      | Date when the order was placed. |
| shipping_date    | DATE      | Date when the order was shipped. |
| due_date         | DATE      | Date when payment for the order was due. |
| sales_amount     | INT       | Total sales value for the line item in whole currency units. |
| quantity         | INT       | Number of units ordered for the line item. |
| price            | INT       | Unit price of the product in whole currency units. |
| etl_load_timestamp | TIMESTAMP | Timestamp when the record was loaded into the Gold layer. |

---

## Notes

- Surrogate keys are used for all dimension-to-fact relationships.
- Natural keys are retained for traceability and audit purposes.
- All Gold tables are stored as **Delta tables** and optimized for analytical workloads.
