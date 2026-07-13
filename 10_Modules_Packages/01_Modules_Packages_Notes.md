# Modules & Packages

## 1. Introduction

A module is a Python file containing reusable code.

A package is a collection of related Python modules.

Modules and packages help organize code and avoid rewriting existing functionality.

For Data Analysts, the most useful concepts are:

- `import`
- `from ... import`
- Aliases
- `datetime`
- `math`
- `os`
- `pathlib`
- `random`
- Creating Custom Modules

Practical analytics use cases include:

- Generate timestamped report names
- Create report folders automatically
- Organize exported files
- Work with dates and times
- Perform mathematical calculations
- Generate sample data
- Calculate processing time
- Build reusable analytics functions
- Automatically generate daily business reports

---

# 2. What Is a Module?

A module is simply a Python file containing reusable Python code.

Example:

```text
kpi_calculations.py
```

Inside the file:

```python
def calculate_profit(revenue, cost):

    return revenue - cost
```

Another Python file can import and reuse this function.

```python
import kpi_calculations
```

Use:

```python
profit = kpi_calculations.calculate_profit(
    850000,
    620000
)
```

The main principle is:

```text
Write Code Once
      ↓
Store in Module
      ↓
Import
      ↓
Reuse Multiple Times
```

---

# 3. What Is a Package?

A package is a collection of related Python modules.

Example:

```text
analytics/
│
├── __init__.py
├── kpi_calculations.py
├── data_cleaning.py
└── report_generation.py
```

Here:

```text
analytics
```

is the package.

The Python files inside it are modules.

---

# 4. Module vs Package

| Module | Package |
|---|---|
| Single Python file | Collection of modules |
| Contains reusable code | Organizes related modules |
| Example: `math` | Example: `pandas` |

Remember:

```text
Module
→ One Python File

Package
→ Collection of Related Modules
```

---

# 5. import Statement

Use `import` to load a module.

Example:

```python
import math
```

Use functions from the module:

```python
result = math.sqrt(100)

print(result)
```

Output:

```text
10.0
```

---

# 6. Import Specific Functions

Instead of importing the complete module:

```python
import math
```

you can import a specific function:

```python
from math import sqrt
```

Use:

```python
result = sqrt(100)

print(result)
```

---

# 7. Import Multiple Functions

```python
from math import sqrt, ceil, floor
```

Use:

```python
print(sqrt(100))

print(ceil(10.25))

print(floor(10.75))
```

---

# 8. Aliases

An alias gives a module a shorter name.

Syntax:

```python
import module_name as alias
```

Example:

```python
import datetime as dt
```

Use:

```python
current_date = dt.date.today()

print(current_date)
```

You will later commonly use:

```python
import numpy as np

import pandas as pd

import matplotlib.pyplot as plt
```

These aliases are standard conventions.

---

# 9. Avoid import *

Avoid:

```python
from math import *
```

This imports everything into the current namespace.

Problems:

- Makes code harder to understand
- Can cause naming conflicts
- Makes it unclear where functions came from

Prefer:

```python
import math
```

or:

```python
from math import sqrt
```

---

# 10. datetime Module

The `datetime` module is used to work with dates and times.

Import:

```python
import datetime
```

Get today's date:

```python
today = datetime.date.today()

print(today)
```

Example output:

```text
2026-07-13
```

---

# 11. Get Current Date and Time

```python
from datetime import datetime

current_datetime = datetime.now()

print(current_datetime)
```

Example:

```text
2026-07-13 21:30:45.123456
```

---

# 12. Get Current Date

```python
from datetime import date

today = date.today()

print(today)
```

---

# 13. Extract Date Components

```python
from datetime import datetime

current_datetime = datetime.now()

print(current_datetime.year)

print(current_datetime.month)

print(current_datetime.day)
```

You can also access:

```python
current_datetime.hour

current_datetime.minute

current_datetime.second
```

---

# 14. strftime()

`strftime()` converts a date or time into a formatted string.

Example:

```python
from datetime import datetime

current_datetime = datetime.now()

formatted_date = current_datetime.strftime(
    "%Y-%m-%d"
)

print(formatted_date)
```

Output:

```text
2026-07-13
```

---

# 15. Important Date Format Codes

| Code | Meaning |
|---|---|
| `%Y` | Four-digit year |
| `%m` | Month number |
| `%d` | Day |
| `%H` | Hour |
| `%M` | Minute |
| `%S` | Second |

Example:

```python
timestamp = datetime.now().strftime(
    "%Y%m%d_%H%M%S"
)
```

