# Advanced Pandas

## 1. Introduction

Advanced Pandas is mainly about combining, transforming, and analyzing multiple business datasets.

For Data Analysts, the most important topics are:

- `merge()`
- Join Types
- `join()`
- `concat()`
- `apply()`
- `map()`
- `transform()`
- MultiIndex Basics
- Combining Orders, Customers, and Products
- Customer Lifetime Value
- Repeat Purchase Rate
- Cross-Functional Business Analysis

The core workflow is:

```text
Multiple Business Datasets
        ↓
Understand Relationships
        ↓
Merge / Join / Concat
        ↓
Transform Data
        ↓
Aggregate Data
        ↓
Calculate Business KPIs
        ↓
Generate Insights
        ↓
Answer Business Questions
```

---

# 2. Why Advanced Pandas Matters

Real-world business data is rarely stored in one dataset.

For example:

```text
Orders Dataset

Customers Dataset

Products Dataset
```

The Orders dataset may contain:

```text
order_id
customer_id
product_id
quantity
sales
order_date
```

The Customers dataset may contain:

```text
customer_id
customer_name
region
segment
```

The Products dataset may contain:

```text
product_id
product_name
category
cost
```

To perform complete business analysis, these datasets must be combined.

---

# 3. Sample Business Data

```python
import pandas as pd
```

Orders:

```python
orders = pd.DataFrame({

    "order_id": [
        101,
        102,
        103,
        104,
        105
    ],

    "customer_id": [
        1,
        2,
        1,
        3,
        2
    ],

    "product_id": [
        201,
        202,
        203,
        201,
        203
    ],

    "quantity": [
        2,
        1,
        3,
        2,
        1
    ],

    "sales": [
        2000,
        1500,
        3000,
        2500,
        1000
    ]
})
```

Customers:

```python
customers = pd.DataFrame({

    "customer_id": [
        1,
        2,
        3
    ],

    "customer_name": [
        "Arun",
        "Ravi",
        "Priya"
    ],

    "region": [
        "South",
        "West",
        "North"
    ]
})
```

Products:

```python
products = pd.DataFrame({

    "product_id": [
        201,
        202,
        203
    ],

    "product_name": [
        "Laptop",
        "Phone",
        "Tablet"
    ],

    "category": [
        "Electronics",
        "Electronics",
        "Electronics"
    ]
})
```

---

# 4. merge()

`merge()` combines DataFrames using common columns.

Syntax:

```python
pd.merge(
    left_dataframe,
    right_dataframe,
    on="common_column"
)
```

Example:

```python
merged_data = pd.merge(
    orders,
    customers,
    on="customer_id"
)
```

Result:

```text
Orders Data
+
Customer Information
```

---

# 5. Common Merge Syntax

```python
pd.merge(
    left,
    right,
    on="key",
    how="inner"
)
```

Important parameters:

```text
left
→ First DataFrame

right
→ Second DataFrame

on
→ Common Column

how
→ Join Type
```

---

# 6. Join Types

The four important join types are:

```text
INNER JOIN

LEFT JOIN

RIGHT JOIN

OUTER JOIN
```

These concepts are similar to SQL Joins.

---

# 7. Inner Join

An Inner Join returns only matching records.

```python
result = pd.merge(
    orders,
    customers,
    on="customer_id",
    how="inner"
)
```

Concept:

```text
Orders
    ∩
Customers
```

Use when:

```text
Only Matching Records Are Required
```

---

# 8. Left Join

A Left Join keeps all records from the left DataFrame.

```python
result = pd.merge(
    orders,
    customers,
    on="customer_id",
    how="left"
)
```

Use when:

```text
Keep All Orders

Add Customer Information Where Available
```

This is extremely common in Data Analysis.

---

# 9. Right Join

A Right Join keeps all records from the right DataFrame.

```python
result = pd.merge(
    orders,
    customers,
    on="customer_id",
    how="right"
)
```

Use when:

```text
Keep All Customers

Add Order Information Where Available
```

---

# 10. Outer Join

An Outer Join keeps all records from both DataFrames.

```python
result = pd.merge(
    orders,
    customers,
    on="customer_id",
    how="outer"
)
```

Use when:

```text
Find Matched and Unmatched Records
```

---

# 11. Validate Merge Results

