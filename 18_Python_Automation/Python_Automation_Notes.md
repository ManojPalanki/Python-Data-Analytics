# Automation with Python

## 1. Introduction

Python Automation means using Python scripts to perform repetitive tasks automatically.

For a Data Analyst, the goal is not complex software automation.

The goal is:

```text
Manual Repetitive Task
        ↓
Identify Repeatable Steps
        ↓
Build Python Workflow
        ↓
Validate Inputs
        ↓
Process Data
        ↓
Generate Outputs
        ↓
Log Execution
        ↓
Handle Errors
        ↓
Repeat Automatically
```

The most important topics are:

- Batch Processing
- File Automation
- Folder Automation
- CSV Processing
- Excel Processing
- Report Automation
- KPI Report Generation
- Monthly Summary Generation
- Exporting Cleaned Datasets
- Logging
- Error Handling
- Reusable Functions
- Automated Data Pipelines

---

# 2. Why Automation Matters for Data Analysts

Many analysts repeatedly perform tasks such as:

```text
Download Files

Open CSV Files

Combine Data

Clean Data

Calculate KPIs

Create Reports

Export Excel Files

Rename Files

Move Files

Generate Monthly Summaries
```

Manual workflow:

```text
Open File
    ↓
Clean Data
    ↓
Calculate KPIs
    ↓
Create Report
    ↓
Export Results
    ↓
Repeat Next Month
```

Automated workflow:

```text
Run Python Script
    ↓
Find Input Files
    ↓
Load Data
    ↓
Validate Data
    ↓
Clean Data
    ↓
Combine Data
    ↓
Calculate KPIs
    ↓
Generate Reports
    ↓
Export Results
    ↓
Create Logs
```

---

# 3. Core Python Libraries

```python
import pandas as pd

from pathlib import Path

import logging

from datetime import datetime
```

Main purposes:

```text
pandas
→ Data Processing and Analysis

pathlib
→ File and Folder Operations

logging
→ Execution and Error Logs

datetime
→ Dates and Report Filenames
```

---

# 4. pathlib

`pathlib` is used to work with files and folders.

Import:

```python
from pathlib import Path
```

Create a path:

```python
data_folder = Path(
    "data"
)
```

---

# 5. Create Folders Automatically

```python
output_folder = Path(
    "output"
)
```

```python
output_folder.mkdir(
    exist_ok=True
)
```

If the folder already exists:

```text
exist_ok=True
```

prevents an error.

---

# 6. Create Nested Folders

```python
output_folder = Path(
    "reports/monthly"
)
```

```python
output_folder.mkdir(
    parents=True,
    exist_ok=True
)
```

`parents=True` creates missing parent folders.

---

# 7. Check Whether a File Exists

```python
file_path = Path(
    "data/sales.csv"
)
```

```python
file_path.exists()
```

Example:

```python
if file_path.exists():

    print(
        "File found."
    )

else:

    print(
        "File not found."
    )
```

---

# 8. Check Whether Path Is a File

```python
file_path.is_file()
```

---

# 9. Check Whether Path Is a Directory

```python
data_folder.is_dir()
```

---

# 10. Find Files in a Folder

Use:

```python
glob()
```

Example:

```python
csv_files = list(

    data_folder.glob(
        "*.csv"
    )

)
```

This finds all CSV files in the folder.

---

# 11. Find Files Recursively

Use:

```python
rglob()
```

Example:

```python
csv_files = list(

    data_folder.rglob(
        "*.csv"
    )

)
```

Difference:

```text
glob()
→ Current Folder

rglob()
→ Current Folder and Subfolders
```

---

# 12. Loop Through Multiple Files

```python
for file in csv_files:

    print(
        file
    )
```

This is the foundation of batch processing.

---

# 13. Batch Processing

Batch Processing means processing multiple files automatically.

Example:

```text
sales_january.csv

sales_february.csv

sales_march.csv

sales_april.csv
```

Instead of:

```text
Open January

Process January

Open February

Process February

Open March

Process March
```

use:

```text
Find All Files
    ↓
Loop Through Files
    ↓
Process Each File
    ↓
Combine Results
```

