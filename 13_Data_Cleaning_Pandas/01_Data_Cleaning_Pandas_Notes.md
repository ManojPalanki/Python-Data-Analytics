# Data Cleaning with Pandas

## 1. Introduction

Data cleaning is the process of identifying and fixing problems in raw data before analysis.

Real-world ERP, CRM, sales, customer, and operational datasets may contain:

- Missing values
- Duplicate records
- Incorrect data types
- Inconsistent column names
- Inconsistent category values
- Extra spaces
- Incorrect text formatting
- Invalid dates
- Incorrect numerical values

For a Data Analyst, the main objective is:

```text
Raw Data
    ↓
Inspect Data Quality
    ↓
Handle Missing Values
    ↓
Remove Duplicates
    ↓
Standardize Columns
    ↓
Fix Data Types
    ↓
Clean Text and Categories
    ↓
Validate Results
    ↓
Clean Dataset Ready for Analysis
```

The most important topics are:

- Missing Values
- Duplicates
- Rename Columns
- Type Conversion
- Replace Values
- `fillna()`
- `dropna()`
- String Cleaning
- Date Cleaning
- Data Validation

---

# 2. Import Pandas

```python
import pandas as pd
```

Load the dataset:

```python
df = pd.read_csv(
    "sales_data.csv"
)
```

Before cleaning, inspect the data.

```python
df.head()
```

```python
df.info()
```

```python
df.isnull().sum()
```

```python
df.duplicated().sum()
```

Never start changing data before understanding the problems.

---

# 3. Data Cleaning Workflow

A practical workflow is:

```text
1. Load Data

2. Inspect Dataset

3. Check Missing Values

4. Check Duplicate Records

5. Review Column Names

6. Review Data Types

7. Inspect Categorical Values

8. Clean Text Data

9. Handle Missing Values

10. Remove Duplicates

11. Convert Data Types

12. Clean Dates

13. Validate Business Rules

14. Recheck Data Quality

15. Save Cleaned Dataset
```

---

# 4. Inspect Dataset Before Cleaning

Use:

```python
df.head()
```

```python
df.sample(5)
```

```python
df.shape
```

```python
df.columns
```

```python
df.dtypes
```

```python
df.info()
```

```python
df.describe()
```

```python
df.isnull().sum()
```

```python
df.duplicated().sum()
```

These commands help identify data-quality problems.

---

# 5. Missing Values

Missing values represent unavailable or incomplete data.

Pandas commonly represents missing values as:

```text
NaN
```

or:

```text
None
```

Example:

```python
data = {
    "Product": [
        "Laptop",
        "Mobile",
        "Tablet"
    ],

    "Sales": [
        850000,
        None,
        650000
    ]
}

df = pd.DataFrame(data)
```

---

# 6. Detect Missing Values

Use:

```python
df.isnull()
```

or:

```python
df.isna()
```

Both detect missing values.

---

# 7. Count Missing Values

```python
df.isnull().sum()
```

Example:

```text
OrderID       0

Product       0

Sales         5

Profit        3
```

This shows the number of missing values in each column.

---

# 8. Total Missing Values

```python
total_missing = (
    df.isnull()
    .sum()
    .sum()
)

print(
    f"Total Missing Values: {total_missing}"
)
```

---

# 9. Missing Value Percentage

Missing-value percentage provides more context than only the count.

```python
missing_percentage = (
    df.isnull().sum()
    /
    len(df)
) * 100
```

Create a summary:

```python
missing_summary = pd.DataFrame({
    "Missing Count":
        df.isnull().sum(),

    "Missing Percentage":
        (
            df.isnull().sum()
            /
            len(df)
        ) * 100
})
```

Display only columns containing missing values:

```python
missing_summary = missing_summary[
    missing_summary[
        "Missing Count"
    ] > 0
]

print(missing_summary)
```

---

# 10. Handling Missing Values

There is no single correct method for handling missing values.

Common options are:

```text
Fill Missing Values

Drop Missing Rows

Drop Missing Columns

Keep Missing Values

Investigate the Data Source
```

The correct choice depends on the business meaning of the data.

Do not automatically replace every missing value with zero.

---

# 11. fillna()

`fillna()` replaces missing values.

Example:

```python
df["Sales"] = (
    df["Sales"]
    .fillna(0)
)
```

This replaces missing Sales values with:

```text
0
```