Never blindly merge datasets and continue analysis.

Check:

```python
orders.shape
```

```python
customers.shape
```

```python
merged_data.shape
```

Also check:

```python
merged_data.head()
```

```python
merged_data.info()
```

```python
merged_data.isnull().sum()
```

Important:

```text
A Successful Merge Does Not Automatically Mean a Correct Merge
```

---

# 12. Merge Indicator

Use:

```python
indicator=True
```

Example:

```python
result = pd.merge(
    orders,
    customers,
    on="customer_id",
    how="outer",
    indicator=True
)
```

This creates:

```text
_merge
```

Possible values:

```text
left_only

right_only

both
```

Useful for identifying unmatched records.

---

# 13. Find Unmatched Records

```python
result[
    result["_merge"] == "left_only"
]
```

This can help identify:

```text
Orders Without Customer Records

Products Without Matching Product Information

Data Quality Problems
```

---

# 14. Merge on Different Column Names

Sometimes key columns have different names.

Example:

```text
orders.customer_id

customers.cust_id
```

Use:

```python
pd.merge(
    orders,
    customers,
    left_on="customer_id",
    right_on="cust_id"
)
```

---

# 15. Merge Multiple DataFrames

First:

```python
analysis_data = pd.merge(
    orders,
    customers,
    on="customer_id",
    how="left"
)
```

Then:

```python
analysis_data = pd.merge(
    analysis_data,
    products,
    on="product_id",
    how="left"
)
```

Now the dataset contains:

```text
Order Information

Customer Information

Product Information
```

---

# 16. Method Chaining Multiple Merges

```python
analysis_data = (
    orders

    .merge(
        customers,
        on="customer_id",
        how="left"
    )

    .merge(
        products,
        on="product_id",
        how="left"
    )
)
```

This is cleaner and easier to read.

---

# 17. Duplicate Keys and Merge Problems

Suppose the Customers dataset contains duplicate customer IDs.

Check:

```python
customers[
    "customer_id"
].duplicated().sum()
```

If duplicate keys exist:

```text
Merge Results May Unexpectedly Increase Row Count
```

Before merging:

```python
customers[
    "customer_id"
].is_unique
```

Always understand:

```text
One-to-One

One-to-Many

Many-to-One

Many-to-Many
```

relationships before merging.

---

# 18. Validate Merge Relationships

Use:

```python
pd.merge(
    orders,
    customers,
    on="customer_id",
    how="left",
    validate="many_to_one"
)
```

Possible values:

```text
one_to_one

one_to_many

many_to_one

many_to_many
```

This is useful for preventing incorrect merges.

---

# 19. join()

`join()` combines DataFrames mainly using indexes.

Example:

```python
customers_indexed = (
    customers.set_index(
        "customer_id"
    )
)
```

```python
orders_indexed = (
    orders.set_index(
        "customer_id"
    )
)
```

Join:

```python
result = orders_indexed.join(
    customers_indexed,
    how="left"
)
```

---

# 20. merge() vs join()

```text
merge()
→ Usually Combines Using Columns

join()
→ Usually Combines Using Index
```

For most Data Analyst workflows:

```text
merge() Is More Common
```

---

# 21. concat()

`concat()` combines DataFrames vertically or horizontally.

Syntax:

```python
pd.concat()
```

---

# 22. Vertical Concatenation

Suppose:

```text
January Orders

February Orders

March Orders
```

Combine:

```python
all_orders = pd.concat(
    [
        january_orders,
        february_orders,
        march_orders
    ]
)
```

Better:

```python
all_orders = pd.concat(
    [
        january_orders,
        february_orders,
        march_orders
    ],

    ignore_index=True
)
```

---

# 23. Why ignore_index=True?

Without:

```python
ignore_index=True
```

old indexes may remain.

With:

```python
ignore_index=True
```

Pandas creates a new continuous index.

---

# 24. Horizontal Concatenation

```python
result = pd.concat(
    [
        dataframe1,
        dataframe2
    ],

    axis=1
)
```

Meaning:

```text
axis=0
→ Rows

axis=1
→ Columns
```

---

# 25. merge() vs concat()

Use `merge()` when:

```text
Datasets Share Common Keys
```

Example:

```text
Orders + Customers
```

Use `concat()` when:

```text
Datasets Have Similar Structures
```

