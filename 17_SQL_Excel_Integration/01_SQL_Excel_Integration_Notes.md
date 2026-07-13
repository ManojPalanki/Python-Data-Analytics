# SQL & Excel Integration with Python

## 1. Introduction

SQL & Excel Integration connects three important Data Analyst tools:

```text
SQL
+
Python / Pandas
+
Excel
```

The practical workflow is:

```text
SQL Database
    ↓
Retrieve Data with SQL
    ↓
Load Data into Pandas
    ↓
Inspect and Validate
    ↓
Clean and Transform
    ↓
Analyze Business Data
    ↓
Create Summary Reports
    ↓
Export Results to Excel
    ↓
Deliver Reports to Stakeholders
```

The most important topics are:

- Database Connections
- SQL Server Connection
- SQLAlchemy Basics
- Reading SQL Queries with Pandas
- Reading SQL Tables
- Parameterized Queries
- Data Validation
- Pandas Analysis
- Excel Export
- Multiple Excel Sheets
- Excel Formatting Basics
- Automated Report Generation
- Error Handling
- End-to-End Reporting Workflow

---

# 2. Why Integration Matters

Business data is often stored in databases.

Example:

```text
SQL Server Database

Tables:

Customers
Orders
Products
Sales
```

Stakeholders may want reports in:

```text
Excel
```

Python acts as the bridge.

```text
SQL Server
    ↓
Python
    ↓
Pandas
    ↓
Analysis
    ↓
Excel Report
```

This allows a Data Analyst to:

- Retrieve business data
- Automate repetitive reporting
- Analyze large datasets
- Create reusable workflows
- Generate stakeholder reports
- Reduce manual copy-paste work

---

# 3. Required Python Libraries

Common libraries:

```text
pandas

sqlalchemy

pyodbc

openpyxl
```

Install:

```powershell
pip install pandas sqlalchemy pyodbc openpyxl
```

Import:

```python
import pandas as pd

from sqlalchemy import create_engine
```

---

# 4. SQLAlchemy

SQLAlchemy helps Python communicate with databases.

Basic concept:

```text
Python
    ↓
SQLAlchemy
    ↓
Database Driver
    ↓
SQL Database
```

For SQL Server, a common driver is:

```text
ODBC Driver
```

---

# 5. Database Connection Workflow

```text
Import Libraries
    ↓
Define Connection Information
    ↓
Create Database Engine
    ↓
Test Connection
    ↓
Execute SQL Query
    ↓
Load Results into Pandas
```

---

# 6. SQL Server Connection

Example:

```python
import pandas as pd

from sqlalchemy import create_engine
```

Create connection string:

```python
server = "SERVER_NAME"

database = "DATABASE_NAME"
```

Create engine:

```python
engine = create_engine(

    f"mssql+pyodbc://@{server}/{database}"

    "?driver=ODBC+Driver+17+for+SQL+Server"

    "&trusted_connection=yes"
)
```

Important:

```text
SERVER_NAME

DATABASE_NAME

ODBC Driver Version
```

must match your computer and SQL Server configuration.

---

# 7. Example Local SQL Server Connection

```python
import pandas as pd

from sqlalchemy import create_engine


server = "localhost"

database = "SalesDatabase"


engine = create_engine(

    f"mssql+pyodbc://@{server}/{database}"

    "?driver=ODBC+Driver+17+for+SQL+Server"

    "&trusted_connection=yes"
)
```

---

# 8. Windows Authentication

If using Windows Authentication:

```python
engine = create_engine(

    f"mssql+pyodbc://@{server}/{database}"

    "?driver=ODBC+Driver+17+for+SQL+Server"

    "&trusted_connection=yes"
)
```

This uses your Windows credentials.

---

# 9. Username and Password Authentication

Example:

```python
username = "username"

password = "password"

server = "server_name"

database = "database_name"
```

```python
engine = create_engine(

    f"mssql+pyodbc://{username}:{password}"

    f"@{server}/{database}"

    "?driver=ODBC+Driver+17+for+SQL+Server"
)
```

Do not store real passwords directly in GitHub repositories.

Bad:

```python
password = "MyRealPassword123"
```

