# ShoppingMart_DataEngg_Fabric: End-to-End Pipeline in Microsoft Fabric
Created end-to-end data engineering project for shopping mart data using Medallion architecture. Created pipelines to ingest structured and unstructured data using API.

## Overview
An end-to-end analytics project built in Microsoft Fabric for a fictional retail chain. Raw order, product and review data is ingested into a lakehouse and refined through the **medallion architecture** (Bronze → Silver → Gold) using PySpark notebooks. A master pipeline runs the whole flow, and a Power BI report presents the results.

The project answers questions such as: Which products and categories earn the most? Who are the top customers? How do sales change month to month? What do customers say in their reviews?

## Architecture

Sources (structured + semi-structured) → Ingestion pipeline → Bronze → Silver → Gold → Power BI

## Components

| Component | Type | Purpose |
|---|---|---|
| ShoppingMart_BronzeLayer | Lakehouse | Landing zone for raw data, kept as received |
| Notebook 1: Initial Process | PySpark notebook | Cleans data, standardises columns and aligns schemas |
| ShoppingMart_dataBronzeLayer | Parameterised pipeline | Ingests multiple sources using parameters |
| ShoppingMart_SilverLayer | Lakehouse | Validated, structured data ready for analysis |
| Notebook 2: Further Transformations | PySpark notebook | Joins, aggregations and business-level modelling |
| ShoppingMart_GoldLayer | Lakehouse | Summary tables and KPIs for reporting |
| Run_MasterPipeline | Master pipeline | Runs ingestion and both notebooks in sequence |
| ShoppingMart_Analysis_KPI's | Power BI report | Dashboard for sales, stock, sentiment and engagement |

## What the project covers
- **Parameterised ingestion:** one reusable pipeline loads different datasets, structured and semi-structured (CSV, JSON).
- **Delta Lake storage:** all layers are Delta tables, which gives reliable, transactional storage.
- **PySpark transformations:** null handling, type casting, joins, and aggregations by category, region and product, plus review sentiment scoring.
- **Orchestration:** a master pipeline calls the child pipelines and notebooks in order: ingest, clean, aggregate.
- **Reporting:** a Power BI report built on the Gold layer.

## Dashboard
The report includes:
- Total revenue and product sales KPIs
- Top 5 products and top 5 customers
- Sales by category
- Sentiment split (positive, neutral, negative)
- Stock quantity overview
- Monthly sales trend

## What I learned
- Designing a medallion flow, and why each layer exists
- Building parameterised pipelines and chaining them with a master pipeline
- Reading structured and semi-structured files in PySpark
- Debugging real issues, such as file path wildcards, JSON read options, and workspace permissions (see `docs/lessons-learned.md`)

## Tech stack
Microsoft Fabric (Lakehouse, Data Factory pipelines, Notebooks), PySpark, Delta Lake, Power BI

## Next steps
- Add watermark-based incremental loading
- Add data quality checks and row-count validation between layers
- Schedule the master pipeline with a trigger

## Acknowledgements
This project was inspired by [NextGen Data](https://www.youtube.com/watch?v=qG65DUcSjws&list=PLbIPP1PzRh4aw4ygCH_9C7Hz6dP-BULim&index=7)  by Reena 

Taskflow
<img width="2560" height="1351" alt="{0D2609A3-3F9D-4E3C-93B9-F57EF139FA9A}" src="https://github.com/user-attachments/assets/7c93c5a4-a2dc-40e6-a064-bdc95c68e65f" />

Master Data Pipeline run
<img width="1637" height="1052" alt="{538C6032-618F-434C-A894-FCDD8FA72FE6}" src="https://github.com/user-attachments/assets/6706ad21-6adb-422e-ab43-b36fd84709f0" />

BI report
<img width="1685" height="1121" alt="{902D264B-9088-4820-9D9E-04A4370ACFF3}" src="https://github.com/user-attachments/assets/0019d5a2-4f15-4ec9-bc5e-f470ff0bad87" />
<img width="2553" height="1352" alt="{F976C75E-05D7-4173-B1FF-2484CA4848C2}" src="https://github.com/user-attachments/assets/1cff3303-6b5c-4682-ad43-ba82378e0f43" />

Structured Data Pipeline
<img width="2556" height="1291" alt="image" src="https://github.com/user-attachments/assets/11761315-ee23-4ebd-bb5e-0f00f2172c37" />

Unstructured Data pipeline
<img width="1470" height="832" alt="{37B5EE8B-9704-4AF7-8838-FEA0C3CFAFAF}" src="https://github.com/user-attachments/assets/e4db9ff0-110a-40e9-a9d3-28782849a123" />

Semantic model
<img width="2495" height="1214" alt="{5910F2BD-8D4E-4C93-8BED-2D48B1DDD727}" src="https://github.com/user-attachments/assets/ab92132f-63ac-4098-8415-599c1ad12bf6" />