---

# 14. Process Multiple CSV Files

```python
from pathlib import Path

import pandas as pd


data_folder = Path(
    "data"
)


csv_files = list(

    data_folder.glob(
        "*.csv"
    )

)


dataframes = []


for file in csv_files:


    df = pd.read_csv(
        file
    )


    dataframes.append(
        df
    )
```

---

# 15. Combine Multiple CSV Files

```python
combined_data = pd.concat(

    dataframes,

    ignore_index=True

)
```

Complete workflow:

```python
from pathlib import Path

import pandas as pd


data_folder = Path(
    "data"
)


csv_files = list(

    data_folder.glob(
        "*.csv"
    )

)


dataframes = []


for file in csv_files:


    df = pd.read_csv(
        file
    )


    dataframes.append(
        df
    )


combined_data = pd.concat(

    dataframes,

    ignore_index=True

)
```

---

# 16. Better Batch Processing

Before combining files, check whether files exist.

```python
if not csv_files:

    raise FileNotFoundError(

        "No CSV files found."

    )
```

Complete:

```python
csv_files = list(

    data_folder.glob(
        "*.csv"
    )

)


if not csv_files:

    raise FileNotFoundError(

        "No CSV files found."

    )
```

---

# 17. Add Source Filename

When combining files, it is useful to know where each row came from.

```python
for file in csv_files:


    df = pd.read_csv(
        file
    )


    df[
        "source_file"
    ] = file.name


    dataframes.append(
        df
    )
```

This creates:

```text
source_file
```

Example values:

```text
sales_january.csv

sales_february.csv

sales_march.csv
```

This is useful for:

```text
Debugging

Data Validation

Audit Tracking

Finding Incorrect Source Files
```

---

# 18. Automated Data Cleaning

Create a reusable function:

```python
def clean_sales_data(
    dataframe
):


    dataframe = dataframe.copy()


    dataframe.columns = (

        dataframe.columns

        .str.strip()

        .str.lower()

        .str.replace(
            " ",
            "_"
        )

    )


    dataframe = (

        dataframe

        .drop_duplicates()

    )


    dataframe[
        "order_date"
    ] = pd.to_datetime(

        dataframe[
            "order_date"
        ],

        errors="coerce"

    )


    return dataframe
```

---

# 19. Why Use Functions for Automation?

Weak approach:

```text
Copy Code

Paste Code

Change File

Run Again
```

Better:

```text
Create Function Once

Reuse Function Many Times
```

Example:

```python
cleaned_data = clean_sales_data(
    combined_data
)
```

---

# 20. Process and Clean Multiple Files

```python
dataframes = []


for file in csv_files:


    df = pd.read_csv(
        file
    )


    df[
        "source_file"
    ] = file.name


    df = clean_sales_data(
        df
    )


    dataframes.append(
        df
    )


combined_data = pd.concat(

    dataframes,

    ignore_index=True

)
```

---

# 21. Validate Required Columns

Automation should not blindly process incorrect files.

Define:

```python
required_columns = {

    "order_id",

    "order_date",

    "customer_id",

    "sales",

    "profit"

}
```

Check:

```python
missing_columns = (

    required_columns

    -

    set(
        df.columns
    )

)
```

Raise error:

```python
if missing_columns:

    raise ValueError(

        f"Missing columns: {missing_columns}"

    )
```

---

# 22. Create Validation Function

```python
def validate_data(
    dataframe
):


    required_columns = {

        "order_id",

        "order_date",

        "customer_id",

        "sales",

        "profit"

    }


    missing_columns = (

        required_columns

        -

        set(
            dataframe.columns
        )

    )


    if missing_columns:

        raise ValueError(

            f"Missing columns: {missing_columns}"

        )


    if dataframe.empty:

        raise ValueError(

            "Dataset is empty."

        )
```

Use:

```python
validate_data(
    df
)
```

---

# 23. Export Cleaned Datasets

Create folder:

```python
cleaned_folder = Path(
    "output/cleaned_data"
)
```

```python
cleaned_folder.mkdir(

    parents=True,

    exist_ok=True

)
```