Possible output:

```text
20260713_213045
```

This is extremely useful for automatically naming report files.

---

# 16. Generate Timestamped Report Name

```python
from datetime import datetime

timestamp = datetime.now().strftime(
    "%Y%m%d_%H%M%S"
)

report_name = f"sales_report_{timestamp}.csv"

print(report_name)
```

Example output:

```text
sales_report_20260713_213045.csv
```

This prevents reports from accidentally overwriting previous files.

---

# 17. Generate Daily Report Name

```python
from datetime import date

today = date.today()

report_name = f"sales_report_{today}.csv"

print(report_name)
```

Output:

```text
sales_report_2026-07-13.csv
```

---

# 18. math Module

The `math` module provides mathematical functions.

Import:

```python
import math
```

Useful functions include:

- `sqrt()`
- `ceil()`
- `floor()`

---

# 19. math.sqrt()

Calculates square root.

```python
import math

result = math.sqrt(100)

print(result)
```

Output:

```text
10.0
```

---

# 20. math.ceil()

Rounds a number upward.

```python
import math

orders = 125.25

result = math.ceil(orders)

print(result)
```

Output:

```text
126
```

---

# 21. math.floor()

Rounds a number downward.

```python
import math

orders = 125.95

result = math.floor(orders)

print(result)
```

Output:

```text
125
```

---

# 22. os Module

The `os` module provides tools for interacting with the operating system.

Import:

```python
import os
```

Common uses:

- Get current working directory
- Create folders
- Check files and directories
- Work with file paths

---

# 23. Get Current Working Directory

```python
import os

current_directory = os.getcwd()

print(current_directory)
```

This helps identify where Python is currently running.

It is useful when debugging:

```text
FileNotFoundError
```

---

# 24. List Files in a Directory

```python
import os

files = os.listdir()

print(files)
```

Specify a directory:

```python
files = os.listdir("data")

print(files)
```

---

# 25. Create a Folder Using os

```python
import os

os.mkdir("reports")
```

This creates:

```text
reports/
```

But if the folder already exists, it raises an error.

A safer approach:

```python
os.makedirs(
    "reports",
    exist_ok=True
)
```

---

# 26. pathlib Module

`pathlib` provides a modern and cleaner way to work with files and folders.

Import:

```python
from pathlib import Path
```

Create a path:

```python
report_folder = Path("reports")
```

---

# 27. Create Report Folder

```python
from pathlib import Path

report_folder = Path("reports")

report_folder.mkdir(
    exist_ok=True
)
```

If the folder already exists, no error occurs.

---

# 28. Create Nested Folders

```python
from pathlib import Path

report_folder = Path(
    "exports/daily_reports"
)

report_folder.mkdir(
    parents=True,
    exist_ok=True
)
```

This creates:

```text
exports/
│
└── daily_reports/
```

---

# 29. Check Whether File Exists

```python
from pathlib import Path

file_path = Path("data/sales.csv")

print(file_path.exists())
```

Output:

```text
True
```

or:

```text
False
```

---

# 30. Check Whether Path Is a File

```python
file_path.is_file()
```

---

# 31. Check Whether Path Is a Directory

```python
file_path.is_dir()
```

---

# 32. Get File Name

```python
from pathlib import Path

file_path = Path(
    "data/sales_report.csv"
)

print(file_path.name)
```

Output:

```text
sales_report.csv
```

---

# 33. Get File Extension

```python
print(file_path.suffix)
```

Output:

```text
.csv
```

---

# 34. Get File Name Without Extension

```python
print(file_path.stem)
```

Output:

```text
sales_report
```

---

# 35. Find All CSV Files

Suppose:

```text
data/
│
├── sales.csv
├── customers.csv
├── products.csv
└── notes.txt
```

Use:

```python
from pathlib import Path

data_folder = Path("data")

csv_files = data_folder.glob("*.csv")

for file in csv_files:

    print(file)
```

Only CSV files are returned.

This is very useful for batch processing.

---

# 36. os vs pathlib

Both can manage files and folders.

Older approach:

```python
import os

os.makedirs(
    "reports/daily",
    exist_ok=True
)
```

Modern approach:

```python
from pathlib import Path

Path(
    "reports/daily"
).mkdir(
    parents=True,
    exist_ok=True
)
```

For new Python data analytics projects, prefer:

```text
pathlib
```

You should still understand basic `os` because you will see it in existing code.

---

# 37. random Module

The `random` module generates random values.

