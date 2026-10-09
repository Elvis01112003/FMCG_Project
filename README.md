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
-   **Amazon S3** --- source-file storage used in the project scenario
-   **SQL** --- querying, transformations, and validation
-   **Databricks SQL / AI-BI tools** --- analytics and visualisation

## Architecture

The project follows the Medallion Architecture:

1.  **Bronze** --- ingested source data.
2.  **Silver** --- cleaned, standardized, and transformed data.
3.  **Gold** --- business-ready dimension and fact tables for analytics.

Conceptual flow:

``` text
Source Files (Amazon S3)
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

The exact path and processing logic for each dataset are defined by the
project's notebooks and pipeline configuration.

## Data Organization

The Databricks workspace includes a catalog/schema structure and
source-file volumes. The observed file layout includes:

``` text
fmcg/
├── bronze/
└── default/
    └── Volumes/
        └── full_load/
            └── full_load/
                ├── customers/
                ├── gross_price/
                └── orders/
                    ├── landing/
                    └── processed/
```

-   **`landing/`** --- holds incoming source order files before
    processing.
-   **`processed/`** --- holds order files produced after processing. In
    the current workspace, these appear as multiple CSV files.
-   **`customers/` and `gross_price/`** --- folders for the
    corresponding source datasets.

The folder names describe the file workflow; the exact transformations
should be verified in the relevant notebook or pipeline.

## Gold-Layer Tables

The observed Gold layer contains tables with names including:

-   `dim_customers`
-   `dim_date`
-   `dim_products`
-   `fact_orders`
-   `sb_dim_customers`
-   `sb_dim_gross_price`
-   `sb_dim_products`

Some table names were truncated in the workspace view. The `sb_` prefix
appears to distinguish acquired-company (Sports Bar) tables from the
parent company's tables in this project scenario. Confirm each table's
exact purpose and lineage from its schema and creation notebook.

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

## Analytics and Reporting

The Gold layer is intended to provide business-ready data for reporting.
Depending on the configured analytics solution, users can compare
performance across the parent and acquired businesses, analyse products
and orders, and explore trends using Databricks SQL, dashboards, or
Genie.

## Current Progress

-   Reviewed the end-to-end FMCG data engineering architecture.
-   Explored the source-file layout for customers, gross price, and
    orders.
-   Identified the `landing` and `processed` folders for order CSV
    files.
-   Worked on fact processing and historical loading.
-   Continuing to understand incremental fact loading and validation.

## Next Steps

-   Complete and verify historical fact processing.
-   Understand and test the incremental loading logic.
-   Validate the final Gold-layer tables.
-   Confirm how parent-company and acquired-company data are
    consolidated.
-   Review the final analytics tables and dashboards.

## Notes

This README describes the project structure and learning progress based
on the workspace components reviewed so far. Update the table names,
source paths, transformation rules, orchestration details, and
validation results as they are confirmed in the notebooks and pipeline
code.