Better approaches include:

```text
Environment Variables

Configuration Files Excluded with .gitignore

Secret Management Tools
```

---

# 10. Test Database Connection

```python
from sqlalchemy import text
```

```python
with engine.connect() as connection:

    result = connection.execute(

        text("SELECT 1")

    )

    print(result.fetchone())
```

Expected result:

```text
(1,)
```

---

# 11. Read SQL Query with Pandas

Use:

```python
pd.read_sql()
```

Example:

```python
query = """

SELECT *

FROM Sales;

"""
```

```python
df = pd.read_sql(
    query,
    engine
)
```

Now SQL data is available as a Pandas DataFrame.

---

# 12. Read SQL Table

Use:

```python
pd.read_sql_table()
```

Example:

```python
df = pd.read_sql_table(
    "Sales",
    engine
)
```

This loads the complete SQL table.

---

# 13. read_sql() vs read_sql_table()

Use:

```text
pd.read_sql()
```

when:

```text
Executing SQL Queries
```

Use:

```text
pd.read_sql_table()
```

when:

```text
Loading an Entire Database Table
```

For Data Analyst work:

```text
pd.read_sql()
```

is usually more useful because you can control which data is retrieved.

---

# 14. Avoid SELECT *

This works:

```sql
SELECT *

FROM Sales;
```

But for real projects, prefer:

```sql
SELECT

    OrderID,

    OrderDate,

    CustomerID,

    ProductID,

    Quantity,

    Sales,

    Profit

FROM Sales;
```

Why?

```text
Retrieve Only Required Data

Reduce Memory Usage

Improve Query Readability

Improve Performance

Create Clear Data Requirements
```

---

# 15. Filter Data in SQL

Instead of loading everything into Pandas:

```sql
SELECT *

FROM Sales;
```

and filtering later:

```python
df = df[
    df["OrderDate"] >= "2026-01-01"
]
```

you can filter in SQL:

```sql
SELECT

    OrderID,

    OrderDate,

    CustomerID,

    Sales,

    Profit

FROM Sales

WHERE OrderDate >= '2026-01-01';
```

This reduces unnecessary data transfer.

---

# 16. SQL vs Pandas Responsibilities

A practical approach:

Use SQL for:

```text
Filtering Large Datasets

Joining Database Tables

Selecting Required Columns

Initial Aggregations

Database-Level Transformations
```

Use Pandas for:

```text
Further Cleaning

Flexible Analysis

Business Calculations

Report Generation

Excel Export

Automation
```

Do not retrieve millions of unnecessary rows from SQL just to filter them later in Pandas.

---

# 17. Read Query from SQL File

Instead of writing large SQL queries directly inside Python:

```python
query = """

SELECT ...

"""
```

save SQL in:

```text
sales_query.sql
```

Example SQL file:

```sql
SELECT

    o.OrderID,

    o.OrderDate,

    c.CustomerName,

    c.Region,

    p.ProductName,

    p.Category,

    o.Quantity,

    o.Sales,

    o.Profit

FROM Orders AS o

LEFT JOIN Customers AS c

    ON o.CustomerID = c.CustomerID

LEFT JOIN Products AS p

    ON o.ProductID = p.ProductID;
```

Read it:

```python
with open(
    "sales_query.sql",
    "r"
) as file:

    query = file.read()
```

Execute:

```python
df = pd.read_sql(
    query,
    engine
)
```

This creates better project organization.

---

# 18. Parameterized SQL Queries

Suppose you want data after a specific date.

Do not build SQL queries using unsafe string concatenation.

Use parameters.

Example:

```python
from sqlalchemy import text
```

```python
query = text("""

SELECT

    OrderID,

    OrderDate,

    CustomerID,

    Sales,

    Profit

FROM Sales

WHERE OrderDate >= :start_date

""")
```

Execute:

```python
df = pd.read_sql(

    query,

    engine,

    params={

        "start_date":
            "2026-01-01"

    }
)
```

Parameterized queries are safer and easier to maintain.

---

# 19. Retrieve Data from Multiple SQL Tables

SQL query:

```python
query = """

SELECT

    o.OrderID,

    o.OrderDate,

    c.CustomerID,

    c.CustomerName,

    c.Region,

    c.Segment,

    p.ProductID,

    p.ProductName,

    p.Category,

    o.Quantity,

    o.Sales,

    o.Profit

FROM Orders AS o

LEFT JOIN Customers AS c

    ON o.CustomerID = c.CustomerID

LEFT JOIN Products AS p

    ON o.ProductID = p.ProductID;

"""
```

Load:

```python
df = pd.read_sql(
    query,
    engine
)
```

---

# 20. Inspect SQL Data

Always inspect after retrieving data.

```python
df.head()
```

```python
df.shape
```

```python
df.info()
```

```python
df.dtypes
```

```python
df.isnull().sum()
```

```python
df.duplicated().sum()
```

Do not assume database data is automatically clean.

---

# 21. Validate SQL Data

Important checks:

```text
Row Count

Column Count

Missing Values

Duplicate Records

Data Types

Date Ranges

Unique Keys

Business Rules
```

Example:

```python
print(
    f"Rows: {df.shape[0]:,}"
)
```

```python
print(
    f"Columns: {df.shape[1]}"
)
```

```python
print(
    df.isnull().sum()
)
```

---

# 22. Check Date Range

```python
print(
    df["OrderDate"].min()
)
```

```python
print(
    df["OrderDate"].max()
)
```

This confirms whether the correct reporting period was retrieved.

---

# 23. Check Unique Orders

```python
total_orders = (
    df["OrderID"]
    .nunique()
)
```

Remember:

```text
Number of Rows

May Not Equal

Number of Orders
```

if one order contains multiple products.

---

# 24. Analyze SQL Data with Pandas

After retrieval:

```python
total_sales = (
    df["Sales"]
    .sum()
)
```

```python
total_profit = (
    df["Profit"]
    .sum()
)
```

```python
total_orders = (
    df["OrderID"]
    .nunique()
)
```

```python
total_customers = (
    df["CustomerID"]
    .nunique()
)
```

---

# 25. Calculate Profit Margin

```python
profit_margin = (

    total_profit

    /

    total_sales

    *

    100
)
```

---

# 26. Calculate Average Order Value

```python
average_order_value = (

    total_sales

    /

    total_orders
)
```

---

# 27. Create KPI Summary

```python
kpi_summary = pd.DataFrame({

    "KPI": [

        "Total Sales",

        "Total Profit",

        "Profit Margin",

        "Total Orders",

        "Total Customers",

        "Average Order Value"

    ],

    "Value": [

        total_sales,

        total_profit,

        profit_margin,

        total_orders,

        total_customers,

        average_order_value

    ]

})
```

---

# 28. Regional Analysis

```python
regional_analysis = (

    df

    .groupby(
        "Region"
    )

    .agg(

        Total_Sales=(
            "Sales",
            "sum"
        ),

        Total_Profit=(
            "Profit",
            "sum"
        ),

        Total_Orders=(
            "OrderID",
            "nunique"
        ),

        Total_Customers=(
            "CustomerID",
            "nunique"
        )

    )

    .reset_index()
)
```

---

# 29. Add Regional Profit Margin

```python
regional_analysis[
    "Profit_Margin"
] = (

    regional_analysis[
        "Total_Profit"
    ]

    /

    regional_analysis[
        "Total_Sales"
    ]

    *

    100
)
```

---

# 30. Product Analysis

```python
product_analysis = (

    df

    .groupby(
        "ProductName"
    )

    .agg(

        Total_Sales=(
            "Sales",
            "sum"
        ),

        Total_Profit=(
            "Profit",
            "sum"
        ),

        Total_Quantity=(
            "Quantity",
            "sum"
        )

    )

    .reset_index()

    .sort_values(

        "Total_Sales",

        ascending=False

    )
)
```

---

# 31. Top 10 Products

```python
top_products = (

    product_analysis

    .head(10)

)
```

---

# 32. Underperforming Products

```python
underperforming_products = (

    product_analysis[

        product_analysis[
            "Total_Profit"
        ]

        <

        0

    ]

    .sort_values(
        "Total_Profit"
    )
)
```

