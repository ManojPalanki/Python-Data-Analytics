# Lists

## 1. Introduction

A list is a Python data structure used to store multiple values in a single variable.

```python
monthly_sales = [850000, 920000, 780000, 1050000]
```

For Data Analysts, lists are useful for storing and processing:

- Monthly Sales
- Product Names
- Revenue Values
- Customer IDs
- Regional Performance
- Business KPIs

Before learning Pandas, lists help you understand how Python stores and processes collections of data.

---

# 2. Creating Lists

Create a list using square brackets `[]`.

```python
monthly_sales = [850000, 920000, 780000, 1050000]
```

String values:

```python
products = ["Laptop", "Mobile", "Tablet", "Monitor"]
```

Mixed data types are allowed:

```python
customer = ["Manoj", 25, 50000.50, True]
```

For Data Analytics, lists usually contain similar types of data.

Better:

```python
sales = [50000, 75000, 90000]
```

---

# 3. List Characteristics

Python lists are:

- Ordered
- Mutable
- Allow duplicate values
- Can contain different data types

Example:

```python
sales = [50000, 75000, 50000]
```

Duplicate values are allowed.

---

# 4. List Indexing

Every list item has an index position.

```python
months = ["January", "February", "March", "April"]
```

Index positions:

```text
January   February   March   April

   0          1        2       3
```

Access the first item:

```python
print(months[0])
```

Output:

```text
January
```

Access the third item:

```python
print(months[2])
```

Output:

```text
March
```

---

# 5. Negative Indexing

Negative indexing accesses values from the end.

```python
monthly_sales = [850000, 920000, 780000, 1050000]
```

Get the last value:

```python
print(monthly_sales[-1])
```

Output:

```text
1050000
```

Get the second-last value:

```python
print(monthly_sales[-2])
```

---

# 6. List Slicing

Slicing extracts multiple values from a list.

Syntax:

```python
list[start:stop]
```

Example:

```python
monthly_sales = [
    850000,
    920000,
    780000,
    1050000,
    1100000,
    950000
]

first_quarter = monthly_sales[0:3]

print(first_quarter)
```

Output:

```text
[850000, 920000, 780000]
```

The `stop` index is excluded.

---

# 7. Slicing Shortcuts

From the beginning:

```python
monthly_sales[:3]
```

From an index to the end:

```python
monthly_sales[3:]
```

Copy all values:

```python
monthly_sales[:]
```

Using steps:

```python
monthly_sales[::2]
```

Reverse a list:

```python
monthly_sales[::-1]
```

---

# 8. Lists Are Mutable

Unlike strings, lists can be modified.

```python
monthly_sales = [850000, 920000, 780000]

monthly_sales[2] = 800000

print(monthly_sales)
```

Output:

```text
[850000, 920000, 800000]
```

This is called modifying or updating a list item.

---

# 9. len()

`len()` returns the number of items.

```python
monthly_sales = [850000, 920000, 780000, 1050000]

print(len(monthly_sales))
```

Output:

```text
4
```

Data Analyst use case:

```python
number_of_months = len(monthly_sales)
```

---

# 10. append()

`append()` adds one item to the end of a list.

```python
monthly_sales = [850000, 920000, 780000]

monthly_sales.append(1050000)

print(monthly_sales)
```

Output:

```text
[850000, 920000, 780000, 1050000]
```

Use case:

Add a new month's sales data.

---

# 11. extend()

`extend()` adds multiple values to a list.

```python
monthly_sales = [850000, 920000]

new_sales = [780000, 1050000]

monthly_sales.extend(new_sales)

print(monthly_sales)
```

Output:

```text
[850000, 920000, 780000, 1050000]
```

---

# 12. append() vs extend()

`append()` adds one item:

```python
sales.append([50000, 75000])
```

Result:

```text
[..., [50000, 75000]]
```

`extend()` adds individual items:

```python
sales.extend([50000, 75000])
```

Result:

```text
[..., 50000, 75000]
```

Remember:

```text
append() → Add One Item

extend() → Add Multiple Items
```

---

# 13. insert()

`insert()` adds an item at a specific index.

```python
products = ["Laptop", "Tablet"]

products.insert(1, "Mobile")

print(products)
```

Output:

```text
["Laptop", "Mobile", "Tablet"]
```

---

# 14. remove()

`remove()` deletes the first matching value.

```python
products = ["Laptop", "Mobile", "Tablet"]

products.remove("Mobile")

print(products)
```

Output:

```text
["Laptop", "Tablet"]
```

---

# 15. pop()

`pop()` removes an item using its index and returns the removed value.