Example:

```text
January Orders
+
February Orders
+
March Orders
```

---

# 26. apply()

`apply()` applies a function to data.

Example:

```python
def classify_sales(sales):

    if sales >= 5000:
        return "High"

    elif sales >= 2000:
        return "Medium"

    else:
        return "Low"
```

Apply:

```python
df["sales_category"] = (
    df["sales"]
    .apply(classify_sales)
)
```

---

# 27. apply() with lambda

```python
df["sales_category"] = (
    df["sales"]
    .apply(
        lambda x:
        "High"
        if x >= 5000
        else "Low"
    )
)
```

Use lambda for simple operations.

Use named functions for complex business logic.

---

# 28. apply() Across Rows

Example:

```python
def calculate_performance(row):

    if (
        row["sales"] >= 5000
        and
        row["profit"] > 0
    ):
        return "Strong"

    return "Weak"
```

Apply:

```python
df["performance"] = df.apply(
    calculate_performance,
    axis=1
)
```

Important:

```text
axis=1
→ Apply Function Across Rows
```

---

# 29. Performance Warning About apply()

Do not automatically use `apply()` for every transformation.

Example:

Slower approach:

```python
df["profit"] = df.apply(
    lambda row:
    row["sales"] - row["cost"],
    axis=1
)
```

Better:

```python
df["profit"] = (
    df["sales"]
    -
    df["cost"]
)
```

Prefer:

```text
Vectorized Pandas Operations
```

when possible.

---

# 30. map()

`map()` is commonly used to transform values in a Series.

Example:

```python
region_mapping = {

    "South": "S",

    "North": "N",

    "East": "E",

    "West": "W"
}
```

Apply:

```python
df["region_code"] = (
    df["region"]
    .map(region_mapping)
)
```

---

# 31. map() Business Use Cases

Common uses:

```text
Convert Codes to Labels

Convert Categories to Scores

Standardize Business Values

Create Region Codes

Create Product Category Mappings
```

Example:

```python
segment_score = {

    "Consumer": 1,

    "Corporate": 2,

    "Home Office": 3
}
```

```python
df["segment_score"] = (
    df["segment"]
    .map(segment_score)
)
```

---

# 32. apply() vs map()

Use `map()`:

```text
For Element-Wise Series Transformations
```

Use `apply()`:

```text
For Custom Functions and More Complex Logic
```

---

# 33. transform()

`transform()` performs group-level calculations while returning results with the same number of rows as the original DataFrame.

Example:

```python
df["regional_avg_sales"] = (
    df.groupby(
        "region"
    )["sales"]
    .transform("mean")
)
```

Original:

```text
1000 Rows
```

Result:

```text
1000 Rows
```

Each row receives its regional average.

---

# 34. transform() Business Example

Calculate regional total sales:

```python
df["regional_total_sales"] = (
    df.groupby(
        "region"
    )["sales"]
    .transform("sum")
)
```

Calculate each row's contribution:

```python
df["regional_sales_share"] = (

    df["sales"]

    /

    df["regional_total_sales"]

    *

    100
)
```

---

# 35. GroupBy Aggregation vs transform()

Aggregation:

```python
df.groupby(
    "region"
)["sales"].sum()
```

Result:

```text
One Row Per Region
```

Transform:

```python
df.groupby(
    "region"
)["sales"].transform("sum")
```

Result:

```text
Same Number of Rows as Original Dataset
```

---

# 36. MultiIndex

A MultiIndex allows multiple index levels.

Example:

```python
regional_category_sales = (
    df.groupby(
        [
            "region",
            "category"
        ]
    )["sales"]
    .sum()
)
```

Result:

```text
Region
    Category
```

Both become index levels.

---

# 37. Create MultiIndex

```python
multi_index_df = (
    df.set_index(
        [
            "region",
            "category"
        ]
    )
)
```

---

# 38. reset_index()

Convert indexes back into columns:

```python
result = (
    regional_category_sales
    .reset_index()
)
```

For most Data Analyst workflows:

```text
reset_index()
```

is frequently useful after GroupBy operations.

---

# 39. Access MultiIndex Data

Example:

```python
regional_category_sales.loc[
    "South"
]
```

Specific combination:

```python
regional_category_sales.loc[
    (
        "South",
        "Electronics"
    )
]
```

