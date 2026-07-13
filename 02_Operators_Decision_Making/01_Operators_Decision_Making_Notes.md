# Operators & Decision Making 

## 1. Introduction

Operators are symbols or keywords used to perform operations on values and variables.

Decision-making statements allow Python programs to execute different code depending on whether a condition is `True` or `False`.

For Data Analysts, operators and conditions are commonly used to:

- Compare actual sales with targets
- Identify profitable and loss-making products
- Categorize customers by spending
- Apply business rules
- Create flags for reporting
- Validate data
- Detect unusual values
- Identify products requiring management attention

---

# 2. Python Operators

The main operators covered in this module are:

| Operator Type | Purpose |
|---|---|
| Arithmetic Operators | Perform mathematical calculations |
| Comparison Operators | Compare values |
| Logical Operators | Combine multiple conditions |
| Assignment Operators | Assign and update values |
| Membership Operators | Check whether a value exists in a collection |
| Identity Operators | Check whether two variables refer to the same object |

---

# 3. Arithmetic Operators

Arithmetic operators perform mathematical calculations.

| Operator | Meaning | Example |
|---|---|---|
| `+` | Addition | `sales + tax` |
| `-` | Subtraction | `revenue - cost` |
| `*` | Multiplication | `price * quantity` |
| `/` | Division | `revenue / orders` |
| `//` | Floor Division | `sales // employees` |
| `%` | Modulus | `orders % 2` |
| `**` | Exponentiation | `growth ** 2` |

---

# 4. Addition Operator

The `+` operator adds values.

```python
online_sales = 500000
store_sales = 350000

total_sales = online_sales + store_sales

print(total_sales)
```

Output:

```text
850000
```

### Data Analytics Use Case

Combine sales from multiple business channels.

---

# 5. Subtraction Operator

The `-` operator subtracts one value from another.

```python
revenue = 850000
cost = 620000

profit = revenue - cost

print(profit)
```

Output:

```text
230000
```

### Data Analytics Use Case

Calculate:

- Profit
- Variance
- Sales difference
- Budget difference

---

# 6. Multiplication Operator

The `*` operator multiplies values.

```python
product_price = 1500
quantity_sold = 250

total_revenue = product_price * quantity_sold

print(total_revenue)
```

Output:

```text
375000
```

### Data Analytics Use Case

Calculate revenue from price and quantity.

---

# 7. Division Operator

The `/` operator divides values.

```python
total_revenue = 1200000
total_orders = 2400

average_order_value = total_revenue / total_orders

print(average_order_value)
```

Output:

```text
500.0
```

Division always returns a `float`.

### Data Analytics Use Case

Calculate:

- Average Order Value
- Revenue Per Customer
- Conversion Rate
- Profit Margin

---

# 8. Floor Division Operator

The `//` operator performs division and returns the whole-number quotient rounded down.

```python
total_customers = 1050
sales_representatives = 20

customers_per_representative = total_customers // sales_representatives

print(customers_per_representative)
```

Output:

```text
52
```

---

# 9. Modulus Operator

The `%` operator returns the remainder after division.

```python
orders = 1501

remainder = orders % 2

print(remainder)
```

Output:

```text
1
```

### Check Even or Odd Values

```python
order_id = 1024

print(order_id % 2)
```

If the result is:

```text
0
```

The number is even.

---

# 10. Exponentiation Operator

The `**` operator raises a value to a power.

```python
value = 5

result = value ** 2

print(result)
```

Output:

```text
25
```

This operator is less common in basic business analytics but is useful in statistics and mathematical calculations.

---

# 11. Arithmetic Operator Example

```python
total_revenue = 1500000
total_cost = 1050000
total_orders = 3000
total_customers = 1800

total_profit = total_revenue - total_cost

profit_margin = (total_profit / total_revenue) * 100

average_order_value = total_revenue / total_orders

revenue_per_customer = total_revenue / total_customers

print(f"Total Profit: ₹{total_profit:,.2f}")
print(f"Profit Margin: {profit_margin:.2f}%")
print(f"Average Order Value: ₹{average_order_value:,.2f}")
print(f"Revenue Per Customer: ₹{revenue_per_customer:,.2f}")
```

