# Pandas Fundamentals

## 1. Introduction

Pandas is the main Python library used for working with structured and tabular data.

For a Data Analyst, Pandas is used to:

- Load CSV files
- Load Excel files
- Inspect datasets
- Work with rows and columns
- Check data types
- Identify missing values
- Generate summary statistics
- Prepare data for cleaning and analysis

The most important topics in this module are:

- Series
- DataFrame
- `read_csv()`
- `read_excel()`
- `head()`
- `tail()`
- `shape`
- `columns`
- `index`
- `dtypes`
- `info()`
- `describe()`
- Missing-value inspection
- Initial dataset exploration

The main workflow is:

```text
Import Pandas
      ↓
Load Dataset
      ↓
Inspect Rows and Columns
      ↓
Check Dataset Size
      ↓
Review Column Names
      ↓
Check Data Types
      ↓
Identify Missing Values
      ↓
Generate Summary Statistics
      ↓
Understand the Dataset
      ↓
Begin Cleaning and Analysis
```

---

# 2. Import Pandas

Pandas is conventionally imported using the alias:

```python
import pandas as pd
```

Use:

```python
pd
```

instead of writing:

```python
pandas
```

The standard convention is:

```python
import pandas as pd
```

---

# 3. Main Pandas Data Structures

Pandas has two main data structures:

```text
Series

DataFrame
```

Think of them as:

```text
Series
→ One Column

DataFrame
→ Complete Table
```

---

# 4. Pandas Series

A Series is a one-dimensional labeled collection of data.

Example:

```python
import pandas as pd

sales = pd.Series([
    850000,
    920000,
    780000,
    1050000
])

print(sales)
```

Output:

```text
0     850000
1     920000
2     780000
3    1050000
dtype: int64
```

A Series contains:

```text
Index + Values
```

---

# 5. Series with Custom Index

```python
sales = pd.Series(
    [
        850000,
        920000,
        780000
    ],
    index=[
        "Laptop",
        "Mobile",
        "Tablet"
    ]
)

print(sales)
```

Output:

```text
Laptop    850000
Mobile    920000
Tablet    780000
dtype: int64
```

Access a value:

```python
print(sales["Laptop"])
```

Output:

```text
850000
```

---

# 6. Create Series from Dictionary

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 920000,
    "Tablet": 780000
}

sales = pd.Series(product_sales)

print(sales)
```

Dictionary keys become the index.

Dictionary values become Series values.

---

# 7. Pandas DataFrame

A DataFrame is a two-dimensional table containing rows and columns.

It is the most important Pandas data structure for Data Analysts.

Example:

```python
import pandas as pd

sales_data = {
    "Product": [
        "Laptop",
        "Mobile",
        "Tablet"
    ],

    "Sales": [
        850000,
        920000,
        780000
    ],

    "Profit": [
        175000,
        210000,
        150000
    ]
}

df = pd.DataFrame(sales_data)

print(df)
```

Output:

```text
  Product   Sales  Profit
0  Laptop  850000  175000
1  Mobile  920000  210000
2  Tablet  780000  150000
```

---

# 8. Understanding DataFrame Structure

A DataFrame contains:

```text
Rows

Columns

Index

Values
```

Example:

```text
Index   Product   Sales    Profit

0       Laptop    850000   175000

1       Mobile    920000   210000

2       Tablet    780000   150000
```

---

# 9. Create DataFrame from Dictionary

The most common beginner method is:

```python
data = {
    "Region": [
        "South",
        "North",
        "East",
        "West"
    ],

    "Sales": [
        850000,
        920000,
        780000,
        1050000
    ]
}

df = pd.DataFrame(data)
```

Display:

```python
print(df)
```

---

# 10. Series vs DataFrame

| Series | DataFrame |
|---|---|
| One-dimensional | Two-dimensional |
| Similar to one column | Similar to a table |
| Contains index and values | Contains rows and columns |
| `pd.Series()` | `pd.DataFrame()` |

Remember:

```text
Series
→ Single Column

DataFrame
→ Complete Dataset
```

---

# 11. Loading CSV Files

Use:

```python
pd.read_csv()
```

Example:

```python
import pandas as pd

