# Tuples, Sets & Dictionaries

## 1. Introduction

Python provides different data structures for storing collections of data.

The three structures covered in this module are:

| Data Structure | Main Purpose |
|---|---|
| Tuple | Store fixed, ordered data |
| Set | Store unique values and remove duplicates |
| Dictionary | Store data as key-value pairs |

For Data Analysts, the practical use cases are:

- Tuple → Store fixed KPI targets
- Set → Remove duplicate customer IDs
- Dictionary → Store Product → Sales mappings
- Dictionary → Store Region → Revenue mappings
- Dictionary → Organize business metrics for quick lookup and reporting

---

# 2. Tuples

A tuple is an ordered collection of values.

Create a tuple using parentheses `()`.

```python
sales_targets = (500000, 750000, 1000000)
```

Tuple characteristics:

- Ordered
- Allows duplicate values
- Supports indexing
- Supports slicing
- Immutable

The most important difference between a list and tuple is:

```text
List  → Mutable

Tuple → Immutable
```

---

# 3. Creating Tuples

```python
monthly_targets = (500000, 750000, 1000000)
```

Strings can also be stored:

```python
regions = ("South", "North", "East", "West")
```

Mixed data types are allowed:

```python
company_data = ("ShopKart", 2026, 850000.50)
```

---

# 4. Tuple Indexing

Tuple items are accessed using index positions.

```python
regions = ("South", "North", "East", "West")

print(regions[0])
```

Output:

```text
South
```

Access the last value:

```python
print(regions[-1])
```

Output:

```text
West
```

---

# 5. Tuple Slicing

Tuple slicing works like list slicing.

```python
sales_targets = (
    500000,
    750000,
    1000000,
    1250000
)

print(sales_targets[0:2])
```

Output:

```text
(500000, 750000)
```

---

# 6. Tuple Immutability

Tuples cannot be modified after creation.

```python
sales_targets = (500000, 750000, 1000000)

sales_targets[0] = 600000
```

This causes an error.

Use tuples when data should remain fixed.

---

# 7. Tuple Methods

Tuples have only two important built-in methods:

```text
count()

index()
```

### count()

Counts how many times a value appears.

```python
ratings = (5, 4, 5, 3, 5)

print(ratings.count(5))
```

Output:

```text
3
```

### index()

Returns the first index position of a value.

```python
regions = ("South", "North", "East")

print(regions.index("North"))
```

Output:

```text
1
```

---

# 8. Tuple Unpacking

Tuple values can be assigned to multiple variables.

```python
sales_targets = (500000, 750000, 1000000)

minimum_target, standard_target, stretch_target = sales_targets
```

Use:

```python
print(minimum_target)

print(standard_target)

print(stretch_target)
```

Tuple unpacking makes fixed business values easier to use.

---

# 9. Data Analyst Use Case — KPI Targets

```python
kpi_targets = (
    1000000,
    250000,
    20
)

revenue_target, profit_target, margin_target = kpi_targets

print(f"Revenue Target: ₹{revenue_target:,.2f}")

print(f"Profit Target: ₹{profit_target:,.2f}")

print(f"Margin Target: {margin_target}%")
```

Use a tuple when the KPI target structure should remain fixed.

---

# 10. Sets

A set is a collection of unique values.

Create a set using curly brackets `{}`.

```python
customer_ids = {101, 102, 103, 104}
```

Set characteristics:

- Stores unique values
- Removes duplicates
- Unordered
- Does not support indexing
- Mutable

---

# 11. Removing Duplicate Values

Consider duplicate customer IDs:

```python
customer_ids = [
    101,
    102,
    103,
    101,
    104,
    102
]
```

Convert the list to a set:

```python
unique_customer_ids = set(customer_ids)

print(unique_customer_ids)
```

Result contains only unique IDs:

```text
{101, 102, 103, 104}
```

This is the most important beginner Data Analyst use case for sets.

---

# 12. Counting Unique Customers

```python
customer_ids = [
    101,
    102,
    103,
    101,
    104,
    102
]

unique_customers = set(customer_ids)

unique_customer_count = len(unique_customers)

print(f"Unique Customers: {unique_customer_count}")
```

Output:

```text
Unique Customers: 4
```

---

# 13. Adding Values to Sets

Use `add()` to add one value.

```python
regions = {"South", "North", "East"}

regions.add("West")

print(regions)
```

---

# 14. Adding Multiple Values

Use `update()` to add multiple values.

```python
regions = {"South", "North"}

regions.update(["East", "West"])

print(regions)
```

---

# 15. Removing Values from Sets

Use `remove()`:

```python
regions = {"South", "North", "East"}

regions.remove("North")
```

If the value does not exist, `remove()` causes an error.

Use `discard()`:

```python
regions.discard("West")
```

