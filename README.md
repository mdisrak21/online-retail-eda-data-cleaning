# Online Retail — Exploratory Data Analysis & Data Integrity Cleaning

## Project Overview

This project was completed as part of an internship Task 2: **Exploratory Data Analysis & Integrity Cleaning Pipeline**.

The project focuses on loading a raw industry dataset, diagnosing data abnormalities, cleaning and preparing the data for analysis, treating outliers systematically, handling missing values, and generating descriptive visualizations to identify important patterns.

## Objective

- Load a large raw retail transaction dataset into Python/Pandas.
- Diagnose missing values, duplicates, cancellations, negative quantities, and invalid prices.
- Apply systematic data-cleaning treatments.
- Impute missing parameters where appropriate.
- Treat extreme observations using an IQR-based outlier filtering method.
- Generate descriptive statistics and visualizations.
- Produce a clean analytical dataset suitable for exploratory analysis.

## Dataset

**Dataset:** Online Retail II

**Source:** UCI Machine Learning Repository

**Dataset page:** https://archive.ics.uci.edu/dataset/502/online+retail+ii

The dataset contains real transaction records from a UK-based online retail business covering a two-year period.

## Tools & Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Jupyter Notebook

## Data Summary

The raw dataset contains:

- **1,067,371 records**
- **8 columns**
- Transaction information including invoice number, product code, description, quantity, invoice date, unit price, customer ID, and country.

## Data Quality Diagnosis

The following data abnormalities were identified:

| Data Quality Issue | Records |
|---|---:|
| Missing Description | 4,382 |
| Missing CustomerID | 243,007 |
| Exact duplicate rows | 34,335 |
| Cancellation invoices | 19,494 |
| Negative Quantity | 22,950 |
| UnitPrice <= 0 | 6,207 |

## Data Cleaning & Treatment

### Missing Description

Missing product descriptions were filled using the most common description associated with the same `StockCode`.

If no matching description was available, the value was labeled as `UNKNOWN_DESCRIPTION`.

### Missing CustomerID

Missing customer IDs were labeled as `UNKNOWN_CUSTOMER`.

Artificial customer IDs were not created because doing so could introduce false customer information into the dataset.

### Duplicate Records

Exact duplicate rows were identified during the data-quality audit.

### Cancellation Transactions

Invoices beginning with `C` were identified as cancellation transactions through the `IsCancellation` flag.

For the business-cleaned analytical view, cancellation invoices were excluded.

### Invalid Transactions

The analytical view excludes records with:

- Cancellation invoices
- Non-positive quantity
- Non-positive unit price
- Missing invoice date

A `Revenue` variable was also created:

`Revenue = Quantity × UnitPrice`

## Outlier Treatment

An IQR-based filtering method was applied separately to:

- Quantity
- UnitPrice
- Revenue

The standard IQR rule was used:

`Lower Bound = Q1 - 1.5 × IQR`

`Upper Bound = Q3 + 1.5 × IQR`

After applying the combined IQR filter:

- **Business-cleaned records:** 1,041,670
- **IQR-filtered analytical records:** 826,813
- **Records removed by IQR filtering:** 214,857
- **Percentage removed:** 20.63%

Extreme retail transactions were treated as statistical outliers for the analytical view; they were not automatically assumed to be data-entry errors.

## Exploratory Analysis & Visualizations

The project includes visualizations for:

1. Quantity distribution
2. Unit Price distribution
3. Revenue distribution after IQR filtering
4. Monthly revenue trend
5. Top 10 countries by revenue

Additional CSV summaries are included for descriptive statistics, monthly revenue, country-level revenue, and product-level revenue.

## Project Structure

```text
online-retail-eda-data-cleaning/
│
├── Progree_Task_2_Final.ipynb
├── Progree_Task_2_Final_Report.docx
├── README.md
│
├── data_quality_audit.csv
├── outlier_treatment_summary.csv
├── descriptive_statistics.csv
├── monthly_revenue.csv
├── top_countries_by_revenue.csv
├── top_products_by_revenue.csv
│
├── 01_quantity_distribution.png
├── 02_unit_price_distribution.png
├── 03_revenue_distribution_after_iqr.png
├── 04_monthly_revenue_trend.png
└── 05_top_countries_revenue.png
```
## How to Run

1. Clone or download this repository.
2. Open `Progree_Task_2_Final.ipynb` using Jupyter Notebook or JupyterLab.
3. Install the required Python libraries.
4. Place the original `online_retail_II.xlsx` dataset in the working directory if you want to rerun the complete notebook from the raw data.
5. Run the notebook cells sequentially.

## Project Scope

This repository focuses specifically on the internship Task 2:

**Exploratory Data Analysis & Integrity Cleaning Pipeline**

The project covers data loading, data-quality diagnosis, missing-value treatment, invalid-record handling, outlier filtering, descriptive statistics, and exploratory visualizations.

## Author

**Internship Project — Task 2**