---

# 12. Comparison Operators

Comparison operators compare two values.

The result of a comparison is always:

```text
True
```

or:

```text
False
```

| Operator | Meaning |
|---|---|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

---

# 13. Equal To Operator

The `==` operator checks whether two values are equal.

```python
region = "South"

print(region == "South")
```

Output:

```text
True
```

Do not confuse:

```text
=
```

with:

```text
==
```

`=` assigns a value.

`==` compares values.

---

# 14. Not Equal To Operator

The `!=` operator checks whether two values are different.

```python
product_status = "Active"

print(product_status != "Inactive")
```

Output:

```text
True
```

---

# 15. Greater Than Operator

```python
monthly_sales = 850000
sales_target = 750000

print(monthly_sales > sales_target)
```

Output:

```text
True
```

---

# 16. Less Than Operator

```python
product_stock = 25
minimum_stock = 50

print(product_stock < minimum_stock)
```

Output:

```text
True
```

### Data Analytics Use Case

Identify products with low inventory.

---

# 17. Greater Than or Equal To

```python
monthly_sales = 750000
sales_target = 750000

print(monthly_sales >= sales_target)
```

Output:

```text
True
```

---

# 18. Less Than or Equal To

```python
customer_complaints = 10
maximum_allowed = 15

print(customer_complaints <= maximum_allowed)
```

Output:

```text
True
```

---

# 19. Logical Operators

Logical operators combine multiple conditions.

Python has three main logical operators:

| Operator | Meaning |
|---|---|
| `and` | All conditions must be True |
| `or` | At least one condition must be True |
| `not` | Reverses the condition |

---

# 20. and Operator

The `and` operator returns `True` only when all conditions are `True`.

```python
sales = 850000
profit = 200000

result = sales > 750000 and profit > 150000

print(result)
```

Output:

```text
True
```

### Business Example

```python
sales_target_achieved = True
profit_target_achieved = True

print(sales_target_achieved and profit_target_achieved)
```

---

# 21. or Operator

The `or` operator returns `True` when at least one condition is `True`.

```python
sales = 500000
profit = 200000

result = sales > 750000 or profit > 150000

print(result)
```

Output:

```text
True
```

---

# 22. not Operator

The `not` operator reverses a Boolean value.

```python
is_profitable = True

print(not is_profitable)
```

Output:

```text
False
```

---

# 23. Combining Logical Operators

```python
sales = 900000
profit = 250000
returns = 25

result = sales > 750000 and profit > 200000 and returns < 50

print(result)
```

Output:

```text
True
```

---

# 24. Assignment Operators

Assignment operators assign or update variable values.

| Operator | Example | Equivalent |
|---|---|---|
| `=` | `sales = 500000` | Assign value |
| `+=` | `sales += 50000` | `sales = sales + 50000` |
| `-=` | `sales -= 50000` | `sales = sales - 50000` |
| `*=` | `sales *= 2` | `sales = sales * 2` |
| `/=` | `sales /= 2` | `sales = sales / 2` |
| `//=` | `sales //= 2` | `sales = sales // 2` |
| `%=` | `sales %= 2` | `sales = sales % 2` |
| `**=` | `sales **= 2` | `sales = sales ** 2` |

---

# 25. Addition Assignment

```python
monthly_sales = 500000

monthly_sales += 75000

print(monthly_sales)
```

Output:

```text
575000
```

---

# 26. Subtraction Assignment

```python
inventory = 500

inventory -= 50

print(inventory)
```

Output:

```text
450
```

---

# 27. Multiplication Assignment

```python
product_price = 500

product_price *= 2

print(product_price)
```

Output:

```text
1000
```

---

# 28. Division Assignment

```python
budget = 100000

budget /= 2

print(budget)
```

