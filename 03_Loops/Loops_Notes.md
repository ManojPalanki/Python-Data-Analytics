# Loops

## 1. Introduction

Loops allow Python to execute the same block of code repeatedly.

Instead of manually writing the same code multiple times, loops automate repetitive operations.

For Data Analysts, loops are useful for:

- Processing multiple sales transactions
- Calculating total sales
- Finding the highest-selling product
- Counting loss-making orders
- Processing multiple products
- Generating monthly sales summaries
- Checking data quality
- Automating repetitive calculations
- Processing multiple files and reports

---

# 2. Why Loops Are Important

Consider the following sales data:

```python
sales = [50000, 75000, 65000, 90000, 85000]
```

Without a loop:

```python
print(sales[0])
print(sales[1])
print(sales[2])
print(sales[3])
print(sales[4])
```

With a loop:

```python
for sale in sales:
    print(sale)
```

The loop automatically processes every value.

---

# 3. Types of Loops

Python mainly provides two types of loops:

| Loop | Purpose |
|---|---|
| `for` loop | Iterate over a sequence of values |
| `while` loop | Repeat code while a condition remains True |

Additional loop concepts covered in this module:

- `range()`
- `break`
- `continue`
- `pass`
- Nested Loops

---

# 4. for Loop

A `for` loop iterates over every item in a sequence.

Syntax:

```python
for variable in sequence:
    code
```

Example:

```python
sales = [50000, 75000, 65000]

for sale in sales:
    print(sale)
```

Output:

```text
50000
75000
65000
```

---

# 5. Understanding for Loop Execution

Consider:

```python
sales = [50000, 75000, 65000]

for sale in sales:
    print(sale)
```

Python executes the loop as follows:

```text
First Iteration  → sale = 50000

Second Iteration → sale = 75000

Third Iteration  → sale = 65000
```

After processing every value, the loop stops.

---

# 6. Loop Variable

The variable used inside a loop temporarily stores the current value.

```python
products = ["Laptop", "Mobile", "Tablet"]

for product in products:
    print(product)
```

During execution:

```text
product = "Laptop"

product = "Mobile"

product = "Tablet"
```

Use meaningful variable names.

Good:

```python
for sale in sales:
```

```python
for product in products:
```

```python
for customer in customers:
```

Avoid meaningless names when possible:

```python
for x in sales:
```

---

# 7. Data Analyst Example — Process Sales Data

```python
monthly_sales = [850000, 920000, 780000, 1050000]

for sales in monthly_sales:
    print(f"Monthly Sales: ₹{sales:,.2f}")
```

Output:

```text
Monthly Sales: ₹850,000.00
Monthly Sales: ₹920,000.00
Monthly Sales: ₹780,000.00
Monthly Sales: ₹1,050,000.00
```

---

# 8. Performing Calculations Inside a Loop

```python
product_prices = [500, 750, 1000]

for price in product_prices:
    discounted_price = price * 0.90

    print(discounted_price)
```

The calculation executes once for every product price.

---

# 9. Using Conditions Inside Loops

Loops and conditions are commonly used together in Data Analytics.

```python
sales = [850000, 450000, 950000, 350000]

for sale in sales:

    if sale >= 750000:
        print(f"₹{sale:,.2f} → High Sales")

    else:
        print(f"₹{sale:,.2f} → Low Sales")
```

---

# 10. Calculating Total Sales

Consider:

```python
sales = [50000, 75000, 65000, 90000]
```

Create a variable to store the total:

```python
total_sales = 0
```

Then process every sale:

```python
for sale in sales:
    total_sales += sale
```

Complete program:

```python
sales = [50000, 75000, 65000, 90000]

total_sales = 0

for sale in sales:
    total_sales += sale

print(f"Total Sales: ₹{total_sales:,.2f}")
```

Output:

```text
Total Sales: ₹280,000.00
```

---

# 11. Understanding Accumulator Variables

An accumulator variable stores a value that is updated during every loop iteration.