```python
products = ["Laptop", "Mobile", "Tablet"]

removed_product = products.pop(1)

print(removed_product)

print(products)
```

Output:

```text
Mobile

["Laptop", "Tablet"]
```

Without an index:

```python
products.pop()
```

removes the last item.

---

# 16. clear()

`clear()` removes all values.

```python
sales = [50000, 75000, 90000]

sales.clear()

print(sales)
```

Output:

```text
[]
```

---

# 17. index()

`index()` returns the index position of a value.

```python
products = ["Laptop", "Mobile", "Tablet"]

position = products.index("Mobile")

print(position)
```

Output:

```text
1
```

---

# 18. count()

`count()` returns how many times a value occurs.

```python
regions = ["South", "North", "South", "West", "South"]

south_count = regions.count("South")

print(south_count)
```

Output:

```text
3
```

---

# 19. Membership Testing

Use `in` to check whether an item exists.

```python
products = ["Laptop", "Mobile", "Tablet"]

print("Laptop" in products)
```

Output:

```text
True
```

Business example:

```python
if "Laptop" in products:
    print("Laptop Data Available")
```

---

# 20. Looping Through Lists

Lists are commonly processed using loops.

```python
monthly_sales = [850000, 920000, 780000]

for sales in monthly_sales:
    print(f"Sales: ₹{sales:,.2f}")
```

This is one of the most important patterns before learning Pandas.

---

# 21. sum()

`sum()` calculates the total of numerical values.

```python
monthly_sales = [850000, 920000, 780000]

total_sales = sum(monthly_sales)

print(f"Total Sales: ₹{total_sales:,.2f}")
```

---

# 22. max()

`max()` returns the highest value.

```python
monthly_sales = [850000, 920000, 780000, 1050000]

highest_sales = max(monthly_sales)

print(f"Highest Sales: ₹{highest_sales:,.2f}")
```

---

# 23. min()

`min()` returns the lowest value.

```python
monthly_sales = [850000, 920000, 780000, 1050000]

lowest_sales = min(monthly_sales)

print(f"Lowest Sales: ₹{lowest_sales:,.2f}")
```

---

# 24. Calculating Average

Python does not have a basic built-in `average()` function.

Calculate average using:

```python
average_sales = sum(monthly_sales) / len(monthly_sales)
```

Example:

```python
monthly_sales = [850000, 920000, 780000, 1050000]

average_sales = sum(monthly_sales) / len(monthly_sales)

print(f"Average Sales: ₹{average_sales:,.2f}")
```

---

# 25. Sorting Lists

Use `sort()` to modify the original list.

```python
monthly_sales = [850000, 1050000, 780000, 920000]

monthly_sales.sort()

print(monthly_sales)
```

Output:

```text
[780000, 850000, 920000, 1050000]
```

---

# 26. Descending Order

```python
monthly_sales.sort(reverse=True)

print(monthly_sales)
```

Output:

```text
[1050000, 920000, 850000, 780000]
```

Useful for ranking business performance.

---

# 27. sorted()

`sorted()` creates a new sorted list.

```python
monthly_sales = [850000, 1050000, 780000, 920000]

sorted_sales = sorted(monthly_sales)

print(sorted_sales)
```

The original list remains unchanged.

---

# 28. sort() vs sorted()

| `sort()` | `sorted()` |
|---|---|
| Modifies original list | Creates a new list |
| List method | Built-in function |
| Returns `None` | Returns sorted values |

Example:

```python
sales.sort()
```

versus:

```python
sorted_sales = sorted(sales)
```

For Data Analytics, `sorted()` is often safer when the original data should remain unchanged.

---

# 29. Copying Lists

Consider:

```python
original_sales = [850000, 920000, 780000]

new_sales = original_sales
```

This does not create an independent copy.

Changing:

```python
new_sales.append(1050000)
```

also affects:

```python
original_sales
```

---

# 30. copy()

Create an independent copy:

```python
original_sales = [850000, 920000, 780000]

sales_copy = original_sales.copy()

sales_copy.append(1050000)

print(original_sales)

print(sales_copy)
```

Output:

```text
[850000, 920000, 780000]

[850000, 920000, 780000, 1050000]
```

---

# 31. Copy Using Slicing

Another method:

```python
sales_copy = original_sales[:]
```

For beginners, `copy()` is clearer:

```python
sales_copy = original_sales.copy()
```

---

# 32. Monthly Sales Analysis

