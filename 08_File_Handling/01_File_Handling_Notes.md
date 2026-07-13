# File Handling

## 1. Introduction

File handling allows Python programs to read data from files, write data to files, and save processed results.

For Data Analysts, file handling is useful for:

- Reading sales and customer data
- Processing daily business files
- Saving cleaned datasets
- Creating KPI summary reports
- Working with CSV files
- Working with JSON data
- Managing file paths
- Automating repetitive reporting workflows

The most important topics are:

- File Paths
- `open()`
- Reading Text Files
- Writing Text Files
- `with` Statement
- CSV Files
- JSON Basics
- Basic File Processing Workflow

---

# 2. Basic File Handling Workflow

The basic workflow is:

```text
Open File
    ↓
Read Data
    ↓
Process / Clean Data
    ↓
Write Results
    ↓
Close File
```

Example:

```python
file = open("sales.txt", "r")

data = file.read()

file.close()
```

A better and recommended approach is:

```python
with open("sales.txt", "r") as file:
    data = file.read()
```

The `with` statement automatically closes the file.

---

# 3. File Paths

A file path tells Python where a file is located.

Example project structure:

```text
Python-Data-Analytics/
│
├── 08_File_Handling/
│   ├── File_Handling_Notes.md
│   ├── File_Handling_Practice.ipynb
│   │
│   └── data/
│       ├── sales.csv
│       └── customers.csv
```

If the notebook is inside:

```text
08_File_Handling/
```

the relative path can be:

```python
"data/sales.csv"
```

---

# 4. Absolute Path vs Relative Path

## Absolute Path

An absolute path contains the complete file location.

Example:

```python
file_path = "C:/Python-Data-Analytics/08_File_Handling/data/sales.csv"
```

## Relative Path

A relative path is based on the current working directory.

Example:

```python
file_path = "data/sales.csv"
```

For projects, relative paths are generally better because absolute paths often break when the project is moved to another computer.

---

# 5. pathlib

`pathlib` provides a cleaner way to work with file paths.

```python
from pathlib import Path
```

Create a path:

```python
file_path = Path("data/sales.csv")
```

Check whether a file exists:

```python
print(file_path.exists())
```

Output:

```text
True
```

For modern Python projects, `pathlib` is worth learning.

---

# 6. open() Function

The `open()` function opens a file.

Syntax:

```python
open(file_path, mode)
```

Example:

```python
file = open("sales.txt", "r")
```

Common file modes:

| Mode | Purpose |
|---|---|
| `"r"` | Read |
| `"w"` | Write |
| `"a"` | Append |

These three modes are enough for your current Data Analyst level.

---

# 7. Read Mode

Use `"r"` to read an existing file.

```python
file = open("sales.txt", "r")

data = file.read()

print(data)

file.close()
```

If the file does not exist, Python raises:

```text
FileNotFoundError
```

---

# 8. Write Mode

Use `"w"` to write data to a file.

```python
file = open("kpi_report.txt", "w")

file.write("Total Revenue: 1500000")

file.close()
```

Important:

```text
"w" overwrites existing file content.
```

If the file does not exist, Python creates it.

---

# 9. Append Mode

Use `"a"` to add content without deleting existing data.

```python
file = open("kpi_report.txt", "a")

file.write("\nTotal Profit: 350000")

file.close()
```

Remember:

```text
r → Read

w → Write / Overwrite

a → Add to Existing Content
```

---

# 10. The with Statement

The recommended method for working with files is:

```python
with open("sales.txt", "r") as file:

    data = file.read()
```

Why use `with`?

- Automatically closes the file
- Cleaner code
- Safer file handling
- Standard Python practice

Prefer:

```python
with open(...)
```

instead of manually using:

```python
file.close()
```

---

# 11. Reading Entire File

Use `read()`.

```python
with open("sales.txt", "r") as file:

    data = file.read()

print(data)
```

`read()` returns the complete file content as one string.

---

# 12. Reading One Line

Use `readline()`.

```python
with open("sales.txt", "r") as file:

    first_line = file.readline()

print(first_line)
```

This reads one line at a time.

---

# 13. Reading All Lines

Use `readlines()`.

```python
with open("sales.txt", "r") as file:

    lines = file.readlines()

print(lines)
```

The result is a list.

Example:

```text
[
    "Laptop,850000\n",
    "Mobile,1250000\n",
    "Tablet,650000\n"
]
```

---

# 14. Reading Files Using a Loop