Example:

```python
total_sales = 0

for sale in sales:
    total_sales += sale
```

Execution:

```text
Starting Total = 0

Iteration 1:
0 + 50000 = 50000

Iteration 2:
50000 + 75000 = 125000

Iteration 3:
125000 + 65000 = 190000

Iteration 4:
190000 + 90000 = 280000
```

`total_sales` is called an accumulator.

---

# 12. Counting Values Using Loops

A counter variable counts how many times a condition occurs.

```python
profits = [50000, -15000, 75000, -25000, 45000]

loss_count = 0

for profit in profits:

    if profit < 0:
        loss_count += 1

print(f"Loss-Making Orders: {loss_count}")
```

Output:

```text
Loss-Making Orders: 2
```

---

# 13. Accumulator vs Counter

| Concept | Purpose |
|---|---|
| Accumulator | Adds or combines values |
| Counter | Counts occurrences |

Accumulator:

```python
total_sales = 0

for sale in sales:
    total_sales += sale
```

Counter:

```python
loss_count = 0

for profit in profits:

    if profit < 0:
        loss_count += 1
```

Both concepts are important for Data Analytics.

---

# 14. Finding the Highest Value Using a Loop

```python
sales = [50000, 75000, 120000, 65000]

highest_sales = sales[0]

for sale in sales:

    if sale > highest_sales:
        highest_sales = sale

print(f"Highest Sales: ₹{highest_sales:,.2f}")
```

Output:

```text
Highest Sales: ₹120,000.00
```

---

# 15. Understanding Highest Value Logic

Starting value:

```text
highest_sales = 50000
```

First comparison:

```text
50000 > 50000 → False
```

Second comparison:

```text
75000 > 50000 → True

highest_sales = 75000
```

Third comparison:

```text
120000 > 75000 → True

highest_sales = 120000
```

Fourth comparison:

```text
65000 > 120000 → False
```

Final result:

```text
120000
```

---

# 16. Finding the Lowest Value Using a Loop

```python
sales = [50000, 75000, 120000, 65000]

lowest_sales = sales[0]

for sale in sales:

    if sale < lowest_sales:
        lowest_sales = sale

print(f"Lowest Sales: ₹{lowest_sales:,.2f}")
```

---

# 17. Calculating Average Sales

```python
sales = [50000, 75000, 65000, 90000]

total_sales = 0
sales_count = 0

for sale in sales:
    total_sales += sale
    sales_count += 1

average_sales = total_sales / sales_count

print(f"Average Sales: ₹{average_sales:,.2f}")
```

---

# 18. range() Function

The `range()` function generates a sequence of numbers.

Syntax:

```python
range(start, stop, step)
```

`range()` is commonly used with `for` loops.

---

# 19. range(stop)

```python
for number in range(5):
    print(number)
```

Output:

```text
0
1
2
3
4
```

Important:

```python
range(5)
```

starts at `0` and stops before `5`.

---

# 20. range(start, stop)

```python
for number in range(1, 6):
    print(number)
```

Output:

```text
1
2
3
4
5
```

---

# 21. range(start, stop, step)

```python
for number in range(0, 11, 2):
    print(number)
```

Output:

```text
0
2
4
6
8
10
```

---

# 22. Data Analyst Example Using range()

```python
for month in range(1, 13):
    print(f"Processing Month {month}")
```

Output:

```text
Processing Month 1
Processing Month 2
...
Processing Month 12
```

---

# 23. Using range() with Sales Targets

```python
monthly_target = 100000

for month in range(1, 7):

    print(f"Month {month} Target: ₹{monthly_target:,.2f}")
```

---

# 24. Using range() with len()

`len()` returns the number of items in a sequence.

```python
products = ["Laptop", "Mobile", "Tablet"]

print(len(products))
```

Output:

```text
3
```

Use with `range()`:

```python
products = ["Laptop", "Mobile", "Tablet"]

for index in range(len(products)):
    print(index, products[index])
```