If the value does not exist, no error occurs.

For safer removal:

```text
discard()
```

is often preferable.

---

# 16. Set Operations

Important set operations are:

| Operation | Purpose |
|---|---|
| Union | Combine unique values |
| Intersection | Find common values |
| Difference | Find values existing only in one set |

---

# 17. Union

Union combines unique values from both sets.

```python
online_customers = {101, 102, 103}

store_customers = {103, 104, 105}

all_customers = online_customers.union(store_customers)

print(all_customers)
```

Result:

```text
{101, 102, 103, 104, 105}
```

---

# 18. Intersection

Intersection finds common values.

```python
online_customers = {101, 102, 103}

store_customers = {103, 104, 105}

common_customers = online_customers.intersection(
    store_customers
)

print(common_customers)
```

Output:

```text
{103}
```

Data Analyst use case:

Identify customers purchasing through both channels.

---

# 19. Difference

Difference finds values present in one set but not another.

```python
online_customers = {101, 102, 103}

store_customers = {103, 104, 105}

online_only = online_customers.difference(
    store_customers
)

print(online_only)
```

Result:

```text
{101, 102}
```

---

# 20. Most Important Set Operations

```python
set_a.union(set_b)
```

Combine unique values.

```python
set_a.intersection(set_b)
```

Find common values.

```python
set_a.difference(set_b)
```

Find values only in the first set.

Do not waste time memorizing every set method. These operations cover the majority of beginner analytics use cases.

---

# 21. Dictionaries

A dictionary stores data using key-value pairs.

Create a dictionary using curly brackets `{}`.

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000,
    "Tablet": 650000
}
```

Structure:

```text
Key → Value
```

Example:

```text
Laptop → 850000

Mobile → 1250000

Tablet → 650000
```

Dictionaries are the most important topic in this module for Data Analysts.

---

# 22. Dictionary Characteristics

Dictionaries:

- Store key-value pairs
- Are mutable
- Preserve insertion order in modern Python
- Require unique keys
- Allow values to be duplicated

Example:

```python
region_revenue = {
    "South": 1500000,
    "North": 1250000,
    "East": 950000
}
```

---

# 23. Accessing Dictionary Values

Access values using keys.

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000,
    "Tablet": 650000
}

print(product_sales["Laptop"])
```

Output:

```text
850000
```

---

# 24. get() Method

Values can also be accessed using `get()`.

```python
print(product_sales.get("Laptop"))
```

Output:

```text
850000
```

The important difference is what happens when a key does not exist.

Using:

```python
product_sales["Monitor"]
```

causes:

```text
KeyError
```

Using:

```python
product_sales.get("Monitor")
```

returns:

```text
None
```

You can provide a default value:

```python
product_sales.get("Monitor", 0)
```

For data lookup tasks, `get()` is often safer.

---

# 25. Adding Dictionary Values

Add a new key-value pair:

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000
}

product_sales["Tablet"] = 650000

print(product_sales)
```

---

# 26. Updating Dictionary Values

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000
}

product_sales["Laptop"] = 950000

print(product_sales)
```

Dictionaries are mutable, so values can be changed.

---

# 27. update() Method

Add or update multiple values:

```python
product_sales.update({
    "Laptop": 950000,
    "Tablet": 650000
})
```

---

# 28. Removing Dictionary Values

Use `pop()`:

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000,
    "Tablet": 650000
}

removed_sales = product_sales.pop("Tablet")
```

Use `del`:

```python
del product_sales["Mobile"]
```

Use `clear()` to remove everything:

```python
product_sales.clear()
```

---

# 29. keys()

`keys()` returns all dictionary keys.

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000,
    "Tablet": 650000
}

print(product_sales.keys())
```

The keys are:

```text
Laptop
Mobile
Tablet
```

---

# 30. values()

`values()` returns all dictionary values.

```python
print(product_sales.values())
```

Values:

```text
850000
1250000
650000
```

---

# 31. items()

`items()` returns key-value pairs.

```python
print(product_sales.items())
```

This method is extremely useful when looping through dictionaries.

---

# 32. Looping Through Dictionary Keys

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000,
    "Tablet": 650000
}

for product in product_sales:

    print(product)
```

Output:

```text
Laptop
Mobile
Tablet
```

---

# 33. Looping Through Values

```python
for sales in product_sales.values():

    print(sales)
```

---

# 34. Looping Through Key-Value Pairs

Use `items()`:

```python
for product, sales in product_sales.items():

    print(f"{product}: ₹{sales:,.2f}")
```

Output:

```text
Laptop: ₹850,000.00

Mobile: ₹1,250,000.00

Tablet: ₹650,000.00
```

This is one of the most important dictionary patterns.

---

# 35. Product → Sales Dictionary

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000,
    "Tablet": 650000,
    "Monitor": 475000
}

for product, sales in product_sales.items():

    print(f"{product}: ₹{sales:,.2f}")
```

