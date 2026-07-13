# Python Foundations 

## Overview

Python is a high-level, general-purpose programming language known for its simple and readable syntax.

For Data Analysts, Python is mainly used to:

- Clean and transform data
- Analyze datasets
- Calculate business KPIs
- Perform Exploratory Data Analysis (EDA)
- Create data visualizations
- Work with CSV and Excel files
- Connect to SQL databases
- Automate repetitive reporting tasks

---

# 1. Introduction to Python

## What is Python?

Python is a programming language that allows us to write instructions that a computer can execute.

A simple Python program:

```python
sales = 100000
cost = 75000

profit = sales - cost

print(profit)
```

Output:

```text
25000
```

In this example:

- `sales` stores total sales
- `cost` stores total cost
- `profit` calculates the difference
- `print()` displays the result

---

# 2. Why Python for Data Analytics?

Data Analysts commonly work with:

- SQL
- Excel
- Power BI
- Python

Each tool has a different purpose.

| Tool | Primary Purpose |
|---|---|
| SQL | Retrieve and manipulate database data |
| Excel | Spreadsheet analysis and reporting |
| Power BI | Dashboards and business intelligence |
| Python | Data cleaning, analysis, EDA and automation |

Python does not replace SQL, Excel, or Power BI.

A Data Analyst should use the right tool for the right problem.

---

# 3. Python Development Environments

Python code can be written and executed using different development environments.

For Data Analytics, two common tools are:

- Jupyter Notebook
- VS Code

---

## Jupyter Notebook

Jupyter Notebook allows Python code to be written and executed in individual cells.

Example:

```python
sales = 50000
profit = 10000

profit_margin = profit / sales * 100

print(profit_margin)
```

Output:

```text
20.0
```

### Jupyter Notebook is useful for:

- Learning Python
- Exploring datasets
- Data cleaning
- Data analysis
- Exploratory Data Analysis
- Data visualization
- Testing code

---

## VS Code

VS Code is a code editor commonly used for Python development.

### VS Code is useful for:

- Python scripts
- Automation
- Larger projects
- File processing
- Organizing multiple Python files

### Simple Rule

```text
Jupyter Notebook → Learning, Analysis and EDA

VS Code → Scripts, Automation and Projects
```

A Data Analyst should eventually become comfortable using both.

---

# 4. Python Syntax Basics

Syntax refers to the rules used to write valid Python code.

Example:

```python
sales = 50000

print(sales)
```

Python is case-sensitive.

```python
sales = 50000
Sales = 60000
SALES = 70000
```

These are three different variables.

Best practice:

```python
total_sales = 50000
```

Use consistent lowercase variable names.

---

# 5. Indentation

Python uses indentation to define blocks of code.

Correct:

```python
sales = 100000

if sales > 50000:
    print("High Sales")
```

Incorrect:

```python
if sales > 50000:
print("High Sales")
```

Indentation is especially important when working with:

- Conditions
- Loops
- Functions

---

# 6. Variables

A variable is a name used to store a value.

Example:

```python
sales = 100000
```

Here:

```text
sales → Variable Name

100000 → Value
```

Data Analytics examples:

```python
company_name = "ABC Retail"

total_sales = 500000

total_profit = 75000

total_customers = 250
```

---

# 7. Variable Assignment

The `=` operator assigns a value to a variable.

Example:

```python
sales = 50000
```

This means:

> Store the value `50000` inside the variable `sales`.

The `=` symbol is called the assignment operator.

---

# 8. Reassigning Variables

The value stored inside a variable can be changed.

Example:

```python
sales = 50000

print(sales)
```

Output:

```text
50000
```

Reassign the variable:

```python
sales = 75000

print(sales)
```

Output:

```text
75000
```

The previous value is replaced with the new value.

---

# 9. Assigning Multiple Variables

Standard method:

```python
sales = 100000
profit = 20000
customers = 500
```

Python also allows:

```python
sales, profit, customers = 100000, 20000, 500
```

For beginners, separate assignments are generally easier to read.

---

# 10. Python Data Types

A data type tells Python what kind of value is stored inside a variable.

The four essential basic data types are:

| Data Type | Python Name | Example | Data Analytics Use |
|---|---|---|---|
| Integer | `int` | `500` | Orders, Customers, Quantity |
| Float | `float` | `25.5` | Revenue, Average, Percentage |
| String | `str` | `"India"` | Customer, Product, Region |
| Boolean | `bool` | `True` | Conditions and Flags |

---

# 11. Integer — int

Integers are whole numbers.

Examples:

```python
orders = 500

customers = 250

quantity = 100
```

Check the data type:

```python
print(type(orders))
```

Output:

```text
<class 'int'>
```

Data Analytics examples:

```python
total_orders = 1500

customer_count = 500

product_quantity = 25
```

---

# 12. Float — float

Floats are numbers containing decimal values.

Examples:

```python
profit_margin = 25.5

average_sales = 1500.75

growth_rate = 12.8
```

Check the data type:

```python
print(type(profit_margin))
```

Output:

```text
<class 'float'>
```

Data Analysts frequently use floats for:

- Averages
- Percentages
- Ratios
- Prices
- Growth rates

---

# 13. String — str

Strings represent text.

Strings must be placed inside quotation marks.

Examples:

```python
company = "ABC Retail"

region = "South"

product = "Laptop"
```

Check the data type:

```python
print(type(region))
```

Output:

```text
<class 'str'>
```

Data Analytics examples:

```python
customer_name = "Rahul"

product_name = "Laptop"

category = "Electronics"

region = "South"
```

---

# 14. Boolean — bool

Boolean values represent:

```text
True
False
```

Example:

```python
target_achieved = True

is_profitable = False
```

Check the data type:

```python
print(type(target_achieved))
```

Output:

```text
<class 'bool'>
```

Booleans are important for:

- Filtering
- Conditions
- Data validation
- Business rules

---

# 15. Business Example Using Data Types

```python
company = "ABC Retail"

orders = 500

revenue = 125000.50

target_achieved = True
```

Data types:

```text
company → str

orders → int

revenue → float

target_achieved → bool
```

---

# 16. type() Function

The `type()` function identifies the data type of a value or variable.

Example:

```python
sales = 50000

print(type(sales))
```

Output:

```text
<class 'int'>
```

Another example:

```python
region = "South"

print(type(region))
```

Output:

```text
<class 'str'>
```

---

# 17. Why Data Types Matter

Consider:

```python
sales = "50000"
```

This is a string.

But:

```python
sales = 50000
```

This is an integer.

They look similar, but Python treats them differently.

Example:

```python
sales = "50000"

profit = 10000

total = sales + profit
```

This produces an error because Python cannot directly add a string and an integer.

This is important in Data Analytics because CSV and Excel files frequently contain incorrect data types.

For example:

```text
Sales
50000
75000
Unknown
90000
```

A column like this may not be recognized as numeric data because it contains the text value `Unknown`.

Understanding data types is essential for data cleaning.

---

# 18. Type Conversion

Type conversion means changing one data type into another.

Important conversion functions:

```python
int()

float()

str()

bool()
```

---

# 19. Convert String to Integer

```python
sales = "50000"

print(type(sales))
```

Output:

```text
<class 'str'>
```

Convert the value:

```python
sales = int(sales)

print(type(sales))
```

Output:

```text
<class 'int'>
```

---

# 20. Convert Integer to Float

```python
sales = 50000

sales = float(sales)

print(sales)
```

Output:

```text
50000.0
```

---

# 21. Convert Number to String

```python
orders = 500

orders = str(orders)

print(type(orders))
```

Output:

```text
<class 'str'>
```

---

# 22. Output Using print()

The `print()` function displays output.

Example:

```python
print("Python for Data Analytics")
```

Output:

```text
Python for Data Analytics
```

Display a variable:

```python
sales = 50000

print(sales)
```

Output:

```text
50000
```

---

# 23. Print Multiple Values

Example:

```python
sales = 100000

profit = 25000

print(sales, profit)
```

Output:

```text
100000 25000
```

Add labels:

```python
print("Sales:", sales)

print("Profit:", profit)
```

Output:

```text
Sales: 100000
Profit: 25000
```

---

# 24. Input Using input()

The `input()` function receives information from the user.

Example:

```python
company = input("Enter Company Name: ")
```

If the user enters:

```text
ABC Retail
```

The value `"ABC Retail"` is stored inside the `company` variable.