---

# 12. Fill Missing Values with Mean

```python
mean_sales = (
    df["Sales"]
    .mean()
)

df["Sales"] = (
    df["Sales"]
    .fillna(mean_sales)
)
```

Use the mean carefully because extreme values can affect it.

---

# 13. Fill Missing Values with Median

```python
median_sales = (
    df["Sales"]
    .median()
)

df["Sales"] = (
    df["Sales"]
    .fillna(median_sales)
)
```

Median can be useful when numerical data contains outliers.

---

# 14. Fill Missing Values with Mode

Mode is the most frequent value.

```python
category_mode = (
    df["Category"]
    .mode()[0]
)

df["Category"] = (
    df["Category"]
    .fillna(category_mode)
)
```

Mode can be useful for categorical data.

---

# 15. Fill Different Columns Differently

```python
df = df.fillna({
    "Sales": 0,

    "Profit": 0,

    "Category": "Unknown",

    "Region": "Unknown"
})
```

Different columns should be handled according to their business meaning.

---

# 16. Forward Fill

Forward fill uses the previous valid value.

```python
df["Region"] = (
    df["Region"]
    .ffill()
)
```

Use only when the data structure makes this logically valid.

---

# 17. Backward Fill

Backward fill uses the next valid value.

```python
df["Region"] = (
    df["Region"]
    .bfill()
)
```

Again, use only when justified by the dataset.

---

# 18. dropna()

`dropna()` removes missing data.

Remove rows containing any missing value:

```python
df = df.dropna()
```

Be careful.

This can remove a large amount of useful data.

---

# 19. Drop Rows Based on Specific Columns

```python
df = df.dropna(
    subset=[
        "OrderID",
        "Sales"
    ]
)
```

This removes rows only when important columns contain missing values.

This is usually better than blindly dropping every incomplete row.

---

# 20. Drop Columns with Missing Values

```python
df = df.dropna(
    axis=1
)
```

This removes columns containing missing values.

Do not use this without understanding the business importance of the columns.

---

# 21. Missing Value Decision Framework

Ask:

```text
Is the column important?

How much data is missing?

Why is the data missing?

Does zero have a valid business meaning?

Can the value be calculated?

Can it be recovered from another source?

Would dropping the row create bias?

Would filling the value create misleading results?
```

Example:

```text
Missing Sales
→ Zero may mean no sale
→ Or it may mean unavailable data

Missing Customer ID
→ Usually should not be replaced with zero

Missing Category
→ May be replaced with "Unknown"

Missing Age
→ Mean or median may be considered depending on analysis
```

---

# 22. Duplicate Records

Duplicate records can cause:

- Incorrect revenue
- Incorrect order counts
- Incorrect customer counts
- Incorrect KPIs
- Misleading dashboards

Check duplicates:

```python
df.duplicated()
```

Count duplicates:

```python
df.duplicated().sum()
```

---

# 23. Display Duplicate Rows

```python
duplicate_rows = df[
    df.duplicated()
]

print(duplicate_rows)
```

Display all copies of duplicate records:

```python
duplicate_rows = df[
    df.duplicated(
        keep=False
    )
]
```

---

# 24. Remove Duplicate Rows

```python
df = df.drop_duplicates()
```

This keeps the first record and removes later duplicates.

---

# 25. Remove Duplicates Based on Specific Columns

Suppose `OrderID` should be unique.

```python
df = df.drop_duplicates(
    subset="OrderID"
)
```

Multiple columns:

```python
df = df.drop_duplicates(
    subset=[
        "OrderID",
        "ProductID"
    ]
)
```

---

# 26. keep Parameter

Keep first occurrence:

```python
df.drop_duplicates(
    keep="first"
)
```

Keep last occurrence:

```python
df.drop_duplicates(
    keep="last"
)
```

Remove every duplicated occurrence:

```python
df.drop_duplicates(
    keep=False
)
```

---

# 27. Important Duplicate Warning

Do not assume:

```text
Same Order ID
=
Duplicate Record
```

One order may legitimately contain multiple products.

Example:

```text
OrderID   Product

1001      Laptop

1001      Mouse

1001      Keyboard
```

These are not necessarily duplicate transactions.

Understand the dataset's grain before removing duplicates.

This is one of the most important Data Analyst concepts.

---

# 28. What Is Data Grain?

Data grain means:

```text
What does one row represent?
```