Output:

```text
0 Laptop
1 Mobile
2 Tablet
```

---

# 25. while Loop

A `while` loop executes repeatedly while a condition remains `True`.

Syntax:

```python
while condition:
    code
```

Example:

```python
month = 1

while month <= 5:
    print(f"Processing Month {month}")

    month += 1
```

Output:

```text
Processing Month 1
Processing Month 2
Processing Month 3
Processing Month 4
Processing Month 5
```

---

# 26. Understanding while Loop Execution

```python
month = 1

while month <= 3:
    print(month)

    month += 1
```

Execution:

```text
month = 1

1 <= 3 → True

Print 1

month becomes 2
```

Then:

```text
2 <= 3 → True

Print 2

month becomes 3
```

Then:

```text
3 <= 3 → True

Print 3

month becomes 4
```

Finally:

```text
4 <= 3 → False

Loop Stops
```

---

# 27. for Loop vs while Loop

| for Loop | while Loop |
|---|---|
| Used to iterate over sequences | Used while a condition remains True |
| Number of iterations is usually known | Number of iterations may be unknown |
| Common for processing datasets | Common for condition-based repetition |
| Less risk of infinite loops | Can create infinite loops |

---

# 28. Data Analyst Example — Process Until Target

```python
total_sales = 0
daily_sales = 50000
sales_target = 250000

while total_sales < sales_target:

    total_sales += daily_sales

    print(f"Current Sales: ₹{total_sales:,.2f}")

print("Sales Target Achieved")
```

---

# 29. Infinite Loops

An infinite loop never stops because its condition always remains `True`.

Incorrect:

```python
month = 1

while month <= 5:
    print(month)
```

`month` is never updated.

Therefore:

```text
month <= 5
```

always remains `True`.

Correct:

```python
month = 1

while month <= 5:
    print(month)

    month += 1
```

Always make sure a `while` loop eventually reaches a stopping condition.

---

# 30. break Statement

The `break` statement immediately stops a loop.

```python
sales = [50000, 75000, 150000, 90000]

for sale in sales:

    if sale >= 100000:
        break

    print(sale)
```

Output:

```text
50000
75000
```

When Python finds:

```text
150000
```

the loop stops.

---

# 31. Data Analyst Example — Stop When Target Is Found

```python
monthly_sales = [650000, 720000, 850000, 950000]

sales_target = 800000

for sales in monthly_sales:

    if sales >= sales_target:
        print(f"Target Achieved: ₹{sales:,.2f}")

        break
```

Only the first month achieving the target is processed.

---

# 32. continue Statement

The `continue` statement skips the current iteration and moves to the next iteration.

```python
profits = [50000, -15000, 75000, -25000, 45000]

for profit in profits:

    if profit < 0:
        continue

    print(profit)
```

Output:

```text
50000
75000
45000
```

Negative values are skipped.

---

# 33. Data Analyst Example — Skip Missing Data

```python
sales = [50000, None, 75000, None, 90000]

for sale in sales:

    if sale is None:
        continue

    print(f"Sales: ₹{sale:,.2f}")
```

The missing values are skipped.

---

# 34. break vs continue

| break | continue |
|---|---|
| Stops the entire loop | Skips only the current iteration |
| No more values are processed | Remaining values are still processed |

Example:

```python
for number in range(1, 6):

    if number == 3:
        break

    print(number)
```

Output:

```text
1
2
```

Using `continue`:

```python
for number in range(1, 6):

    if number == 3:
        continue

    print(number)
```

Output:

```text
1
2
4
5
```

---

# 35. pass Statement

The `pass` statement does nothing.

It acts as a placeholder where Python requires code syntactically.

```python
sales = [50000, 75000, 90000]

for sale in sales:
    pass
```

The program runs without performing any operation.

---

# 36. Why Use pass?

Suppose you plan to add business logic later:

```python
for sale in sales:

    if sale > 100000:
        pass
```