---

# 33. Export Data to Excel

Use:

```python
df.to_excel()
```

Example:

```python
df.to_excel(

    "sales_report.xlsx",

    index=False
)
```

Important:

```text
index=False
```

prevents Pandas from exporting the DataFrame index as an unnecessary Excel column.

---

# 34. Export Analysis Results

```python
regional_analysis.to_excel(

    "regional_analysis.xlsx",

    index=False
)
```

---

# 35. ExcelWriter

Use:

```python
pd.ExcelWriter()
```

when exporting multiple DataFrames into one Excel workbook.

Example:

```python
with pd.ExcelWriter(

    "business_report.xlsx",

    engine="openpyxl"

) as writer:

    df.to_excel(

        writer,

        sheet_name="Raw Data",

        index=False

    )

    regional_analysis.to_excel(

        writer,

        sheet_name="Regional Analysis",

        index=False

    )
```

---

# 36. Export Multiple Sheets

```python
with pd.ExcelWriter(

    "business_report.xlsx",

    engine="openpyxl"

) as writer:


    kpi_summary.to_excel(

        writer,

        sheet_name="KPI Summary",

        index=False

    )


    regional_analysis.to_excel(

        writer,

        sheet_name="Regional Analysis",

        index=False

    )


    product_analysis.to_excel(

        writer,

        sheet_name="Product Analysis",

        index=False

    )


    top_products.to_excel(

        writer,

        sheet_name="Top Products",

        index=False

    )


    underperforming_products.to_excel(

        writer,

        sheet_name="Underperformers",

        index=False

    )
```

---

# 37. Stakeholder Excel Report Structure

A useful workbook structure:

```text
Business_Report.xlsx

│

├── KPI Summary

├── Regional Analysis

├── Product Analysis

├── Customer Analysis

├── Monthly Performance

├── Top Products

├── Underperformers

└── Data Extract
```

Do not dump everything into one giant Excel sheet.

Separate reports based on business purpose.

---

# 38. Export Data Extract

```python
df.to_excel(

    writer,

    sheet_name="Data Extract",

    index=False
)
```

The Data Extract sheet provides detailed data supporting the report.

---

# 39. Read Excel with Pandas

Use:

```python
pd.read_excel()
```

Example:

```python
df = pd.read_excel(

    "sales_data.xlsx"
)
```

---

# 40. Read Specific Excel Sheet

```python
df = pd.read_excel(

    "business_report.xlsx",

    sheet_name="Regional Analysis"
)
```

---

# 41. Read Multiple Excel Sheets

```python
excel_data = pd.read_excel(

    "business_report.xlsx",

    sheet_name=None
)
```

This returns a dictionary of DataFrames.

Example:

```python
regional_data = excel_data[
    "Regional Analysis"
]
```

---

# 42. Write Multiple DataFrames to Excel

```python
reports = {

    "KPI Summary":
        kpi_summary,

    "Regional Analysis":
        regional_analysis,

    "Product Analysis":
        product_analysis

}
```

Export:

```python
with pd.ExcelWriter(

    "business_report.xlsx",

    engine="openpyxl"

) as writer:


    for sheet_name, dataframe in reports.items():


        dataframe.to_excel(

            writer,

            sheet_name=sheet_name,

            index=False

        )
```

This is cleaner when exporting many reports.

---

# 43. Basic Excel Formatting with openpyxl

Import:

```python
from openpyxl import load_workbook
```

Load workbook:

```python
workbook = load_workbook(

    "business_report.xlsx"
)
```

Select sheet:

```python
worksheet = workbook[
    "Regional Analysis"
]
```

---

# 44. Freeze Header Row

```python
worksheet.freeze_panes = "A2"
```

This keeps headers visible while scrolling.

---

# 45. Add Excel Filters

```python
worksheet.auto_filter.ref = (
    worksheet.dimensions
)
```

This adds filtering functionality to the Excel report.

---

# 46. Adjust Column Width

