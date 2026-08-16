# Enterprise Data Reconciliation & Analytics

An end-to-end data reconciliation and analytics project that integrates structured and unstructured data sources, performs financial reconciliation, and generates business insights using Python and SQL.

## Project Overview

This project focuses on integrating data from multiple enterprise sources and transforming it into a clean, reconciled, and analysis-ready dataset.

The project uses three primary data sources:

- A SQLite database containing user information and status records
- Server logs containing unstructured transaction information
- Daily EUR-to-USD exchange-rate data

The processed data is used to identify active users, extract transaction details, convert EUR transactions into USD, calculate revenue, and generate business insights through aggregation and visualization.

## Objectives

- Identify users whose latest recorded status is Active.
- Extract transaction information from unstructured server logs.
- Handle missing exchange-rate dates.
- Convert EUR transaction values into USD.
- Integrate user, transaction, and exchange-rate datasets.
- Calculate monthly USD revenue.
- Identify the top five customers by total USD revenue.
- Generate visualizations to support financial analysis.

## Technology Stack

| Technology | Purpose |
|------------|---------|
| Python | Data processing and analysis |
| SQL | Database querying and data extraction |
| SQLite | User and status data storage |
| Pandas | Data cleaning, transformation, merging, and aggregation |
| Regular Expressions (Regex) | Extracting structured information from server logs |
| Matplotlib | Data visualization |
| Seaborn | Data visualization |
| Jupyter Notebook | Development and analysis environment |
| VS Code | Code development and project execution |

## Project Workflow

The project is implemented in four phases.

### Phase 1: SQL Extraction

The first phase focuses on identifying users whose most recent status is Active.

SQL window functions, specifically `ROW_NUMBER()`, are used to:

1. Partition status records by user.
2. Order records by their update timestamp.
3. Identify the latest status record for each user.
4. Filter the results to retain only users whose latest status is Active.

The resulting data is stored in the `df_active_users` DataFrame.

### Phase 2: Regex and Unstructured Data Processing

The second phase processes transaction information stored as unstructured server-log text.

Python Regular Expressions are used to extract:

- Date
- User ID
- Product ID
- EUR transaction value

The server log contains 100,001 total records, including 94,902 INFO records used for transaction extraction.

The extracted information is converted into a structured Pandas DataFrame named `extracted_data`.

### Phase 3: Financial Reconciliation and Data Integration

The third phase integrates transaction data with daily EUR-to-USD exchange rates.

Missing exchange-rate dates are handled using forward filling (`ffill`) so that the most recent available exchange rate is carried forward.

The transaction data is then merged with the exchange-rate data using the transaction date.

USD revenue is calculated using:

```text
USD Revenue = EUR Value × EUR-to-USD Exchange Rate