---

# 25. Important input() Rule

By default, `input()` always returns a string.

Example:

```python
sales = input("Enter Sales: ")

print(type(sales))
```

Even if the user enters:

```text
50000
```

The data type is:

```text
<class 'str'>
```

---

# 26. Converting User Input

To accept an integer:

```python
orders = int(input("Enter Total Orders: "))
```

To accept a decimal number:

```python
sales = float(input("Enter Total Sales: "))
```

Important patterns:

```python
int(input())
```

```python
float(input())
```

Data Analyst example:

```python
company_name = input("Enter Company Name: ")

total_sales = float(input("Enter Total Sales: "))

total_orders = int(input("Enter Total Orders: "))
```

---

# 27. Comments

Comments are notes written inside Python code.

Python ignores comments during program execution.

Single-line comments use the `#` symbol.

Example:

```python
# Calculate total company sales

sales = 50000
```

Another example:

```python
# Business KPI Data

revenue = 500000

profit = 75000
```

---

# 28. Why Data Analysts Use Comments

Comments help explain:

- Business logic
- Data cleaning decisions
- Calculations
- Assumptions
- Complex code

Good comment:

```python
# Calculate profit margin as a percentage

profit_margin = profit / revenue * 100
```

Unnecessary comment:

```python
# Create sales variable

sales = 50000
```

Good comments should explain why something is being done when the reason is not obvious.

---

# 29. Naming Conventions

Good variable names make code easier to understand.

Bad:

```python
x = 50000

y = 10000
```

Better:

```python
sales = 50000

profit = 10000
```

More descriptive:

```python
total_sales = 50000

total_profit = 10000
```

For Data Analytics, descriptive variable names make notebooks and scripts easier to understand.

---

# 30. snake_case

Python commonly uses `snake_case` for variable names.

Example:

```python
total_sales = 50000

average_order_value = 1500

customer_count = 250

monthly_revenue = 500000
```

Use underscores `_` between words.

---

# 31. Variable Naming Rules

Valid variable names:

```python
sales = 50000

total_sales = 50000

sales2026 = 50000

_sales = 50000
```

Invalid:

```python
total sales = 50000
```

Spaces are not allowed.

Invalid:

```python
2026sales = 50000
```

Variable names cannot start with numbers.

Invalid:

```python
total-sales = 50000
```

Hyphens are not allowed in variable names.

---

# 32. Avoid Python Keywords

Do not use Python keywords as variable names.

Examples of Python keywords include:

```text
if
else
for
while
def
class
True
False
```

Wrong:

```python
class = "Electronics"
```

Better:

```python
product_class = "Electronics"
```

---

# 33. Case Sensitivity

Python is case-sensitive.

These are different variables:

```python
sales = 50000

Sales = 60000

SALES = 70000
```

Best practice:

Use consistent lowercase `snake_case`.

Example:

```python
total_sales
```

---

# 34. f-Strings

f-Strings provide a clean way to insert variables into text.

Example:

```python
company = "ABC Retail"

sales = 50000
```

Without an f-string:

```python
print("Company:", company, "Sales:", sales)
```

With an f-string:

```python
print(f"Company: {company}, Sales: {sales}")
```

Output:

```text
Company: ABC Retail, Sales: 50000
```

Data Analysts can use f-strings for:

- KPI reports
- Automated messages
- Report summaries
- Dynamic file names
- Displaying calculation results

---

# 35. Formatting Decimal Values

Suppose:

```python
profit_margin = 23.456789
```

To display only two decimal places:

```python
print(f"Profit Margin: {profit_margin:.2f}%")
```

Output:

```text
Profit Margin: 23.46%
```

The syntax:

```python
:.2f
```

means:

> Display the floating-point number using two decimal places.

---

# 36. Basic KPI Calculations

## Total Profit

Formula:

```text
Total Profit = Total Sales - Total Cost
```

Python:

```python
total_sales = 750000

total_cost = 525000

total_profit = total_sales - total_cost

print(total_profit)
```

Output:

```text
225000
```

---

## Profit Margin

Formula:

```text
Profit Margin = (Total Profit / Total Sales) × 100
```

Python:

```python
profit_margin = total_profit / total_sales * 100

print(f"{profit_margin:.2f}%")
```

