# FMCG Data Engineering Project using Databricks

## Project Overview

This project demonstrates an end-to-end data engineering workflow for an
FMCG/retail business using Databricks. The business scenario involves
processing data from an acquired company and preparing it for
integration with the parent company's existing data so both businesses
can be analysed together.

The project covers source-file ingestion, data transformation, dimension
and fact processing, historical loading, incremental loading, data
validation, and analytics-ready outputs.

## Objectives

-   Ingest source data files into the Databricks environment.
-   Organize and process data using the Medallion Architecture.
-   Prepare customer, product, date, pricing, and order data.
-   Process historical transaction data for the initial load.
-   Support incremental processing for subsequent data arrivals.
-   Prepare Gold-layer tables for consolidated analytics and reporting.
-   Explore the final data through Databricks SQL, dashboards, and Genie
    where configured.

## Technology Stack

-   **Databricks** --- data engineering and processing platform
-   **Apache Spark / PySpark** --- distributed data processing
-   **Delta Lake** --- lakehouse table storage and processing
-   **Unity Catalog** --- data organization and access management
-   **Unity Catalog Volumes** --- storing and accessing source files
-   **SQL** --- querying, transformations, and validation
-   **Databricks SQL / dashboards** --- analytics and visualisation
-   **Lakeflow Jobs / workflow orchestration** --- coordinating pipeline tasks
-   **Genie** --- explored for AI-powered, natural-language analytics

## Architecture

The project follows the Medallion Architecture:

1.  **Bronze** --- ingested source data.
2.  **Silver** --- cleaned, standardized, and transformed data.
3.  **Gold** --- business-ready dimension and fact tables for analytics.

Conceptual flow:

``` text
Source Files / Databricks Volumes
        |
        v
Ingestion into Databricks
        |
        v
Bronze Layer
        |
        v
Silver Layer
        |
        v
Gold Layer
        |
        v
Consolidated Analytics / Dashboards
```

Pipeline tasks are orchestrated so that ingestion, transformation, and
validation steps run in the appropriate sequence. The curated Gold data is
then used for dashboards and business analysis.

## Data Organization

The Databricks workspace includes a catalog/schema structure and
source-file volumes. The observed file layout includes:

``` text
/Volumes/fmcg/default/full_load/full_load/
├── customers/
├── gross_price/
├── products/
└── orders/
    ├── landing/
    └── processed/
```

-   **`landing/`** --- holds incoming source order files before
    processing.
-   **`processed/`** --- holds order files produced after processing. In
    the current workspace, these appear as multiple CSV files.
-   **`customers/`, `gross_price/`, and `products/`** --- folders for
    the corresponding source datasets.

The folder names describe the file workflow; the exact transformations
should be verified in the relevant notebook or pipeline.

## Gold-Layer Tables

The observed Gold layer contains tables with names including:

-   `dim_customers`
-   `dim_date`
-   `dim_gross_price`
-   `dim_products`
-   `fact_orders`
-   `sb_dim_customers`
-   `sb_dim_gross_price`
-   `sb_dim_products`
-   `sb_fact_orders`

The `sb_` prefix distinguishes the additional source's dimension and
fact tables from the existing Gold-layer tables. The fact tables contain
order-level measures, while the dimension tables provide descriptive
context for analytical queries.

## Fact Processing

### Historical Load

Historical loading processes the existing order/transaction history for
the initial load. The project scenario includes historical data from the
acquired business. The data is read, processed, and prepared for the
Gold layer so that historical activity can be included in consolidated
analytics.

### Incremental Load

Incremental loading processes subsequent new or changed data instead of
reprocessing the entire historical dataset on every run. The exact
change-detection method and how updates are applied should be documented
from the implementation notebooks.

## Dimension Processing

Dimension processing prepares descriptive data, such as customers and
products, for use in analytics. Depending on the dataset and business
rules, this can include standardizing data, applying transformations,
handling invalid or duplicate records, and preparing target tables.

## Validation

Validation should be used to confirm that processing produced the
expected results. Useful checks include:

-   Source and target row counts
-   Duplicate business keys
-   Null values in required columns
-   Schema and data-type consistency
-   Correct relationships between fact and dimension tables
-   Historical and incremental load results

## Pipeline Orchestration

Pipeline orchestration coordinates the processing steps and their
execution order, helping make the workflow repeatable. The project
workflow brings together data ingestion, transformation, fact and
dimension processing, incremental loading, and validation.

## Analytics and Reporting

The Gold layer provides business-ready data for reporting. Dashboards
present key results in a visual format, helping users review sales
performance and explore product, customer, and order trends. Genie was
also explored for AI-powered, natural-language analytics over the data.

## What I Implemented and Learned

Through implementing the project, I gained hands-on experience with:

- Building an end-to-end FMCG data engineering workflow in Databricks.
- Processing data through the Bronze, Silver, and Gold layers.
- Loading historical data and processing incremental fact data.
- Preparing dimension and fact tables for analytics.
- Consolidating data from multiple sources into the Gold layer.
- Orchestrating pipeline tasks and validating processed outputs.
- Creating dashboards and exploring Genie for AI-powered analytics.

## Business Outcome

The pipeline transforms raw business data into structured, analytics-ready
datasets. These datasets support sales reporting, product-performance
analysis, customer-trend analysis, dashboards, and more informed,
data-driven business decisions.

## Project Status

The project workflow has been implemented and reviewed across historical
loading, dimension processing, incremental fact processing, pipeline
orchestration, and dashboarding. Validation and refinement can continue
as data and reporting requirements evolve.

## Notes

Table names and folder paths reflect the Databricks workspace components
observed during the project. Transformation rules and incremental-loading
behaviour should be checked against the relevant notebooks and pipeline
configuration when extending or maintaining the implementation.