Export:

```python
combined_data.to_csv(

    cleaned_folder
    /
    "cleaned_sales_data.csv",

    index=False

)
```

---

# 24. Automate Individual File Cleaning

```python
for file in csv_files:


    df = pd.read_csv(
        file
    )


    df = clean_sales_data(
        df
    )


    output_file = (

        cleaned_folder

        /

        f"cleaned_{file.name}"

    )


    df.to_csv(

        output_file,

        index=False

    )
```

Workflow:

```text
Raw Files
    ↓
Loop
    ↓
Clean Each File
    ↓
Export Each Cleaned File
```

---

# 25. Report Automation

Report Automation means automatically:

```text
Load Data

Clean Data

Calculate KPIs

Create Summaries

Export Reports
```

Example:

```text
Monthly Sales Files
        ↓
Python Script
        ↓
Combined Dataset
        ↓
KPI Calculation
        ↓
Regional Analysis
        ↓
Product Analysis
        ↓
Excel Report
```

---

# 26. Create KPI Report Function

```python
def calculate_kpis(
    dataframe
):


    total_sales = (

        dataframe[
            "sales"
        ]

        .sum()

    )


    total_profit = (

        dataframe[
            "profit"
        ]

        .sum()

    )


    total_orders = (

        dataframe[
            "order_id"
        ]

        .nunique()

    )


    total_customers = (

        dataframe[
            "customer_id"
        ]

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


    return pd.DataFrame({

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

# 27. Generate KPI Report

```python
kpi_report = calculate_kpis(

    combined_data

)
```

Export:

```python
kpi_report.to_excel(

    "output/kpi_report.xlsx",

    index=False

)
```

---

# 28. Automated Regional Summary

```python
def create_regional_summary(
    dataframe
):


    regional_summary = (

        dataframe

        .groupby(
            "region"
        )

        .agg(

            total_sales=(
                "sales",
                "sum"
            ),

            total_profit=(
                "profit",
                "sum"
            ),

            total_orders=(
                "order_id",
                "nunique"
            ),

            total_customers=(
                "customer_id",
                "nunique"
            )

        )

        .reset_index()

    )


    regional_summary[
        "profit_margin"
    ] = (

        regional_summary[
            "total_profit"
        ]

        /

        regional_summary[
            "total_sales"
        ]

        *

        100

    )


    return regional_summary
```

---

# 29. Automated Product Summary

```python
def create_product_summary(
    dataframe
):


    return (

        dataframe

        .groupby(
            "product_name"
        )

        .agg(

            total_sales=(
                "sales",
                "sum"
            ),

            total_profit=(
                "profit",
                "sum"
            ),

            total_quantity=(
                "quantity",
                "sum"
            )

        )

        .reset_index()

        .sort_values(

            "total_sales",

            ascending=False

        )

    )
```

---

# 30. Monthly Summary Generation

Convert date:

```python
combined_data[
    "order_date"
] = pd.to_datetime(

    combined_data[
        "order_date"
    ]
)
```

Create month:

```python
combined_data[
    "order_month"
] = (

    combined_data[
        "order_date"
    ]

    .dt.to_period(
        "M"
    )

)
```

Generate summary:

```python
monthly_summary = (

    combined_data

    .groupby(
        "order_month"
    )

    .agg(

        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        ),

        total_orders=(
            "order_id",
            "nunique"
        ),

        total_customers=(
            "customer_id",
            "nunique"
        )

    )

    .reset_index()

)
```

---

# 31. Convert Period to String

Before exporting:

```python
monthly_summary[
    "order_month"
] = (

    monthly_summary[
        "order_month"
    ]

    .astype(str)

)
```

---

# 32. Export Automated Excel Report

```python
with pd.ExcelWriter(

    "output/business_report.xlsx",

    engine="openpyxl"

) as writer:


    kpi_report.to_excel(

        writer,

        sheet_name="KPI Summary",

        index=False

    )


    monthly_summary.to_excel(

        writer,

        sheet_name="Monthly Summary",

        index=False

    )


    regional_summary.to_excel(

        writer,

        sheet_name="Regional Summary",

        index=False

    )


    product_summary.to_excel(

        writer,

        sheet_name="Product Summary",

        index=False

    )