This provides fast lookup and organized reporting.

---

# 36. Region → Revenue Dictionary

```python
region_revenue = {
    "South": 1500000,
    "North": 1250000,
    "East": 950000,
    "West": 1750000
}

for region, revenue in region_revenue.items():

    print(f"{region}: ₹{revenue:,.2f}")
```

---

# 37. Calculating Total Revenue

```python
region_revenue = {
    "South": 1500000,
    "North": 1250000,
    "East": 950000,
    "West": 1750000
}

total_revenue = sum(region_revenue.values())

print(f"Total Revenue: ₹{total_revenue:,.2f}")
```

---

# 38. Calculating Average Revenue

```python
average_revenue = (
    sum(region_revenue.values())
    / len(region_revenue)
)

print(f"Average Revenue: ₹{average_revenue:,.2f}")
```

---

# 39. Finding Highest Revenue

```python
highest_revenue = max(region_revenue.values())

print(f"Highest Revenue: ₹{highest_revenue:,.2f}")
```

But this only returns the value.

To identify the corresponding region:

```python
highest_region = max(
    region_revenue,
    key=region_revenue.get
)

print(f"Highest Revenue Region: {highest_region}")

print(
    f"Revenue: ₹{region_revenue[highest_region]:,.2f}"
)
```

---

# 40. Business KPI Dictionary

```python
business_kpis = {
    "Revenue": 1500000,
    "Profit": 350000,
    "Orders": 2500,
    "Customers": 1800
}
```

Access individual KPIs:

```python
print(business_kpis["Revenue"])
```

Loop through all KPIs:

```python
for kpi, value in business_kpis.items():

    print(f"{kpi}: {value}")
```

---

# 41. Nested Dictionaries

A dictionary can contain other dictionaries.

```python
product_data = {
    "Laptop": {
        "Sales": 850000,
        "Profit": 175000
    },

    "Mobile": {
        "Sales": 1250000,
        "Profit": 275000
    }
}
```

---

# 42. Accessing Nested Dictionary Values

Get Laptop data:

```python
print(product_data["Laptop"])
```

Get Laptop sales:

```python
print(product_data["Laptop"]["Sales"])
```

Output:

```text
850000
```

Get Mobile profit:

```python
print(product_data["Mobile"]["Profit"])
```

---

# 43. Looping Through Nested Dictionaries

```python
for product, metrics in product_data.items():

    print(f"Product: {product}")

    print(f"Sales: ₹{metrics['Sales']:,.2f}")

    print(f"Profit: ₹{metrics['Profit']:,.2f}")
```

Nested dictionaries are useful for representing structured business data before learning Pandas DataFrames.

---

# 44. Real-World Business Analysis

```python
# FIXED KPI TARGETS

kpi_targets = (
    1000000,
    250000,
    20
)

revenue_target, profit_target, margin_target = kpi_targets


# CUSTOMER DATA WITH DUPLICATES

customer_ids = [
    101,
    102,
    103,
    101,
    104,
    102,
    105
]

unique_customers = set(customer_ids)


# PRODUCT SALES DATA

product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000,
    "Tablet": 650000,
    "Monitor": 475000
}


# REGION REVENUE DATA

region_revenue = {
    "South": 1500000,
    "North": 1250000,
    "East": 950000,
    "West": 1750000
}


# CALCULATIONS

unique_customer_count = len(unique_customers)

total_product_sales = sum(product_sales.values())

highest_selling_product = max(
    product_sales,
    key=product_sales.get
)

total_region_revenue = sum(region_revenue.values())

highest_revenue_region = max(
    region_revenue,
    key=region_revenue.get
)


# BUSINESS REPORT

print("=" * 55)

print("BUSINESS PERFORMANCE REPORT")

print("=" * 55)

print(f"Revenue Target: ₹{revenue_target:,.2f}")

print(f"Profit Target: ₹{profit_target:,.2f}")

print(f"Margin Target: {margin_target}%")

print("-" * 55)

print(f"Unique Customers: {unique_customer_count}")

print(f"Total Product Sales: ₹{total_product_sales:,.2f}")

print(f"Highest-Selling Product: {highest_selling_product}")

print(f"Total Region Revenue: ₹{total_region_revenue:,.2f}")

print(f"Highest Revenue Region: {highest_revenue_region}")

print("=" * 55)
```

---

# 45. List vs Tuple vs Set vs Dictionary

| Structure | Ordered | Mutable | Duplicates | Main Analytics Use |
|---|---|---|---|---|
| List | Yes | Yes | Yes | Store sequences of data |
| Tuple | Yes | No | Yes | Store fixed values |
| Set | No | Yes | No | Remove duplicates |
| Dictionary | Yes | Yes | Keys: No | Store key-value mappings |