Examples:

```text
One Row
→ One Order

One Row
→ One Order Item

One Row
→ One Customer

One Row
→ One Product

One Row
→ One Daily Store Sale
```

Never remove duplicates until you understand the data grain.

---

# 29. Column Names

Raw datasets may contain inconsistent column names.

Example:

```text
Order ID

Customer Name

Product-Category

Sales Amount
```

These names can make coding inconvenient.

---

# 30. Rename Columns

Use:

```python
df.rename()
```

Example:

```python
df = df.rename(
    columns={
        "Order ID": "OrderID",

        "Customer Name":
            "CustomerName",

        "Sales Amount":
            "Sales"
    }
)
```

---

# 31. Rename All Columns

```python
df.columns = [
    "OrderID",
    "CustomerName",
    "Category",
    "Sales"
]
```

Use this only when you know the exact column order.

---

# 32. Standardize Column Names

A common cleaning approach:

```python
df.columns = (
    df.columns
    .str.strip()
    .str.lower()
    .str.replace(
        " ",
        "_"
    )
)
```

Example:

```text
Order ID
```

becomes:

```text
order_id
```

```text
Customer Name
```

becomes:

```text
customer_name
```

---

# 33. Better Column Name Cleaning

```python
df.columns = (
    df.columns
    .str.strip()
    .str.lower()
    .str.replace(
        " ",
        "_"
    )
    .str.replace(
        "-",
        "_"
    )
)
```

This creates cleaner and more consistent column names.

---

# 34. Data Type Conversion

Incorrect data types can cause analysis problems.

Check:

```python
df.dtypes
```

Example:

```text
OrderDate      object

Sales          object

Quantity       object
```

But these should be:

```text
OrderDate      datetime

Sales          float

Quantity       integer
```

---

# 35. astype()

Use:

```python
astype()
```

Convert to integer:

```python
df["Quantity"] = (
    df["Quantity"]
    .astype(int)
)
```

Convert to float:

```python
df["Sales"] = (
    df["Sales"]
    .astype(float)
)
```

Convert to string:

```python
df["OrderID"] = (
    df["OrderID"]
    .astype(str)
)
```

---

# 36. Problem with astype()

This:

```python
df["Sales"].astype(float)
```

fails if values contain:

```text
Unknown

N/A

₹50,000

Invalid
```

For messy business data, use:

```python
pd.to_numeric()
```

---

# 37. pd.to_numeric()

Convert numerical columns:

```python
df["Sales"] = pd.to_numeric(
    df["Sales"]
)
```

Safer approach:

```python
df["Sales"] = pd.to_numeric(
    df["Sales"],
    errors="coerce"
)
```

Invalid values become:

```text
NaN
```

---

# 38. errors="coerce"

Example:

```python
sales = pd.Series([
    "850000",
    "920000",
    "Invalid",
    "780000"
])
```

Convert:

```python
sales = pd.to_numeric(
    sales,
    errors="coerce"
)
```

Result:

```text
850000

920000

NaN

780000
```

This is extremely useful when cleaning raw business data.

---

# 39. Convert Dates

Use:

```python
pd.to_datetime()
```

Example:

```python
df["OrderDate"] = (
    pd.to_datetime(
        df["OrderDate"]
    )
)
```

---

# 40. Handle Invalid Dates

Safer approach:

```python
df["OrderDate"] = (
    pd.to_datetime(
        df["OrderDate"],
        errors="coerce"
    )
)
```

Invalid dates become:

```text
NaT
```

`NaT` means:

```text
Not a Time
```

---

# 41. Specify Date Format

```python
df["OrderDate"] = (
    pd.to_datetime(
        df["OrderDate"],
        format="%Y-%m-%d",
        errors="coerce"
    )
)
```

Specifying the correct format can improve consistency and prevent ambiguous date interpretation.

---

# 42. String Cleaning

Raw text data may contain:

- Extra spaces
- Incorrect capitalization
- Inconsistent formatting

Example:

```text
 laptop

LAPTOP

Laptop 

lapTop
```

These should usually represent one category:

```text
Laptop
```

---

# 43. strip()

Remove leading and trailing spaces:

```python
df["Product"] = (
    df["Product"]
    .str.strip()
)
```

Example:

```text
" Laptop "
```

becomes:

```text
"Laptop"
```

---

# 44. lower()