Output:

```text
50000.0
```

---

# 29. Membership Operators

Membership operators check whether a value exists inside a collection.

Python has two membership operators:

```text
in
```

```text
not in
```

---

# 30. in Operator

```python
regions = ["North", "South", "East", "West"]

print("South" in regions)
```

Output:

```text
True
```

### Data Analytics Use Case

Check whether a region, category, product, or customer belongs to a specific group.

---

# 31. not in Operator

```python
regions = ["North", "South", "East", "West"]

print("Central" not in regions)
```

Output:

```text
True
```

---

# 32. Membership Operator Business Example

```python
high_priority_regions = ["South", "West"]

customer_region = "South"

print(customer_region in high_priority_regions)
```

Output:

```text
True
```

---

# 33. Identity Operators

Identity operators check whether two variables refer to the same object in memory.

Python has two identity operators:

```text
is
```

```text
is not
```

---

# 34. is Operator

```python
value = None

print(value is None)
```

Output:

```text
True
```

A common Data Analytics use case is checking for `None`.

```python
sales_data = None

print(sales_data is None)
```

---

# 35. is not Operator

```python
sales_data = 500000

print(sales_data is not None)
```

Output:

```text
True
```

---

# 36. Important Difference Between == and is

`==` compares values.

`is` compares object identity.

Example:

```python
sales = None

if sales is None:
    print("Sales data is missing")
```

For beginners, remember:

```text
== → Compare Values

is → Compare Object Identity
```

The most common beginner use of `is` is:

```python
value is None
```

and:

```python
value is not None
```

---

# 37. Decision Making

Decision-making statements allow Python programs to execute code based on conditions.

The main decision-making statements are:

```text
if

elif

else
```

---

# 38. if Statement

The `if` statement executes code when a condition is `True`.

Syntax:

```python
if condition:
    code
```

Example:

```python
monthly_sales = 850000
sales_target = 750000

if monthly_sales >= sales_target:
    print("Sales Target Achieved")
```

Output:

```text
Sales Target Achieved
```

---

# 39. Indentation in Conditions

Python uses indentation to identify the code belonging to a condition.

Correct:

```python
sales = 850000

if sales > 750000:
    print("High Sales")
```

Incorrect:

```python
sales = 850000

if sales > 750000:
print("High Sales")
```

The standard indentation is four spaces.

---

# 40. if-else Statement

The `else` block executes when the `if` condition is `False`.

```python
monthly_sales = 650000
sales_target = 750000

if monthly_sales >= sales_target:
    print("Sales Target Achieved")
else:
    print("Sales Target Not Achieved")
```

Output:

```text
Sales Target Not Achieved
```

---

# 41. Product Profit or Loss Classification

```python
revenue = 750000
cost = 600000

profit = revenue - cost

if profit > 0:
    print("Profitable Product")
else:
    print("Loss-Making Product")
```

---

# 42. Important Problem with Two-Way Profit Classification

Consider:

```python
if profit > 0:
    print("Profit")
else:
    print("Loss")
```

If profit is exactly `0`, this code incorrectly classifies the result as a loss.

A better solution is:

```python
if profit > 0:
    print("Profit")
elif profit < 0:
    print("Loss")
else:
    print("Break-Even")
```

This is why understanding business requirements matters when writing conditions.

---

# 43. elif Statement

The `elif` statement checks additional conditions.

Syntax:

```python
if condition_1:
    code

elif condition_2:
    code

else:
    code
```

---

# 44. Customer Spending Classification

```python
customer_spending = 75000

if customer_spending >= 100000:
    print("Platinum Customer")

elif customer_spending >= 50000:
    print("Gold Customer")

elif customer_spending >= 25000:
    print("Silver Customer")

else:
    print("Standard Customer")
```

Output:

```text
Gold Customer
```

---

# 45. Why Condition Order Matters

Consider:

```python
customer_spending = 120000

if customer_spending >= 25000:
    print("Silver")

elif customer_spending >= 50000:
    print("Gold")

elif customer_spending >= 100000:
    print("Platinum")
```

Output:

```text
Silver
```

This result is logically wrong.

Python stops checking conditions after finding the first `True` condition.

Correct order:

```python
if customer_spending >= 100000:
    print("Platinum")

elif customer_spending >= 50000:
    print("Gold")

elif customer_spending >= 25000:
    print("Silver")

else:
    print("Standard")
```

When working with numerical ranges, generally check conditions from the most restrictive/highest threshold downward.

---

# 46. Sales Performance Classification

```python
sales = 850000

if sales >= 1000000:
    print("Excellent Performance")

elif sales >= 750000:
    print("Good Performance")

elif sales >= 500000:
    print("Average Performance")

else:
    print("Poor Performance")
```

---

# 47. Multiple Conditions Using and

```python
sales = 900000
profit = 250000

if sales >= 750000 and profit >= 200000:
    print("Strong Business Performance")
else:
    print("Performance Needs Improvement")
```

Both conditions must be `True`.

---

# 48. Multiple Conditions Using or

```python
sales = 500000
profit = 250000

if sales >= 750000 or profit >= 200000:
    print("At Least One Business Target Achieved")
else:
    print("No Business Targets Achieved")
```

At least one condition must be `True`.

---

# 49. Using not with Conditions

```python
product_active = False

if not product_active:
    print("Product Is Inactive")
```

---

# 50. Nested Conditions

A nested condition is an `if` statement inside another `if` statement.

Syntax:

```python
if condition_1:

    if condition_2:
        code
```

---

# 51. Nested Condition Example

```python
sales = 900000
profit = 250000

if sales >= 750000:

    if profit >= 200000:
        print("Excellent Business Performance")

    else:
        print("High Sales but Low Profit")

else:
    print("Sales Target Not Achieved")
```

---

# 52. Data Analyst Scenario — Sales Target

```python
monthly_sales = 850000
sales_target = 800000

if monthly_sales >= sales_target:
    print("Target Achieved")
else:
    print("Target Not Achieved")
```

---

# 53. Data Analyst Scenario — Profit Classification

```python
revenue = 850000
cost = 620000

profit = revenue - cost

if profit > 0:
    print("Profit")

elif profit < 0:
    print("Loss")

else:
    print("Break-Even")
```

---

# 54. Data Analyst Scenario — Customer Segmentation

```python
customer_spending = 85000

if customer_spending >= 100000:
    customer_segment = "Platinum"

elif customer_spending >= 50000:
    customer_segment = "Gold"

elif customer_spending >= 25000:
    customer_segment = "Silver"

else:
    customer_segment = "Standard"

print(f"Customer Segment: {customer_segment}")
```

---

# 55. Data Analyst Scenario — Product Performance

```python
product_name = "Laptop"
sales = 850000
profit = 175000

if sales >= 750000 and profit >= 150000:
    performance = "High Performing Product"

elif sales >= 500000 and profit >= 75000:
    performance = "Average Performing Product"

else:
    performance = "Low Performing Product"

print(f"Product: {product_name}")
print(f"Performance: {performance}")
```

---

# 56. Real-World Scenario — Management Attention Flag

### Business Requirement

Management wants products automatically flagged using the following rules:

- High Sales + High Profit → Strong Performer
- High Sales + Low Profit → Review Profitability
- Low Sales + High Profit → Growth Opportunity
- Low Sales + Low Profit → Management Attention Required

---

# 57. Management Attention Program

```python
product_name = "Laptop"
total_sales = 650000
total_profit = 75000

sales_threshold = 750000
profit_threshold = 150000

if total_sales >= sales_threshold and total_profit >= profit_threshold:
    product_status = "Strong Performer"

elif total_sales >= sales_threshold and total_profit < profit_threshold:
    product_status = "Review Profitability"

elif total_sales < sales_threshold and total_profit >= profit_threshold:
    product_status = "Growth Opportunity"

else:
    product_status = "Management Attention Required"

print("========== PRODUCT PERFORMANCE REPORT ==========")

print(f"Product: {product_name}")
print(f"Total Sales: ₹{total_sales:,.2f}")
print(f"Total Profit: ₹{total_profit:,.2f}")
print(f"Product Status: {product_status}")
```