Without `pass`, leaving the block empty causes an error.

Example:

```python
if sales > 100000:
```

This is invalid because Python expects an indented code block.

Using:

```python
if sales > 100000:
    pass
```

is valid.

---

# 37. break, continue, and pass Comparison

| Statement | Purpose |
|---|---|
| `break` | Stop the entire loop |
| `continue` | Skip the current iteration |
| `pass` | Do nothing |

---

# 38. Nested Loops

A nested loop is a loop inside another loop.

Syntax:

```python
for outer_variable in outer_sequence:

    for inner_variable in inner_sequence:
        code
```

---

# 39. Basic Nested Loop Example

```python
regions = ["South", "North"]

products = ["Laptop", "Mobile"]

for region in regions:

    for product in products:

        print(region, product)
```

Output:

```text
South Laptop
South Mobile
North Laptop
North Mobile
```

---

# 40. Understanding Nested Loop Execution

Outer loop:

```text
region = South
```

Inner loop executes completely:

```text
Laptop

Mobile
```

Then outer loop moves to:

```text
region = North
```

Inner loop executes again:

```text
Laptop

Mobile
```

---

# 41. Data Analyst Example — Region and Product Analysis

```python
regions = ["South", "North", "West"]

products = ["Laptop", "Mobile"]

for region in regions:

    for product in products:

        print(f"Analyzing {product} Sales in {region} Region")
```

---

# 42. Data Analyst Example — Monthly Product Reports

```python
months = ["January", "February", "March"]

products = ["Laptop", "Mobile", "Tablet"]

for month in months:

    print(f"\n{month} Report")

    for product in products:

        print(f"Analyzing {product}")
```

---

# 43. Counting Profitable Orders

```python
profits = [50000, -15000, 75000, -25000, 45000]

profitable_orders = 0

for profit in profits:

    if profit > 0:
        profitable_orders += 1

print(f"Profitable Orders: {profitable_orders}")
```

---

# 44. Counting Loss-Making Orders

```python
profits = [50000, -15000, 75000, -25000, 45000]

loss_making_orders = 0

for profit in profits:

    if profit < 0:
        loss_making_orders += 1

print(f"Loss-Making Orders: {loss_making_orders}")
```

---

# 45. Calculating Total Revenue

```python
revenues = [150000, 225000, 175000, 300000]

total_revenue = 0

for revenue in revenues:
    total_revenue += revenue

print(f"Total Revenue: ₹{total_revenue:,.2f}")
```

---

# 46. Finding the Highest-Selling Product

```python
products = ["Laptop", "Mobile", "Tablet", "Monitor"]

sales = [850000, 1250000, 650000, 475000]

highest_sales = sales[0]

highest_selling_product = products[0]

for index in range(len(sales)):

    if sales[index] > highest_sales:

        highest_sales = sales[index]

        highest_selling_product = products[index]

print(f"Highest-Selling Product: {highest_selling_product}")

print(f"Sales: ₹{highest_sales:,.2f}")
```

---

# 47. Understanding Highest-Selling Product Logic

Two related sequences are used:

```python
products = ["Laptop", "Mobile", "Tablet"]

sales = [850000, 1250000, 650000]
```

The same index represents related information:

```text
products[0] → Laptop
sales[0]    → 850000
```

```text
products[1] → Mobile
sales[1]    → 1250000
```

The loop checks each sales value and stores both:

- Highest sales value
- Corresponding product

---

# 48. Sales Target Achievement Count

```python
monthly_sales = [650000, 850000, 720000, 950000, 1050000]

sales_target = 800000

target_achieved_count = 0

for sales in monthly_sales:

    if sales >= sales_target:
        target_achieved_count += 1

print(f"Months Target Achieved: {target_achieved_count}")
```

---

# 49. Sales Performance Classification