Output:

```text
30.00%
```

---

## Average Order Value

Formula:

```text
Average Order Value = Total Sales / Total Orders
```

Python:

```python
total_orders = 1500

average_order_value = total_sales / total_orders

print(f"₹{average_order_value:.2f}")
```

Output:

```text
₹500.00
```

---

## Revenue Per Customer

Formula:

```text
Revenue Per Customer = Total Revenue / Total Customers
```

Python:

```python
total_customers = 850

revenue_per_customer = total_sales / total_customers

print(f"₹{revenue_per_customer:.2f}")
```

Output:

```text
₹882.35
```

---

# 37. Complete Data Analyst Example

```python
# Company Information

company_name = "ABC Retail"
region = "South India"


# Business Metrics

total_sales = 750000
total_cost = 525000
total_orders = 1500
total_customers = 850


# KPI Calculations

total_profit = total_sales - total_cost

profit_margin = total_profit / total_sales * 100

average_order_value = total_sales / total_orders

revenue_per_customer = total_sales / total_customers


# Business KPI Report

print("========== BUSINESS KPI REPORT ==========")

print(f"Company: {company_name}")

print(f"Region: {region}")

print(f"Total Sales: ₹{total_sales}")

print(f"Total Cost: ₹{total_cost}")

print(f"Total Profit: ₹{total_profit}")

print(f"Profit Margin: {profit_margin:.2f}%")

print(f"Total Orders: {total_orders}")

print(f"Total Customers: {total_customers}")

print(f"Average Order Value: ₹{average_order_value:.2f}")

print(f"Revenue Per Customer: ₹{revenue_per_customer:.2f}")
```

Output:

```text
========== BUSINESS KPI REPORT ==========

Company: ABC Retail
Region: South India
Total Sales: ₹750000
Total Cost: ₹525000
Total Profit: ₹225000
Profit Margin: 30.00%
Total Orders: 1500
Total Customers: 850
Average Order Value: ₹500.00
Revenue Per Customer: ₹882.35
```

---

# 38. Common Beginner Errors

## Error 1: Forgetting Quotation Marks

Wrong:

```python
company = ABC Retail
```

Correct:

```python
company = "ABC Retail"
```

---

## Error 2: Mixing Strings and Numbers

Wrong:

```python
sales = "50000"

profit = 10000

total = sales + profit
```

Correct:

```python
sales = int("50000")

profit = 10000

total = sales + profit
```

---

## Error 3: Wrong Variable Name

```python
total_sales = 50000

print(totalsales)
```

This produces an error because:

```text
total_sales
```

and:

```text
totalsales
```

are different variable names.

---

## Error 4: Wrong Capitalization

Wrong:

```python
sales = 50000

print(Sales)
```

This produces an error because:

```text
sales
```

and:

```text
Sales
```

are different variables.

---

## Error 5: Forgetting Input Conversion

Wrong:

```python
sales = input("Enter Sales: ")

profit = sales - 10000
```

Correct:

```python
sales = float(input("Enter Sales: "))

profit = sales - 10000
```

---

# 39. Key Takeaways

- Python is widely used for Data Analytics.
- Variables store data.
- The `=` operator assigns values to variables.
- Python is case-sensitive.
- The four essential basic data types are `int`, `float`, `str`, and `bool`.
- The `type()` function checks the data type.
- Type conversion changes data from one type to another.
- The `print()` function displays output.
- The `input()` function accepts user input.
- `input()` returns a string by default.
- Comments help document business logic and assumptions.
- Python commonly uses `snake_case` for variable names.
- f-Strings provide a clean way to display variables and calculation results.
- `:.2f` formats floating-point numbers to two decimal places.
- Basic Python can already be used to calculate business KPIs.

---

# # Python Foundations Final Outcome

After completing Python Foundations, you should be able to:

- Understand Python's role in Data Analytics
- Use Jupyter Notebook and VS Code appropriately
- Understand basic Python syntax
- Create and reassign variables
- Work with `int`, `float`, `str`, and `bool`
- Check data types using `type()`
- Perform type conversion
- Accept user input
- Display output
- Write useful comments
- Follow Python naming conventions
- Use f-strings
- Format numerical output
- Calculate basic business KPIs
- Create a simple Business KPI Report