df = pd.read_csv(
    "Superstore.csv"
)
```

Display:

```python
print(df)
```

For real Data Analysis, you will usually load an existing dataset instead of manually creating a DataFrame.

---

# 12. Loading CSV Using pathlib

A cleaner project structure is:

```text
12_Pandas_Fundamentals/
│
├── Pandas_Fundamentals_Notes.md
├── Pandas_Fundamentals_Practice.ipynb
│
└── data/
    └── Superstore.csv
```

Use:

```python
from pathlib import Path

import pandas as pd


file_path = Path(
    "data/Superstore.csv"
)


df = pd.read_csv(file_path)
```

---

# 13. Loading Excel Files

Use:

```python
pd.read_excel()
```

Example:

```python
df = pd.read_excel(
    "Superstore.xlsx"
)
```

---

# 14. Loading a Specific Excel Sheet

```python
df = pd.read_excel(
    "Superstore.xlsx",
    sheet_name="Orders"
)
```

This loads only the:

```text
Orders
```

worksheet.

---

# 15. Data Analyst Dataset Inspection Workflow

After loading a dataset, do not immediately start writing analysis code.

First inspect the data.

A good initial workflow is:

```python
df.head()

df.tail()

df.shape

df.columns

df.index

df.dtypes

df.info()

df.describe()

df.isnull().sum()
```

These commands answer the first important questions about the dataset.

---

# 16. head()

`head()` displays the first five rows by default.

```python
df.head()
```

Use:

```python
df.head(10)
```

to display the first 10 rows.

Use `head()` to:

- Preview the dataset
- Check column values
- Understand the general structure
- Identify obvious data-quality problems

---

# 17. tail()

`tail()` displays the last five rows by default.

```python
df.tail()
```

Display the last 10 rows:

```python
df.tail(10)
```

Use `tail()` to inspect the end of the dataset.

---

# 18. shape

`shape` returns the number of rows and columns.

```python
df.shape
```

Example output:

```text
(9994, 21)
```

Meaning:

```text
9994 Rows

21 Columns
```

Store separately:

```python
rows = df.shape[0]

columns = df.shape[1]
```

Display:

```python
print(f"Rows: {rows}")

print(f"Columns: {columns}")
```

---

# 19. columns

`columns` returns all column names.

```python
df.columns
```

Example:

```text
Index([
    'Row ID',
    'Order ID',
    'Order Date',
    'Ship Date',
    'Customer ID',
    'Customer Name',
    'Segment',
    'Country',
    'City',
    'State',
    'Region',
    'Product ID',
    'Category',
    'Sub-Category',
    'Product Name',
    'Sales',
    'Quantity',
    'Discount',
    'Profit'
])
```

---

# 20. Display Column Names Clearly

```python
for column in df.columns:

    print(column)
```

Or:

```python
column_names = df.columns.tolist()

print(column_names)
```

---

# 21. index

`index` returns information about the DataFrame index.

```python
df.index
```

Possible output:

```text
RangeIndex(start=0, stop=9994, step=1)
```

The index identifies DataFrame rows.

---

# 22. dtypes

`dtypes` displays the data type of every column.

```python
df.dtypes
```

Possible output:

```text
Order ID          object

Order Date        object

Sales            float64

Quantity           int64

Discount         float64

Profit           float64
```

Use `dtypes` to identify:

- Numeric columns
- Text columns
- Date columns stored incorrectly
- Columns requiring data-type conversion

---

# 23. Common Pandas Data Types

| Pandas Data Type | Meaning |
|---|---|
| `int64` | Integer |
| `float64` | Decimal number |
| `object` | Usually text or mixed data |
| `bool` | True / False |
| `datetime64` | Date and time |
| `category` | Categorical data |

Understanding data types is critical before analysis.

---

# 24. info()

`info()` provides a technical summary of the dataset.

```python
df.info()
```

It shows:

- Number of rows
- Number of columns
- Column names
- Non-null counts
- Data types
- Memory usage

Example:

```text
<class 'pandas.core.frame.DataFrame'>

RangeIndex: 9994 entries

Data columns:

Sales       9994 non-null float64

Profit      9994 non-null float64

Region      9994 non-null object
```

---

# 25. Why info() Is Important

`info()` quickly answers:

```text
How many rows exist?

How many columns exist?

Which columns contain missing values?

What are the data types?

