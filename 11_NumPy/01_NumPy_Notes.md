# NumPy

## 1. Introduction

NumPy stands for Numerical Python.

It is a Python library used for fast numerical calculations and array operations.

For Data Analysts, NumPy is mainly useful for:

- Numerical data processing
- Working with arrays
- Fast calculations
- Vectorized operations
- Filtering numerical data
- Aggregations
- Broadcasting
- KPI calculations

The most important topics are:

- NumPy Arrays
- Array Creation
- Array Properties
- Indexing
- Slicing
- Boolean Filtering
- Vectorization
- Broadcasting
- Aggregations
- Basic Business Calculations

The main goal is:

```text
Store Numerical Data
        ↓
Process Data Efficiently
        ↓
Perform Vectorized Calculations
        ↓
Filter Business Data
        ↓
Calculate KPIs
```

---

# 2. Import NumPy

NumPy is commonly imported using the alias:

```python
import numpy as np
```

Use:

```python
np
```

instead of repeatedly writing:

```python
numpy
```

The standard convention is:

```python
import numpy as np
```

---

# 3. Python List vs NumPy Array

Python list:

```python
sales = [
    850000,
    920000,
    780000,
    1050000
]
```

NumPy array:

```python
import numpy as np

sales = np.array([
    850000,
    920000,
    780000,
    1050000
])
```

Main difference:

```text
Python List
→ General-purpose collection

NumPy Array
→ Efficient numerical calculations
```

---

# 4. Creating NumPy Arrays

Use:

```python
np.array()
```

Example:

```python
import numpy as np

monthly_sales = np.array([
    850000,
    920000,
    780000,
    1050000
])

print(monthly_sales)
```

Output:

```text
[ 850000  920000  780000 1050000]
```

---

# 5. One-Dimensional Array

A one-dimensional array contains a single sequence of values.

```python
sales = np.array([
    850000,
    920000,
    780000
])
```

Structure:

```text
[850000, 920000, 780000]
```

This is called a:

```text
1D Array
```

---

# 6. Two-Dimensional Array

A two-dimensional array contains rows and columns.

```python
sales_data = np.array([
    [850000, 175000],
    [920000, 210000],
    [780000, 150000]
])
```

Structure:

```text
Sales    Profit

850000   175000
920000   210000
780000   150000
```

This is called a:

```text
2D Array
```

---

# 7. Array Properties

Important array properties are:

- `ndim`
- `shape`
- `size`
- `dtype`

---

# 8. ndim

`ndim` returns the number of dimensions.

```python
sales = np.array([
    850000,
    920000,
    780000
])

print(sales.ndim)
```

Output:

```text
1
```

For a 2D array:

```python
sales_data = np.array([
    [850000, 175000],
    [920000, 210000]
])

print(sales_data.ndim)
```

Output:

```text
2
```

---

# 9. shape

`shape` returns the number of rows and columns.

```python
sales_data = np.array([
    [850000, 175000],
    [920000, 210000],
    [780000, 150000]
])

print(sales_data.shape)
```

Output:

```text
(3, 2)
```

Meaning:

```text
3 Rows

2 Columns
```

---

# 10. size

`size` returns the total number of values.

```python
print(sales_data.size)
```

Output:

```text
6
```

---

# 11. dtype

`dtype` returns the data type stored in the array.

```python
sales = np.array([
    850000,
    920000,
    780000
])

print(sales.dtype)
```

Possible output:

```text
int64
```

---

# 12. NumPy Data Types

Common NumPy data types include:

```text
int

float

bool

str
```

Example:

```python
sales = np.array([
    850000.50,
    920000.75
])

print(sales.dtype)
```

The array stores floating-point values.

---

# 13. Creating Arrays with arange()

`arange()` creates a sequence of values.

```python
numbers = np.arange(1, 11)

print(numbers)
```

Output:

```text
[1 2 3 4 5 6 7 8 9 10]
```

With steps:

```python
numbers = np.arange(0, 100, 10)
```

Output:

```text
[ 0 10 20 30 40 50 60 70 80 90]
```

---

# 14. Creating Arrays with zeros()

```python
values = np.zeros(5)

print(values)
```

Output:

```text
[0. 0. 0. 0. 0.]
```