Import:

```python
import random
```

For Data Analysts, it is mainly useful for:

- Creating practice data
- Selecting random samples
- Testing code

---

# 38. Generate Random Integer

```python
import random

sales = random.randint(
    50000,
    500000
)

print(sales)
```

---

# 39. Select Random Value

```python
import random

regions = [
    "South",
    "North",
    "East",
    "West"
]

selected_region = random.choice(regions)

print(selected_region)
```

---

# 40. Select Random Sample

```python
import random

customer_ids = [
    101,
    102,
    103,
    104,
    105
]

sample_customers = random.sample(
    customer_ids,
    3
)

print(sample_customers)
```

---

# 41. Generate Practice Sales Data

```python
import random

monthly_sales = []

for month in range(12):

    sales = random.randint(
        500000,
        1500000
    )

    monthly_sales.append(sales)

print(monthly_sales)
```

This is useful for creating temporary practice datasets.

---

# 42. Calculate Processing Time

The `time` module can measure how long code takes to execute.

Import:

```python
import time
```

Record starting time:

```python
start_time = time.time()
```

Run code:

```python
total = 0

for number in range(1000000):

    total += number
```

Record ending time:

```python
end_time = time.time()
```

Calculate processing time:

```python
processing_time = end_time - start_time

print(
    f"Processing Time: {processing_time:.4f} seconds"
)
```

---

# 43. Data Processing Time Example

```python
import time

start_time = time.time()


sales = [
    850000,
    920000,
    780000,
    1050000
]

total_sales = sum(sales)

average_sales = (
    total_sales / len(sales)
)


end_time = time.time()

processing_time = (
    end_time - start_time
)


print(
    f"Total Sales: ₹{total_sales:,.2f}"
)

print(
    f"Average Sales: ₹{average_sales:,.2f}"
)

print(
    f"Processing Time: {processing_time:.6f} seconds"
)
```

---

# 44. Automatically Create Report Folder

```python
from pathlib import Path

report_folder = Path("reports")

report_folder.mkdir(
    exist_ok=True
)

print("Report folder is ready")
```

---

# 45. Automatically Generate Daily Report Path

```python
from datetime import date

from pathlib import Path


report_folder = Path("reports")

report_folder.mkdir(
    exist_ok=True
)


today = date.today()

report_name = (
    f"sales_report_{today}.txt"
)

report_path = (
    report_folder / report_name
)

print(report_path)
```

Possible output:

```text
reports/sales_report_2026-07-13.txt
```

---

# 46. Save Daily Business Report

```python
from datetime import date

from pathlib import Path


revenue = 1500000

cost = 1150000

orders = 2500


profit = revenue - cost

profit_margin = (
    profit / revenue
) * 100

average_order_value = (
    revenue / orders
)


report_folder = Path("reports")

report_folder.mkdir(
    exist_ok=True
)


today = date.today()

report_name = (
    f"sales_report_{today}.txt"
)

report_path = (
    report_folder / report_name
)


with open(report_path, "w") as file:

    file.write(
        "DAILY BUSINESS REPORT\n"
    )

    file.write(
        "=" * 45 + "\n"
    )

    file.write(
        f"Report Date: {today}\n"
    )

    file.write(
        f"Revenue: ₹{revenue:,.2f}\n"
    )

    file.write(
        f"Profit: ₹{profit:,.2f}\n"
    )

    file.write(
        f"Profit Margin: {profit_margin:.2f}%\n"
    )

    file.write(
        f"Average Order Value: ₹{average_order_value:,.2f}\n"
    )


print(
    f"Report Created: {report_path}"
)
```

This combines:

- Modules
- `datetime`
- `pathlib`
- File Handling
- Functions
- Business KPIs

---

# 47. Timestamped Report Generation

Daily filenames can overwrite reports if the script runs multiple times on the same day.

A better solution is to use timestamps.

```python
from datetime import datetime

from pathlib import Path


report_folder = Path("reports")

report_folder.mkdir(
    exist_ok=True
)


timestamp = datetime.now().strftime(
    "%Y%m%d_%H%M%S"
)


report_name = (
    f"sales_report_{timestamp}.txt"
)


report_path = (
    report_folder / report_name
)


print(report_path)
```

Possible output:

```text
reports/sales_report_20260713_214530.txt
```

---

# 48. Organize Reports by Date

Create a folder for each day:

```python
from datetime import date

from pathlib import Path


today = date.today()


report_folder = Path(
    f"reports/{today}"
)


report_folder.mkdir(
    parents=True,
    exist_ok=True
)


print(report_folder)
```