---

# 40. MultiIndex Recommendation

Understand MultiIndex.

Do not over-focus on advanced MultiIndex operations.

For most Data Analyst work:

```text
GroupBy
+
Multiple Columns
+
reset_index()
```

is more important.

---

# 41. Combining Orders, Customers, and Products

Load datasets:

```python
orders = pd.read_csv(
    "orders.csv"
)

customers = pd.read_csv(
    "customers.csv"
)

products = pd.read_csv(
    "products.csv"
)
```

Check:

```python
orders.info()
```

```python
customers.info()
```

```python
products.info()
```

---

# 42. Validate Keys Before Merge

Check Orders:

```python
orders[
    "order_id"
].is_unique
```

Check Customers:

```python
customers[
    "customer_id"
].is_unique
```

Check Products:

```python
products[
    "product_id"
].is_unique
```

---

# 43. Merge Business Datasets

```python
business_data = (
    orders

    .merge(
        customers,
        on="customer_id",
        how="left",
        validate="many_to_one"
    )

    .merge(
        products,
        on="product_id",
        how="left",
        validate="many_to_one"
    )
)
```

---

# 44. Validate Final Dataset

```python
business_data.shape
```

```python
business_data.head()
```

```python
business_data.info()
```

```python
business_data.isnull().sum()
```

```python
business_data.duplicated().sum()
```

---

# 45. Customer Lifetime Value

Customer Lifetime Value in a simplified historical analysis can be calculated as:

```text
Total Revenue Generated by Each Customer
```

Calculate:

```python
customer_clv = (
    business_data

    .groupby(
        [
            "customer_id",
            "customer_name"
        ]
    )

    .agg(

        customer_lifetime_value=(
            "sales",
            "sum"
        )

    )

    .reset_index()

    .sort_values(
        "customer_lifetime_value",
        ascending=False
    )
)
```

---

# 46. Important CLV Note

Do not blindly call total historical revenue "true CLV."

A more accurate description may be:

```text
Historical Customer Value
```

True predictive CLV may consider:

```text
Purchase Frequency

Average Order Value

Customer Lifespan

Retention

Churn

Future Expected Revenue

Profitability
```

For beginner Data Analyst projects, a simplified CLV calculation is acceptable if clearly defined.

---

# 47. Customer Order Count

Calculate:

```python
customer_orders = (
    business_data

    .groupby(
        "customer_id"
    )

    .agg(

        total_orders=(
            "order_id",
            "nunique"
        )

    )

    .reset_index()
)
```

Important:

```text
Use nunique()
```

when one order can contain multiple product rows.

Using:

```python
count()
```

may incorrectly count order lines instead of unique orders.

---

# 48. Identify Repeat Customers

```python
customer_orders[
    "repeat_customer"
] = (

    customer_orders[
        "total_orders"
    ]

    >

    1
)
```

---

# 49. Repeat Purchase Rate

Formula:

```text
Repeat Purchase Rate

=

Customers With More Than One Order
÷
Total Customers

×
100
```

Calculate:

```python
repeat_customers = (

    customer_orders[
        "repeat_customer"
    ]

    .sum()
)
```

```python
total_customers = (

    customer_orders[
        "customer_id"
    ]

    .nunique()
)
```

```python
repeat_purchase_rate = (

    repeat_customers

    /

    total_customers

    *

    100
)
```

---

# 50. Customer Performance Analysis

```python
customer_performance = (
    business_data

    .groupby(
        [
            "customer_id",
            "customer_name"
        ]
    )

    .agg(

        total_orders=(
            "order_id",
            "nunique"
        ),

        total_revenue=(
            "sales",
            "sum"
        ),

        average_order_value=(
            "sales",
            "mean"
        )

    )

    .reset_index()
)
```

Be careful:

```text
Mean Sales Per Row

Is Not Always

Average Order Value
```

If one order contains multiple rows, calculate order totals first.

---

# 51. Correct Average Order Value

First calculate order-level sales:

```python
order_values = (
    business_data

    .groupby(
        [
            "customer_id",
            "order_id"
        ]
    )["sales"]

    .sum()

    .reset_index()
)
```

Then calculate customer-level AOV:

```python
customer_aov = (
    order_values

    .groupby(
        "customer_id"
    )["sales"]

    .mean()

    .reset_index(
        name="average_order_value"
    )
)
```