Useful when initializing storage for calculations.

---

# 15. Creating Arrays with ones()

```python
values = np.ones(5)

print(values)
```

Output:

```text
[1. 1. 1. 1. 1.]
```

---

# 16. Array Indexing

NumPy indexing works similarly to Python lists.

```python
sales = np.array([
    850000,
    920000,
    780000,
    1050000
])
```

Access first value:

```python
print(sales[0])
```

Output:

```text
850000
```

Access last value:

```python
print(sales[-1])
```

Output:

```text
1050000
```

---

# 17. Array Slicing

Syntax:

```python
array[start:stop]
```

Example:

```python
sales = np.array([
    850000,
    920000,
    780000,
    1050000,
    1100000,
    950000
])

q1_sales = sales[0:3]

print(q1_sales)
```

Output:

```text
[850000 920000 780000]
```

---

# 18. Slicing Shortcuts

First three values:

```python
sales[:3]
```

From index 3 to end:

```python
sales[3:]
```

Every second value:

```python
sales[::2]
```

Reverse array:

```python
sales[::-1]
```

---

# 19. Two-Dimensional Indexing

Consider:

```python
sales_data = np.array([
    [850000, 175000],
    [920000, 210000],
    [780000, 150000]
])
```

Syntax:

```python
array[row, column]
```

Get first row, first column:

```python
print(sales_data[0, 0])
```

Output:

```text
850000
```

Get second row, second column:

```python
print(sales_data[1, 1])
```

Output:

```text
210000
```

---

# 20. Selecting Rows

Get first row:

```python
sales_data[0]
```

Get first two rows:

```python
sales_data[:2]
```

---

# 21. Selecting Columns

Get the Sales column:

```python
sales_data[:, 0]
```

Get the Profit column:

```python
sales_data[:, 1]
```

Remember:

```text
:
→ Select All Rows

0
→ Select First Column
```

---

# 22. Vectorization

Vectorization means performing operations on entire arrays without manually writing loops.

This is one of the most important NumPy concepts.

Python approach:

```python
sales = [
    1000,
    2000,
    3000
]

new_sales = []

for value in sales:

    new_sales.append(
        value * 1.10
    )
```

NumPy approach:

```python
sales = np.array([
    1000,
    2000,
    3000
])

new_sales = sales * 1.10
```

Output:

```text
[1100. 2200. 3300.]
```

This is:

```text
Vectorization
```

---

# 23. Why Vectorization Matters

Without NumPy:

```text
Loop Through Value
        ↓
Calculate
        ↓
Store Result
        ↓
Repeat
```

With NumPy:

```text
Entire Array
      ↓
One Operation
      ↓
Result Array
```

Vectorized operations are:

- Cleaner
- Easier to read
- Faster for large numerical datasets

---

# 24. Array Arithmetic

Create arrays:

```python
revenue = np.array([
    850000,
    920000,
    780000
])

cost = np.array([
    620000,
    680000,
    590000
])
```

Calculate profit:

```python
profit = revenue - cost

print(profit)
```

Output:

```text
[230000 240000 190000]
```

No loop is required.

---

# 25. Addition

```python
result = array1 + array2
```

Example:

```python
online_sales = np.array([
    500000,
    650000,
    700000
])

store_sales = np.array([
    350000,
    400000,
    450000
])

total_sales = online_sales + store_sales
```

---

# 26. Subtraction

Calculate profit:

```python
profit = revenue - cost
```

---

# 27. Multiplication

Apply a 10% increase:

```python
new_sales = sales * 1.10
```

---

# 28. Division

Calculate Average Order Value:

```python
revenue = np.array([
    850000,
    920000,
    780000
])

orders = np.array([
    1700,
    2000,
    1500
])

average_order_value = revenue / orders
```

---

# 29. Calculate Product Discounts

```python
prices = np.array([
    50000,
    75000,
    30000,
    45000
])

discount_rate = 0.10

discount_amount = prices * discount_rate

final_prices = prices - discount_amount
```

Display:

```python
print(final_prices)
```

This applies the discount to every product simultaneously.

---

# 30. Broadcasting

Broadcasting allows NumPy to perform operations between arrays and single values.

Example:

```python
sales = np.array([
    850000,
    920000,
    780000
])

updated_sales = sales * 1.10
```