```python
for column_cells in worksheet.columns:

    max_length = 0

    column_letter = (
        column_cells[0]
        .column_letter
    )


    for cell in column_cells:

        if cell.value is not None:

            max_length = max(

                max_length,

                len(
                    str(
                        cell.value
                    )
                )

            )


    worksheet.column_dimensions[
        column_letter
    ].width = (

        max_length

        +

        2
    )
```

---

# 47. Apply Formatting to All Sheets

```python
from openpyxl import load_workbook


workbook = load_workbook(

    "business_report.xlsx"
)


for worksheet in workbook.worksheets:


    worksheet.freeze_panes = "A2"


    worksheet.auto_filter.ref = (

        worksheet.dimensions

    )


    for column_cells in worksheet.columns:


        max_length = 0


        column_letter = (

            column_cells[0]
            .column_letter

        )


        for cell in column_cells:


            if cell.value is not None:


                max_length = max(

                    max_length,

                    len(
                        str(
                            cell.value
                        )
                    )

                )


        worksheet.column_dimensions[
            column_letter
        ].width = (

            min(
                max_length + 2,

                40
            )

        )


workbook.save(

    "business_report.xlsx"
)
```

---

# 48. Why Limit Column Width?

Without a limit:

```text
One Very Long Value

Can Create

An Extremely Wide Excel Column
```

Use:

```python
min(
    max_length + 2,
    40
)
```

to limit maximum width.

---

# 49. Automated Report Generation

Manual workflow:

```text
Open SQL Server

Run Query

Copy Data

Open Excel

Paste Data

Create Calculations

Create Reports

Save Workbook
```

Automated workflow:

```text
Run Python Script
    ↓
Connect to SQL Server
    ↓
Execute Query
    ↓
Load Data into Pandas
    ↓
Validate Data
    ↓
Analyze Data
    ↓
Generate Reports
    ↓
Export Excel Workbook
    ↓
Format Workbook
    ↓
Save Final Report
```

This is the main purpose of this module.

---

# 50. Create Output Folder

```python
from pathlib import Path
```

```python
output_folder = Path(

    "reports"

)
```

```python
output_folder.mkdir(

    exist_ok=True
)
```

Create output path:

```python
output_file = (

    output_folder

    /

    "business_report.xlsx"
)
```

---

# 51. Add Report Date to Filename

```python
from datetime import datetime
```

```python
report_date = (

    datetime.now()

    .strftime(
        "%Y-%m-%d"
    )
)
```

```python
output_file = (

    output_folder

    /

    f"business_report_{report_date}.xlsx"
)
```

Example:

```text
business_report_2026-07-13.xlsx
```

---

# 52. Create Reusable SQL Function

```python
def load_sql_data(

    query,

    engine

):

    dataframe = pd.read_sql(

        query,

        engine

    )

    return dataframe
```

Use:

```python
df = load_sql_data(

    query,

    engine

)
```

---

# 53. Create Reusable Analysis Function

```python
def create_regional_analysis(

    dataframe

):

    result = (

        dataframe

        .groupby(
            "Region"
        )

        .agg(

            Total_Sales=(
                "Sales",
                "sum"
            ),

            Total_Profit=(
                "Profit",
                "sum"
            ),

            Total_Orders=(
                "OrderID",
                "nunique"
            )

        )

        .reset_index()

    )


    result[
        "Profit_Margin"
    ] = (

        result[
            "Total_Profit"
        ]

        /

        result[
            "Total_Sales"
        ]

        *

        100

    )


    return result
```

---

# 54. Create Reusable Excel Export Function

```python
def export_reports(

    reports,

    output_file

):


    with pd.ExcelWriter(

        output_file,

        engine="openpyxl"

    ) as writer:


        for sheet_name, dataframe in reports.items():


            dataframe.to_excel(

                writer,

                sheet_name=sheet_name,

                index=False

            )
```

Use:

```python
reports = {

    "KPI Summary":
        kpi_summary,

    "Regional Analysis":
        regional_analysis,

    "Product Analysis":
        product_analysis

}
```

```python
export_reports(

    reports,

    output_file

)
```

---

# 55. Error Handling

Database connections can fail.

File exports can fail.

Queries can fail.

Use:

```python
try:
```

```python
except:
```

Example:

```python
try:


    df = pd.read_sql(

        query,

        engine

    )


    print(

        "Data retrieved successfully."

    )


except Exception as error:


    print(

        f"Error: {error}"

    )
```

---

# 56. Better Error Handling Workflow

```python
try:


    print(

        "Connecting to database..."

    )


    df = pd.read_sql(

        query,

        engine

    )


    print(

        f"{len(df):,} rows retrieved."

    )


except Exception as error:


    print(

        "Database operation failed."

    )


    print(

        error

    )


    raise
```

Using:

```python
raise
```

stops execution instead of continuing with missing or incorrect data.

---

# 57. Validate Before Export

Before generating the stakeholder report:

```python
if df.empty:

    raise ValueError(

        "SQL query returned no data."

    )
```

Check required columns:

```python
required_columns = {

    "OrderID",

    "CustomerID",

    "Sales",

    "Profit"

}
```

```python
missing_columns = (

    required_columns

    -

    set(
        df.columns
    )
)
```

```python
if missing_columns:

    raise ValueError(

        f"Missing columns: {missing_columns}"

    )
```

---

# 58. Complete End-to-End Workflow

```python
import pandas as pd

from pathlib import Path

from datetime import datetime

from sqlalchemy import create_engine


# DATABASE CONFIGURATION

server = "SERVER_NAME"

database = "DATABASE_NAME"


# CREATE ENGINE

engine = create_engine(

    f"mssql+pyodbc://@{server}/{database}"

    "?driver=ODBC+Driver+17+for+SQL+Server"

    "&trusted_connection=yes"
)


# SQL QUERY

query = """

SELECT

    o.OrderID,

    o.OrderDate,

    c.CustomerID,

    c.CustomerName,

    c.Region,

    c.Segment,

    p.ProductID,

    p.ProductName,

    p.Category,

    o.Quantity,

    o.Sales,

    o.Profit

FROM Orders AS o

LEFT JOIN Customers AS c

    ON o.CustomerID = c.CustomerID

LEFT JOIN Products AS p

    ON o.ProductID = p.ProductID;

"""


# RETRIEVE DATA

df = pd.read_sql(

    query,

    engine

)


# VALIDATE DATA

if df.empty:

    raise ValueError(

        "SQL query returned no data."

    )


# CALCULATE KPIs

total_sales = (

    df["Sales"]

    .sum()
)

total_profit = (

    df["Profit"]

    .sum()
)

total_orders = (

    df["OrderID"]

    .nunique()
)

total_customers = (

    df["CustomerID"]

    .nunique()
)

profit_margin = (

    total_profit

    /

    total_sales

    *

    100
)

average_order_value = (

    total_sales

    /

    total_orders
)


# KPI SUMMARY

kpi_summary = pd.DataFrame({

    "KPI": [

        "Total Sales",

        "Total Profit",

        "Profit Margin",

        "Total Orders",

        "Total Customers",

        "Average Order Value"

    ],

    "Value": [

        total_sales,

        total_profit,

        profit_margin,

        total_orders,

        total_customers,

        average_order_value

    ]

})


# REGIONAL ANALYSIS

regional_analysis = (

    df

    .groupby(
        "Region"
    )

    .agg(

        Total_Sales=(
            "Sales",
            "sum"
        ),

        Total_Profit=(
            "Profit",
            "sum"
        ),

        Total_Orders=(
            "OrderID",
            "nunique"
        ),

        Total_Customers=(
            "CustomerID",
            "nunique"
        )

    )

    .reset_index()
)


regional_analysis[
    "Profit_Margin"
] = (

    regional_analysis[
        "Total_Profit"
    ]

    /

    regional_analysis[
        "Total_Sales"
    ]

    *

    100
)


# PRODUCT ANALYSIS

product_analysis = (

    df

    .groupby(
        "ProductName"
    )

    .agg(

        Total_Sales=(
            "Sales",
            "sum"
        ),

        Total_Profit=(
            "Profit",
            "sum"
        ),

        Total_Quantity=(
            "Quantity",
            "sum"
        )

    )

    .reset_index()

    .sort_values(

        "Total_Sales",

        ascending=False

    )
)


# TOP PRODUCTS

top_products = (

    product_analysis

    .head(10)

)


# UNDERPERFORMERS

underperformers = (

    product_analysis[

        product_analysis[
            "Total_Profit"
        ]

        <

        0

    ]

    .sort_values(
        "Total_Profit"
    )
)


# OUTPUT DIRECTORY

output_folder = Path(

    "reports"

)


output_folder.mkdir(

    exist_ok=True
)


# REPORT DATE

report_date = (

    datetime.now()

    .strftime(
        "%Y-%m-%d"
    )
)


# OUTPUT FILE

output_file = (

    output_folder

    /

    f"business_report_{report_date}.xlsx"
)


# REPORTS

reports = {

    "KPI Summary":
        kpi_summary,

    "Regional Analysis":
        regional_analysis,

    "Product Analysis":
        product_analysis,

    "Top Products":
        top_products,

    "Underperformers":
        underperformers,

    "Data Extract":
        df

}


# EXPORT EXCEL REPORT

with pd.ExcelWriter(

    output_file,

    engine="openpyxl"

) as writer:


    for sheet_name, dataframe in reports.items():


        dataframe.to_excel(

            writer,

            sheet_name=sheet_name,

            index=False

        )


print(

    f"Report created successfully: {output_file}"

)
```