Result:

```text
reports/
│
└── 2026-07-13/
```

---

# 49. Organize Reports by Year and Month

```python
from datetime import datetime

from pathlib import Path


current_date = datetime.now()


year = current_date.strftime("%Y")

month = current_date.strftime("%m")


report_folder = Path(
    "reports"
) / year / month


report_folder.mkdir(
    parents=True,
    exist_ok=True
)


print(report_folder)
```

Result:

```text
reports/
│
└── 2026/
    │
    └── 07/
```

This is useful for automated reporting systems.

---

# 50. Creating a Custom Module

Create:

```text
kpi_calculations.py
```

Add:

```python
def calculate_profit(
    revenue,
    cost
):

    return revenue - cost


def calculate_profit_margin(
    revenue,
    cost
):

    profit = revenue - cost

    return (
        profit / revenue
    ) * 100


def calculate_average_order_value(
    revenue,
    orders
):

    return revenue / orders
```

---

# 51. Import Custom Module

Suppose your project contains:

```text
project/
│
├── main.py
└── kpi_calculations.py
```

Inside:

```text
main.py
```

Import:

```python
import kpi_calculations
```

Use:

```python
profit = (
    kpi_calculations.calculate_profit(
        850000,
        620000
    )
)

print(profit)
```

---

# 52. Import Specific Custom Function

```python
from kpi_calculations import calculate_profit
```

Use:

```python
profit = calculate_profit(
    850000,
    620000
)
```

---

# 53. Custom Module Alias

```python
import kpi_calculations as kpi
```

Use:

```python
profit = kpi.calculate_profit(
    850000,
    620000
)
```

---

# 54. Complete Automated Daily Business Report

```python
import time

from datetime import datetime

from pathlib import Path


# START PROCESSING TIMER

start_time = time.time()


# BUSINESS DATA

company_name = "ShopKart India"

revenue = 1500000

cost = 1150000

orders = 2500


# KPI CALCULATIONS

profit = revenue - cost

profit_margin = (
    profit / revenue
) * 100

average_order_value = (
    revenue / orders
)


# CURRENT DATE AND TIME

current_datetime = datetime.now()


year = current_datetime.strftime("%Y")

month = current_datetime.strftime("%m")

timestamp = current_datetime.strftime(
    "%Y%m%d_%H%M%S"
)


# CREATE REPORT FOLDER

report_folder = (
    Path("reports")
    / year
    / month
)


report_folder.mkdir(
    parents=True,
    exist_ok=True
)


# CREATE REPORT NAME

report_name = (
    f"business_report_{timestamp}.txt"
)


report_path = (
    report_folder / report_name
)


# WRITE BUSINESS REPORT

with open(report_path, "w") as file:

    file.write(
        f"{company_name.upper()}\n"
    )

    file.write(
        "DAILY BUSINESS REPORT\n"
    )

    file.write(
        "=" * 50 + "\n"
    )

    file.write(
        f"Generated: {current_datetime}\n"
    )

    file.write(
        f"Revenue: ₹{revenue:,.2f}\n"
    )

    file.write(
        f"Profit: ₹{profit:,.2f}\n"
    )

    file.write(
        f"Profit Margin: {profit_margin:.2f}%\n"
    )

    file.write(
        f"Average Order Value: ₹{average_order_value:,.2f}\n"
    )


# END PROCESSING TIMER

end_time = time.time()


processing_time = (
    end_time - start_time
)


# PROCESS SUMMARY

print("=" * 55)

print("REPORT GENERATION COMPLETED")

print("=" * 55)

print(
    f"Report Path: {report_path}"
)

print(
    f"Processing Time: {processing_time:.6f} seconds"
)

print("=" * 55)
```

This is the key outcome of this module:

```text
Business Data
      ↓
Calculate KPIs
      ↓
Get Current Date & Time
      ↓
Create Report Folder
      ↓
Generate Timestamped Filename
      ↓
Save Business Report
      ↓
Calculate Processing Time
```

---

# 55. Most Important Modules for This Stage

| Module | Main Use |
|---|---|
| `datetime` | Dates, timestamps, report names |
| `math` | Mathematical operations |
| `os` | Operating system interaction |
| `pathlib` | Files and folder paths |
| `random` | Generate sample data |
| `time` | Measure processing time |

For your Data Analyst path, prioritize:

```text
datetime

pathlib

time
```

Do not waste time trying to memorize every function in every module.