A memory-friendly approach is to process the file line by line.

```python
with open("sales.txt", "r") as file:

    for line in file:

        print(line.strip())
```

For large files, processing line by line can be better than loading the complete file at once.

---

# 15. Writing Text Files

Use `write()`.

```python
with open("report.txt", "w") as file:

    file.write("BUSINESS KPI REPORT")
```

Write multiple lines:

```python
with open("report.txt", "w") as file:

    file.write("Revenue: 1500000\n")

    file.write("Profit: 350000\n")

    file.write("Orders: 2500\n")
```

`\n` creates a new line.

---

# 16. Writing KPI Summary Report

```python
revenue = 1500000

cost = 1150000

orders = 2500

profit = revenue - cost

profit_margin = (profit / revenue) * 100

average_order_value = revenue / orders
```

Write the results:

```python
with open("kpi_summary.txt", "w") as file:

    file.write("BUSINESS KPI SUMMARY\n")

    file.write("=" * 40 + "\n")

    file.write(f"Revenue: ₹{revenue:,.2f}\n")

    file.write(f"Profit: ₹{profit:,.2f}\n")

    file.write(f"Profit Margin: {profit_margin:.2f}%\n")

    file.write(
        f"Average Order Value: ₹{average_order_value:,.2f}\n"
    )
```

This creates a reusable business report file.

---

# 17. CSV Files

CSV stands for:

```text
Comma-Separated Values
```

Example:

```text
Product,Sales,Profit
Laptop,850000,175000
Mobile,1250000,275000
Tablet,650000,95000
```

CSV is one of the most common file formats used by Data Analysts.

---

# 18. csv Module

Python provides the built-in `csv` module.

Import it:

```python
import csv
```

---

# 19. Reading CSV Files

```python
import csv

with open("sales.csv", "r") as file:

    reader = csv.reader(file)

    for row in reader:

        print(row)
```

Each row is returned as a list.

Example:

```text
["Laptop", "850000", "175000"]
```

---

# 20. Reading CSV Using DictReader

`DictReader` reads each row as a dictionary.

Consider:

```text
Product,Sales,Profit
Laptop,850000,175000
Mobile,1250000,275000
```

Code:

```python
import csv

with open("sales.csv", "r") as file:

    reader = csv.DictReader(file)

    for row in reader:

        print(row)
```

Each row becomes:

```python
{
    "Product": "Laptop",
    "Sales": "850000",
    "Profit": "175000"
}
```

For beginner business data processing, `DictReader` is easier to understand because column names can be used directly.

---

# 21. Accessing CSV Columns

```python
import csv

with open("sales.csv", "r") as file:

    reader = csv.DictReader(file)

    for row in reader:

        product = row["Product"]

        sales = row["Sales"]

        print(product, sales)
```

---

# 22. Important CSV Data Type Problem

Values read from CSV files are usually strings.

Example:

```python
sales = row["Sales"]
```

The value may look like:

```text
850000
```

but its data type is:

```text
str
```

Convert it:

```python
sales = float(row["Sales"])
```

or:

```python
sales = int(row["Sales"])
```

This is extremely important when performing calculations.

---

# 23. Calculate Total Sales from CSV

```python
import csv

total_sales = 0

with open("sales.csv", "r") as file:

    reader = csv.DictReader(file)

    for row in reader:

        sales = float(row["Sales"])

        total_sales += sales

print(f"Total Sales: ₹{total_sales:,.2f}")
```

---

# 24. Writing CSV Files

Use `csv.writer()`.

```python
import csv

with open("cleaned_sales.csv", "w", newline="") as file:

    writer = csv.writer(file)

    writer.writerow([
        "Product",
        "Sales",
        "Profit"
    ])

    writer.writerow([
        "Laptop",
        850000,
        175000
    ])
```

`newline=""` helps prevent unnecessary blank lines when writing CSV files.

---

# 25. Writing CSV Using DictWriter

```python
import csv

fieldnames = [
    "Product",
    "Sales",
    "Profit"
]

with open("cleaned_sales.csv", "w", newline="") as file:

    writer = csv.DictWriter(
        file,
        fieldnames=fieldnames
    )

    writer.writeheader()

    writer.writerow({
        "Product": "Laptop",
        "Sales": 850000,
        "Profit": 175000
    })
```

---

# 26. Read sales.csv and Save cleaned_sales.csv

Suppose `sales.csv` contains:

```text
Product,Sales,Profit
 laptop ,850000,175000
 MOBILE,1250000,275000
 tablet ,650000,95000
```