This is more accurate.

---

# 52. Customer 360 Analysis

Create customer metrics:

```python
customer_summary = (
    business_data

    .groupby(
        [
            "customer_id",
            "customer_name",
            "region"
        ]
    )

    .agg(

        total_revenue=(
            "sales",
            "sum"
        ),

        total_orders=(
            "order_id",
            "nunique"
        ),

        products_purchased=(
            "product_id",
            "nunique"
        )

    )

    .reset_index()
)
```

This creates a basic:

```text
Customer 360 View
```

---

# 53. Regional Customer Analysis

```python
regional_customer_analysis = (
    business_data

    .groupby(
        "region"
    )

    .agg(

        total_customers=(
            "customer_id",
            "nunique"
        ),

        total_orders=(
            "order_id",
            "nunique"
        ),

        total_revenue=(
            "sales",
            "sum"
        )

    )

    .reset_index()
)
```

---

# 54. Product Performance Analysis

```python
product_performance = (
    business_data

    .groupby(
        [
            "product_id",
            "product_name",
            "category"
        ]
    )

    .agg(

        total_quantity=(
            "quantity",
            "sum"
        ),

        total_revenue=(
            "sales",
            "sum"
        ),

        unique_customers=(
            "customer_id",
            "nunique"
        )

    )

    .reset_index()

    .sort_values(
        "total_revenue",
        ascending=False
    )
)
```

---

# 55. Cross-Functional Business Analysis

Combining datasets allows you to answer questions involving multiple business areas.

Example:

```text
Customer Data
+
Order Data
+
Product Data
```

Questions:

```text
Which customer segments generate the most revenue?

Which products are popular in each region?

Which customers make repeat purchases?

Which products generate revenue but attract few customers?

Which regions have high customer counts but low revenue?

Who are the highest-value customers?

Which categories perform best among repeat customers?
```

---

# 56. Revenue by Customer Segment

```python
segment_revenue = (
    business_data

    .groupby(
        "segment"
    )

    .agg(

        total_revenue=(
            "sales",
            "sum"
        ),

        unique_customers=(
            "customer_id",
            "nunique"
        )

    )

    .reset_index()

    .sort_values(
        "total_revenue",
        ascending=False
    )
)
```

---

# 57. Product Performance by Region

```python
regional_product_performance = (
    business_data

    .groupby(
        [
            "region",
            "product_name"
        ]
    )

    .agg(

        total_revenue=(
            "sales",
            "sum"
        ),

        total_quantity=(
            "quantity",
            "sum"
        )

    )

    .reset_index()
)
```

---

# 58. Top Product in Each Region

First aggregate:

```python
regional_products = (
    business_data

    .groupby(
        [
            "region",
            "product_name"
        ]
    )["sales"]

    .sum()

    .reset_index()
)
```

Rank:

```python
regional_products[
    "rank"
] = (

    regional_products

    .groupby(
        "region"
    )["sales"]

    .rank(
        method="dense",
        ascending=False
    )
)
```

Filter:

```python
top_products = (

    regional_products[

        regional_products[
            "rank"
        ]

        ==

        1

    ]

)
```

---

# 59. Repeat Customer Revenue

Create customer order counts:

```python
customer_order_counts = (
    business_data

    .groupby(
        "customer_id"
    )["order_id"]

    .nunique()

    .reset_index(
        name="total_orders"
    )
)
```

Merge:

```python
business_data = (
    business_data

    .merge(
        customer_order_counts,
        on="customer_id",
        how="left"
    )
)
```

Create customer type:

```python
business_data[
    "customer_type"
] = (

    business_data[
        "total_orders"
    ]

    .apply(

        lambda x:

        "Repeat Customer"

        if x > 1

        else "One-Time Customer"

    )
)
```

Analyze:

```python
customer_type_analysis = (
    business_data

    .groupby(
        "customer_type"
    )

    .agg(

        total_revenue=(
            "sales",
            "sum"
        ),

        unique_customers=(
            "customer_id",
            "nunique"
        )

    )

    .reset_index()
)
```

---

# 60. Complete Business Analysis Workflow