```

---

# 33. Dynamic Report Filenames

Avoid overwriting old reports.

Import:

```python
from datetime import datetime
```

Create date:

```python
report_date = (

    datetime.now()

    .strftime(
        "%Y-%m-%d"
    )

)
```

Create filename:

```python
report_file = (

    Path(
        "output"
    )

    /

    f"business_report_{report_date}.xlsx"

)
```

Example:

```text
business_report_2026-07-13.xlsx
```

---

# 34. Logging

`logging` records what happens when the automation runs.

Import:

```python
import logging
```

Basic configuration:

```python
logging.basicConfig(

    level=logging.INFO

)
```

Write log:

```python
logging.info(

    "Automation started."

)
```

---

# 35. Why Logging Matters

`print()`:

```text
Displays Messages
```

`logging`:

```text
Records Execution Information

Records Errors

Records Warnings

Creates Audit History

Helps Debug Automation
```

For automation:

```text
logging > print
```

---

# 36. Logging Levels

Important logging levels:

```text
DEBUG

INFO

WARNING

ERROR

CRITICAL
```

Examples:

```python
logging.info(

    "Data loaded successfully."

)
```

```python
logging.warning(

    "Missing values detected."

)
```

```python
logging.error(

    "File processing failed."

)
```

---

# 37. Create Log File

```python
logging.basicConfig(

    filename="automation.log",

    level=logging.INFO,

    format=(

        "%(asctime)s - "

        "%(levelname)s - "

        "%(message)s"

    )

)
```

Example log:

```text
2026-07-13 10:00:00 - INFO - Automation started.

2026-07-13 10:00:01 - INFO - Files loaded successfully.

2026-07-13 10:00:02 - INFO - Data cleaning completed.

2026-07-13 10:00:03 - INFO - Report generated successfully.
```

---

# 38. Logging File Processing

```python
for file in csv_files:


    logging.info(

        f"Processing file: {file.name}"

    )


    df = pd.read_csv(
        file
    )


    logging.info(

        f"{len(df):,} rows loaded."

    )
```

---

# 39. Error Handling in Automation

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


    df = pd.read_csv(
        file
    )


    logging.info(

        f"Successfully processed {file.name}"

    )


except Exception as error:


    logging.error(

        f"Failed to process {file.name}: {error}"

    )
```

---

# 40. Continue Processing After File Error

Suppose:

```text
January File
→ Success

February File
→ Error

March File
→ Success
```

You may want the automation to continue.

Example:

```python
for file in csv_files:


    try:


        df = pd.read_csv(
            file
        )


        dataframes.append(
            df
        )


    except Exception as error:


        logging.error(

            f"Failed: {file.name} - {error}"

        )


        continue
```

---

# 41. Stop Automation for Critical Errors

Some errors should stop execution.

Example:

```python
if not csv_files:

    logging.critical(

        "No input files found."

    )


    raise FileNotFoundError(

        "No input files found."

    )
```

---

# 42. finally

`finally` executes whether an error occurs or not.

Example:

```python
try:


    print(
        "Running automation..."
    )


except Exception as error:


    print(
        error
    )


finally:


    print(
        "Automation execution finished."
    )
```

---

# 43. Create Main Function

A clean automation script should have:

```python
def main():

    pass
```

Example:

```python
def main():


    logging.info(

        "Automation started."

    )


    # Load Data


    # Validate Data


    # Clean Data


    # Analyze Data


    # Export Reports


    logging.info(

        "Automation completed."

    )
```

---

# 44. Run Main Function

```python
if __name__ == "__main__":

    main()
```

This is standard Python script structure.

---

# 45. Complete Automation Structure

```text
Imports
    ↓
Configuration
    ↓
Logging Setup
    ↓
Reusable Functions
    ↓
Main Function
    ↓
Run Script
```

Example:

```python
import pandas as pd

from pathlib import Path

import logging


def load_data():

    pass


def validate_data():

    pass


def clean_data():

    pass


def calculate_kpis():

    pass


def export_report():

    pass


def main():

    pass


if __name__ == "__main__":

    main()
```