Are date columns stored correctly?
```

For initial exploration:

```python
df.info()
```

is one of the most useful commands.

---

# 26. describe()

`describe()` generates summary statistics for numerical columns.

```python
df.describe()
```

It returns:

- Count
- Mean
- Standard deviation
- Minimum
- 25th percentile
- Median
- 75th percentile
- Maximum

---

# 27. Understanding describe()

Example:

```text
              Sales       Profit

count       9994.00      9994.00

mean         229.86        28.66

std          623.25       234.26

min            0.44     -6599.98

25%           17.28         1.73

50%           54.49         8.67

75%          209.94        29.36

max        22638.48      8399.98
```

---

# 28. Important Statistics

## count

Number of non-missing values.

## mean

Average value.

## std

Standard deviation.

Measures how spread out the values are.

## min

Lowest value.

## 25%

First quartile.

## 50%

Median.

## 75%

Third quartile.

## max

Highest value.

---

# 29. describe() for All Columns

By default:

```python
df.describe()
```

mainly analyzes numerical columns.

To include all columns:

```python
df.describe(
    include="all"
)
```

This can provide information about text columns too.

---

# 30. Inspect a Single Column

Select one column:

```python
df["Sales"]
```

This returns a:

```text
Series
```

Example:

```python
sales = df["Sales"]

print(sales)
```

---

# 31. Inspect Multiple Columns

Select multiple columns:

```python
df[
    [
        "Product Name",
        "Sales",
        "Profit"
    ]
]
```

This returns a:

```text
DataFrame
```

Remember:

```python
df["Sales"]
```

returns a Series.

```python
df[["Sales"]]
```

returns a DataFrame.

---

# 32. Check Unique Values

Use:

```python
df["Region"].unique()
```

Possible output:

```text
['South' 'West' 'Central' 'East']
```

This helps understand categorical columns.

---

# 33. Count Unique Values

Use:

```python
df["Region"].nunique()
```

Possible output:

```text
4
```

For customer IDs:

```python
df["Customer ID"].nunique()
```

This can help answer:

```text
How many unique customers exist?
```

---

# 34. value_counts()

`value_counts()` counts how often each unique value appears.

```python
df["Region"].value_counts()
```

Possible output:

```text
West       3203

East       2848

Central    2323

South      1620
```

Use this for categorical data exploration.

---

# 35. Missing Values

Real-world datasets frequently contain missing data.

Pandas represents missing values using:

```text
NaN
```

or:

```text
None
```

depending on the data type.

Before analysis, check for missing values.

---

# 36. isnull()

Use:

```python
df.isnull()
```

This returns:

```text
True
```

for missing values and:

```text
False
```

for non-missing values.

---

# 37. Count Missing Values

Use:

```python
df.isnull().sum()
```

Example:

```text
Order ID          0

Customer Name     0

Sales             5

Profit            3
```

This is one of the most important initial inspection commands.

---

# 38. isna()

You can also use:

```python
df.isna()
```

and:

```python
df.isna().sum()
```

For practical purposes:

```text
isnull()

isna()
```

perform the same missing-value detection task.

---

# 39. Total Missing Values

Calculate the total number of missing values:

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

# 40. Missing Values by Percentage

Count:

```python
missing_count = df.isnull().sum()
```

Calculate percentage:

```python
missing_percentage = (
    df.isnull().sum()
    /
    len(df)
) * 100
```

Create summary:

```python
missing_summary = pd.DataFrame({
    "Missing Count": missing_count,
    "Missing Percentage": missing_percentage
})
```

Display:

```python
print(missing_summary)
```

This is more useful than checking only the missing-value count.

---

# 41. Display Only Columns with Missing Values

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


missing_summary = missing_summary[
    missing_summary[
        "Missing Count"
    ] > 0
]


print(missing_summary)
```

---

# 42. Check Duplicate Rows

Use:

```python
df.duplicated()
```

Count duplicates:

```python
df.duplicated().sum()
```

Example:

```python
duplicate_count = (
    df.duplicated().sum()
)

print(
    f"Duplicate Rows: {duplicate_count}"
)
```

Checking duplicates should be part of initial dataset inspection.

---

# 43. Memory Usage

`info()` shows basic memory information.

For deeper inspection:

```python
df.memory_usage()
```

Include object columns:

```python
df.memory_usage(
    deep=True
)
```

Calculate total memory:

```python
total_memory = (
    df.memory_usage(
        deep=True
    ).sum()
)

print(total_memory)
```

At your current level, understanding the concept is enough.

---

# 44. Inspect Dataset Sample