Clean the product names:

```python
import csv

cleaned_data = []

with open("sales.csv", "r") as file:

    reader = csv.DictReader(file)

    for row in reader:

        product = row["Product"].strip().title()

        sales = float(row["Sales"])

        profit = float(row["Profit"])

        cleaned_data.append({
            "Product": product,
            "Sales": sales,
            "Profit": profit
        })
```

Write cleaned data:

```python
with open("cleaned_sales.csv", "w", newline="") as file:

    fieldnames = [
        "Product",
        "Sales",
        "Profit"
    ]

    writer = csv.DictWriter(
        file,
        fieldnames=fieldnames
    )

    writer.writeheader()

    writer.writerows(cleaned_data)
```

This is a basic Data Analyst workflow:

```text
Read Raw Data
    ↓
Clean Data
    ↓
Save Processed Data
```

---

# 27. JSON Basics

JSON stands for:

```text
JavaScript Object Notation
```

JSON stores structured data.

Example:

```json
{
    "Company": "ShopKart India",
    "Revenue": 1500000,
    "Profit": 350000
}
```

JSON data is similar to Python dictionaries.

---

# 28. json Module

Import the built-in module:

```python
import json
```

---

# 29. Reading JSON Files

Suppose `business_data.json` contains:

```json
{
    "Company": "ShopKart India",
    "Revenue": 1500000,
    "Profit": 350000
}
```

Read it:

```python
import json

with open("business_data.json", "r") as file:

    business_data = json.load(file)

print(business_data)
```

Access values:

```python
print(business_data["Company"])

print(business_data["Revenue"])
```

---

# 30. Writing JSON Files

```python
import json

business_kpis = {
    "Revenue": 1500000,
    "Profit": 350000,
    "Orders": 2500
}

with open("business_kpis.json", "w") as file:

    json.dump(
        business_kpis,
        file,
        indent=4
    )
```

`indent=4` makes the JSON file easier to read.

---

# 31. json.load() vs json.dump()

Remember:

```text
json.load()

JSON File → Python Object
```

```text
json.dump()

Python Object → JSON File
```

---

# 32. Read customers.csv

```python
import csv

with open("customers.csv", "r") as file:

    reader = csv.DictReader(file)

    for row in reader:

        customer_name = row["CustomerName"].strip().title()

        city = row["City"].strip().title()

        print(customer_name, city)
```

This combines:

- File Handling
- CSV
- Dictionaries
- Loops
- Strings
- Data Cleaning

---

# 33. Import Daily Sales Files

Suppose a folder contains:

```text
daily_sales/
│
├── sales_monday.csv
├── sales_tuesday.csv
├── sales_wednesday.csv
```

Use `pathlib`:

```python
from pathlib import Path

sales_folder = Path("daily_sales")

sales_files = sales_folder.glob("*.csv")

for file in sales_files:

    print(file)
```

This finds all CSV files in the folder.

---

# 34. Process Multiple Daily Sales Files

```python
import csv

from pathlib import Path


sales_folder = Path("daily_sales")

sales_files = sales_folder.glob("*.csv")


for file_path in sales_files:

    print(f"Processing: {file_path.name}")

    with open(file_path, "r") as file:

        reader = csv.DictReader(file)

        for row in reader:

            product = row["Product"].strip().title()

            sales = float(row["Sales"])

            print(product, sales)
```

This is the foundation of file-processing automation.

---

# 35. Complete Data Analyst File Workflow

```python
import csv

from pathlib import Path


# FILE PATHS

input_file = Path("sales.csv")

output_file = Path("cleaned_sales.csv")

report_file = Path("kpi_summary.txt")


# STORAGE

cleaned_data = []

total_sales = 0

total_profit = 0


# READ AND CLEAN DATA

with open(input_file, "r") as file:

    reader = csv.DictReader(file)

    for row in reader:

        product = row["Product"].strip().title()

        sales = float(row["Sales"])

        profit = float(row["Profit"])

        total_sales += sales

        total_profit += profit

        cleaned_data.append({
            "Product": product,
            "Sales": sales,
            "Profit": profit
        })


# CALCULATE KPI

profit_margin = (
    total_profit / total_sales
) * 100


# SAVE CLEANED DATA

with open(output_file, "w", newline="") as file:

    fieldnames = [
        "Product",
        "Sales",
        "Profit"
    ]

    writer = csv.DictWriter(
        file,
        fieldnames=fieldnames
    )

    writer.writeheader()

    writer.writerows(cleaned_data)


# SAVE KPI REPORT

with open(report_file, "w") as file:

    file.write("BUSINESS KPI SUMMARY\n")

    file.write("=" * 40 + "\n")

    file.write(
        f"Total Sales: ₹{total_sales:,.2f}\n"
    )

    file.write(
        f"Total Profit: ₹{total_profit:,.2f}\n"
    )

    file.write(
        f"Profit Margin: {profit_margin:.2f}%\n"
    )


print("Data Processing Completed")
```