---

# 58. Nested Condition Version

The same business problem can be solved using nested conditions.

```python
product_name = "Laptop"
total_sales = 650000
total_profit = 75000

sales_threshold = 750000
profit_threshold = 150000

if total_sales >= sales_threshold:

    if total_profit >= profit_threshold:
        product_status = "Strong Performer"

    else:
        product_status = "Review Profitability"

else:

    if total_profit >= profit_threshold:
        product_status = "Growth Opportunity"

    else:
        product_status = "Management Attention Required"

print(f"Product Status: {product_status}")
```

---

# 59. Flat Conditions vs Nested Conditions

Flat conditions:

```python
if condition_1 and condition_2:
    code

elif condition_3:
    code

else:
    code
```

Nested conditions:

```python
if condition_1:

    if condition_2:
        code
```

For most Data Analytics business rules, flat `if-elif-else` conditions are usually easier to read.

Use nested conditions when the second decision logically depends on the first decision.

---

# 60. Common Beginner Errors

## Using = Instead of ==

Wrong:

```python
if region = "South":
    print("South Region")
```

Correct:

```python
if region == "South":
    print("South Region")
```

---

## Missing Colon

Wrong:

```python
if sales > 500000
    print("High Sales")
```

Correct:

```python
if sales > 500000:
    print("High Sales")
```

---

## Incorrect Indentation

Wrong:

```python
if sales > 500000:
print("High Sales")
```

Correct:

```python
if sales > 500000:
    print("High Sales")
```

---

## Incorrect Condition Order

Wrong:

```python
if sales >= 500000:
    print("Average")

elif sales >= 1000000:
    print("Excellent")
```

The second condition may never execute for values above `1000000`.

Correct:

```python
if sales >= 1000000:
    print("Excellent")

elif sales >= 500000:
    print("Average")
```

---

## Confusing and with or

```python
if sales >= 750000 and profit >= 150000:
```

Both conditions must be `True`.

```python
if sales >= 750000 or profit >= 150000:
```

Only one condition needs to be `True`.

---

## Using is Instead of ==

Avoid:

```python
if region is "South":
    print("South Region")
```

Use:

```python
if region == "South":
    print("South Region")
```

Use `is` mainly for identity checks such as:

```python
if value is None:
    print("Missing Value")
```

---

# 61. Complete Data Analyst Example

```python
# BUSINESS DATA

product_name = "Laptop"
total_revenue = 950000
total_cost = 725000
total_sales_target = 900000
total_orders = 1750

# KPI CALCULATIONS

total_profit = total_revenue - total_cost

profit_margin = (total_profit / total_revenue) * 100

average_order_value = total_revenue / total_orders

# SALES TARGET STATUS

if total_revenue >= total_sales_target:
    sales_status = "Target Achieved"
else:
    sales_status = "Target Not Achieved"

# PROFIT CLASSIFICATION

if total_profit > 0:
    profit_status = "Profitable"

elif total_profit < 0:
    profit_status = "Loss"

else:
    profit_status = "Break-Even"

# PRODUCT PERFORMANCE

if total_revenue >= 900000 and profit_margin >= 20:
    product_performance = "Strong Performer"

elif total_revenue >= 750000 and profit_margin >= 10:
    product_performance = "Average Performer"

else:
    product_performance = "Management Attention Required"

# BUSINESS PERFORMANCE REPORT

print("=" * 55)
print("             BUSINESS PERFORMANCE REPORT")
print("=" * 55)

print(f"Product:                 {product_name}")
print(f"Total Revenue:           ₹{total_revenue:,.2f}")
print(f"Total Cost:              ₹{total_cost:,.2f}")
print(f"Total Profit:            ₹{total_profit:,.2f}")
print(f"Profit Margin:           {profit_margin:.2f}%")
print(f"Average Order Value:     ₹{average_order_value:,.2f}")

print("-" * 55)

print(f"Sales Status:            {sales_status}")
print(f"Profit Status:           {profit_status}")
print(f"Product Performance:     {product_performance}")

print("=" * 55)
```