```python
monthly_sales = [
    850000,
    920000,
    780000,
    1050000,
    1100000,
    950000
]

total_sales = sum(monthly_sales)

average_sales = total_sales / len(monthly_sales)

highest_sales = max(monthly_sales)

lowest_sales = min(monthly_sales)

print(f"Total Sales: ₹{total_sales:,.2f}")

print(f"Average Sales: ₹{average_sales:,.2f}")

print(f"Highest Sales: ₹{highest_sales:,.2f}")

print(f"Lowest Sales: ₹{lowest_sales:,.2f}")
```

---

# 33. Calculating Quarterly Revenue

Store 12 months of sales:

```python
monthly_sales = [
    850000,
    920000,
    780000,
    1050000,
    1100000,
    950000,
    1200000,
    1150000,
    1080000,
    1250000,
    1300000,
    1400000
]
```

Calculate quarterly revenue:

```python
q1_revenue = sum(monthly_sales[0:3])

q2_revenue = sum(monthly_sales[3:6])

q3_revenue = sum(monthly_sales[6:9])

q4_revenue = sum(monthly_sales[9:12])
```

Display:

```python
print(f"Q1 Revenue: ₹{q1_revenue:,.2f}")

print(f"Q2 Revenue: ₹{q2_revenue:,.2f}")

print(f"Q3 Revenue: ₹{q3_revenue:,.2f}")

print(f"Q4 Revenue: ₹{q4_revenue:,.2f}")
```

This combines:

- Lists
- Slicing
- `sum()`

---

# 34. Identifying Highest Sales Month

```python
months = [
    "January",
    "February",
    "March",
    "April"
]

monthly_sales = [
    850000,
    920000,
    780000,
    1050000
]

highest_sales = max(monthly_sales)

highest_sales_index = monthly_sales.index(highest_sales)

highest_sales_month = months[highest_sales_index]

print(f"Highest Sales Month: {highest_sales_month}")

print(f"Sales: ₹{highest_sales:,.2f}")
```

---

# 35. Identifying Lowest Sales Month

```python
lowest_sales = min(monthly_sales)

lowest_sales_index = monthly_sales.index(lowest_sales)

lowest_sales_month = months[lowest_sales_index]

print(f"Lowest Sales Month: {lowest_sales_month}")

print(f"Sales: ₹{lowest_sales:,.2f}")
```

---

# 36. Top-Selling Products

```python
product_sales = [
    850000,
    1250000,
    650000,
    950000
]

sorted_sales = sorted(
    product_sales,
    reverse=True
)

top_three_sales = sorted_sales[:3]

print(top_three_sales)
```

This demonstrates:

- Sorting
- Descending order
- Slicing

---

# 37. Nested Lists

A nested list is a list containing other lists.

```python
sales_data = [
    ["January", 850000],
    ["February", 920000],
    ["March", 780000]
]
```

Each inner list represents one business record.

---

# 38. Accessing Nested Lists

```python
sales_data = [
    ["January", 850000],
    ["February", 920000],
    ["March", 780000]
]
```

Get the first record:

```python
print(sales_data[0])
```

Output:

```text
["January", 850000]
```

Get January sales:

```python
print(sales_data[0][1])
```

Output:

```text
850000
```

---

# 39. Processing Nested Lists

```python
sales_data = [
    ["January", 850000],
    ["February", 920000],
    ["March", 780000]
]

for record in sales_data:

    month = record[0]

    sales = record[1]

    print(f"{month}: ₹{sales:,.2f}")
```

---

# 40. Real-World Monthly Business Analysis

```python
months = [
    "January",
    "February",
    "March",
    "April",
    "May",
    "June"
]

monthly_sales = [
    850000,
    920000,
    780000,
    1050000,
    1100000,
    950000
]


# KPI CALCULATIONS

total_sales = sum(monthly_sales)

average_sales = total_sales / len(monthly_sales)

highest_sales = max(monthly_sales)

lowest_sales = min(monthly_sales)


# IDENTIFY MONTHS

highest_month_index = monthly_sales.index(highest_sales)

lowest_month_index = monthly_sales.index(lowest_sales)

highest_sales_month = months[highest_month_index]

lowest_sales_month = months[lowest_month_index]


# QUARTERLY REVENUE

q1_revenue = sum(monthly_sales[:3])

q2_revenue = sum(monthly_sales[3:6])


# BUSINESS REPORT

print("=" * 55)

print("MONTHLY BUSINESS PERFORMANCE ANALYSIS")

print("=" * 55)

print(f"Total Sales:          ₹{total_sales:,.2f}")

print(f"Average Sales:        ₹{average_sales:,.2f}")

print(f"Highest Sales:        ₹{highest_sales:,.2f}")

print(f"Highest Sales Month:  {highest_sales_month}")

print(f"Lowest Sales:         ₹{lowest_sales:,.2f}")

print(f"Lowest Sales Month:   {lowest_sales_month}")

print(f"Q1 Revenue:           ₹{q1_revenue:,.2f}")

print(f"Q2 Revenue:           ₹{q2_revenue:,.2f}")

print("=" * 55)
```