The practical decision is:

```text
Need an ordered, changeable collection?
→ List

Need fixed values?
→ Tuple

Need unique values?
→ Set

Need Key → Value relationships?
→ Dictionary
```

---

# 46. Most Important Dictionary Methods

| Method | Purpose |
|---|---|
| `get()` | Safely retrieve a value |
| `keys()` | Get all keys |
| `values()` | Get all values |
| `items()` | Get key-value pairs |
| `update()` | Add or modify values |
| `pop()` | Remove a key-value pair |
| `clear()` | Remove all values |

Do not memorize every dictionary method. Master these first.

---

# 47. Core Patterns to Remember

## Store Fixed KPI Targets

```python
kpi_targets = (
    1000000,
    250000,
    20
)
```

## Remove Duplicate Customers

```python
unique_customers = set(customer_ids)
```

## Count Unique Customers

```python
unique_customer_count = len(set(customer_ids))
```

## Store Product Sales

```python
product_sales = {
    "Laptop": 850000,
    "Mobile": 1250000
}
```

## Safely Access Values

```python
product_sales.get("Laptop", 0)
```

## Process Dictionary Data

```python
for product, sales in product_sales.items():

    print(product, sales)
```

## Calculate Total

```python
total_sales = sum(product_sales.values())
```

## Find Highest-Performing Key

```python
highest_product = max(
    product_sales,
    key=product_sales.get
)
```

---

# 48. Common Beginner Errors

## Creating an Empty Set Incorrectly

Wrong:

```python
empty_set = {}
```

This creates an empty dictionary.

Correct:

```python
empty_set = set()
```

---

## Trying to Modify a Tuple

Wrong:

```python
targets = (500000, 750000)

targets[0] = 600000
```

Tuples are immutable.

---

## Trying to Access Set Values by Index

Wrong:

```python
customer_ids = {101, 102, 103}

print(customer_ids[0])
```

Sets do not support indexing.

---

## Accessing a Missing Dictionary Key

This can cause an error:

```python
product_sales["Monitor"]
```

Safer:

```python
product_sales.get("Monitor", 0)
```

---

## Forgetting items() When Looping Through Key-Value Pairs

Wrong:

```python
for product, sales in product_sales:

    print(product, sales)
```

Correct:

```python
for product, sales in product_sales.items():

    print(product, sales)
```

---

# 49. Interview Questions

1. What is a tuple?
2. What is the difference between a list and a tuple?
3. What does immutable mean?
4. What is tuple unpacking?
5. When should a Data Analyst use a tuple?
6. What is a set?
7. Why do sets automatically remove duplicates?
8. How do you count unique customers?
9. What is the difference between `remove()` and `discard()`?
10. What are union, intersection, and difference?
11. What is a dictionary?
12. What is a key-value pair?
13. How do you access dictionary values?
14. What is the difference between `dictionary[key]` and `get()`?
15. What do `keys()`, `values()`, and `items()` return?
16. How do you loop through dictionary key-value pairs?
17. How do you calculate total sales from a dictionary?
18. How do you identify the highest-performing product?
19. What is a nested dictionary?
20. When should you use a list, tuple, set, or dictionary?

---

# 50. Completion Checklist

Before moving to the next module, you should be able to:

- [ ] Create tuples
- [ ] Access tuple values
- [ ] Slice tuples
- [ ] Explain tuple immutability
- [ ] Use tuple unpacking
- [ ] Store fixed KPI targets
- [ ] Create sets
- [ ] Remove duplicate values
- [ ] Count unique customers
- [ ] Use `add()`
- [ ] Use `update()`
- [ ] Use `remove()` and `discard()`
- [ ] Use union
- [ ] Use intersection
- [ ] Use difference
- [ ] Create dictionaries
- [ ] Explain key-value pairs
- [ ] Access dictionary values
- [ ] Use `get()`
- [ ] Add and update dictionary values
- [ ] Remove dictionary values
- [ ] Use `keys()`
- [ ] Use `values()`
- [ ] Use `items()`
- [ ] Loop through dictionaries
- [ ] Store Product → Sales data
- [ ] Store Region → Revenue data
- [ ] Calculate totals from dictionaries
- [ ] Find the highest-performing key
- [ ] Create basic nested dictionaries
- [ ] Choose correctly between List, Tuple, Set, and Dictionary

---

# Final Outcome

After completing Tuples, Sets, and Dictionaries, you should be able to store fixed KPI targets using tuples, remove duplicate customer IDs using sets, identify common and unique customers using set operations, organize Product → Sales and Region → Revenue relationships using dictionaries, perform quick business data lookups, calculate metrics, and create structured business reports.