---

# 62. Operator Precedence

When an expression contains multiple operators, Python follows an order of operations.

A simplified order is:

```text
()

**

*, /, //, %

+, -

Comparison Operators

not

and

or
```

Example:

```python
result = 10 + 5 * 2

print(result)
```

Output:

```text
20
```

Multiplication executes before addition.

Using parentheses:

```python
result = (10 + 5) * 2

print(result)
```

Output:

```text
30
```

For business calculations, use parentheses when they make formulas easier to understand.

Example:

```python
profit_margin = (total_profit / total_revenue) * 100
```

---

# 63. Truth Tables

## and

| Condition 1 | Condition 2 | Result |
|---|---|---|
| True | True | True |
| True | False | False |
| False | True | False |
| False | False | False |

## or

| Condition 1 | Condition 2 | Result |
|---|---|---|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

## not

| Condition | Result |
|---|---|
| True | False |
| False | True |

---

# 64. Day 2 Practice Topics

Before taking the assessment, practice:

- Arithmetic calculations
- Comparison operators
- Logical operators
- Assignment operators
- Membership operators
- Identity operators
- Sales target classification
- Profit/Loss/Break-Even classification
- Customer spending segmentation
- Product performance classification
- Multiple business conditions
- Nested conditions
- Management attention flags

---

# 65. Operators & Decision Making Interview Questions

1. What are operators in Python?
2. What is the difference between `/` and `//`?
3. What does the `%` operator return?
4. What is the difference between `=` and `==`?
5. What do comparison operators return?
6. What is the difference between `and` and `or`?
7. What does the `not` operator do?
8. What are assignment operators?
9. What is the difference between `in` and `not in`?
10. What is the difference between `==` and `is`?
11. When should `is None` be used?
12. What is an `if` statement?
13. What is the difference between `if`, `elif`, and `else`?
14. Why is indentation important in Python?
15. Why does condition order matter?
16. What are nested conditions?
17. When should nested conditions be used?
18. How can multiple business conditions be combined?
19. How would you classify a product as Profit, Loss, or Break-Even?
20. How would you automatically flag products requiring management attention?

---

# 66. Operators & Decision Making Completion Checklist

Before moving to Day 3, you should be able to:

- [ ] Use addition `+`
- [ ] Use subtraction `-`
- [ ] Use multiplication `*`
- [ ] Use division `/`
- [ ] Use floor division `//`
- [ ] Use modulus `%`
- [ ] Use exponentiation `**`
- [ ] Use all comparison operators
- [ ] Explain the difference between `=` and `==`
- [ ] Use `and`
- [ ] Use `or`
- [ ] Use `not`
- [ ] Use assignment operators
- [ ] Use `in`
- [ ] Use `not in`
- [ ] Explain the difference between `==` and `is`
- [ ] Use `is None`
- [ ] Write an `if` statement
- [ ] Write an `if-else` statement
- [ ] Write an `if-elif-else` statement
- [ ] Use correct indentation
- [ ] Order numerical conditions correctly
- [ ] Combine multiple business conditions
- [ ] Write nested conditions
- [ ] Determine whether a sales target was achieved
- [ ] Classify Profit, Loss, and Break-Even
- [ ] Categorize customers by spending
- [ ] Classify product performance
- [ ] Automatically flag products requiring management attention

---

# Operators & Decision Making Final Outcome

After completing Operators and Decision Making, you should be able to use Python operators to perform business calculations, compare KPI values, combine multiple business conditions, classify customers and products, evaluate sales targets, and automatically flag business situations requiring management attention.
