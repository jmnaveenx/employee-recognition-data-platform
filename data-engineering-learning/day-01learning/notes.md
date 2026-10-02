# Day 1 – Data Engineering Foundations

## 1. What is Data Engineering?

Data Engineering is the process of building systems that ingest,
store, transform, validate, and deliver data for analytics,
applications, reporting, and AI.

A simple Data Engineering flow is:

Source
→ Ingestion
→ Storage
→ Transformation
→ Validation
→ Curated Data
→ Analytics / Applications / AI


## 2. Data Sources

Data can come from many different sources:

- CSV files
- JSON files
- Databases
- APIs
- Applications
- Logs
- Events

Example:

employees.csv
recognition.json
employee database
application events


## 3. Ingestion

Ingestion means bringing data from the source into our
data platform.

Example:

employees.csv
    ↓
Ingestion
    ↓
ADLS Data Lake


## 4. ETL

ETL means:

Extract → Transform → Load

The data is transformed before it is loaded into the target.

Example:

employees.csv
    ↓
Extract
    ↓
Clean / Transform
    ↓
Load
    ↓
Target


## 5. ELT

ELT means:

Extract → Load → Transform

The data is first loaded into the data platform and
transformed later.

Example:

employees.csv
    ↓
Extract
    ↓
ADLS Data Lake
    ↓
Databricks
    ↓
Transform


## 6. ETL vs ELT

ETL:

Extract → Transform → Load

ELT:

Extract → Load → Transform

The main difference is when the transformation happens.


## 7. Data Lake

A Data Lake is a flexible storage layer for storing large
amounts of data, including raw and varied data.

Examples of data that can be stored:

- CSV
- JSON
- Parquet
- Logs
- Events
- Other files

A Data Lake does not mean that every piece of data must
remain raw forever. Processed and curated data can also
exist in the lake.


## 8. Azure Storage Account vs Data Lake

An Azure Storage Account is an Azure storage resource.

When Hierarchical Namespace is enabled, it provides
ADLS Gen2 capabilities suitable for Data Lake workloads.

Simple mental model:

Azure Storage Account
        ↓
Hierarchical Namespace / ADLS Gen2
        ↓
Data Lake storage


## 9. Data Warehouse

A Data Warehouse provides structured, analytics-oriented
data.

It is commonly used for:

- SQL analytics
- Reporting
- Business Intelligence
- Business analysis

Example tables:

fact_sales
dim_customer
dim_product
dim_date


## 10. Data Lake vs Data Warehouse

Data Lake:

- Flexible storage
- Can store raw and varied data
- Suitable for large volumes of different data types
- Useful as a source for reprocessing

Data Warehouse:

- Structured data
- Analytics-oriented
- Business-ready datasets
- Commonly used for reporting and BI


## 11. Data Lakehouse

A Data Lakehouse combines the flexibility of a Data Lake
with capabilities associated with Data Warehouse analytics.

Examples of capabilities can include:

- SQL analytics
- ACID transactions
- Schema management
- Table management
- Historical versions of data

Important:

CDC, SCD Type 1, and SCD Type 2 are data engineering
patterns that can be implemented using lakehouse technologies.
They are not the definition of a Data Lakehouse.


## 12. Why Preserve Raw Data?

We preserve raw data so that we can:

- Reprocess data
- Perform backfills
- Validate records
- Investigate problems
- Recover from processing problems
- Apply new transformation/business rules
- Rebuild downstream datasets


## 13. Business Rule Change Example

Suppose today's business rule is:

"Count all employees equally."

Later the business changes the rule:

"IT employees should be counted differently."

If we preserved the raw data:

Raw Data
   ↓
New Transformation Rule
   ↓
New Silver Data
   ↓
New Gold Data
   ↓
Updated Report

We can reprocess the original data using the new rule.


## 14. Medallion Architecture

A common data processing pattern is:

Bronze → Silver → Gold


### Bronze

Bronze contains raw or minimally processed data.

Purpose:

- Preserve source data
- Enable reprocessing
- Support backfills
- Support investigation and validation


### Silver

Silver contains cleaned and standardized data.

Typical activities include:

- Deduplication
- Data type correction
- Validation
- Handling missing values
- Standardization
- Transformations


Important:

We should not automatically remove every NULL value.
Whether a NULL is valid depends on the business rule.


### Gold

Gold contains curated, business-ready data.

It is designed for:

- Reporting
- Business Intelligence
- Analytics
- Business decision-making


## 15. Why Not Put Raw Data Directly into Gold?

Gold is intended for business consumption.

Raw data may contain:

- Missing values
- Duplicate records
- Invalid values
- Inconsistent formats
- Unprocessed information

Therefore, data normally goes through processing and
validation before becoming a business-ready Gold dataset.


## 16. Complete Mental Model

Source
   ↓
Ingestion
   ↓
ADLS Data Lake
   ↓
Bronze
   ↓
Silver
   ↓
Gold
   ↓
BI / Analytics / Applications / AI


## 17. Employee Recognition Project Connection

Our Employee Recognition project can be viewed as:

Employee Data
Recognition Data
Manager Data
Department Data
        ↓
      ADLS
        ↓
    Databricks
        ↓
Bronze
        ↓
Silver
        ↓
Gold
        ↓
Recognition Analytics


## 18. Day 1 Key Takeaways

1. Data Engineering builds reliable data pipelines.
2. ETL transforms before loading.
3. ELT loads before transforming.
4. Data Lake provides flexible data storage.
5. ADLS Gen2 can provide the storage layer for an Azure Data Lake.
6. Data Warehouse provides structured analytics-oriented data.
7. Data Lakehouse combines Data Lake flexibility with
   warehouse-style analytics capabilities.
8. Bronze preserves raw data.
9. Silver cleans and standardizes data.
10. Gold provides business-ready data.
11. Preserving raw data allows reprocessing and backfilling.
12. Business rule changes may require reprocessing from raw data.

## Day 1 – My Understanding

The most important thing I learned today:

Data Engineering is not just about writing SQL or using
Databricks. It is about building a reliable flow of data
from source to business-ready data.

My mental model:

Source
→ Ingestion
→ Data Lake
→ Bronze
→ Silver
→ Gold
→ Analytics / BI / AI