Here:

```text
1.10
```

is automatically applied to every value.

This is broadcasting.

---

# 31. Broadcasting Example — Tax Calculation

```python
prices = np.array([
    50000,
    75000,
    30000
])

tax_rate = 0.18

tax_amount = prices * tax_rate

final_prices = prices + tax_amount
```

---

# 32. Broadcasting Example — Fixed Cost

```python
product_costs = np.array([
    5000,
    7500,
    9000
])

shipping_cost = 500

total_cost = product_costs + shipping_cost
```

The fixed shipping cost is added to every product.

---

# 33. Boolean Filtering

Boolean filtering allows you to select values that meet conditions.

Example:

```python
sales = np.array([
    850000,
    1200000,
    650000,
    1500000,
    950000
])
```

Find sales above ₹1,000,000:

```python
high_sales = sales[
    sales > 1000000
]

print(high_sales)
```

Output:

```text
[1200000 1500000]
```

---

# 34. Boolean Mask

This:

```python
sales > 1000000
```

creates:

```text
[False True False True False]
```

This is called a:

```text
Boolean Mask
```

Use it:

```python
high_sales = sales[
    sales > 1000000
]
```

---

# 35. Multiple Conditions

Use:

```python
&
```

for AND.

Example:

```python
filtered_sales = sales[
    (sales >= 800000)
    &
    (sales <= 1200000)
]
```

Use parentheses around each condition.

---

# 36. OR Condition

Use:

```python
|
```

for OR.

Example:

```python
filtered_sales = sales[
    (sales < 700000)
    |
    (sales > 1200000)
]
```

Remember:

```text
& → AND

| → OR
```

---

# 37. Aggregations

Aggregation functions summarize numerical data.

Important NumPy aggregations:

- `sum()`
- `mean()`
- `min()`
- `max()`
- `median()`
- `std()`

---

# 38. Calculate Total Sales

```python
sales = np.array([
    850000,
    920000,
    780000,
    1050000
])

total_sales = np.sum(sales)

print(total_sales)
```

---

# 39. Calculate Average Sales

```python
average_sales = np.mean(sales)

print(
    f"Average Sales: ₹{average_sales:,.2f}"
)
```

---

# 40. Calculate Highest Sales

```python
highest_sales = np.max(sales)
```

---

# 41. Calculate Lowest Sales

```python
lowest_sales = np.min(sales)
```

---

# 42. Calculate Median

```python
median_sales = np.median(sales)
```

Median is useful when data contains extreme values or outliers.

---

# 43. Calculate Standard Deviation

```python
sales_std = np.std(sales)
```

Standard deviation measures how spread out the values are around the mean.

You will study this concept more deeply in Statistics.

---

# 44. Axis in NumPy

For 2D arrays, `axis` controls the calculation direction.

Consider:

```python
regional_sales = np.array([
    [850000, 920000, 780000],
    [650000, 750000, 800000],
    [950000, 1100000, 1050000]
])
```

Structure:

```text
           Jan       Feb       Mar

South      850000    920000    780000

North      650000    750000    800000

West       950000   1100000   1050000
```

---

# 45. axis=0

Calculate column-wise.

```python
monthly_totals = np.sum(
    regional_sales,
    axis=0
)

print(monthly_totals)
```

Concept:

```text
axis=0
→ Calculate Down Rows
→ Result for Each Column
```

---

# 46. axis=1

Calculate row-wise.

```python
regional_totals = np.sum(
    regional_sales,
    axis=1
)

print(regional_totals)
```

Concept:

```text
axis=1
→ Calculate Across Columns
→ Result for Each Row
```

This is one of the most important NumPy concepts.

---

# 47. Regional Sales Totals

```python
regional_sales = np.array([
    [850000, 920000, 780000],
    [650000, 750000, 800000],
    [950000, 1100000, 1050000]
])

regional_totals = np.sum(
    regional_sales,
    axis=1
)

print(regional_totals)
```

Each result represents total sales for one region.

---

# 48. Monthly Sales Totals

```python
monthly_totals = np.sum(
    regional_sales,
    axis=0
)

print(monthly_totals)
```

Each result represents total sales for one month.

---

# 49. Revenue Growth Calculation

Formula:

```text
Growth %

=

((Current - Previous) / Previous) × 100
```

Using NumPy:

```python
previous_sales = np.array([
    750000,
    850000,
    900000
])

current_sales = np.array([
    850000,
    920000,
    1050000
])

growth_percentage = (
    (
        current_sales
        -
        previous_sales
    )
    /
    previous_sales
) * 100
```

Display:

```python
print(
    np.round(
        growth_percentage,
        2
    )
)
```

---

# 50. np.round()

`np.round()` rounds numerical values.

```python
profit_margin = np.array([
    27.058823,
    26.086956,
    24.358974
])

rounded_margin = np.round(
    profit_margin,
    2
)

print(rounded_margin)
```

---

# 51. Profit Margin Calculation

```python
revenue = np.array([
    850000,
    920000,
    780000
])

cost = np.array([
    620000,
    680000,
    590000
])

profit = revenue - cost

profit_margin = (
    profit / revenue
) * 100

profit_margin = np.round(
    profit_margin,
    2
)
```

Display:

```python
print(profit)

print(profit_margin)
```

---

# 52. Average Order Value Calculation

```python
revenue = np.array([
    850000,
    920000,
    780000
])

orders = np.array([
    1700,
    2000,
    1500
])

average_order_value = (
    revenue / orders
)

average_order_value = np.round(
    average_order_value,
    2
)
```

---

# 53. Product Discount Analysis

```python
product_prices = np.array([
    50000,
    75000,
    30000,
    45000
])

discount_rates = np.array([
    0.10,
    0.15,
    0.05,
    0.20
])

discount_amounts = (
    product_prices
    *
    discount_rates
)

final_prices = (
    product_prices
    -
    discount_amounts
)

print(final_prices)
```

---

# 54. np.where()

`np.where()` applies conditional logic to arrays.

Syntax:

```python
np.where(
    condition,
    value_if_true,
    value_if_false
)
```

Example:

```python
sales = np.array([
    850000,
    1200000,
    650000,
    1500000
])

performance = np.where(
    sales >= 1000000,
    "High",
    "Low"
)

print(performance)
```

Output:

```text
['Low' 'High' 'Low' 'High']
```

This is similar to:

```text
CASE WHEN
```

in SQL.

---

# 55. Product Performance Classification

```python
product_sales = np.array([
    850000,
    1250000,
    650000,
    1500000
])

performance = np.where(
    product_sales >= 1000000,
    "Target Achieved",
    "Below Target"
)

print(performance)
```

---

# 56. Handling Missing Values

NumPy represents missing numerical values using:

```python
np.nan
```

Example:

```python
sales = np.array([
    850000,
    np.nan,
    780000,
    1050000
])
```

---

# 57. Problem with Regular Aggregations

```python
np.mean(sales)
```

may return:

```text
nan
```

because the array contains a missing value.

Use:

```python
np.nanmean(sales)
```

---

# 58. Missing-Value Aggregations

Important functions:

```python
np.nansum()
```

```python
np.nanmean()
```

```python
np.nanmin()
```

```python
np.nanmax()
```

Example:

```python
average_sales = np.nanmean(sales)
```

These ignore `NaN` values.

---

# 59. Detect Missing Values

```python
np.isnan(sales)
```

Output:

```text
[False True False False]
```

Count missing values:

```python
missing_count = np.sum(
    np.isnan(sales)
)

print(missing_count)
```

---

# 60. Complete Business KPI Analysis