Convert text to lowercase:

```python
df["Category"] = (
    df["Category"]
    .str.lower()
)
```

---

# 45. upper()

Convert text to uppercase:

```python
df["Region"] = (
    df["Region"]
    .str.upper()
)
```

---

# 46. title()

Convert text to title case:

```python
df["Category"] = (
    df["Category"]
    .str.title()
)
```

Example:

```text
office supplies
```

becomes:

```text
Office Supplies
```

---

# 47. Combine String Cleaning Operations

```python
df["Category"] = (
    df["Category"]
    .str.strip()
    .str.lower()
    .str.title()
)
```

This:

```text
" OFFICE supplies "
```

becomes:

```text
"Office Supplies"
```

---

# 48. Standardize Category Names

Suppose:

```text
Technology

technology

TECH

Tech
```

All should become:

```text
Technology
```

Use:

```python
df["Category"] = (
    df["Category"]
    .replace({
        "technology":
            "Technology",

        "TECH":
            "Technology",

        "Tech":
            "Technology"
    })
)
```

---

# 49. replace()

Use:

```python
replace()
```

to replace specific values.

Example:

```python
df["Region"] = (
    df["Region"]
    .replace({
        "S": "South",

        "N": "North",

        "E": "East",

        "W": "West"
    })
)
```

---

# 50. replace() vs fillna()

Use:

```text
replace()
```

when changing existing values.

Example:

```text
"TECH"
→ "Technology"
```

Use:

```text
fillna()
```

when replacing missing values.

Example:

```text
NaN
→ "Unknown"
```

---

# 51. Replace Multiple Invalid Values

```python
df["Sales"] = (
    df["Sales"]
    .replace(
        [
            "N/A",
            "Unknown",
            "Missing",
            "-"
        ],
        pd.NA
    )
)
```

Then convert:

```python
df["Sales"] = pd.to_numeric(
    df["Sales"],
    errors="coerce"
)
```

---

# 52. Remove Currency Symbols

Suppose:

```text
₹850,000

₹920,000

₹780,000
```

Clean:

```python
df["Sales"] = (
    df["Sales"]
    .str.replace(
        "₹",
        "",
        regex=False
    )
    .str.replace(
        ",",
        "",
        regex=False
    )
)
```

Convert:

```python
df["Sales"] = pd.to_numeric(
    df["Sales"],
    errors="coerce"
)
```

---

# 53. Remove Percentage Symbols

Suppose:

```text
10%

15%

20%
```

Clean:

```python
df["Discount"] = (
    df["Discount"]
    .str.replace(
        "%",
        "",
        regex=False
    )
)
```

Convert:

```python
df["Discount"] = pd.to_numeric(
    df["Discount"],
    errors="coerce"
)
```

If required as decimal values:

```python
df["Discount"] = (
    df["Discount"] / 100
)
```

---

# 54. Clean Customer Names

```python
df["CustomerName"] = (
    df["CustomerName"]
    .str.strip()
    .str.title()
)
```

Example:

```text
" manoj palanki "
```

becomes:

```text
"Manoj Palanki"
```

---

# 55. Clean Multiple Text Columns

```python
text_columns = [
    "CustomerName",
    "Category",
    "Region"
]

for column in text_columns:

    df[column] = (
        df[column]
        .str.strip()
        .str.title()
    )
```

This avoids repeating the same cleaning code.

---

# 56. Filter Invalid Numerical Values

Suppose sales should never be negative.

Check:

```python
invalid_sales = df[
    df["Sales"] < 0
]

print(invalid_sales)
```

Depending on the business rules, you may:

- Investigate
- Correct
- Remove
- Flag

Do not automatically delete negative values.

For example, negative values may represent refunds or returns.

---

# 57. Validate Quantity

Check zero or negative quantities:

```python
invalid_quantity = df[
    df["Quantity"] <= 0
]

print(invalid_quantity)
```

Again, understand the business meaning before modifying data.

---

# 58. Validate Dates

Check missing or invalid dates:

```python
invalid_dates = df[
    df["OrderDate"].isnull()
]

print(invalid_dates)
```

---

# 59. Check Future Dates

```python
today = pd.Timestamp.today()

future_orders = df[
    df["OrderDate"] > today
]

print(future_orders)
```

Future dates may indicate a data-quality problem depending on the dataset.

---

# 60. Remove Duplicate Orders Carefully