`head()` always returns the first rows.

To inspect random rows:

```python
df.sample(5)
```

This is useful because the first five rows may not represent the complete dataset well.

---

# 45. Initial Superstore Dataset Exploration

Load dataset:

```python
import pandas as pd


df = pd.read_csv(
    "Superstore.csv"
)
```

Preview:

```python
df.head()
```

Check last rows:

```python
df.tail()
```

Check size:

```python
df.shape
```

Check columns:

```python
df.columns
```

Check data types:

```python
df.dtypes
```

Technical summary:

```python
df.info()
```

Statistical summary:

```python
df.describe()
```

Check missing values:

```python
df.isnull().sum()
```

Check duplicates:

```python
df.duplicated().sum()
```

---

# 46. Complete Initial Data Exploration Workflow

```python
import pandas as pd


# LOAD DATASET

df = pd.read_csv(
    "Superstore.csv"
)


# PREVIEW DATASET

print("=" * 60)

print("FIRST 5 ROWS")

print("=" * 60)

print(df.head())


# LAST ROWS

print("=" * 60)

print("LAST 5 ROWS")

print("=" * 60)

print(df.tail())


# DATASET SIZE

print("=" * 60)

print("DATASET SHAPE")

print("=" * 60)

print(
    f"Rows: {df.shape[0]}"
)

print(
    f"Columns: {df.shape[1]}"
)


# COLUMN NAMES

print("=" * 60)

print("COLUMN NAMES")

print("=" * 60)

for column in df.columns:

    print(column)


# DATA TYPES

print("=" * 60)

print("DATA TYPES")

print("=" * 60)

print(df.dtypes)


# DATASET INFORMATION

print("=" * 60)

print("DATASET INFORMATION")

print("=" * 60)

df.info()


# SUMMARY STATISTICS

print("=" * 60)

print("SUMMARY STATISTICS")

print("=" * 60)

print(df.describe())


# MISSING VALUES

print("=" * 60)

print("MISSING VALUES")

print("=" * 60)

print(
    df.isnull().sum()
)


# DUPLICATE ROWS

print("=" * 60)

print("DUPLICATE ROWS")

print("=" * 60)

print(
    df.duplicated().sum()
)


# UNIQUE VALUES

print("=" * 60)

print("UNIQUE REGIONS")

print("=" * 60)

print(
    df["Region"].unique()
)


# REGION DISTRIBUTION

print("=" * 60)

print("REGION DISTRIBUTION")

print("=" * 60)

print(
    df["Region"].value_counts()
)
```

---

# 47. Better Initial Exploration Function

Instead of repeatedly writing the same commands, create a function:

```python
def inspect_dataset(df):

    print("=" * 60)

    print("DATASET SHAPE")

    print("=" * 60)

    print(
        f"Rows: {df.shape[0]}"
    )

    print(
        f"Columns: {df.shape[1]}"
    )


    print("\nCOLUMN NAMES")

    print(df.columns.tolist())


    print("\nDATA TYPES")

    print(df.dtypes)


    print("\nMISSING VALUES")

    print(df.isnull().sum())


    print("\nDUPLICATE ROWS")

    print(df.duplicated().sum())


    print("\nSUMMARY STATISTICS")

    print(df.describe())
```

Use:

```python
inspect_dataset(df)
```

This combines:

- Functions
- Pandas
- Dataset inspection
- Reusable analytics code

---

# 48. Questions to Ask During Initial Exploration

Before cleaning or analyzing a dataset, answer:

```text
How many rows are there?

How many columns are there?

What does each column represent?

What are the data types?

Are date columns stored as dates?

Are numerical columns actually numeric?

Are there missing values?

How many values are missing?

Are there duplicate rows?

What are the minimum and maximum values?

Are there suspicious values?

What categories exist?

How many unique customers exist?

How many unique products exist?

Does the data appear ready for analysis?
```

This is the real purpose of Pandas Fundamentals.

Running commands without interpreting the output is not Data Analysis.

---

# 49. Data Analyst Example — Dataset Health Summary