---

# 36. Most Important Concepts

## Open Files Safely

```python
with open(file_path, mode) as file:
```

## Read Complete Text

```python
file.read()
```

## Process Line by Line

```python
for line in file:
```

## Write Data

```python
file.write()
```

## Read CSV Data

```python
csv.DictReader(file)
```

## Write CSV Data

```python
csv.DictWriter()
```

## Read JSON

```python
json.load(file)
```

## Write JSON

```python
json.dump(data, file)
```

## Manage Paths

```python
Path("data/sales.csv")
```

---

# 37. Common Beginner Errors

## Incorrect File Path

```python
with open("sales.csv", "r") as file:
```

may cause:

```text
FileNotFoundError
```

Check your current working directory and file location.

---

## Forgetting File Mode

Always specify what you want to do:

```python
"r"
```

```python
"w"
```

```python
"a"
```

---

## Accidentally Overwriting a File

Using:

```python
"w"
```

deletes the existing content before writing new content.

Use:

```python
"a"
```

when you need to add content.

---

## Forgetting CSV Values Are Strings

Wrong:

```python
total_sales += row["Sales"]
```

Correct:

```python
total_sales += float(row["Sales"])
```

---

## Not Using with

Avoid unnecessary manual file management:

```python
file = open("sales.csv", "r")

file.close()
```

Prefer:

```python
with open("sales.csv", "r") as file:
```

---

# 38. Interview Questions

1. What is file handling?
2. Why is file handling useful for Data Analysts?
3. What is the difference between absolute and relative paths?
4. What does `open()` do?
5. What is the difference between `"r"`, `"w"`, and `"a"`?
6. Why should you use the `with` statement?
7. What is the difference between `read()`, `readline()`, and `readlines()`?
8. What is a CSV file?
9. What is the difference between `csv.reader()` and `csv.DictReader()`?
10. Why should CSV numeric values be converted before calculations?
11. What does `csv.DictWriter()` do?
12. Why is `newline=""` used when writing CSV files?
13. What is JSON?
14. What is the difference between `json.load()` and `json.dump()`?
15. What is `pathlib`?
16. How would you check whether a file exists?
17. How would you find all CSV files inside a folder?
18. How would you read `sales.csv` and save `cleaned_sales.csv`?
19. How would you generate a KPI summary text report?
20. How would you process multiple daily sales files automatically?

---

# 39. Completion Checklist

Before moving to the next module, you should be able to:

- [ ] Explain file handling
- [ ] Understand file paths
- [ ] Explain absolute vs relative paths
- [ ] Use `pathlib`
- [ ] Use `open()`
- [ ] Use `"r"` mode
- [ ] Use `"w"` mode
- [ ] Use `"a"` mode
- [ ] Use the `with` statement
- [ ] Use `read()`
- [ ] Use `readline()`
- [ ] Use `readlines()`
- [ ] Process files line by line
- [ ] Write text files
- [ ] Create KPI summary reports
- [ ] Explain CSV files
- [ ] Use `csv.reader()`
- [ ] Use `csv.DictReader()`
- [ ] Convert CSV values to correct data types
- [ ] Calculate KPIs from CSV data
- [ ] Use `csv.writer()`
- [ ] Use `csv.DictWriter()`
- [ ] Read `sales.csv`
- [ ] Read `customers.csv`
- [ ] Save `cleaned_sales.csv`
- [ ] Understand basic JSON
- [ ] Use `json.load()`
- [ ] Use `json.dump()`
- [ ] Find multiple CSV files using `pathlib`
- [ ] Process daily sales files
- [ ] Build a basic Read → Clean → Process → Save workflow

---

# Final Outcome

After completing File Handling, you should be able to read and write text files, work with CSV and basic JSON data, manage file paths using `pathlib`, read sales and customer datasets, clean raw business data, save processed CSV files, generate KPI summary reports, and process multiple daily sales files as the foundation for Python reporting automation.