Suppose one row represents one order.

Then:

```python
df = df.drop_duplicates(
    subset="OrderID"
)
```

But suppose one row represents one product within an order.

Then use:

```python
df = df.drop_duplicates(
    subset=[
        "OrderID",
        "ProductID"
    ]
)
```

The correct logic depends on the data grain.

---

# 61. Fill Missing Sales Carefully

Simple approach:

```python
df["Sales"] = (
    df["Sales"]
    .fillna(0)
)
```

But ask:

```text
Does missing Sales actually mean zero sales?
```

If not, this creates incorrect data.

Alternative:

```python
df["Sales"] = (
    df["Sales"]
    .fillna(
        df["Sales"].median()
    )
)
```

Another alternative:

```python
df = df.dropna(
    subset=["Sales"]
)
```

The correct method depends on the business requirement.

---

# 62. Standardize Category Names

Inspect categories:

```python
df["Category"].value_counts(
    dropna=False
)
```

Clean spaces and capitalization:

```python
df["Category"] = (
    df["Category"]
    .str.strip()
    .str.title()
)
```

Replace inconsistent values:

```python
df["Category"] = (
    df["Category"]
    .replace({
        "Tech":
            "Technology",

        "Office Supply":
            "Office Supplies"
    })
)
```

Recheck:

```python
df["Category"].value_counts(
    dropna=False
)
```

---

# 63. Clean Dates

Convert:

```python
df["OrderDate"] = (
    pd.to_datetime(
        df["OrderDate"],
        errors="coerce"
    )
)
```

Check invalid dates:

```python
df["OrderDate"].isnull().sum()
```

Extract year:

```python
df["OrderYear"] = (
    df["OrderDate"]
    .dt.year
)
```

Extract month:

```python
df["OrderMonth"] = (
    df["OrderDate"]
    .dt.month
)
```

Extract month name:

```python
df["OrderMonthName"] = (
    df["OrderDate"]
    .dt.month_name()
)
```

---

# 64. Reset Index

After dropping rows, the index may contain gaps.

Example:

```text
0

1

4

7

9
```

Reset:

```python
df = df.reset_index(
    drop=True
)
```

Result:

```text
0

1

2

3

4
```

---

# 65. inplace Parameter

You may see:

```python
df.drop_duplicates(
    inplace=True
)
```

This modifies the existing DataFrame.

Another approach:

```python
df = df.drop_duplicates()
```

For learning and readable analysis workflows, assigning the result back to `df` is often clearer:

```python
df = df.drop_duplicates()
```

---

# 66. Copy Original Data Before Cleaning

A useful practice:

```python
df_raw = pd.read_csv(
    "sales_data.csv"
)

df = df_raw.copy()
```

Now:

```text
df_raw
→ Original Data

df
→ Working Copy
```

This allows you to compare raw and cleaned data.

---

# 67. Compare Rows Before and After Cleaning

Before cleaning:

```python
rows_before = df.shape[0]
```

Clean:

```python
df = df.drop_duplicates()
```

After cleaning:

```python
rows_after = df.shape[0]
```

Calculate removed rows:

```python
rows_removed = (
    rows_before
    -
    rows_after
)
```

Display:

```python
print(
    f"Rows Before: {rows_before}"
)

print(
    f"Rows After: {rows_after}"
)

print(
    f"Rows Removed: {rows_removed}"
)
```

---

# 68. Data Cleaning Audit Summary

```python
rows_before = df.shape[0]

missing_before = (
    df.isnull()
    .sum()
    .sum()
)

duplicates_before = (
    df.duplicated()
    .sum()
)
```

Perform cleaning.

Then:

```python
rows_after = df.shape[0]

missing_after = (
    df.isnull()
    .sum()
    .sum()
)

duplicates_after = (
    df.duplicated()
    .sum()
)
```

Display:

```python
print("=" * 55)

print("DATA CLEANING SUMMARY")

print("=" * 55)

print(
    f"Rows Before Cleaning: {rows_before}"
)

print(
    f"Rows After Cleaning: {rows_after}"
)

print(
    f"Missing Before: {missing_before}"
)

print(
    f"Missing After: {missing_after}"
)

print(
    f"Duplicates Before: {duplicates_before}"
)

print(
    f"Duplicates After: {duplicates_after}"
)

print("=" * 55)
```

---

# 69. Complete Data Cleaning Example

