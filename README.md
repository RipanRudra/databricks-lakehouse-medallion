# 🚴 Aurora Cycles – Enterprise Sales Lakehouse  
**Medallion Architecture | Databricks | Delta Lake | Analytics-Ready Design**

---

## 📖 Project Overview

This repository presents an end-to-end, enterprise-style **Data Lakehouse** built on **Databricks** using the **Medallion Architecture (Bronze, Silver, Gold)**.

The project demonstrates how raw operational data can be ingested, cleaned, standardized, integrated, and transformed into **trusted, analytics-ready Delta tables** suitable for reporting, ad-hoc analysis, and machine learning workloads.

The solution follows modern **lakehouse best practices**, including:
- ELT-based processing
- Layered data architecture
- Delta Lake tables
- Dimensional modeling
- Data lineage and documentation
- Notebook-based transformations and job orchestration

While the underlying dataset is inspired by **Adventure Works**, the project is framed around a **fictitious business scenario** to reflect how a real-world analytics platform would be designed and implemented.

---

## 🏢 Business Context (Fictitious Company)

**Aurora Cycles** is a global retailer and distributor of bicycles and cycling accessories.  
The company sells road bikes, mountain bikes, touring bikes, and related components across multiple regions.

Aurora Cycles operates multiple operational systems:

- **CRM System**
  - Customer information
  - Product details
  - Sales transactions
- **ERP System**
  - Customer attributes
  - Product categories
  - Geographic and reference data

---

### Business Challenges

- Data siloed across CRM and ERP systems  
- Inconsistent customer and product definitions  
- Limited visibility into end-to-end sales performance  
- No centralized, trusted analytics layer  

The business requires a **scalable lakehouse platform** to support:
- Sales performance reporting
- Customer and product analytics
- Executive dashboards
- Self-service BI

---

## 🚧 Project Requirements

### Data Engineering (Lakehouse Design)

Build a modern **Databricks Lakehouse** to consolidate CRM and ERP data into a unified analytics platform.

#### Specifications

- **Data Sources:** CSV files from CRM and ERP systems  
- **Ingestion:** Raw data landed into the Bronze layer  
- **Data Quality:** Cleaning and validation before analytics  
- **Integration:** Conformed customer and product entities  
- **Scope:** Latest snapshot of data (no historical SCD tracking required)  
- **Documentation:** Clear diagrams and data catalogs for transparency  

---

### 📊 Analytics & Reporting

The Gold layer exposes **business-ready Delta tables** designed for analytical workloads.

#### Key Analytics Focus Areas

- Customer behavior and segmentation  
- Product and category performance  
- Sales trends and revenue analysis  
- Time-based reporting (daily, monthly, yearly)

The Gold layer can be consumed by:
- BI tools (e.g., Power BI)
- Databricks SQL
- Ad-hoc Spark queries

---

## 👥 Stakeholders

- **Sales Leadership** – revenue trends and order performance  
- **Finance Team** – pricing, quantity, and sales value analysis  
- **Operations Team** – product lifecycle insights  
- **BI & Analytics Teams** – trusted, analytics-ready datasets  

---

## ❗ Problem Statement

Aurora Cycles lacks a centralized analytics platform that integrates CRM and ERP data into a single source of truth. Reporting teams struggle with inconsistent metrics, duplicated logic, and fragmented data models.

The objective of this project is to design and implement a **Databricks Lakehouse** that resolves these issues and enables scalable, reliable analytics.

---
## 🏗 Solution Architecture

The solution follows the **Medallion Architecture**, separating data responsibilities across three layers to improve **data quality, traceability, and scalability** in a Databricks Lakehouse.

### High-Level Architecture

This diagram shows the overall lakehouse design, including source systems, medallion layers, and downstream consumption.

![High Level Architecture](docs/High%20Level%20Architecture.jpg)

### Medallion Layers

| Layer  | Description                                      | Storage |
|--------|--------------------------------------------------|---------|
| Bronze | Raw, immutable data ingested from source systems | Delta Tables |
| Silver | Cleaned, standardized, validated data            | Delta Tables |
| Gold   | Business-ready, analytics-optimized data         | Delta Tables |

---

## 🧩 Pipeline Design Overview

This diagram represents the **logical pipeline design**, showing how data flows across Bronze, Silver, and Gold layers and how notebooks are structured conceptually.