---

# 56. Core Patterns to Remember

## Import Module

```python
import math
```

## Import Specific Function

```python
from datetime import datetime
```

## Import with Alias

```python
import pandas as pd
```

## Get Current Timestamp

```python
datetime.now()
```

## Create Timestamped Filename

```python
timestamp = datetime.now().strftime(
    "%Y%m%d_%H%M%S"
)
```

## Create Folder

```python
Path("reports").mkdir(
    exist_ok=True
)
```

## Create Nested Folders

```python
Path(
    "reports/2026/07"
).mkdir(
    parents=True,
    exist_ok=True
)
```

## Find CSV Files

```python
Path("data").glob("*.csv")
```

## Calculate Processing Time

```python
start_time = time.time()

# Process

end_time = time.time()

processing_time = end_time - start_time
```

---

# 57. Common Beginner Errors

## Forgetting to Import a Module

Wrong:

```python
print(datetime.now())
```

without importing `datetime`.

Correct:

```python
from datetime import datetime
```

---

## Confusing Import Styles

This:

```python
import datetime
```

requires:

```python
datetime.datetime.now()
```

This:

```python
from datetime import datetime
```

requires:

```python
datetime.now()
```

Understand which import style you are using.

---

## Using Absolute Paths Everywhere

Avoid hardcoding:

```python
"C:/Users/Name/Desktop/project/reports"
```

Prefer project-relative paths:

```python
Path("reports")
```

---

## Forgetting parents=True

This may fail:

```python
Path(
    "reports/2026/07"
).mkdir()
```

when parent folders do not exist.

Use:

```python
Path(
    "reports/2026/07"
).mkdir(
    parents=True,
    exist_ok=True
)
```

---

## Overwriting Daily Reports

Using only:

```python
sales_report.txt
```

causes previous reports to be overwritten.

Prefer:

```python
sales_report_20260713_214530.txt
```

---

## Creating Unnecessary Custom Modules

Do not split a tiny script into ten Python files just to look advanced.

Create custom modules when:

- Functions are reused
- Code becomes difficult to manage
- Related logic should be organized separately

---

# 58. Interview Questions

1. What is a Python module?
2. What is a Python package?
3. What is the difference between a module and a package?
4. How do you import a module?
5. How do you import a specific function?
6. What is an import alias?
7. Why should `from module import *` usually be avoided?
8. What is the `datetime` module used for?
9. How do you get the current date and time?
10. What does `strftime()` do?
11. How would you generate a timestamped report filename?
12. What is the `math` module used for?
13. What is the `os` module used for?
14. What is `pathlib`?
15. What is the difference between `os` and `pathlib`?
16. How do you create a folder using `pathlib`?
17. What do `parents=True` and `exist_ok=True` mean?
18. How do you check whether a file exists?
19. How do you find all CSV files inside a folder?
20. What is the `random` module used for?
21. How would you generate sample sales data?
22. How do you calculate Python code processing time?
23. How would you automatically generate daily business reports?
24. How would you organize reports by year and month?
25. How do you create and import a custom module?

---

# 59. Completion Checklist

Before moving to the next module, you should be able to:

- [ ] Explain modules
- [ ] Explain packages
- [ ] Explain module vs package
- [ ] Use `import`
- [ ] Use `from ... import`
- [ ] Use aliases
- [ ] Avoid unnecessary `import *`
- [ ] Import `datetime`
- [ ] Get current date
- [ ] Get current date and time
- [ ] Use `strftime()`
- [ ] Generate timestamped filenames
- [ ] Import `math`
- [ ] Use basic mathematical functions
- [ ] Import `os`
- [ ] Get current working directory
- [ ] List directory contents
- [ ] Import `pathlib`
- [ ] Create file paths
- [ ] Check whether files exist
- [ ] Create folders
- [ ] Create nested folders
- [ ] Find all CSV files
- [ ] Import `random`
- [ ] Generate random practice data
- [ ] Select random samples
- [ ] Calculate processing time
- [ ] Generate daily report names
- [ ] Generate timestamped report names
- [ ] Create report folders automatically
- [ ] Organize exports by year and month
- [ ] Create a custom module
- [ ] Import custom functions
- [ ] Build an automated daily business report workflow

---

# Final Outcome

After completing Modules and Packages, you should be able to import and reuse Python functionality, work with dates and timestamps, create report folders automatically, organize exports, generate sample data, calculate processing time, create reusable custom modules, and automatically generate daily business reports with date-based or timestamped filenames.