---

# 41. Most Important List Methods

| Method / Function | Purpose |
|---|---|
| `append()` | Add one item |
| `extend()` | Add multiple items |
| `insert()` | Add at specific position |
| `remove()` | Remove by value |
| `pop()` | Remove by index |
| `index()` | Find item position |
| `count()` | Count occurrences |
| `sort()` | Sort original list |
| `sorted()` | Create sorted list |
| `copy()` | Copy a list |
| `len()` | Count items |
| `sum()` | Calculate total |
| `max()` | Find highest value |
| `min()` | Find lowest value |

These are the list operations you should master before moving to Pandas.

---

# 42. Core Patterns to Remember

## Store Business Data

```python
monthly_sales = [850000, 920000, 780000]
```

## Calculate Total

```python
total_sales = sum(monthly_sales)
```

## Calculate Average

```python
average_sales = sum(monthly_sales) / len(monthly_sales)
```

## Find Highest

```python
highest_sales = max(monthly_sales)
```

## Find Lowest

```python
lowest_sales = min(monthly_sales)
```

## Find Corresponding Month

```python
index = monthly_sales.index(highest_sales)

month = months[index]
```

## Calculate Quarterly Revenue

```python
q1_revenue = sum(monthly_sales[0:3])
```

## Rank Values

```python
sorted_sales = sorted(
    monthly_sales,
    reverse=True
)
```

---

# 43. Common Beginner Errors

## Accessing Invalid Index

```python
sales = [50000, 75000]

print(sales[5])
```

This causes:

```text
IndexError
```

---

## Confusing append() and extend()

Wrong when adding multiple individual values:

```python
sales.append([50000, 75000])
```

Use:

```python
sales.extend([50000, 75000])
```

---

## Incorrect List Copy

Avoid:

```python
sales_copy = original_sales
```

Use:

```python
sales_copy = original_sales.copy()
```

---

## Confusing sort() and sorted()

This is wrong:

```python
sorted_sales = sales.sort()
```

`sort()` returns `None`.

Use:

```python
sales.sort()
```

or:

```python
sorted_sales = sorted(sales)
```

---

# 44. Interview Questions

1. What is a list?
2. Why are lists useful for Data Analysts?
3. What does mutable mean?
4. How do you access list items?
5. What is negative indexing?
6. What is list slicing?
7. What is the difference between `append()` and `extend()`?
8. What is the difference between `remove()` and `pop()`?
9. How do you calculate total sales from a list?
10. How do you calculate average sales?
11. How do you find the highest and lowest values?
12. What is the difference between `sort()` and `sorted()`?
13. Why is `new_list = old_list` not a true independent copy?
14. How do you copy a list?
15. What is a nested list?
16. How would you calculate quarterly revenue from monthly sales?
17. How would you identify the highest sales month?
18. How would you identify the lowest sales month?
19. How would you find top-selling values?
20. How are lists useful before learning Pandas?

---

# 45. Completion Checklist

Before moving to the next module, you should be able to:

- [ ] Create lists
- [ ] Explain list characteristics
- [ ] Use positive indexing
- [ ] Use negative indexing
- [ ] Slice lists
- [ ] Modify list values
- [ ] Use `len()`
- [ ] Use `append()`
- [ ] Use `extend()`
- [ ] Explain `append()` vs `extend()`
- [ ] Use `insert()`
- [ ] Use `remove()`
- [ ] Use `pop()`
- [ ] Use `index()`
- [ ] Use `count()`
- [ ] Loop through lists
- [ ] Use `sum()`
- [ ] Use `max()`
- [ ] Use `min()`
- [ ] Calculate averages
- [ ] Use `sort()`
- [ ] Use `sorted()`
- [ ] Explain `sort()` vs `sorted()`
- [ ] Copy lists correctly
- [ ] Create nested lists
- [ ] Process nested lists
- [ ] Store monthly sales
- [ ] Calculate quarterly revenue
- [ ] Identify highest sales month
- [ ] Identify lowest sales month
- [ ] Find top-selling values
- [ ] Analyze monthly business performance before Pandas

---

# Final Outcome

After completing Lists, you should be able to store and modify business data, access and slice values, use essential list methods, sort and copy data correctly, work with nested lists, calculate total and average sales, calculate quarterly revenue, identify highest and lowest sales months, and perform basic monthly business performance analysis before moving to Pandas.