![Pipeline Overview](docs/Pipeline%20View.jpg)

---

## 🔄 Data Pipeline & Orchestration

Data processing is implemented using **Databricks notebooks**, orchestrated via **Databricks Jobs**.

This diagram reflects the **actual pipeline execution** in Databricks.

- EL (Extract & Load) into Bronze
- Transformations applied in Silver and Gold
- Layer-by-layer dependency execution

![Data Pipeline](docs/Data%20Pipeline.jpg)

---

## 🔄 Data Flow & Lineage

End-to-end data lineage is maintained from source files to Gold analytics tables, ensuring full traceability.

- CRM and ERP CSV files → Bronze  
- Data standardization and validation → Silver  
- Dimensional modeling → Gold  

![Data Lineage](docs/Data%20Lineage.jpg)

---

## 🔗 Data Integration Model

Customer and product data from CRM and ERP systems are integrated to form **conformed business entities**, enabling consistent and reliable reporting across the organization.

![Integration Model](docs/Integration%20Model.jpg)

---

## ⭐ Gold Layer – Sales Data Mart

The Gold layer exposes a **Sales Data Mart** modeled using a **Star Schema**, optimized for analytical queries and BI consumption.

![Star Schema](docs/Star%20Schema.jpg)

### Dimensions
- **dim_customers** – customer attributes enriched with ERP data  
- **dim_products** – product and category information  

### Fact Table
- **fact_sales** – transactional sales metrics (sales amount, quantity, price)

All fact-to-dimension relationships use **surrogate keys** for performance and consistency.

---

## 🧠 ELT & Transformation Approach

This project follows a modern **ELT approach** aligned with Databricks Lakehouse best practices:

- Raw data is loaded directly into the lakehouse
- Transformations occur inside Databricks using Spark
- Business logic is applied progressively from Bronze → Silver → Gold

### Key Transformation Activities
- Schema standardization  
- Data cleansing and validation  
- Deduplication  
- Derived attributes  
- Source system integration  

---

<h2>📂 Repository Structure</h2>

<pre>
dataset/
├── crm/
│   ├── cust_info.csv
│   ├── prd_info.csv
│   └── sales_details.csv
│
├── erp/
│   ├── CUST_AZ12.csv
│   ├── LOC_A101.csv
│   └── PX_CAT_G1V2.csv
│
docs/
├── Data Lineage.jpg
├── Data Pipeline.jpg
├── High Level Architecture.jpg
├── Integration Model.jpg
├── Pipeline View.jpg
├── Star Schema.jpg
├── data_dictionary.md
└── naming_convention.md
│
scripts/
├── bronze/
├── silver/
└── gold/
│
.gitignore
LICENSE
README.md
</pre>


---

## 📘 Documentation

Supporting documentation is available in the `docs` folder:

- **Data Dictionary** – Gold layer table and column definitions  
- **Naming Conventions** – standards for tables, columns, notebooks, and jobs  
- **Architecture Diagrams** – visual documentation of the lakehouse design  

---

## ✅ Data Quality & Validation

Data quality is enforced throughout the pipeline:

- Schema validation during ingestion
- Data type normalization
- Referential integrity between fact and dimension tables
- Clear separation of raw data and business logic

---

## 🚀 How to Run the Project (High-Level)

1. Upload source CSV files to Databricks Volumes or DBFS  
2. Run Bronze notebooks to ingest raw data into Delta tables  
3. Execute Silver notebooks for cleaning and standardization  
4. Run Gold notebooks to build dimensional models  
5. Query Gold tables using Databricks SQL or BI tools  

---

## 🔮 Future Improvements

Potential enhancements include:

- Incremental and CDC-based ingestion  
- Advanced orchestration with job dependencies  
- Unity Catalog integration for governance  
- CI/CD pipelines for notebooks  
- Machine learning models built on Gold data  

---

## 📌 Final Notes

This project demonstrates how a modern organization can design and implement a **scalable, maintainable Databricks Lakehouse** using industry best practices. It showcases both technical execution and architectural decision-making suitable for real-world analytics platforms.

---

## 🙌 Credits

This project was inspired by the educational content from **Baraa Salkini**.

---

## 📫 Contact Me

- **LinkedIn:** https://linkedin.com/in/rrudra98
- **Email:** ripanrudra@yahoo.com