```python
import numpy as np


# BUSINESS DATA

revenue = np.array([
    850000,
    920000,
    780000,
    1050000,
    1200000
])

cost = np.array([
    620000,
    680000,
    590000,
    750000,
    850000
])

orders = np.array([
    1700,
    2000,
    1500,
    2200,
    2500
])

previous_revenue = np.array([
    750000,
    850000,
    800000,
    950000,
    1100000
])


# KPI CALCULATIONS

profit = revenue - cost

profit_margin = (
    profit / revenue
) * 100

average_order_value = (
    revenue / orders
)

revenue_growth = (
    (
        revenue
        -
        previous_revenue
    )
    /
    previous_revenue
) * 100


# AGGREGATIONS

total_revenue = np.sum(revenue)

average_revenue = np.mean(revenue)

highest_revenue = np.max(revenue)

lowest_revenue = np.min(revenue)


# FILTERING

high_revenue_records = revenue[
    revenue >= 1000000
]


# PERFORMANCE CLASSIFICATION

performance = np.where(
    revenue >= 1000000,
    "Target Achieved",
    "Below Target"
)


# BUSINESS REPORT

print("=" * 60)

print("NUMPY BUSINESS KPI ANALYSIS")

print("=" * 60)

print(
    f"Total Revenue: ₹{total_revenue:,.2f}"
)

print(
    f"Average Revenue: ₹{average_revenue:,.2f}"
)

print(
    f"Highest Revenue: ₹{highest_revenue:,.2f}"
)

print(
    f"Lowest Revenue: ₹{lowest_revenue:,.2f}"
)

print("-" * 60)

print(
    "Profit:",
    profit
)

print(
    "Profit Margin:",
    np.round(
        profit_margin,
        2
    )
)

print(
    "Average Order Value:",
    np.round(
        average_order_value,
        2
    )
)

print(
    "Revenue Growth:",
    np.round(
        revenue_growth,
        2
    )
)

print(
    "High Revenue Records:",
    high_revenue_records
)

print(
    "Performance:",
    performance
)

print("=" * 60)
```

---

# 61. NumPy Workflow for Data Analysts

```text
Import NumPy
      ↓
Create / Load Numerical Arrays
      ↓
Inspect Shape and Data Type
      ↓
Index and Slice Data
      ↓
Filter Using Conditions
      ↓
Perform Vectorized Calculations
      ↓
Use Broadcasting
      ↓
Calculate Aggregations
      ↓
Calculate Business KPIs
      ↓
Interpret Results
```

---

# 62. Most Important NumPy Concepts

| Concept | Purpose |
|---|---|
| `np.array()` | Create arrays |
| `ndim` | Check dimensions |
| `shape` | Check array structure |
| `size` | Count total values |
| `dtype` | Check data type |
| Indexing | Access individual values |
| Slicing | Extract sections |
| Boolean Filtering | Filter values |
| Vectorization | Calculate without manual loops |
| Broadcasting | Apply operations efficiently |
| `np.sum()` | Calculate totals |
| `np.mean()` | Calculate averages |
| `np.min()` | Find minimum |
| `np.max()` | Find maximum |
| `np.median()` | Calculate median |
| `np.std()` | Calculate standard deviation |
| `np.where()` | Conditional calculations |
| `np.round()` | Round numerical results |
| `np.isnan()` | Detect missing values |
| `np.nanmean()` | Average while ignoring NaN |

---

# 63. What You Should Prioritize

For a Data Analyst role, master:

```text
np.array()

Indexing

Slicing

Boolean Filtering

Vectorization

Broadcasting

sum()

mean()

min()

max()

median()

axis

np.where()

np.nan
```

Do not waste time memorizing the entire NumPy library.

Your main tool for tabular Data Analysis will be Pandas.

NumPy is important because it builds your understanding of efficient numerical data processing and supports many Python Data Analytics libraries.

---

# 64. Core Patterns to Remember

## Create Array

```python
sales = np.array([
    850000,
    920000,
    780000
])
```

## Vectorized Profit Calculation

```python
profit = revenue - cost
```

## Calculate Profit Margin

```python
profit_margin = (
    profit / revenue
) * 100
```

## Filter Data

```python
high_sales = sales[
    sales > 1000000
]
```

## Calculate Total

```python
np.sum(sales)
```

## Calculate Average

```python
np.mean(sales)
```

## Regional Totals

```python
np.sum(
    regional_sales,
    axis=1
)
```

## Monthly Totals

```python
np.sum(
    regional_sales,
    axis=0
)
```

## Apply Business Condition

```python
np.where(
    sales >= target,
    "Achieved",
    "Below Target"
)
```

## Calculate Growth

```python
growth = (
    (
        current
        -
        previous
    )
    /
    previous
) * 100
```

---

# 65. Common Beginner Errors

## Forgetting to Import NumPy

Wrong:

```python
sales = np.array([100, 200])
```

without:

```python
import numpy as np
```

---

## Confusing Lists and Arrays

Python list:

```python
[1, 2, 3] * 2
```

