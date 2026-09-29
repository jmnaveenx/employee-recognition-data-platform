# Employee Recognition Data Platform Architecture

## Objective

Build an end-to-end data engineering platform for analyzing employee recognition activity.

## Business Questions

- Who is giving recognition?
- Who is receiving recognition?
- Who has not given recognition in the last 30 days?
- Who has not given recognition in the last 90 days?
- Which employees under a particular manager have not given recognition?
- Which recognition types are used most?
- Which departments have the highest recognition?
- Has recognition increased or decreased over time?
- Why has recognition reduced?
- Which managers and teams have low recognition participation?

## High-Level Architecture

Source Systems
      ↓
Azure Data Factory
      ↓
Azure Data Lake Storage Gen2
      ↓
Bronze Layer
      ↓
Databricks / PySpark
      ↓
Data Quality & Quarantine
      ↓
Silver Layer
      ↓
Gold Layer
      ↓
Analytics / ML / GenAI / RAG

## Core Technologies

- Azure Data Factory
- Azure Data Lake Storage Gen2
- Azure Databricks
- PySpark
- Delta Lake
- SQL
- GitHub

## Engineering Features

- Metadata-driven pipelines
- Incremental processing
- Data quality validation
- Quarantine handling
- Idempotency
- Backfill
- CDC
- SCD Type 2
- Spark optimization
- Pipeline monitoring