---

# 46. Complete Data Analyst Automation Workflow

```python
import pandas as pd

from pathlib import Path

from datetime import datetime

import logging


# PATHS

INPUT_FOLDER = Path(
    "data"
)

OUTPUT_FOLDER = Path(
    "output"
)

LOG_FOLDER = Path(
    "logs"
)


# CREATE FOLDERS

OUTPUT_FOLDER.mkdir(

    exist_ok=True

)

LOG_FOLDER.mkdir(

    exist_ok=True

)


# LOGGING

logging.basicConfig(

    filename=(
        LOG_FOLDER
        /
        "automation.log"
    ),

    level=logging.INFO,

    format=(

        "%(asctime)s - "

        "%(levelname)s - "

        "%(message)s"

    )

)


# CLEAN DATA

def clean_data(
    dataframe
):


    dataframe = dataframe.copy()


    dataframe.columns = (

        dataframe.columns

        .str.strip()

        .str.lower()

        .str.replace(
            " ",
            "_"
        )

    )


    dataframe = (

        dataframe

        .drop_duplicates()

    )


    dataframe[
        "order_date"
    ] = pd.to_datetime(

        dataframe[
            "order_date"
        ],

        errors="coerce"

    )


    return dataframe


# VALIDATE DATA

def validate_data(
    dataframe
):


    required_columns = {

        "order_id",

        "order_date",

        "customer_id",

        "product_name",

        "quantity",

        "sales",

        "profit",

        "region"

    }


    missing_columns = (

        required_columns

        -

        set(
            dataframe.columns
        )

    )


    if missing_columns:


        raise ValueError(

            f"Missing columns: {missing_columns}"

        )


    if dataframe.empty:


        raise ValueError(

            "Dataset is empty."

        )


# LOAD FILES

def load_files():


    csv_files = list(

        INPUT_FOLDER.glob(
            "*.csv"
        )

    )


    if not csv_files:


        raise FileNotFoundError(

            "No CSV files found."

        )


    dataframes = []


    for file in csv_files:


        try:


            logging.info(

                f"Processing {file.name}"

            )


            dataframe = pd.read_csv(
                file
            )


            dataframe[
                "source_file"
            ] = file.name


            dataframe = clean_data(
                dataframe
            )


            validate_data(
                dataframe
            )


            dataframes.append(
                dataframe
            )


            logging.info(

                f"Successfully processed {file.name}"

            )


        except Exception as error:


            logging.error(

                f"Failed to process {file.name}: {error}"

            )


            continue


    if not dataframes:


        raise ValueError(

            "No valid datasets were processed."

        )


    return pd.concat(

        dataframes,

        ignore_index=True

    )


# KPI REPORT

def create_kpi_report(
    dataframe
):


    total_sales = (

        dataframe[
            "sales"
        ]

        .sum()

    )


    total_profit = (

        dataframe[
            "profit"
        ]

        .sum()

    )


    total_orders = (

        dataframe[
            "order_id"
        ]

        .nunique()

    )


    total_customers = (

        dataframe[
            "customer_id"
        ]

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


    return pd.DataFrame({

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


# MONTHLY SUMMARY

def create_monthly_summary(
    dataframe
):


    dataframe = dataframe.copy()


    dataframe[
        "order_month"
    ] = (

        dataframe[
            "order_date"
        ]

        .dt.to_period(
            "M"
        )

        .astype(str)

    )


    return (

        dataframe

        .groupby(
            "order_month"
        )

        .agg(

            total_sales=(
                "sales",
                "sum"
            ),

            total_profit=(
                "profit",
                "sum"
            ),

            total_orders=(
                "order_id",
                "nunique"
            ),

            total_customers=(
                "customer_id",
                "nunique"
            )

        )

        .reset_index()

    )


# REGIONAL SUMMARY

def create_regional_summary(
    dataframe
):


    return (

        dataframe

        .groupby(
            "region"
        )

        .agg(

            total_sales=(
                "sales",
                "sum"
            ),

            total_profit=(
                "profit",
                "sum"
            ),

            total_orders=(
                "order_id",
                "nunique"
            )

        )

        .reset_index()

    )


# EXPORT REPORT

def export_report(

    dataframe,

    kpi_report,

    monthly_summary,

    regional_summary

):


    report_date = (

        datetime.now()

        .strftime(
            "%Y-%m-%d"
        )

    )


    report_file = (

        OUTPUT_FOLDER

        /

        f"business_report_{report_date}.xlsx"

    )


    with pd.ExcelWriter(

        report_file,

        engine="openpyxl"

    ) as writer:


        kpi_report.to_excel(

            writer,

            sheet_name="KPI Summary",

            index=False

        )


        monthly_summary.to_excel(

            writer,

            sheet_name="Monthly Summary",

            index=False

        )


        regional_summary.to_excel(

            writer,

            sheet_name="Regional Summary",

            index=False

        )


        dataframe.to_excel(

            writer,

            sheet_name="Cleaned Data",

            index=False

        )


    logging.info(

        f"Report created: {report_file}"

    )


# MAIN FUNCTION

def main():


    try:


        logging.info(

            "Automation started."

        )


        dataframe = load_files()


        kpi_report = create_kpi_report(

            dataframe

        )


        monthly_summary = create_monthly_summary(

            dataframe

        )


        regional_summary = create_regional_summary(

            dataframe

        )


        export_report(

            dataframe,

            kpi_report,

            monthly_summary,

            regional_summary

        )


        logging.info(

            "Automation completed successfully."

        )


    except Exception as error:


        logging.critical(

            f"Automation failed: {error}"

        )


        raise


if __name__ == "__main__":

    main()
```