```python
import pandas as pd


# LOAD RAW DATA

df_raw = pd.read_csv(
    "sales_data.csv"
)


# CREATE WORKING COPY

df = df_raw.copy()


# RECORD INITIAL QUALITY METRICS

rows_before = df.shape[0]

missing_before = (
    df.isnull()
    .sum()
    .sum()
)

duplicates_before = (
    df.duplicated()
    .sum()
)


# STANDARDIZE COLUMN NAMES

df.columns = (
    df.columns
    .str.strip()
    .str.lower()
    .str.replace(
        " ",
        "_"
    )
    .str.replace(
        "-",
        "_"
    )
)


# REMOVE EXACT DUPLICATES

df = df.drop_duplicates()


# CLEAN CUSTOMER NAMES

df["customer_name"] = (
    df["customer_name"]
    .str.strip()
    .str.title()
)


# CLEAN CATEGORY VALUES

df["category"] = (
    df["category"]
    .str.strip()
    .str.title()
)


# STANDARDIZE CATEGORY VALUES

df["category"] = (
    df["category"]
    .replace({
        "Tech":
            "Technology",

        "Office Supply":
            "Office Supplies"
    })
)


# CLEAN SALES VALUES

df["sales"] = (
    df["sales"]
    .astype(str)
    .str.replace(
        "₹",
        "",
        regex=False
    )
    .str.replace(
        ",",
        "",
        regex=False
    )
)


# CONVERT SALES TO NUMERIC

df["sales"] = pd.to_numeric(
    df["sales"],
    errors="coerce"
)


# HANDLE MISSING SALES

df["sales"] = (
    df["sales"]
    .fillna(
        df["sales"].median()
    )
)


# CLEAN ORDER DATES

df["order_date"] = (
    pd.to_datetime(
        df["order_date"],
        errors="coerce"
    )
)


# REMOVE ROWS MISSING CRITICAL DATA

df = df.dropna(
    subset=[
        "order_id",
        "order_date"
    ]
)


# RESET INDEX

df = df.reset_index(
    drop=True
)


# FINAL QUALITY METRICS

rows_after = df.shape[0]

missing_after = (
    df.isnull()
    .sum()
    .sum()
)

duplicates_after = (
    df.duplicated()
    .sum()
)


# CLEANING SUMMARY

print("=" * 60)

print("DATA CLEANING SUMMARY")

print("=" * 60)

print(
    f"Rows Before: {rows_before:,}"
)

print(
    f"Rows After: {rows_after:,}"
)

print(
    f"Rows Removed: {rows_before - rows_after:,}"
)

print(
    f"Missing Before: {missing_before:,}"
)

print(
    f"Missing After: {missing_after:,}"
)

print(
    f"Duplicates Before: {duplicates_before:,}"
)

print(
    f"Duplicates After: {duplicates_after:,}"
)

print("=" * 60)
```

---

# 70. Validate the Cleaned Dataset

Cleaning is not finished after running transformation code.

Recheck the dataset.

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

```python
df["Category"].value_counts(
    dropna=False
)
```

```python
df.describe()
```

The workflow is:

```text
Inspect
    ↓
Clean
    ↓
Validate
```

Not:

```text
Inspect
    ↓
Clean
    ↓
Assume Everything Is Correct
```

---

# 71. Save Cleaned Dataset

Save to CSV:

```python
df.to_csv(
    "cleaned_sales_data.csv",
    index=False
)
```

Save to Excel:

```python
df.to_excel(
    "cleaned_sales_data.xlsx",
    index=False
)
```

---

# 72. Save Cleaned Dataset to Output Folder

```python
from pathlib import Path

output_folder = Path("output")

output_folder.mkdir(
    exist_ok=True
)

output_file = (
    output_folder
    /
    "cleaned_sales_data.csv"
)

df.to_csv(
    output_file,
    index=False
)
```

---

# 73. Raw ERP / CRM Data Cleaning Workflow

A realistic workflow:

```text
ERP / CRM Export
        ↓
Load CSV / Excel
        ↓
Create Raw Data Copy
        ↓
Inspect Structure
        ↓
Check Missing Values
        ↓
Check Duplicate Records
        ↓
Understand Data Grain
        ↓
Standardize Column Names
        ↓
Clean Text Fields
        ↓
Standardize Categories
        ↓
Convert Numerical Columns
        ↓
Convert Date Columns
        ↓
Handle Missing Data
        ↓
Validate Business Rules
        ↓
Recheck Data Quality
        ↓
Export Clean Dataset
        ↓
SQL / Excel / Power BI / Python Analysis
```

