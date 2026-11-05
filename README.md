# Azure Data Factory & Azure Databricks – End-to-End Data Engineering Assignment

## Project Overview

This project demonstrates an end-to-end data engineering pipeline using **Azure Data Factory (ADF), Azure Data Lake Storage Gen2 (ADLS Gen2), Azure Databricks, PySpark, and Delta Lake**.

The objective is to ingest, process, transform, and analyze Customer, Product, Store, and Sales datasets using the Medallion Architecture (Bronze, Silver, and Gold layers).

## Technologies Used

- Azure Data Factory (ADF)
- Azure Data Lake Storage Gen2 (ADLS Gen2)
- Azure Databricks
- Apache Spark / PySpark
- Delta Lake
- Python
- SQL
- Git & GitHub

## Project Architecture

The project follows the Medallion Architecture.

### 1. Bronze Layer – Raw Data

- Store raw source files from ADLS Gen2.
- Organize data into Customer, Product, Store, and Sales folders.
- Use Azure Data Factory to ingest the latest modified files.
- Maintain the original source data.

### 2. Silver Layer – Transformed Data

Perform data cleaning and transformations using PySpark.

**Customer Transformations**
- Convert column names into lowercase snake_case using a reusable UDF.
- Split customer names into first_name and last_name.
- Extract domain information from email addresses.
- Convert gender values into M and F.
- Separate joining date and time.
- Format dates as yyyy-MM-dd.
- Create expenditure_status based on the spent amount.
- Perform UPSERT operations using Delta Lake.

**Product Transformations**
- Standardize column names.
- Create sub_category based on category_id.
- Perform UPSERT operations.

**Store Transformations**
- Standardize column names.
- Extract store category from email addresses.
- Format created_at and updated_at dates.
- Perform UPSERT operations.

**Sales Transformations**
- Standardize column names.
- Process sales transaction data.
- Perform UPSERT operations into the customer_sales table.

### 3. Gold Layer – Business Analytics

- Join Product and Store datasets.
- Integrate the transformed data with Customer Sales.
- Select the required business and analytical columns.
- Create the final StoreProductSalesAnalysis dataset.
- Store the final output in Delta format using overwrite mode.

## Data Profiling

Data profiling is performed to understand the structure, quality, and characteristics of the source datasets.

The following checks are included:

- Total number of records and columns.
- Column names and data types.
- NULL and missing value identification.
- Duplicate record detection.
- Distinct value analysis.
- Minimum, maximum, and average values.
- Primary key and foreign key validation.
- Date and email format validation.
- Data quality checks.

## Azure Data Factory Pipeline

The ADF pipeline is designed to:

1. Identify the latest modified files from ADLS Gen2 folders.
2. Use dynamic pipeline parameters.
3. Configure source and destination datasets.
4. Copy files into the Bronze layer.
5. Process Customer, Product, Store, and Sales files dynamically.
6. Execute and validate the ingestion process.

## Project Folder Structure

```text
Azure_ADF_Assignment/
│
├── README.md
│
└── src/
    │
    └── ADF ASSIGNMENT-Gnanendra.pdf
```

## Data Lake Folder Structure

```text
ADLS Gen2/
│
├── Bronze/
│   ├── customer/
│   ├── product/
│   ├── store/
│   └── sales/
│
├── Silver/
│   └── sales_view/
│       ├── customer/
│       ├── product/
│       ├── store/
│       └── customer_sales/
│
└── Gold/
    └── sales_view/
        └── StoreProductSalesAnalysis/
```

## Key Concepts Covered

- Azure Data Factory Pipeline Development
- Dynamic Pipeline Parameterization
- Latest Modified File Processing
- ADLS Gen2 Integration
- Data Profiling and Data Quality
- PySpark Data Transformations
- User Defined Functions (UDFs)
- Delta Lake UPSERT and OVERWRITE Operations
- Medallion Architecture
- Data Integration and Analytical Dataset Creation

## Expected Final Output

**Gold Table:** `StoreProductSalesAnalysis`

The final dataset combines customer sales, product information, and store details to support business reporting and analytics.

## Author

**Gnanendra Reddy**

Azure Data Factory | Azure Databricks | PySpark | Data Engineering