---

# 47. Recommended Project Folder Structure

```text
18_Automation_with_Python/

│

├── Automation_with_Python_Notes.md

├── Automation_with_Python_Practice.ipynb

├── Automation_with_Python_Assessment.ipynb

│

├── data/

│   ├── sales_january.csv

│   ├── sales_february.csv

│   └── sales_march.csv

│

├── output/

│   ├── cleaned_data/

│   └── business_report.xlsx

│

├── logs/

│   └── automation.log

│

└── automation.py
```

---

# 48. Common Beginner Errors

## Automating a Bad Process

Automation does not fix bad analysis.

Wrong:

```text
Incorrect Manual Process
        ↓
Automate It
        ↓
Incorrect Results Faster
```

Correct:

```text
Understand Process
        ↓
Validate Logic
        ↓
Automate Process
```

---

## No Input Validation

Wrong:

```text
Load File
    ↓
Process Immediately
```

Better:

```text
Load File
    ↓
Check Required Columns
    ↓
Check Empty Dataset
    ↓
Check Data Types
    ↓
Process
```

---

## Using Only print()

Weak:

```python
print(
    "File processed."
)
```

Better:

```python
logging.info(

    "File processed."

)
```

---

## No Error Handling

One corrupted file should not necessarily destroy the complete batch workflow.

Use:

```python
try

except

continue
```

when appropriate.

---

## Catching Errors and Ignoring Them

Bad:

```python
try:

    process_data()


except:

    pass
```

This hides problems.

Better:

```python
except Exception as error:


    logging.error(

        error

    )
```

---

## Hardcoding Every Filename

Weak:

```python
january = pd.read_csv(
    "january.csv"
)

february = pd.read_csv(
    "february.csv"
)

march = pd.read_csv(
    "march.csv"
)
```

Better:

```python
csv_files = list(

    data_folder.glob(
        "*.csv"
    )

)
```

---

## Repeating Code

Weak:

```text
Copy

Paste

Modify

Repeat
```

Better:

```text
Functions

Loops

Reusable Workflows
```

---

## Overwriting Reports

Weak:

```text
business_report.xlsx
```

every month.

Better:

```text
business_report_2026-07-13.xlsx
```

---

## No Logs

If automation fails overnight and there are no logs:

```text
You Do Not Know

What Failed

Where It Failed

When It Failed

Why It Failed
```

---

# 49. Interview Questions