```python
import pandas as pd


# LOAD DATA

orders = pd.read_csv(
    "orders.csv"
)

customers = pd.read_csv(
    "customers.csv"
)

products = pd.read_csv(
    "products.csv"
)


# VALIDATE KEYS

print(
    customers[
        "customer_id"
    ].is_unique
)

print(
    products[
        "product_id"
    ].is_unique
)


# MERGE DATA

business_data = (
    orders

    .merge(
        customers,
        on="customer_id",
        how="left",
        validate="many_to_one"
    )

    .merge(
        products,
        on="product_id",
        how="left",
        validate="many_to_one"
    )
)


# VALIDATE MERGE

print(
    business_data.shape
)

print(
    business_data.isnull().sum()
)


# CUSTOMER ANALYSIS

customer_analysis = (
    business_data

    .groupby(
        [
            "customer_id",
            "customer_name"
        ]
    )

    .agg(

        total_orders=(
            "order_id",
            "nunique"
        ),

        total_revenue=(
            "sales",
            "sum"
        ),

        unique_products=(
            "product_id",
            "nunique"
        )

    )

    .reset_index()
)


# REPEAT CUSTOMERS

customer_analysis[
    "customer_type"
] = (

    customer_analysis[
        "total_orders"
    ]

    .apply(

        lambda x:

        "Repeat Customer"

        if x > 1

        else "One-Time Customer"

    )
)


# REPEAT PURCHASE RATE

repeat_purchase_rate = (

    customer_analysis[
        "total_orders"
    ]

    .gt(1)

    .mean()

    *

    100
)


# REGIONAL ANALYSIS

regional_analysis = (
    business_data

    .groupby(
        "region"
    )

    .agg(

        total_revenue=(
            "sales",
            "sum"
        ),

        total_orders=(
            "order_id",
            "nunique"
        ),

        total_customers=(
            "customer_id",
            "nunique"
        )

    )

    .reset_index()

    .sort_values(
        "total_revenue",
        ascending=False
    )
)


# PRODUCT ANALYSIS

product_analysis = (
    business_data

    .groupby(
        [
            "product_id",
            "product_name"
        ]
    )

    .agg(

        total_revenue=(
            "sales",
            "sum"
        ),

        total_quantity=(
            "quantity",
            "sum"
        ),

        unique_customers=(
            "customer_id",
            "nunique"
        )

    )

    .reset_index()

    .sort_values(
        "total_revenue",
        ascending=False
    )
)


# RESULTS

print(
    customer_analysis.head()
)

print(
    repeat_purchase_rate
)

print(
    regional_analysis
)

print(
    product_analysis.head()
)
```

---

# 61. Common Beginner Errors

## Blindly Merging Data

Wrong:

```python
df = orders.merge(
    customers
)
```

Better:

```python
df = orders.merge(
    customers,
    on="customer_id",
    how="left",
    validate="many_to_one"
)
```

---

## Not Checking Row Counts

Always compare:

```python
orders.shape
```

Before and after merging.

Unexpected row increases may indicate:

```text
Duplicate Keys

Many-to-Many Relationships

Incorrect Merge Logic
```

---

## Using count() Instead of nunique()

Wrong:

```python
df.groupby(
    "customer_id"
)["order_id"].count()
```

when one order contains multiple rows.

Better:

```python
df.groupby(
    "customer_id"
)["order_id"].nunique()
```

---

## Using apply() for Simple Calculations

Wrong:

```python
df["profit"] = df.apply(
    lambda row:
    row["sales"] - row["cost"],
    axis=1
)
```

Better:

```python
df["profit"] = (
    df["sales"]
    -
    df["cost"]
)
```

---

## Confusing merge() and concat()

Remember:

```text
merge()
→ Common Keys

concat()
→ Stack Similar DataFrames
```

---

## Calling Revenue True CLV

Historical customer revenue is not automatically predictive Customer Lifetime Value.

Define your metric clearly.

---

## Ignoring Data Granularity

Always know:

```text
What Does One Row Represent?
```

Possible answers:

```text
One Customer

One Order

One Order Line

One Product

One Transaction
```

Many analysis mistakes happen because the analyst ignores data granularity.

---

# 62. Interview Questions

