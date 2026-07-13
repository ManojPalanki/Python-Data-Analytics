# Functions

## 1. Introduction

A function is a reusable block of code designed to perform a specific task.

Instead of writing the same calculation repeatedly, write the logic once inside a function and reuse it.

For Data Analysts, functions are useful for:

- KPI calculations
- Profit Margin calculations
- Growth calculations
- Average Order Value calculations
- Customer discount calculations
- Data cleaning logic
- Reusable business rules
- Report automation

---

# 2. Why Functions Matter

Without a function:

```python
revenue = 850000
cost = 620000

profit = revenue - cost

print(profit)
```

For another report:

```python
revenue = 1200000
cost = 850000

profit = revenue - cost

print(profit)
```

The same logic is repeated.

Using a function:

```python
def calculate_profit(revenue, cost):
    return revenue - cost
```

Now reuse it:

```python
print(calculate_profit(850000, 620000))

print(calculate_profit(1200000, 850000))
```

The main principle is:

```text
Write Once → Reuse Multiple Times
```

---

# 3. Creating a Function

Use the `def` keyword to create a function.

Syntax:

```python
def function_name():
    code
```

Example:

```python
def display_report():
    print("Business Performance Report")
```

The function is now defined but has not executed.

---

# 4. Calling a Function

To execute a function, call it using its name:

```python
display_report()
```

Complete example:

```python
def display_report():
    print("Business Performance Report")


display_report()
```

Output:

```text
Business Performance Report
```

---

# 5. Function Naming

Use meaningful `snake_case` names.

Good:

```python
calculate_profit()
```

```python
calculate_profit_margin()
```

```python
calculate_average_order_value()
```

Avoid:

```python
fun1()
```

```python
calc()
```

```python
x()
```

The function name should explain what the function does.

---

# 6. Parameters

Parameters are variables defined inside the function declaration.

```python
def calculate_profit(revenue, cost):
    profit = revenue - cost

    print(profit)
```

Here:

```text
revenue
cost
```

are parameters.

Parameters allow functions to process different data.

---

# 7. Arguments

Arguments are the actual values passed when calling a function.

```python
calculate_profit(850000, 620000)
```

Here:

```text
850000
620000
```

are arguments.

Remember:

```text
Parameter → Variable in Function Definition

Argument → Actual Value Passed to Function
```

---

# 8. Function with Parameters

```python
def calculate_profit(revenue, cost):

    profit = revenue - cost

    print(f"Profit: ₹{profit:,.2f}")


calculate_profit(850000, 620000)
```

Output:

```text
Profit: ₹230,000.00
```

Reuse the function:

```python
calculate_profit(1200000, 850000)

calculate_profit(950000, 700000)
```

---

# 9. Return Values

The `return` statement sends a result back from a function.

```python
def calculate_profit(revenue, cost):

    profit = revenue - cost

    return profit
```

Call the function:

```python
result = calculate_profit(850000, 620000)

print(result)
```

Output:

```text
230000
```

---

# 10. print() vs return

This is one of the most important function concepts.

Using `print()`:

```python
def calculate_profit(revenue, cost):

    profit = revenue - cost

    print(profit)
```

The function only displays the value.

Using `return`:

```python
def calculate_profit(revenue, cost):

    profit = revenue - cost

    return profit
```

The returned value can be stored and reused:

```python
total_profit = calculate_profit(850000, 620000)

profit_after_tax = total_profit * 0.80
```

For Data Analytics functions, prefer `return` when the calculated result needs to be reused.

---

# 11. Direct Return

This:

```python
def calculate_profit(revenue, cost):

    profit = revenue - cost

    return profit
```

Can be simplified:

```python
def calculate_profit(revenue, cost):

    return revenue - cost
```

Both are correct.

Use the version that is easiest to understand.

---

# 12. Multiple Parameters

Functions can accept multiple parameters.

```python
def calculate_business_kpis(revenue, cost, orders):

    profit = revenue - cost

    average_order_value = revenue / orders

    return profit, average_order_value
```

Call:

```python
profit, aov = calculate_business_kpis(850000, 620000, 1700)

print(profit)

print(aov)
```

---

# 13. Positional Arguments

By default, Python assigns arguments based on position.

```python
def calculate_profit(revenue, cost):

    return revenue - cost
```

Call:

```python
calculate_profit(850000, 620000)
```

Python assigns:

```text
revenue = 850000

cost = 620000
```

Order matters.

---

# 14. Keyword Arguments

Arguments can also be passed using parameter names.

```python
calculate_profit(
    revenue=850000,
    cost=620000
)
```

Keyword arguments improve readability.

The order does not matter:

```python
calculate_profit(
    cost=620000,
    revenue=850000
)
```

---

# 15. Default Parameters

Default parameters provide a default value.