1. What is Python Automation?
2. How can Python Automation help a Data Analyst?
3. What is Batch Processing?
4. How do you process multiple CSV files?
5. What is `pathlib`?
6. What is the difference between `glob()` and `rglob()`?
7. How do you create folders automatically?
8. What does `exist_ok=True` do?
9. What does `parents=True` do?
10. How do you check whether a file exists?
11. How do you combine multiple CSV files?
12. Why should you use `ignore_index=True`?
13. Why should you add source filenames when combining datasets?
14. How do you automate data cleaning?
15. Why should automation logic be organized into functions?
16. How do you validate required columns?
17. How do you export cleaned datasets automatically?
18. What is Report Automation?
19. How would you automate KPI report generation?
20. How would you generate monthly summaries?
21. How would you generate regional summaries?
22. How do you create dynamic report filenames?
23. What is Python logging?
24. Why is logging better than `print()` for automation?
25. What are the main logging levels?
26. How do you create a log file?
27. How do you log file-processing errors?
28. How do you continue batch processing after one file fails?
29. When should automation stop completely?
30. What is the purpose of `finally`?
31. Why should automated workflows validate data?
32. What is the purpose of a `main()` function?
33. What does `if __name__ == "__main__":` mean?
34. How would you structure an automation project?
35. What is the difference between manual and automated reporting?
36. How would you automate monthly sales reporting?
37. What should happen when an input file is corrupted?
38. Why should errors never be silently ignored?
39. What are common mistakes when building Python automation?
40. Explain an end-to-end automated Data Analyst workflow.

---

# 50. Completion Checklist

Before moving to EDA, you should be able to:

- [ ] Explain Python Automation
- [ ] Explain Batch Processing
- [ ] Use `pathlib`
- [ ] Create file paths
- [ ] Create folders automatically
- [ ] Create nested folders
- [ ] Check whether files exist
- [ ] Use `glob()`
- [ ] Use `rglob()`
- [ ] Find multiple CSV files
- [ ] Loop through multiple files
- [ ] Read multiple CSV files
- [ ] Combine multiple DataFrames
- [ ] Use `ignore_index=True`
- [ ] Add source filenames
- [ ] Create reusable cleaning functions
- [ ] Validate required columns
- [ ] Validate empty datasets
- [ ] Export cleaned datasets
- [ ] Process individual files automatically
- [ ] Automate KPI calculations
- [ ] Calculate Total Sales
- [ ] Calculate Total Profit
- [ ] Calculate Profit Margin
- [ ] Calculate Total Orders
- [ ] Calculate Total Customers
- [ ] Calculate Average Order Value
- [ ] Generate monthly summaries
- [ ] Generate regional summaries
- [ ] Generate product summaries
- [ ] Export automated Excel reports
- [ ] Create multiple Excel sheets
- [ ] Create dynamic report filenames
- [ ] Use `logging`
- [ ] Understand logging levels
- [ ] Create log files
- [ ] Log successful operations
- [ ] Log warnings
- [ ] Log errors
- [ ] Use `try` and `except`
- [ ] Use `finally`
- [ ] Continue processing after non-critical errors
- [ ] Stop automation after critical errors
- [ ] Create reusable automation functions
- [ ] Create a `main()` function
- [ ] Use `if __name__ == "__main__":`
- [ ] Build a complete automated reporting workflow
- [ ] Organize an automation project
- [ ] Replace a repetitive manual reporting process with Python

---

# Final Outcome

After completing Automation with Python, you should be able to process multiple CSV files automatically, combine datasets, clean and validate data, export cleaned datasets, calculate business KPIs, generate monthly and regional summaries, create automated Excel reports, use dynamic filenames, implement logging and error handling, organize code into reusable functions, and build an end-to-end automated reporting workflow.

The core skill is:

```text
Multiple Input Files
        ↓
Batch Processing
        ↓
Validation
        ↓
Data Cleaning
        ↓
Combine Data
        ↓
Business Analysis
        ↓
KPI Calculation
        ↓
Monthly Summaries
        ↓
Automated Excel Report
        ↓
Logging
        ↓
Reusable Reporting Workflow
```