---

# 59. Recommended Project Folder Structure

```text
17_SQL_Excel_Integration/

│

├── SQL_Excel_Integration_Notes.md

├── SQL_Excel_Integration_Practice.ipynb

├── SQL_Excel_Integration_Assessment.ipynb

│

├── queries/

│   └── sales_analysis.sql

│

├── reports/

│   └── business_report.xlsx

│

└── README.md
```

Do not upload real database credentials.

Add sensitive files to:

```text
.gitignore
```

---

# 60. Common Beginner Errors

## Hardcoding Passwords

Wrong:

```python
password = "real_password"
```

Never push database passwords to GitHub.

---

## Loading the Entire Database

Weak:

```sql
SELECT *

FROM HugeSalesTable;
```

Better:

```sql
SELECT

    RequiredColumns

FROM HugeSalesTable

WHERE OrderDate >= '2026-01-01';
```

---

## Filtering Everything in Pandas

Weak workflow:

```text
SQL
    ↓
Load 10 Million Rows
    ↓
Filter to 50,000 Rows in Pandas
```

Better:

```text
SQL
    ↓
Filter Required Data
    ↓
Load 50,000 Rows into Pandas
```

---

## Assuming SQL Data Is Clean

Always validate:

```python
df.info()

df.isnull().sum()

df.duplicated().sum()
```

---

## Exporting Everything to One Excel Sheet

Better:

```text
KPI Summary

Regional Analysis

Product Analysis

Underperformers

Data Extract
```

---

## Forgetting index=False

Weak:

```python
df.to_excel(
    "report.xlsx"
)
```

Better:

```python
df.to_excel(
    "report.xlsx",
    index=False
)
```

---

## Incorrect Order Counts

Wrong:

```python
df["OrderID"].count()
```

when orders contain multiple rows.

Better:

```python
df["OrderID"].nunique()
```

---

## No Validation Before Report Generation

Never automate:

```text
Retrieve Data
    ↓
Immediately Send Report
```

Use:

```text
Retrieve
    ↓
Validate
    ↓
Analyze
    ↓
Validate Results
    ↓
Export
```

---

# 61. Interview Questions