```python
monthly_sales = [450000, 750000, 950000, 1200000]

for sales in monthly_sales:

    if sales >= 1000000:
        performance = "Excellent"

    elif sales >= 750000:
        performance = "Good"

    elif sales >= 500000:
        performance = "Average"

    else:
        performance = "Poor"

    print(f"₹{sales:,.2f} → {performance}")
```

---

# 50. Processing Multiple Sales Transactions

```python
transactions = [15000, 25000, 18000, 32000, 22000]

total_sales = 0
transaction_count = 0

for transaction in transactions:

    total_sales += transaction

    transaction_count += 1

average_transaction_value = total_sales / transaction_count

print(f"Total Sales: ₹{total_sales:,.2f}")

print(f"Transactions: {transaction_count}")

print(f"Average Transaction Value: ₹{average_transaction_value:,.2f}")
```

---

# 51. Monthly Sales Summary

```python
monthly_sales = [
    850000,
    920000,
    780000,
    1050000,
    1150000,
    890000
]

total_sales = 0
highest_sales = monthly_sales[0]
lowest_sales = monthly_sales[0]
months_above_target = 0

sales_target = 900000

for sales in monthly_sales:

    total_sales += sales

    if sales > highest_sales:
        highest_sales = sales

    if sales < lowest_sales:
        lowest_sales = sales

    if sales >= sales_target:
        months_above_target += 1

average_sales = total_sales / len(monthly_sales)

print("=" * 50)

print("MONTHLY SALES SUMMARY")

print("=" * 50)

print(f"Total Sales: ₹{total_sales:,.2f}")

print(f"Average Sales: ₹{average_sales:,.2f}")

print(f"Highest Sales: ₹{highest_sales:,.2f}")

print(f"Lowest Sales: ₹{lowest_sales:,.2f}")

print(f"Months Target Achieved: {months_above_target}")

print("=" * 50)
```

---

# 52. Real-World Scenario

## Business Requirement

A retail company has hundreds of sales transactions.

Management wants Python to automatically calculate:

- Total sales
- Number of transactions
- Average transaction value
- Highest transaction
- Lowest transaction
- Number of high-value transactions
- Number of low-value transactions

---

# 53. Automated Sales Transaction Analysis

```python
transactions = [
    15000,
    45000,
    85000,
    25000,
    120000,
    65000,
    35000,
    95000,
    150000,
    55000
]

total_sales = 0
transaction_count = 0

highest_transaction = transactions[0]
lowest_transaction = transactions[0]

high_value_transactions = 0
low_value_transactions = 0

high_value_threshold = 75000

for transaction in transactions:

    total_sales += transaction

    transaction_count += 1

    if transaction > highest_transaction:
        highest_transaction = transaction

    if transaction < lowest_transaction:
        lowest_transaction = transaction

    if transaction >= high_value_threshold:
        high_value_transactions += 1

    else:
        low_value_transactions += 1

average_transaction_value = total_sales / transaction_count

print("=" * 55)

print("            SALES TRANSACTION ANALYSIS")

print("=" * 55)

print(f"Total Sales:                 ₹{total_sales:,.2f}")

print(f"Number of Transactions:      {transaction_count}")

print(f"Average Transaction Value:   ₹{average_transaction_value:,.2f}")

print(f"Highest Transaction:         ₹{highest_transaction:,.2f}")

print(f"Lowest Transaction:          ₹{lowest_transaction:,.2f}")

print(f"High-Value Transactions:     {high_value_transactions}")

print(f"Low-Value Transactions:      {low_value_transactions}")

print("=" * 55)
```

---

# 54. Common Beginner Errors

## Forgetting Indentation

Wrong:

```python
for sale in sales:
print(sale)
```

Correct:

```python
for sale in sales:
    print(sale)
```

---

## Forgetting to Initialize an Accumulator

Wrong:

```python
for sale in sales:
    total_sales += sale
```

Correct:

```python
total_sales = 0

for sale in sales:
    total_sales += sale
```

---

## Resetting an Accumulator Inside the Loop

Wrong:

```python
for sale in sales:

    total_sales = 0

    total_sales += sale
```

`total_sales` becomes `0` during every iteration.

Correct:

```python
total_sales = 0

for sale in sales:
    total_sales += sale
```

---

## Creating an Infinite while Loop

Wrong:

```python
month = 1

while month <= 12:
    print(month)
```

Correct:

```python
month = 1

while month <= 12:
    print(month)

    month += 1
```

---

## Confusing break and continue

`break`:

```text
Stops the entire loop.
```

`continue`:

```text
Skips only the current iteration.
```

---

## Incorrect Highest Value Initialization

Avoid:

```python
highest_sales = 0
```

This can fail with datasets containing only negative values.

Better:

```python
highest_sales = sales[0]
```

---

# 55. Important Data Analyst Concepts

After studying loops, understand these patterns clearly:

## Processing Pattern

```python
for value in values:
    process_value
```

## Accumulation Pattern

```python
total = 0

for value in values:
    total += value
```

## Counting Pattern

```python
count = 0

for value in values:

    if condition:
        count += 1
```

## Maximum Pattern

```python
highest = values[0]

for value in values:

    if value > highest:
        highest = value
```

## Minimum Pattern

```python
lowest = values[0]

for value in values:

    if value < lowest:
        lowest = value
```

## Filtering Pattern

```python
for value in values:

    if condition:
        print(value)
```

These patterns are more important than memorizing isolated loop syntax.

---

# 56. Interview Questions

1. What is a loop?
2. Why are loops useful in Data Analytics?
3. What is the difference between a `for` loop and a `while` loop?
4. How does a `for` loop work?
5. What is a loop variable?
6. What is an accumulator variable?
7. What is a counter variable?
8. What is the difference between an accumulator and a counter?
9. How do you calculate total sales using a loop?
10. How do you count loss-making transactions?
11. How do you find the highest value using a loop?
12. How do you find the lowest value using a loop?
13. What does `range()` do?
14. Explain `range(start, stop, step)`.
15. Why does `range(5)` stop at `4`?
16. What causes an infinite loop?
17. What does `break` do?
18. What does `continue` do?
19. What does `pass` do?
20. What is the difference between `break`, `continue`, and `pass`?
21. What is a nested loop?
22. When would a Data Analyst use nested loops?
23. How would you calculate average transaction value using a loop?
24. How would you identify the highest-selling product?
25. How would you automatically generate a monthly sales summary?

---

# 57. Completion Checklist

Before moving to the next module, you should be able to:

- [ ] Explain why loops are used
- [ ] Write a `for` loop
- [ ] Process sales data using a `for` loop
- [ ] Perform calculations inside loops
- [ ] Use conditions inside loops
- [ ] Create accumulator variables
- [ ] Calculate total sales manually using loops
- [ ] Create counter variables
- [ ] Count profitable transactions
- [ ] Count loss-making transactions
- [ ] Find the highest value using loops
- [ ] Find the lowest value using loops
- [ ] Calculate averages using loops
- [ ] Use `range(stop)`
- [ ] Use `range(start, stop)`
- [ ] Use `range(start, stop, step)`
- [ ] Use `range()` with `len()`
- [ ] Write a `while` loop
- [ ] Explain the difference between `for` and `while`
- [ ] Prevent infinite loops
- [ ] Use `break`
- [ ] Use `continue`
- [ ] Use `pass`
- [ ] Explain the difference between `break`, `continue`, and `pass`
- [ ] Write nested loops
- [ ] Process regions and products using nested loops
- [ ] Calculate total sales
- [ ] Find the highest-selling product
- [ ] Count loss-making orders
- [ ] Generate monthly sales summaries
- [ ] Process multiple sales transactions automatically

---

# Final Outcome

After completing Loops, you should be able to use Python to repeatedly process business data, automate calculations across multiple transactions, calculate totals and averages, count values matching business conditions, identify highest and lowest performance, control loop execution, and generate automated sales summaries.