---

# 74. Most Important Pandas Cleaning Methods

| Method | Purpose |
|---|---|
| `isnull()` | Detect missing values |
| `fillna()` | Fill missing values |
| `dropna()` | Remove missing data |
| `duplicated()` | Detect duplicates |
| `drop_duplicates()` | Remove duplicates |
| `rename()` | Rename columns |
| `astype()` | Convert data type |
| `pd.to_numeric()` | Safely convert numerical data |
| `pd.to_datetime()` | Convert date data |
| `replace()` | Replace specific values |
| `str.strip()` | Remove extra spaces |
| `str.lower()` | Convert to lowercase |
| `str.upper()` | Convert to uppercase |
| `str.title()` | Standardize capitalization |
| `reset_index()` | Reset row index |
| `to_csv()` | Export CSV |
| `to_excel()` | Export Excel |

---

# 75. What You Should Prioritize

For a Data Analyst role, master:

```text
isnull().sum()

fillna()

dropna()

duplicated()

drop_duplicates()

rename()

Column Name Standardization

astype()

pd.to_numeric()

pd.to_datetime()

replace()

str.strip()

str.lower()

str.upper()

str.title()

reset_index()

Data Validation

to_csv()
```

Do not waste time memorizing every Pandas cleaning method.

The real skill is deciding:

```text
What is wrong with the data?

Why is it wrong?

Should it be fixed, removed, replaced, or investigated?

How will the decision affect business analysis?
```

---

# 76. Core Patterns to Remember

## Check Missing Values

```python
df.isnull().sum()
```

## Fill Missing Values

```python
df["Sales"] = (
    df["Sales"]
    .fillna(
        df["Sales"].median()
    )
)
```

## Remove Missing Critical Records

```python
df = df.dropna(
    subset=["OrderID"]
)
```

## Check Duplicates

```python
df.duplicated().sum()
```

## Remove Duplicates

```python
df = df.drop_duplicates()
```

## Rename Columns

```python
df = df.rename(
    columns={
        "Order ID":
            "OrderID"
    }
)
```

## Standardize Column Names

```python
df.columns = (
    df.columns
    .str.strip()
    .str.lower()
    .str.replace(
        " ",
        "_"
    )
)
```

## Convert Numerical Data

```python
df["Sales"] = pd.to_numeric(
    df["Sales"],
    errors="coerce"
)
```

## Convert Dates

```python
df["OrderDate"] = (
    pd.to_datetime(
        df["OrderDate"],
        errors="coerce"
    )
)
```

## Standardize Categories

```python
df["Category"] = (
    df["Category"]
    .str.strip()
    .str.title()
)
```

## Replace Values

```python
df["Category"] = (
    df["Category"]
    .replace({
        "Tech":
            "Technology"
    })
)
```

## Reset Index

```python
df = df.reset_index(
    drop=True
)
```

## Export Clean Data

```python
df.to_csv(
    "cleaned_data.csv",
    index=False
)
```

---

# 77. Common Beginner Errors

## Filling Every Missing Value with Zero

Wrong mindset:

```text
Missing Data
→ Replace Everything with 0
```

This can destroy the meaning of the data.

Always understand what the missing value represents.

---

## Dropping Every Missing Row

```python
df = df.dropna()
```

This may remove a large amount of valuable information.

Use:

```python
df.dropna(
    subset=[
        "CriticalColumn"
    ]
)
```

when appropriate.

---

## Removing Duplicates Without Understanding Data Grain

An Order ID appearing multiple times does not automatically mean duplicate data.

Understand what one row represents first.

---

## Using astype() on Dirty Data

This may fail:

```python
df["Sales"].astype(float)
```

Prefer:

```python
pd.to_numeric(
    df["Sales"],
    errors="coerce"
)
```

for messy data.

---

## Cleaning Without Validation

Do not assume the dataset is clean because the code ran successfully.

Always recheck:

```python
df.info()

df.isnull().sum()

df.duplicated().sum()

df.describe()
```

---

## Modifying the Only Copy of Raw Data

Better:

```python
df_raw = pd.read_csv(
    "sales.csv"
)

df = df_raw.copy()
```