Result:

```text
[1, 2, 3, 1, 2, 3]
```

NumPy array:

```python
np.array([1, 2, 3]) * 2
```

Result:

```text
[2 4 6]
```

---

## Using and Instead of &

Wrong:

```python
sales[
    sales > 500000
    and
    sales < 1000000
]
```

Correct:

```python
sales[
    (sales > 500000)
    &
    (sales < 1000000)
]
```

---

## Forgetting Parentheses in Multiple Conditions

Wrong:

```python
sales > 500000 & sales < 1000000
```

Correct:

```python
(sales > 500000) & (sales < 1000000)
```

---

## Confusing axis=0 and axis=1

Remember:

```text
axis=0
→ Calculate Down Rows
→ Column Results
```

```text
axis=1
→ Calculate Across Columns
→ Row Results
```

---

## Using Loops for Simple Array Calculations

Avoid:

```python
for value in sales:

    new_value = value * 1.10
```

Prefer:

```python
new_sales = sales * 1.10
```

This is the core reason for learning NumPy.

---

# 66. Interview Questions

1. What is NumPy?
2. Why is NumPy useful for Data Analysts?
3. What is a NumPy array?
4. What is the difference between a Python list and a NumPy array?
5. How do you create a NumPy array?
6. What do `ndim`, `shape`, `size`, and `dtype` return?
7. What is array indexing?
8. What is array slicing?
9. How do you select rows and columns from a 2D array?
10. What is vectorization?
11. Why is vectorization better than manually writing loops?
12. What is broadcasting?
13. How would you calculate profit using NumPy?
14. How would you calculate product discounts?
15. What is Boolean filtering?
16. What is a Boolean mask?
17. How do you apply multiple filtering conditions?
18. What is the difference between `&` and `|`?
19. How do you calculate total sales?
20. How do you calculate average sales?
21. How do you calculate median sales?
22. What does standard deviation measure?
23. What does `axis=0` mean?
24. What does `axis=1` mean?
25. How would you calculate regional totals?
26. How would you calculate monthly totals?
27. How would you calculate revenue growth?
28. What does `np.where()` do?
29. What is `np.nan`?
30. How do you calculate an average while ignoring missing values?

---

# 67. Completion Checklist

Before moving to Pandas, you should be able to:

- [ ] Import NumPy
- [ ] Explain Python lists vs NumPy arrays
- [ ] Create 1D arrays
- [ ] Create 2D arrays
- [ ] Use `ndim`
- [ ] Use `shape`
- [ ] Use `size`
- [ ] Use `dtype`
- [ ] Use `arange()`
- [ ] Use `zeros()`
- [ ] Use `ones()`
- [ ] Use indexing
- [ ] Use slicing
- [ ] Select rows from 2D arrays
- [ ] Select columns from 2D arrays
- [ ] Explain vectorization
- [ ] Perform array arithmetic
- [ ] Explain broadcasting
- [ ] Apply product discounts
- [ ] Use Boolean filtering
- [ ] Create Boolean masks
- [ ] Filter using multiple conditions
- [ ] Use `np.sum()`
- [ ] Use `np.mean()`
- [ ] Use `np.min()`
- [ ] Use `np.max()`
- [ ] Use `np.median()`
- [ ] Understand basic `np.std()`
- [ ] Explain `axis=0`
- [ ] Explain `axis=1`
- [ ] Calculate regional totals
- [ ] Calculate monthly totals
- [ ] Calculate Profit
- [ ] Calculate Profit Margin
- [ ] Calculate Average Order Value
- [ ] Calculate Revenue Growth
- [ ] Use `np.round()`
- [ ] Use `np.where()`
- [ ] Understand `np.nan`
- [ ] Detect missing values
- [ ] Calculate aggregations while ignoring missing values
- [ ] Analyze numerical business data without unnecessary Python loops

---

# Final Outcome

After completing NumPy, you should be able to create and manipulate numerical arrays, use indexing and slicing, filter business data using Boolean conditions, perform efficient vectorized calculations, apply broadcasting, calculate aggregations across rows and columns, handle basic missing numerical values, and calculate average sales, revenue growth, regional totals, product discounts, Profit Margin, Average Order Value, and other business KPIs across thousands of numerical records efficiently.