1. What is `merge()` in Pandas?
2. What is the difference between Inner, Left, Right, and Outer Joins?
3. What is the difference between `merge()` and `join()`?
4. What is the difference between `merge()` and `concat()`?
5. When would you use `concat()`?
6. What does `ignore_index=True` do?
7. How do you merge DataFrames using different column names?
8. How do you merge more than two DataFrames?
9. Why should you validate a merge?
10. What does `indicator=True` do?
11. How do you identify unmatched records?
12. What problems can duplicate keys cause?
13. What does the `validate` parameter do?
14. Explain one-to-one and one-to-many relationships.
15. What is `apply()`?
16. What is `map()`?
17. What is `transform()`?
18. What is the difference between `apply()` and `map()`?
19. What is the difference between GroupBy aggregation and `transform()`?
20. Why should vectorized operations be preferred over `apply()`?
21. What is MultiIndex?
22. How do you create a MultiIndex?
23. What does `reset_index()` do?
24. How would you combine Orders, Customers, and Products?
25. What should you check before merging business datasets?
26. What should you check after merging datasets?
27. How would you calculate customer historical value?
28. What is Customer Lifetime Value?
29. Why is total historical revenue not necessarily true predictive CLV?
30. How would you calculate Repeat Purchase Rate?
31. Why is `nunique()` important when calculating order counts?
32. How would you calculate Average Order Value correctly?
33. What is a Customer 360 view?
34. How would you identify repeat customers?
35. How would you calculate revenue by customer segment?
36. How would you identify the top product in each region?
37. What does data granularity mean?
38. Why is understanding data granularity important?
39. How can incorrect merges produce incorrect business insights?
40. How would you combine multiple business datasets to answer cross-functional questions?

---

# 63. Completion Checklist

Before moving to SQL & Excel Integration, you should be able to:

- [ ] Use `merge()`
- [ ] Perform Inner Joins
- [ ] Perform Left Joins
- [ ] Perform Right Joins
- [ ] Perform Outer Joins
- [ ] Merge using different column names
- [ ] Merge multiple DataFrames
- [ ] Use method chaining for merges
- [ ] Check duplicate keys
- [ ] Understand table relationships
- [ ] Validate merge relationships
- [ ] Use `indicator=True`
- [ ] Find unmatched records
- [ ] Validate row counts after merging
- [ ] Use `join()`
- [ ] Explain `merge()` vs `join()`
- [ ] Use `concat()`
- [ ] Concatenate DataFrames vertically
- [ ] Concatenate DataFrames horizontally
- [ ] Explain `merge()` vs `concat()`
- [ ] Use `apply()`
- [ ] Use lambda functions
- [ ] Apply functions across rows
- [ ] Prefer vectorized operations when possible
- [ ] Use `map()`
- [ ] Use `transform()`
- [ ] Explain aggregation vs `transform()`
- [ ] Understand MultiIndex basics
- [ ] Use `reset_index()`
- [ ] Combine Orders, Customers, and Products
- [ ] Validate combined business datasets
- [ ] Calculate historical customer value
- [ ] Explain the limitations of simplified CLV
- [ ] Calculate unique customer orders
- [ ] Identify repeat customers
- [ ] Calculate Repeat Purchase Rate
- [ ] Calculate Average Order Value correctly
- [ ] Create a Customer 360 analysis
- [ ] Analyze regional performance
- [ ] Analyze product performance
- [ ] Analyze customer segment revenue
- [ ] Identify top products by region
- [ ] Analyze repeat customer revenue
- [ ] Answer cross-functional business questions
- [ ] Understand data granularity
- [ ] Avoid incorrect merge logic
- [ ] Convert analysis results into business insights

---

# Final Outcome

After completing Advanced Pandas, you should be able to combine multiple business datasets using `merge()`, `join()`, and `concat()`; transform data using `apply()`, `map()`, and `transform()`; understand MultiIndex basics; validate dataset relationships and merge results; combine Orders, Customers, and Products; calculate customer metrics such as historical customer value, Repeat Purchase Rate, and Average Order Value; create Customer 360 analysis; and answer cross-functional business questions using Pandas.

The goal is:

```text
Orders
+
Customers
+
Products
        ↓
Validate Relationships
        ↓
Merge Data
        ↓
Transform Data
        ↓
Analyze Customers
        ↓
Analyze Products
        ↓
Analyze Regions
        ↓
Calculate Business KPIs
        ↓
Generate Cross-Functional Insights
        ↓
Support Business Decisions
```