```python
def calculate_discount(price, discount_rate=10):

    discount = price * (discount_rate / 100)

    return discount
```

Call without providing the discount:

```python
calculate_discount(5000)
```

Python uses:

```text
discount_rate = 10
```

Call with a different discount:

```python
calculate_discount(5000, 20)
```

Python uses:

```text
discount_rate = 20
```

---

# 16. Data Analyst Use Case — Customer Discount

```python
def calculate_customer_discount(
    purchase_amount,
    discount_rate=10
):

    discount = purchase_amount * (discount_rate / 100)

    final_amount = purchase_amount - discount

    return final_amount
```

Use:

```python
amount = calculate_customer_discount(50000)

print(f"Final Amount: ₹{amount:,.2f}")
```

---

# 17. Revenue Function

```python
def calculate_revenue(price, quantity):

    return price * quantity
```

Use:

```python
revenue = calculate_revenue(1500, 500)

print(f"Revenue: ₹{revenue:,.2f}")
```

---

# 18. Profit Function

```python
def calculate_profit(revenue, cost):

    return revenue - cost
```

Use:

```python
profit = calculate_profit(850000, 620000)

print(f"Profit: ₹{profit:,.2f}")
```

---

# 19. Profit Margin Function

Formula:

```text
Profit Margin = (Profit / Revenue) × 100
```

Function:

```python
def calculate_profit_margin(revenue, cost):

    profit = revenue - cost

    profit_margin = (profit / revenue) * 100

    return profit_margin
```

Use:

```python
margin = calculate_profit_margin(850000, 620000)

print(f"Profit Margin: {margin:.2f}%")
```

---

# 20. Growth Percentage Function

Formula:

```text
Growth % = ((Current - Previous) / Previous) × 100
```

Function:

```python
def calculate_growth(previous_sales, current_sales):

    growth = (
        (current_sales - previous_sales)
        / previous_sales
    ) * 100

    return growth
```

Use:

```python
growth = calculate_growth(750000, 900000)

print(f"Sales Growth: {growth:.2f}%")
```

---

# 21. Average Order Value Function

Formula:

```text
AOV = Revenue / Number of Orders
```

Function:

```python
def calculate_average_order_value(revenue, orders):

    return revenue / orders
```

Use:

```python
aov = calculate_average_order_value(850000, 1700)

print(f"Average Order Value: ₹{aov:,.2f}")
```

---

# 22. Variable Scope

Variable scope determines where a variable can be accessed.

The two basic types to understand are:

```text
Local Scope

Global Scope
```

---

# 23. Local Variables

A variable created inside a function is a local variable.

```python
def calculate_profit(revenue, cost):

    profit = revenue - cost

    return profit
```

Here:

```text
profit
```

is a local variable.

It exists only inside the function.

This will cause an error:

```python
print(profit)
```

because `profit` is not available outside the function.

---

# 24. Global Variables

A variable created outside a function is a global variable.

```python
company_name = "ShopKart India"


def display_company():

    print(company_name)


display_company()
```

The function can access the global variable.

For reusable analytics functions, passing values as parameters is generally cleaner than depending heavily on global variables.

Prefer:

```python
def display_company(company_name):

    print(company_name)
```

---

# 25. Lambda Functions

A lambda is a small anonymous function.

Normal function:

```python
def calculate_profit(revenue, cost):

    return revenue - cost
```

Lambda version:

```python
calculate_profit = lambda revenue, cost: revenue - cost
```

Use:

```python
profit = calculate_profit(850000, 620000)

print(profit)
```

---

# 26. Lambda Syntax

```python
lambda arguments: expression
```

Example:

```python
square = lambda number: number ** 2

print(square(5))
```

Output:

```text
25
```

---

# 27. Data Analyst Lambda Example

```python
profit_margin = lambda profit, revenue: (profit / revenue) * 100

result = profit_margin(230000, 850000)

print(f"Profit Margin: {result:.2f}%")
```

Lambda functions become more useful later with Pandas methods such as:

```text
apply()

map()
```

Do not overuse lambda functions. For complex business logic, normal functions are easier to read.

---

# 28. Reusable KPI Functions

```python
def calculate_revenue(price, quantity):

    return price * quantity


def calculate_profit(revenue, cost):

    return revenue - cost


def calculate_profit_margin(revenue, cost):

    profit = revenue - cost

    return (profit / revenue) * 100


def calculate_growth(previous_value, current_value):

    return (
        (current_value - previous_value)
        / previous_value
    ) * 100


def calculate_average_order_value(revenue, orders):

    return revenue / orders
```

These functions can be reused across multiple business reports.

---

# 29. Complete Business KPI Report