Preserve the original data.

---

# 78. Interview Questions

1. What is data cleaning?
2. Why is data cleaning important for Data Analysts?
3. How do you identify missing values in Pandas?
4. What is the difference between `isnull()` and `isna()`?
5. How do you count missing values?
6. How do you calculate missing-value percentage?
7. What does `fillna()` do?
8. When would you fill missing data with mean?
9. When would you use median instead of mean?
10. When would you use mode?
11. What does `dropna()` do?
12. Why should you not blindly use `dropna()`?
13. How do you detect duplicate records?
14. How do you remove duplicate records?
15. How do you remove duplicates based on specific columns?
16. What is data grain?
17. Why should you understand data grain before removing duplicates?
18. How do you rename columns?
19. How do you standardize column names?
20. What does `astype()` do?
21. What does `pd.to_numeric()` do?
22. What does `errors="coerce"` mean?
23. How do you convert a column to datetime?
24. What does `pd.to_datetime()` do?
25. What is `NaT`?
26. How do you remove extra spaces from text?
27. How do you standardize capitalization?
28. What is the difference between `replace()` and `fillna()`?
29. How would you remove currency symbols from sales data?
30. How would you clean percentage data?
31. How would you standardize category names?
32. Why should negative sales not automatically be deleted?
33. How would you validate future dates?
34. Why should raw data be preserved?
35. How do you validate a dataset after cleaning?
36. How would you prepare an ERP or CRM export for Power BI?
37. How would you create a data-cleaning audit summary?
38. What are the main steps in a data-cleaning workflow?
39. How do you export cleaned data?
40. What is more important: knowing cleaning methods or making correct cleaning decisions? Why?

---

# 79. Completion Checklist

Before moving to Data Analysis with Pandas, you should be able to:

- [ ] Explain data cleaning
- [ ] Describe a complete cleaning workflow
- [ ] Inspect raw data before cleaning
- [ ] Detect missing values
- [ ] Count missing values
- [ ] Calculate missing-value percentages
- [ ] Use `fillna()`
- [ ] Fill numerical values with mean
- [ ] Fill numerical values with median
- [ ] Fill categorical values with mode
- [ ] Fill different columns differently
- [ ] Understand forward fill
- [ ] Understand backward fill
- [ ] Use `dropna()`
- [ ] Drop rows based on critical columns
- [ ] Explain why missing values should not automatically become zero
- [ ] Detect duplicates
- [ ] Display duplicate records
- [ ] Remove exact duplicates
- [ ] Remove duplicates using specific columns
- [ ] Explain data grain
- [ ] Remove duplicate orders correctly based on dataset grain
- [ ] Rename columns
- [ ] Standardize column names
- [ ] Check data types
- [ ] Use `astype()`
- [ ] Use `pd.to_numeric()`
- [ ] Use `errors="coerce"`
- [ ] Use `pd.to_datetime()`
- [ ] Handle invalid dates
- [ ] Remove extra spaces
- [ ] Standardize text capitalization
- [ ] Clean multiple text columns
- [ ] Use `replace()`
- [ ] Explain `replace()` vs `fillna()`
- [ ] Remove currency symbols
- [ ] Clean percentage values
- [ ] Standardize category names
- [ ] Validate negative numerical values
- [ ] Validate dates
- [ ] Check future dates
- [ ] Reset the DataFrame index
- [ ] Preserve raw data
- [ ] Compare rows before and after cleaning
- [ ] Create a data-cleaning audit summary
- [ ] Recheck missing values after cleaning
- [ ] Recheck duplicates after cleaning
- [ ] Recheck data types after cleaning
- [ ] Validate categorical values after cleaning
- [ ] Export cleaned CSV data
- [ ] Export cleaned Excel data
- [ ] Prepare raw ERP/CRM exports for reporting
- [ ] Prepare clean data for Excel, SQL, Power BI, and Python analysis

---

# Final Outcome

After completing Data Cleaning with Pandas, you should be able to inspect raw business datasets, identify and handle missing values, detect and remove genuine duplicate records, understand data grain before deleting data, rename and standardize columns, convert incorrect data types, clean numerical and date values, standardize category names, validate business rules, preserve raw data, create a cleaning audit summary, verify the cleaned dataset, and prepare raw ERP/CRM exports for reliable reporting and dashboard development.