1. How do you connect Python to SQL Server?
2. What is SQLAlchemy?
3. What is pyodbc?
4. How do you create a SQLAlchemy engine?
5. How do you test a database connection?
6. What does `pd.read_sql()` do?
7. What does `pd.read_sql_table()` do?
8. What is the difference between `read_sql()` and `read_sql_table()`?
9. Why should you avoid `SELECT *`?
10. Should filtering be done in SQL or Pandas?
11. How do you read a SQL query from a `.sql` file?
12. What is a parameterized SQL query?
13. Why should you use parameterized queries?
14. How do you retrieve data from multiple SQL tables?
15. What should you validate after retrieving SQL data?
16. How do you calculate Total Sales?
17. How do you calculate Profit Margin?
18. How do you calculate Average Order Value?
19. Why should `nunique()` be used for order counts?
20. How do you export a DataFrame to Excel?
21. Why should you use `index=False`?
22. What is `ExcelWriter`?
23. How do you export multiple DataFrames to multiple Excel sheets?
24. How do you read a specific Excel sheet?
25. How do you read all Excel sheets?
26. What is openpyxl?
27. How do you freeze the header row in Excel?
28. How do you add filters to an Excel report?
29. How do you automatically adjust Excel column widths?
30. How would you structure a stakeholder Excel report?
31. How do you create reusable report-generation functions?
32. How do you handle database connection errors?
33. Why should an automated report validate data before exporting?
34. How do you check whether a SQL query returned no data?
35. How do you validate required columns?
36. How would you automate SQL-to-Excel reporting?
37. Why should passwords not be stored in Python scripts?
38. How do you prevent database credentials from being pushed to GitHub?
39. What tasks should SQL handle versus Pandas?
40. Explain an end-to-end SQL Server → Pandas → Excel reporting workflow.

---

# 62. Completion Checklist

Before moving to Python Automation, you should be able to:

- [ ] Explain the SQL → Pandas → Excel workflow
- [ ] Install required libraries
- [ ] Understand SQLAlchemy basics
- [ ] Understand pyodbc basics
- [ ] Create a SQL Server connection
- [ ] Use Windows Authentication
- [ ] Understand username/password authentication
- [ ] Avoid hardcoding credentials
- [ ] Test a database connection
- [ ] Use `pd.read_sql()`
- [ ] Use `pd.read_sql_table()`
- [ ] Explain `read_sql()` vs `read_sql_table()`
- [ ] Avoid unnecessary `SELECT *`
- [ ] Filter large data in SQL
- [ ] Understand SQL vs Pandas responsibilities
- [ ] Store queries in `.sql` files
- [ ] Read SQL queries from files
- [ ] Use parameterized SQL queries
- [ ] Retrieve data from multiple SQL tables
- [ ] Inspect retrieved data
- [ ] Validate row counts
- [ ] Validate missing values
- [ ] Validate duplicates
- [ ] Validate data types
- [ ] Validate date ranges
- [ ] Count unique orders correctly
- [ ] Analyze SQL data using Pandas
- [ ] Calculate Total Sales
- [ ] Calculate Total Profit
- [ ] Calculate Profit Margin
- [ ] Calculate Average Order Value
- [ ] Create KPI summaries
- [ ] Create regional analysis
- [ ] Create product analysis
- [ ] Identify Top 10 products
- [ ] Identify underperforming products
- [ ] Export DataFrames to Excel
- [ ] Use `index=False`
- [ ] Use `ExcelWriter`
- [ ] Export multiple sheets
- [ ] Create stakeholder-friendly workbook structures
- [ ] Read Excel files
- [ ] Read specific Excel sheets
- [ ] Read multiple Excel sheets
- [ ] Use openpyxl basics
- [ ] Freeze Excel headers
- [ ] Add Excel filters
- [ ] Adjust column widths
- [ ] Create output folders
- [ ] Add dates to report filenames
- [ ] Create reusable SQL functions
- [ ] Create reusable analysis functions
- [ ] Create reusable Excel export functions
- [ ] Handle database errors
- [ ] Validate data before exporting
- [ ] Generate an end-to-end automated Excel report
- [ ] Organize an integration project properly

---

# Final Outcome

After completing SQL & Excel Integration, you should be able to connect Python to SQL Server, retrieve database tables and query results using Pandas, validate and analyze SQL data, calculate business KPIs, generate regional and product reports, export analysis results to Excel, create multiple-sheet stakeholder workbooks, apply basic Excel formatting, handle database and reporting errors, and build an end-to-end SQL Server → Pandas → Excel automated reporting workflow.

The core skill is:

```text
SQL Server
    ↓
Retrieve Only Required Data
    ↓
Pandas
    ↓
Validate
    ↓
Analyze
    ↓
Generate Business Reports
    ↓
Excel
    ↓
Deliver to Stakeholders
```