```python
def calculate_profit(revenue, cost):

    return revenue - cost


def calculate_profit_margin(revenue, cost):

    profit = calculate_profit(revenue, cost)

    return (profit / revenue) * 100


def calculate_average_order_value(revenue, orders):

    return revenue / orders


def calculate_growth(previous_sales, current_sales):

    return (
        (current_sales - previous_sales)
        / previous_sales
    ) * 100


# BUSINESS DATA

company_name = "ShopKart India"

current_revenue = 1200000

previous_revenue = 1000000

total_cost = 850000

total_orders = 2400


# KPI CALCULATIONS

total_profit = calculate_profit(
    current_revenue,
    total_cost
)

profit_margin = calculate_profit_margin(
    current_revenue,
    total_cost
)

average_order_value = calculate_average_order_value(
    current_revenue,
    total_orders
)

revenue_growth = calculate_growth(
    previous_revenue,
    current_revenue
)


# BUSINESS REPORT

print("=" * 55)

print(f"BUSINESS KPI REPORT: {company_name.upper()}")

print("=" * 55)

print(f"Revenue:             ₹{current_revenue:,.2f}")

print(f"Profit:              ₹{total_profit:,.2f}")

print(f"Profit Margin:       {profit_margin:.2f}%")

print(f"Average Order Value: ₹{average_order_value:,.2f}")

print(f"Revenue Growth:      {revenue_growth:.2f}%")

print("=" * 55)
```

---

# 30. Common Beginner Errors

## Forgetting to Call the Function

Defining:

```python
def calculate_profit(revenue, cost):

    return revenue - cost
```

does not execute it.

Call:

```python
calculate_profit(850000, 620000)
```

---

## Forgetting return

Wrong:

```python
def calculate_profit(revenue, cost):

    profit = revenue - cost
```

If you need the result outside the function:

```python
def calculate_profit(revenue, cost):

    profit = revenue - cost

    return profit
```

---

## Confusing Parameters and Arguments

```python
def calculate_profit(revenue, cost):
```

`revenue` and `cost` are parameters.

```python
calculate_profit(850000, 620000)
```

`850000` and `620000` are arguments.

---

## Incorrect Argument Order

```python
def calculate_growth(previous_sales, current_sales):

    return (
        (current_sales - previous_sales)
        / previous_sales
    ) * 100
```

Correct:

```python
calculate_growth(750000, 900000)
```

Reversing the values changes the calculation.

---

## Printing Instead of Returning

Avoid:

```python
def calculate_profit(revenue, cost):

    print(revenue - cost)
```

when the result needs to be reused.

Prefer:

```python
def calculate_profit(revenue, cost):

    return revenue - cost
```

---

# 31. Core Patterns to Remember

## Basic Function

```python
def function_name():

    code
```

## Function with Parameters

```python
def function_name(parameter):

    code
```

## Function with Return

```python
def function_name(parameter):

    return result
```

## Function with Default Parameter

```python
def function_name(value, rate=10):

    return result
```

## Lambda Function

```python
lambda arguments: expression
```

---

# 32. Interview Questions

1. What is a function?
2. Why are functions useful in Data Analytics?
3. How do you define a function?
4. What is the difference between defining and calling a function?
5. What is a parameter?
6. What is an argument?
7. What is the difference between parameters and arguments?
8. What does `return` do?
9. What is the difference between `print()` and `return`?
10. What are positional arguments?
11. What are keyword arguments?
12. What are default parameters?
13. What is variable scope?
14. What is a local variable?
15. What is a global variable?
16. What is a lambda function?
17. When should lambda functions be used?
18. How would you create a reusable Profit Margin function?
19. How would you calculate Growth Percentage using a function?
20. Why are reusable functions useful across multiple business reports?

---

# 33. Completion Checklist

Before moving to the next module, you should be able to:

- [ ] Explain what a function is
- [ ] Create user-defined functions
- [ ] Call functions
- [ ] Use meaningful function names
- [ ] Use parameters
- [ ] Pass arguments
- [ ] Explain parameters vs arguments
- [ ] Use positional arguments
- [ ] Use keyword arguments
- [ ] Return calculated values
- [ ] Explain `print()` vs `return`
- [ ] Use default parameters
- [ ] Understand local scope
- [ ] Understand global scope
- [ ] Write basic lambda functions
- [ ] Create a Revenue function
- [ ] Create a Profit function
- [ ] Create a Profit Margin function
- [ ] Create a Growth Percentage function
- [ ] Create an Average Order Value function
- [ ] Create a Customer Discount function
- [ ] Build reusable KPI functions
- [ ] Use functions across multiple business reports

---

# Final Outcome

After completing Functions, you should be able to convert repeated business calculations into reusable Python functions, pass business data using parameters and arguments, return KPI results, use default values, understand basic variable scope, write simple lambda functions, and build reusable Revenue, Profit Margin, Growth, Average Order Value, and Customer Discount calculations.