```python
import pandas as pd


df = pd.read_csv(
    "Superstore.csv"
)


total_rows = df.shape[0]

total_columns = df.shape[1]

total_missing = (
    df.isnull()
    .sum()
    .sum()
)

duplicate_rows = (
    df.duplicated()
    .sum()
)

unique_customers = (
    df["Customer ID"]
    .nunique()
)

unique_products = (
    df["Product ID"]
    .nunique()
)


print("=" * 55)

print("DATASET HEALTH SUMMARY")

print("=" * 55)

print(
    f"Total Rows: {total_rows:,}"
)

print(
    f"Total Columns: {total_columns}"
)

print(
    f"Missing Values: {total_missing}"
)

print(
    f"Duplicate Rows: {duplicate_rows}"
)

print(
    f"Unique Customers: {unique_customers:,}"
)

print(
    f"Unique Products: {unique_products:,}"
)

print("=" * 55)
```

---

# 50. Initial Business Data Review

After inspecting the technical structure, begin understanding the business data.

Example:

```python
print(
    df["Category"].unique()
)
```

```python
print(
    df["Region"].unique()
)
```

```python
print(
    df["Segment"].unique()
)
```

```python
print(
    df["Ship Mode"].unique()
)
```

```python
print(
    df["Customer ID"].nunique()
)
```

```python
print(
    df["Product ID"].nunique()
)
```

This helps answer:

```text
What business dimensions exist?

How many customers exist?

How many products exist?

Which categories exist?

Which regions exist?
```

---

# 51. Technical Inspection vs Business Inspection

## Technical Inspection

Focuses on:

- Rows
- Columns
- Data types
- Missing values
- Duplicates
- Memory usage

Commands:

```python
df.shape

df.columns

df.dtypes

df.info()

df.isnull().sum()

df.duplicated().sum()
```

## Business Inspection

Focuses on:

- Customers
- Products
- Categories
- Regions
- Segments
- Business measures

Commands:

```python
df["Customer ID"].nunique()

df["Product ID"].nunique()

df["Category"].unique()

df["Region"].value_counts()

df["Sales"].describe()
```

A Data Analyst should do both.

---

# 52. Most Important Pandas Fundamentals

| Concept | Purpose |
|---|---|
| `pd.Series()` | Create one-dimensional data |
| `pd.DataFrame()` | Create tabular data |
| `pd.read_csv()` | Load CSV files |
| `pd.read_excel()` | Load Excel files |
| `head()` | Preview first rows |
| `tail()` | Preview last rows |
| `sample()` | Preview random rows |
| `shape` | Check rows and columns |
| `columns` | Check column names |
| `index` | Inspect row index |
| `dtypes` | Check data types |
| `info()` | Dataset technical summary |
| `describe()` | Statistical summary |
| `unique()` | Return unique values |
| `nunique()` | Count unique values |
| `value_counts()` | Count category frequency |
| `isnull()` | Detect missing values |
| `duplicated()` | Detect duplicate rows |

---

# 53. What You Should Prioritize

For Data Analyst work, master:

```text
Series

DataFrame

read_csv()

read_excel()

head()

tail()

sample()

shape

columns

dtypes

info()

describe()

unique()

nunique()

value_counts()

isnull().sum()

duplicated().sum()
```

Do not waste time memorizing every Pandas function.

Your goal at this stage is simple:

```text
Load Dataset

Inspect Dataset

Understand Structure

Identify Data Quality Problems

Understand Business Data

Prepare for Cleaning
```

---

# 54. Core Patterns to Remember

## Import Pandas

```python
import pandas as pd
```

## Load CSV

```python
df = pd.read_csv(
    "Superstore.csv"
)
```

## Load Excel

```python
df = pd.read_excel(
    "Superstore.xlsx"
)
```

## Preview Dataset

```python
df.head()
```

## Check Dataset Size

```python
df.shape
```

## Check Column Names

```python
df.columns
```

## Check Data Types

```python
df.dtypes
```

## Get Technical Summary

```python
df.info()
```

## Get Statistical Summary

```python
df.describe()
```

## Check Missing Values

```python
df.isnull().sum()
```

## Check Duplicates

```python
df.duplicated().sum()
```

## Count Unique Values

```python
df["Customer ID"].nunique()
```

## Check Category Distribution

```python
df["Region"].value_counts()
```

---

# 55. Common Beginner Errors

## Forgetting to Import Pandas

Wrong:

```python
df = pd.read_csv(
    "Superstore.csv"
)
```

without:

```python
import pandas as pd
```

---

## Incorrect File Path

This:

```python
pd.read_csv(
    "Superstore.csv"
)
```

causes:

```text
FileNotFoundError
```

if the file is not in the expected location.

Check:

```python
from pathlib import Path

file_path = Path(
    "Superstore.csv"
)

print(file_path.exists())
```

---

## Using Parentheses with shape

Wrong:

```python
df.shape()
```

Correct:

```python
df.shape
```

`shape` is an attribute, not a method.

---

## Using Parentheses with columns

Wrong:

```python
df.columns()
```

Correct:

```python
df.columns
```

---

## Forgetting Parentheses with info()

Wrong:

```python
df.info
```

Correct:

```python
df.info()
```

---

## Forgetting Parentheses with describe()

Wrong:

```python
df.describe
```

Correct:

```python
df.describe()
```

---

## Confusing Series and DataFrame Selection

This:

```python
df["Sales"]
```

returns:

```text
Series
```

This:

```python
df[["Sales"]]
```

returns:

```text
DataFrame
```

---

## Starting Analysis Before Inspecting Data

Bad workflow:

```text
Load Data
    ↓
Immediately Calculate KPIs
```

Better workflow:

```text
Load Data
    ↓
Inspect Structure
    ↓
Check Data Types
    ↓
Check Missing Values
    ↓
Check Duplicates
    ↓
Understand Business Columns
    ↓
Clean Data
    ↓
Analyze Data
```

---

# 56. Interview Questions

1. What is Pandas?
2. Why is Pandas useful for Data Analysts?
3. What is a Series?
4. What is a DataFrame?
5. What is the difference between a Series and DataFrame?
6. How do you create a Series?
7. How do you create a DataFrame?
8. How do you load a CSV file?
9. How do you load an Excel file?
10. What does `head()` do?
11. What does `tail()` do?
12. What does `sample()` do?
13. What does `shape` return?
14. What does `columns` return?
15. What does `dtypes` return?
16. What information does `info()` provide?
17. What does `describe()` return?
18. What is the difference between `info()` and `describe()`?
19. How do you check for missing values?
20. How do you count total missing values?
21. How do you check for duplicate rows?
22. What does `unique()` return?
23. What does `nunique()` return?
24. What does `value_counts()` do?
25. What is the difference between `df["Sales"]` and `df[["Sales"]]`?
26. How would you identify columns with missing values?
27. How would you calculate missing-value percentages?
28. What should you inspect immediately after loading a dataset?
29. What is the difference between technical inspection and business inspection?
30. Why is understanding the dataset necessary before cleaning and analysis?

---

# 57. Completion Checklist

Before moving to Data Cleaning with Pandas, you should be able to:

- [ ] Import Pandas
- [ ] Explain Series
- [ ] Create a Series
- [ ] Explain DataFrames
- [ ] Create a DataFrame
- [ ] Explain Series vs DataFrame
- [ ] Load CSV files
- [ ] Load Excel files
- [ ] Load a specific Excel sheet
- [ ] Use `head()`
- [ ] Use `tail()`
- [ ] Use `sample()`
- [ ] Use `shape`
- [ ] Use `columns`
- [ ] Use `index`
- [ ] Use `dtypes`
- [ ] Use `info()`
- [ ] Use `describe()`
- [ ] Understand basic summary statistics
- [ ] Select one column
- [ ] Select multiple columns
- [ ] Explain Series vs DataFrame column selection
- [ ] Use `unique()`
- [ ] Use `nunique()`
- [ ] Use `value_counts()`
- [ ] Detect missing values
- [ ] Count missing values
- [ ] Calculate missing-value percentages
- [ ] Identify only columns containing missing values
- [ ] Detect duplicate rows
- [ ] Inspect random dataset samples
- [ ] Load the Superstore dataset
- [ ] Inspect Superstore structure
- [ ] Review Superstore data types
- [ ] Identify Superstore missing values
- [ ] Identify Superstore duplicate rows
- [ ] Review business categories
- [ ] Count unique customers
- [ ] Count unique products
- [ ] Create a basic dataset health summary
- [ ] Perform initial data exploration before analysis

---

# Final Outcome

After completing Pandas Fundamentals, you should be able to create Series and DataFrames, load CSV and Excel files, load the Superstore dataset, inspect rows and columns, review dataset structure, check data types, generate statistical summaries, identify missing values and duplicate rows, inspect categorical data, count unique customers and products, and perform a complete initial dataset exploration before beginning data cleaning and business analysis.