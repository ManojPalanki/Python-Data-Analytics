# Data Analysis with Pandas

## 1. Introduction

Data Analysis with Pandas is the process of transforming cleaned data into useful business information.

At this stage, the dataset should already be:

- Loaded
- Inspected
- Cleaned
- Correctly formatted
- Validated

The next goal is:

```text
Clean Data
    ↓
Filter Relevant Records
    ↓
Sort Results
    ↓
Create Calculated Columns
    ↓
Group Business Data
    ↓
Calculate Aggregations
    ↓
Create Pivot Tables
    ↓
Compare Business Segments
    ↓
Identify Opportunities
    ↓
Identify Underperforming Areas
    ↓
Generate Management Reports
```

The most important topics are:

- Column Selection
- Row Filtering
- `loc[]`
- `iloc[]`
- Sorting
- `query()`
- Calculated Columns
- `groupby()`
- Aggregations
- Named Aggregations
- Pivot Tables
- Crosstab
- Top-N Analysis
- Bottom-N Analysis
- Business KPI Analysis
- Management Reporting

---

# 2. Import Pandas

```python
import pandas as pd
```

Load cleaned data:

```python
df = pd.read_csv(
    "cleaned_sales_data.csv"
)
```

Inspect:

```python
df.head()
```

```python
df.info()
```

```python
df.shape
```

---

# 3. Basic Data Analysis Workflow

A practical workflow is:

```text
1. Understand Business Question

2. Select Required Columns

3. Filter Relevant Records

4. Sort Results

5. Create Calculated Columns

6. Group Data

7. Calculate KPIs

8. Compare Categories

9. Identify Top Performers

10. Identify Underperformers

11. Create Summary Tables

12. Generate Business Insights

13. Prepare Management Report
```

The most important point is:

```text
Do Not Analyze Data Without a Business Question
```

---

# 4. Selecting a Single Column

```python
df["sales"]
```

This returns a:

```text
Series
```

Store:

```python
sales = df["sales"]
```

---

# 5. Selecting Multiple Columns

```python
df[
    [
        "product_name",
        "sales",
        "profit"
    ]
]
```

This returns a:

```text
DataFrame
```

---

# 6. Select Columns for Business Analysis

```python
sales_analysis = df[
    [
        "order_id",
        "product_name",
        "category",
        "region",
        "sales",
        "profit"
    ]
]
```

Selecting only required columns can make analysis easier to understand.

---

# 7. Filtering Rows

Filter sales above ₹100,000:

```python
high_sales = df[
    df["sales"] > 100000
]
```

---

# 8. Filter Using Equal Condition

```python
south_sales = df[
    df["region"] == "South"
]
```

---

# 9. Filter Using Not Equal

```python
non_south_sales = df[
    df["region"] != "South"
]
```

---

# 10. Multiple Conditions with AND

Use:

```python
&
```

Example:

```python
high_profit_south = df[
    (df["region"] == "South")
    &
    (df["profit"] > 50000)
]
```

Always use parentheses around conditions.

---

# 11. Multiple Conditions with OR

Use:

```python
|
```

Example:

```python
selected_regions = df[
    (df["region"] == "South")
    |
    (df["region"] == "West")
]
```

---

# 12. isin()

Use `isin()` when checking multiple values.

Instead of:

```python
df[
    (df["region"] == "South")
    |
    (df["region"] == "West")
]
```

Use:

```python
df[
    df["region"].isin(
        [
            "South",
            "West"
        ]
    )
]
```

---

# 13. between()

Filter a numerical range:

```python
df[
    df["sales"].between(
        50000,
        100000
    )
]
```

Equivalent logic:

```text
Sales >= 50000

AND

Sales <= 100000
```

---

# 14. Filter Missing Values

Rows with missing profit:

```python
df[
    df["profit"].isna()
]
```

Rows without missing profit:

```python
df[
    df["profit"].notna()
]
```

---

# 15. loc[]

`loc[]` selects rows and columns using labels and conditions.

Syntax:

```python
df.loc[
    row_condition,
    column_selection
]
```

Example:

```python
df.loc[
    df["sales"] > 100000,
    [
        "product_name",
        "sales",
        "profit"
    ]
]
```

---

# 16. Why loc[] Is Useful

Instead of:

```python
df[
    df["sales"] > 100000
][
    [
        "product_name",
        "sales",
        "profit"
    ]
]
```

Use:

```python
df.loc[
    df["sales"] > 100000,
    [
        "product_name",
        "sales",
        "profit"
    ]
]
```

This is usually clearer.

---

# 17. iloc[]

`iloc[]` selects data using integer positions.

First row:

```python
df.iloc[0]
```

First five rows:

```python
df.iloc[0:5]
```

First five rows and first three columns:

```python
df.iloc[
    0:5,
    0:3
]
```

Remember:

```text
loc
→ Labels and Conditions

iloc
→ Integer Positions
```

---

# 18. Sorting Data

Use:

```python
sort_values()
```

Sort sales from lowest to highest:

```python
df.sort_values(
    by="sales"
)
```

---

# 19. Sort Descending

```python
df.sort_values(
    by="sales",
    ascending=False
)
```

This is useful for identifying top-performing records.

---

# 20. Sort Multiple Columns

```python
df.sort_values(
    by=[
        "region",
        "sales"
    ],
    ascending=[
        True,
        False
    ]
)
```

Meaning:

```text
Region
→ Ascending

Sales
→ Descending
```

---

# 21. nlargest()

Find the highest values:

```python
df.nlargest(
    10,
    "sales"
)
```

This returns the 10 records with the highest sales.

---

# 22. nsmallest()

Find the lowest values:

```python
df.nsmallest(
    10,
    "profit"
)
```

This can help identify least profitable or highest-loss records.

---

# 23. query()

`query()` provides another way to filter data.

Example:

```python
df.query(
    "sales > 100000"
)
```

---

# 24. query() with Multiple Conditions

```python
df.query(
    "sales > 100000 and profit > 20000"
)
```

Filter category:

```python
df.query(
    "category == 'Technology'"
)
```

---

# 25. Boolean Filtering vs query()

Boolean filtering:

```python
df[
    (df["sales"] > 100000)
    &
    (df["profit"] > 20000)
]
```

Using `query()`:

```python
df.query(
    "sales > 100000 and profit > 20000"
)
```

Both are valid.

For Data Analyst work, understand both.

---

# 26. Creating Calculated Columns

Suppose the dataset contains:

```text
Sales

Profit
```

Create Profit Margin:

```python
df["profit_margin"] = (
    df["profit"]
    /
    df["sales"]
) * 100
```

---

# 27. Calculate Cost

If:

```text
Profit = Sales - Cost
```

Then:

```text
Cost = Sales - Profit
```

Create:

```python
df["cost"] = (
    df["sales"]
    -
    df["profit"]
)
```

---

# 28. Calculate Average Selling Price

Suppose the dataset contains quantity.

```python
df["average_selling_price"] = (
    df["sales"]
    /
    df["quantity"]
)
```

Always check for zero quantities before division.

---

# 29. GroupBy

`groupby()` is one of the most important Pandas methods for Data Analysts.

It follows the concept:

```text
Split
    ↓
Apply
    ↓
Combine
```

Example:

```python
df.groupby(
    "region"
)["sales"].sum()
```

This calculates total sales by region.

---

# 30. GroupBy Concept

Suppose:

```text
Region    Sales

South     100

North     200

South     300

North     400
```

Group by region:

```text
South
→ 100 + 300
→ 400

North
→ 200 + 400
→ 600
```

---

# 31. Sales by Region

```python
sales_by_region = (
    df.groupby(
        "region"
    )["sales"]
    .sum()
)
```

Display:

```python
print(sales_by_region)
```

---

# 32. Sales by Category

```python
sales_by_category = (
    df.groupby(
        "category"
    )["sales"]
    .sum()
)
```

---

# 33. Profit by Region

```python
profit_by_region = (
    df.groupby(
        "region"
    )["profit"]
    .sum()
)
```

---

# 34. Average Sales by Segment

```python
average_sales_by_segment = (
    df.groupby(
        "segment"
    )["sales"]
    .mean()
)
```

---

# 35. GroupBy Multiple Columns

```python
sales_by_region_category = (
    df.groupby(
        [
            "region",
            "category"
        ]
    )["sales"]
    .sum()
)
```

This answers:

```text
How much sales did each category generate within each region?
```

---

# 36. reset_index()

A grouped result may use group columns as an index.

Example:

```python
sales_by_region = (
    df.groupby(
        "region"
    )["sales"]
    .sum()
    .reset_index()
)
```

Result:

```text
Region     Sales

South      850000

North      920000

East       780000
```

This is easier to use for further analysis.

---

# 37. Basic Aggregation Functions

Important aggregation functions:

```text
sum()

mean()

median()

min()

max()

count()

nunique()
```

---

# 38. Multiple Aggregations

Use:

```python
agg()
```

Example:

```python
region_analysis = (
    df.groupby(
        "region"
    )["sales"]
    .agg(
        [
            "sum",
            "mean",
            "min",
            "max"
        ]
    )
)
```

---

# 39. Aggregate Multiple Columns

```python
business_summary = (
    df.groupby(
        "region"
    )
    .agg({
        "sales": "sum",

        "profit": "sum",

        "order_id": "nunique",

        "customer_id": "nunique"
    })
)
```

This calculates:

```text
Total Sales

Total Profit

Unique Orders

Unique Customers
```

for every region.

---

# 40. Named Aggregations

Named aggregations produce cleaner column names.

```python
regional_summary = (
    df.groupby(
        "region"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
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
)
```

This is one of the most useful patterns for Data Analyst work.

---

# 41. Add Profit Margin to Grouped Analysis

Do not calculate overall Profit Margin using:

```python
df["profit_margin"].mean()
```

if the business question asks for total business Profit Margin.

Correct:

```python
regional_summary[
    "profit_margin"
] = (
    regional_summary[
        "total_profit"
    ]
    /
    regional_summary[
        "total_sales"
    ]
) * 100
```

This is:

```text
Total Profit
÷
Total Sales
×
100
```

---

# 42. Important Aggregation Warning

These two calculations are not necessarily equal:

```python
df["profit_margin"].mean()
```

and:

```python
(
    df["profit"].sum()
    /
    df["sales"].sum()
) * 100
```

For overall business Profit Margin, the second calculation is generally the correct KPI.

Do not blindly average percentages.

---

# 43. count() vs size()

`count()` counts non-missing values.

```python
df.groupby(
    "region"
)["sales"].count()
```

`size()` counts rows.

```python
df.groupby(
    "region"
).size()
```

Difference:

```text
count()
→ Ignores Missing Values

size()
→ Counts Rows
```

---

# 44. Number of Unique Orders

```python
total_orders = (
    df["order_id"]
    .nunique()
)
```

By region:

```python
orders_by_region = (
    df.groupby(
        "region"
    )["order_id"]
    .nunique()
)
```

---

# 45. Number of Unique Customers

```python
unique_customers = (
    df["customer_id"]
    .nunique()
)
```

By segment:

```python
customers_by_segment = (
    df.groupby(
        "segment"
    )["customer_id"]
    .nunique()
)
```

---

# 46. Pivot Tables

Pivot tables summarize business data across multiple dimensions.

Use:

```python
pd.pivot_table()
```

Example:

```python
sales_pivot = pd.pivot_table(
    df,
    values="sales",
    index="region",
    columns="category",
    aggfunc="sum"
)
```

---

# 47. Understanding Pivot Tables

Input:

```text
Region    Category      Sales

South     Technology    500

South     Furniture     300

North     Technology    700

North     Furniture     400
```

Pivot result:

```text
Category     Furniture    Technology

North        400          700

South        300          500
```

---

# 48. Pivot Table with fill_value

Missing combinations may create:

```text
NaN
```

Use:

```python
sales_pivot = pd.pivot_table(
    df,
    values="sales",
    index="region",
    columns="category",
    aggfunc="sum",
    fill_value=0
)
```

---

# 49. Pivot Table with Multiple Values

```python
business_pivot = pd.pivot_table(
    df,
    values=[
        "sales",
        "profit"
    ],
    index="region",
    columns="category",
    aggfunc="sum",
    fill_value=0
)
```

---

# 50. Pivot Table with Multiple Aggregations

```python
sales_pivot = pd.pivot_table(
    df,
    values="sales",
    index="region",
    columns="category",
    aggfunc=[
        "sum",
        "mean"
    ],
    fill_value=0
)
```

---

# 51. Pivot Table with Margins

```python
sales_pivot = pd.pivot_table(
    df,
    values="sales",
    index="region",
    columns="category",
    aggfunc="sum",
    fill_value=0,
    margins=True
)
```

This adds totals.

---

# 52. Crosstab

`crosstab()` creates frequency tables.

Example:

```python
pd.crosstab(
    df["region"],
    df["segment"]
)
```

This counts how many records exist for every Region and Segment combination.

---

# 53. Crosstab with Totals

```python
pd.crosstab(
    df["region"],
    df["segment"],
    margins=True
)
```

---

# 54. Crosstab with Percentages

Row percentages:

```python
pd.crosstab(
    df["region"],
    df["segment"],
    normalize="index"
) * 100
```

Column percentages:

```python
pd.crosstab(
    df["region"],
    df["segment"],
    normalize="columns"
) * 100
```

Overall percentages:

```python
pd.crosstab(
    df["region"],
    df["segment"],
    normalize=True
) * 100
```

---

# 55. Pivot Table vs Crosstab

| Pivot Table | Crosstab |
|---|---|
| Summarizes numerical values | Mainly creates frequency tables |
| Uses `values` | Counts combinations by default |
| Supports aggregations | Useful for categorical comparisons |
| Example: Sales by Region | Example: Orders by Region and Segment |

---

# 56. Analyze Top-Selling Products

Business question:

```text
Which products generate the highest sales?
```

Analysis:

```python
top_products = (
    df.groupby(
        "product_name"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        ),

        total_quantity=(
            "quantity",
            "sum"
        )
    )
    .reset_index()
    .sort_values(
        by="total_sales",
        ascending=False
    )
    .head(10)
)
```

Display:

```python
print(top_products)
```

---

# 57. Analyze Least Profitable Products

Business question:

```text
Which products are generating the lowest profits or highest losses?
```

```python
least_profitable_products = (
    df.groupby(
        "product_name"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        )
    )
    .reset_index()
    .sort_values(
        by="total_profit"
    )
    .head(10)
)
```

---

# 58. Important Business Interpretation

A product can have:

```text
High Sales

But

Low Profit
```

This may indicate:

- Excessive discounting
- High costs
- Poor pricing
- Low-margin products

Do not analyze sales alone.

Always compare:

```text
Sales

Profit

Profit Margin
```

---

# 59. Analyze Sales by Region

```python
regional_performance = (
    df.groupby(
        "region"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
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
)
```

Add Profit Margin:

```python
regional_performance[
    "profit_margin"
] = (
    regional_performance[
        "total_profit"
    ]
    /
    regional_performance[
        "total_sales"
    ]
) * 100
```

Sort:

```python
regional_performance = (
    regional_performance
    .sort_values(
        by="total_sales",
        ascending=False
    )
)
```

---

# 60. Analyze Customer Segments

```python
segment_performance = (
    df.groupby(
        "segment"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
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
)
```

---

# 61. Calculate Average Order Value

Calculate total business AOV:

```python
total_sales = (
    df["sales"].sum()
)

total_orders = (
    df["order_id"].nunique()
)

average_order_value = (
    total_sales
    /
    total_orders
)
```

Formula:

```text
Average Order Value

=

Total Sales
÷
Unique Orders
```

---

# 62. Calculate AOV by Region

First create grouped summary:

```python
regional_summary = (
    df.groupby(
        "region"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_orders=(
            "order_id",
            "nunique"
        )
    )
    .reset_index()
)
```

Calculate:

```python
regional_summary[
    "average_order_value"
] = (
    regional_summary[
        "total_sales"
    ]
    /
    regional_summary[
        "total_orders"
    ]
)
```

---

# 63. Analyze Category Performance

```python
category_performance = (
    df.groupby(
        "category"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        ),

        total_quantity=(
            "quantity",
            "sum"
        ),

        total_orders=(
            "order_id",
            "nunique"
        )
    )
    .reset_index()
)
```

Add Profit Margin:

```python
category_performance[
    "profit_margin"
] = (
    category_performance[
        "total_profit"
    ]
    /
    category_performance[
        "total_sales"
    ]
) * 100
```

---

# 64. Analyze Sub-Category Performance

```python
subcategory_performance = (
    df.groupby(
        "sub_category"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        )
    )
    .reset_index()
)
```

Add Profit Margin:

```python
subcategory_performance[
    "profit_margin"
] = (
    subcategory_performance[
        "total_profit"
    ]
    /
    subcategory_performance[
        "total_sales"
    ]
) * 100
```

Sort:

```python
subcategory_performance = (
    subcategory_performance
    .sort_values(
        by="total_profit"
    )
)
```

---

# 65. Identify Loss-Making Products

```python
product_performance = (
    df.groupby(
        "product_name"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        )
    )
    .reset_index()
)
```

Filter:

```python
loss_making_products = (
    product_performance[
        product_performance[
            "total_profit"
        ] < 0
    ]
)
```

Sort:

```python
loss_making_products = (
    loss_making_products
    .sort_values(
        by="total_profit"
    )
)
```

---

# 66. Analyze Discount Impact

```python
discount_analysis = (
    df.groupby(
        "discount"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        ),

        total_orders=(
            "order_id",
            "nunique"
        )
    )
    .reset_index()
)
```

This can help investigate:

```text
Are higher discounts associated with lower profitability?
```

Do not automatically claim causation.

This analysis shows association, not necessarily cause.

---

# 67. Analyze Monthly Sales

Ensure date type:

```python
df["order_date"] = (
    pd.to_datetime(
        df["order_date"]
    )
)
```

Create month:

```python
df["order_month"] = (
    df["order_date"]
    .dt.to_period("M")
)
```

Analyze:

```python
monthly_sales = (
    df.groupby(
        "order_month"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        )
    )
    .reset_index()
)
```

---

# 68. Analyze Yearly Sales

Create year:

```python
df["order_year"] = (
    df["order_date"]
    .dt.year
)
```

Analyze:

```python
yearly_performance = (
    df.groupby(
        "order_year"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        )
    )
    .reset_index()
)
```

---

# 69. Management KPI Summary

```python
total_sales = (
    df["sales"].sum()
)

total_profit = (
    df["profit"].sum()
)

total_orders = (
    df["order_id"].nunique()
)

total_customers = (
    df["customer_id"].nunique()
)

total_products = (
    df["product_id"].nunique()
)
```

Profit Margin:

```python
profit_margin = (
    total_profit
    /
    total_sales
) * 100
```

Average Order Value:

```python
average_order_value = (
    total_sales
    /
    total_orders
)
```

---

# 70. Display Management KPIs

```python
print("=" * 60)

print("MANAGEMENT KPI SUMMARY")

print("=" * 60)

print(
    f"Total Sales: ₹{total_sales:,.2f}"
)

print(
    f"Total Profit: ₹{total_profit:,.2f}"
)

print(
    f"Profit Margin: {profit_margin:.2f}%"
)

print(
    f"Total Orders: {total_orders:,}"
)

print(
    f"Total Customers: {total_customers:,}"
)

print(
    f"Total Products: {total_products:,}"
)

print(
    f"Average Order Value: ₹{average_order_value:,.2f}"
)

print("=" * 60)
```

---

# 71. Management Report — Regional Performance

```python
regional_report = (
    df.groupby(
        "region"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
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
)
```

Add KPIs:

```python
regional_report[
    "profit_margin"
] = (
    regional_report[
        "total_profit"
    ]
    /
    regional_report[
        "total_sales"
    ]
) * 100
```

```python
regional_report[
    "average_order_value"
] = (
    regional_report[
        "total_sales"
    ]
    /
    regional_report[
        "total_orders"
    ]
)
```

Sort:

```python
regional_report = (
    regional_report
    .sort_values(
        by="total_sales",
        ascending=False
    )
)
```

---

# 72. Management Report — Product Performance

```python
product_report = (
    df.groupby(
        "product_name"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
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

Add Profit Margin:

```python
product_report[
    "profit_margin"
] = (
    product_report[
        "total_profit"
    ]
    /
    product_report[
        "total_sales"
    ]
) * 100
```

---

# 73. Identify Business Opportunities

Business opportunities may include:

```text
High-Sales Products with Strong Profit Margin

High-Profit Regions

High-Value Customer Segments

Growing Categories

Products with Strong Demand

Regions with High Average Order Value
```

Example:

```python
opportunities = (
    product_report[
        (
            product_report[
                "total_sales"
            ]
            >
            product_report[
                "total_sales"
            ].median()
        )
        &
        (
            product_report[
                "profit_margin"
            ] > 20
        )
    ]
)
```

---

# 74. Identify Underperforming Areas

Underperforming areas may include:

```text
Loss-Making Products

Low-Profit Regions

High-Sales but Low-Margin Categories

Products with Excessive Discounts

Segments with Weak Profitability

Regions with Low Average Order Value
```

Example:

```python
underperforming_products = (
    product_report[
        product_report[
            "total_profit"
        ] < 0
    ]
    .sort_values(
        by="total_profit"
    )
)
```

---

# 75. Business Insight Structure

Do not write:

```text
West has the highest sales.
```

That is only an observation.

A better structure is:

```text
Finding
    ↓
Business Meaning
    ↓
Possible Cause
    ↓
Recommended Action
```

Example:

```text
Finding:

The West region generates the highest sales but has a lower Profit Margin than the South region.

Business Meaning:

Strong revenue is not translating into equally strong profitability.

Possible Cause:

High discounting, expensive product mix, or higher operational costs.

Recommended Action:

Investigate discount levels and product-level profitability within the West region.
```

---

# 76. Observation vs Insight

## Observation

```text
Technology generated ₹5 million in sales.
```

## Insight

```text
Technology generated the highest sales, but its Profit Margin is below Furniture, suggesting that revenue growth is not producing proportional profitability.
```

## Recommendation

```text
Review Technology discounting and prioritize high-margin Technology products.
```

Your goal is not just:

```text
Calculate Numbers
```

Your goal is:

```text
Calculate
    ↓
Compare
    ↓
Interpret
    ↓
Recommend
```

---

# 77. Complete Business Analysis Workflow

```python
import pandas as pd


# LOAD CLEAN DATA

df = pd.read_csv(
    "cleaned_sales_data.csv"
)


# CONVERT DATE

df["order_date"] = (
    pd.to_datetime(
        df["order_date"]
    )
)


# CALCULATE OVERALL KPIs

total_sales = (
    df["sales"].sum()
)

total_profit = (
    df["profit"].sum()
)

total_orders = (
    df["order_id"].nunique()
)

total_customers = (
    df["customer_id"].nunique()
)

profit_margin = (
    total_profit
    /
    total_sales
) * 100

average_order_value = (
    total_sales
    /
    total_orders
)


# REGIONAL ANALYSIS

regional_performance = (
    df.groupby(
        "region"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
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
)


regional_performance[
    "profit_margin"
] = (
    regional_performance[
        "total_profit"
    ]
    /
    regional_performance[
        "total_sales"
    ]
) * 100


regional_performance[
    "average_order_value"
] = (
    regional_performance[
        "total_sales"
    ]
    /
    regional_performance[
        "total_orders"
    ]
)


# PRODUCT ANALYSIS

product_performance = (
    df.groupby(
        "product_name"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        ),

        total_quantity=(
            "quantity",
            "sum"
        )
    )
    .reset_index()
)


product_performance[
    "profit_margin"
] = (
    product_performance[
        "total_profit"
    ]
    /
    product_performance[
        "total_sales"
    ]
) * 100


# TOP PRODUCTS

top_products = (
    product_performance
    .sort_values(
        by="total_sales",
        ascending=False
    )
    .head(10)
)


# LEAST PROFITABLE PRODUCTS

least_profitable_products = (
    product_performance
    .sort_values(
        by="total_profit"
    )
    .head(10)
)


# SEGMENT ANALYSIS

segment_performance = (
    df.groupby(
        "segment"
    )
    .agg(
        total_sales=(
            "sales",
            "sum"
        ),

        total_profit=(
            "profit",
            "sum"
        ),

        total_orders=(
            "order_id",
            "nunique"
        )
    )
    .reset_index()
)


# MANAGEMENT SUMMARY

print("=" * 60)

print("MANAGEMENT KPI SUMMARY")

print("=" * 60)

print(
    f"Total Sales: ₹{total_sales:,.2f}"
)

print(
    f"Total Profit: ₹{total_profit:,.2f}"
)

print(
    f"Profit Margin: {profit_margin:.2f}%"
)

print(
    f"Total Orders: {total_orders:,}"
)

print(
    f"Total Customers: {total_customers:,}"
)

print(
    f"Average Order Value: ₹{average_order_value:,.2f}"
)

print("=" * 60)


print("\nREGIONAL PERFORMANCE")

print(regional_performance)


print("\nTOP-SELLING PRODUCTS")

print(top_products)


print("\nLEAST PROFITABLE PRODUCTS")

print(least_profitable_products)


print("\nCUSTOMER SEGMENT PERFORMANCE")

print(segment_performance)
```

---

# 78. Export Management Reports

Create output folder:

```python
from pathlib import Path


output_folder = Path(
    "management_reports"
)


output_folder.mkdir(
    exist_ok=True
)
```

Export regional report:

```python
regional_performance.to_csv(
    output_folder
    /
    "regional_performance.csv",
    index=False
)
```

Export top products:

```python
top_products.to_csv(
    output_folder
    /
    "top_products.csv",
    index=False
)
```

Export least profitable products:

```python
least_profitable_products.to_csv(
    output_folder
    /
    "least_profitable_products.csv",
    index=False
)
```

Export segment performance:

```python
segment_performance.to_csv(
    output_folder
    /
    "segment_performance.csv",
    index=False
)
```

---

# 79. Most Important Pandas Analysis Methods

| Method | Purpose |
|---|---|
| Column Selection | Select required variables |
| Boolean Filtering | Filter records |
| `isin()` | Filter multiple categories |
| `between()` | Filter numerical ranges |
| `loc[]` | Select using labels and conditions |
| `iloc[]` | Select using positions |
| `sort_values()` | Sort data |
| `nlargest()` | Find highest values |
| `nsmallest()` | Find lowest values |
| `query()` | Filter using expressions |
| `groupby()` | Group business data |
| `agg()` | Calculate multiple aggregations |
| `reset_index()` | Convert grouped index to columns |
| `nunique()` | Count unique values |
| `pivot_table()` | Create summary tables |
| `crosstab()` | Compare categorical frequencies |

---

# 80. What You Should Prioritize

For a Data Analyst role, master:

```text
Filtering

Multiple Conditions

isin()

between()

loc[]

Sorting

query()

Calculated Columns

groupby()

sum()

mean()

count()

nunique()

agg()

Named Aggregations

reset_index()

Pivot Tables

Crosstab

Top-N Analysis

Bottom-N Analysis

Profit Margin

Average Order Value

Regional Analysis

Product Analysis

Customer Segment Analysis

Management Reporting

Business Insights
```

Do not waste time memorizing every Pandas method.

The real goal is:

```text
Business Question
      ↓
Correct Pandas Analysis
      ↓
Correct KPI Calculation
      ↓
Business Comparison
      ↓
Insight
      ↓
Recommendation
```

---

# 81. Core Patterns to Remember

## Filter Data

```python
df[
    df["sales"] > 100000
]
```

## Filter Multiple Conditions

```python
df[
    (df["sales"] > 100000)
    &
    (df["profit"] > 20000)
]
```

## Sort Data

```python
df.sort_values(
    by="sales",
    ascending=False
)
```

## GroupBy

```python
df.groupby(
    "region"
)["sales"].sum()
```

## Named Aggregation

```python
df.groupby(
    "region"
).agg(
    total_sales=(
        "sales",
        "sum"
    ),

    total_profit=(
        "profit",
        "sum"
    )
)
```

## Top Products

```python
product_sales = (
    df.groupby(
        "product_name"
    )["sales"]
    .sum()
    .sort_values(
        ascending=False
    )
    .head(10)
)
```

## Least Profitable Products

```python
product_profit = (
    df.groupby(
        "product_name"
    )["profit"]
    .sum()
    .sort_values()
    .head(10)
)
```

## Pivot Table

```python
pd.pivot_table(
    df,
    values="sales",
    index="region",
    columns="category",
    aggfunc="sum",
    fill_value=0
)
```

## Crosstab

```python
pd.crosstab(
    df["region"],
    df["segment"]
)
```

## Profit Margin

```python
profit_margin = (
    total_profit
    /
    total_sales
) * 100
```

## Average Order Value

```python
average_order_value = (
    total_sales
    /
    total_orders
)
```

---

# 82. Common Beginner Errors

## Analyzing Before Cleaning

Wrong workflow:

```text
Raw Data
    ↓
Analysis
```

Correct:

```text
Raw Data
    ↓
Inspect
    ↓
Clean
    ↓
Validate
    ↓
Analyze
```

---

## Forgetting Parentheses in Filters

Wrong:

```python
df[
    df["sales"] > 100000
    &
    df["profit"] > 20000
]
```

Correct:

```python
df[
    (df["sales"] > 100000)
    &
    (df["profit"] > 20000)
]
```

---

## Using and Instead of &

Wrong:

```python
df[
    (df["sales"] > 100000)
    and
    (df["profit"] > 20000)
]
```

Correct:

```python
df[
    (df["sales"] > 100000)
    &
    (df["profit"] > 20000)
]
```

---

## Counting Rows Instead of Unique Orders

Wrong:

```python
len(df)
```

if one order can contain multiple product rows.

Correct:

```python
df["order_id"].nunique()
```

Again, understand the data grain.

---

## Averaging Percentages Incorrectly

Potentially wrong:

```python
df["profit_margin"].mean()
```

For total business Profit Margin:

```python
(
    df["profit"].sum()
    /
    df["sales"].sum()
) * 100
```

---

## Looking Only at Sales

High Sales does not automatically mean strong business performance.

Compare:

```text
Sales

Profit

Profit Margin

Orders

Customers

Average Order Value
```

---

## Reporting Numbers Without Insights

Weak:

```text
South Sales = ₹5 Million
```

Better:

```text
South generated ₹5 million in sales with the highest Profit Margin among all regions, indicating stronger revenue quality and potential for further investment.
```

---

## Claiming Causation Without Evidence

Weak:

```text
Discounts caused low profits.
```

Better:

```text
Higher discount levels are associated with lower profitability and should be investigated further.
```

Analysis should not claim causation without sufficient evidence.

---

# 83. Interview Questions

1. How do you filter rows in Pandas?
2. How do you filter using multiple conditions?
3. What is the difference between `&` and `|`?
4. What does `isin()` do?
5. What does `between()` do?
6. What is `loc[]`?
7. What is `iloc[]`?
8. What is the difference between `loc[]` and `iloc[]`?
9. How do you sort a DataFrame?
10. How do you sort using multiple columns?
11. What does `nlargest()` do?
12. What does `nsmallest()` do?
13. What is `query()`?
14. How do you create calculated columns?
15. What is `groupby()`?
16. Explain Split-Apply-Combine.
17. How do you calculate sales by region?
18. How do you group by multiple columns?
19. What does `agg()` do?
20. What are named aggregations?
21. What does `reset_index()` do?
22. What is the difference between `count()` and `size()`?
23. How do you count unique orders?
24. What is a Pivot Table?
25. How do you create a Pivot Table in Pandas?
26. What is a Crosstab?
27. What is the difference between Pivot Table and Crosstab?
28. How would you identify top-selling products?
29. How would you identify least profitable products?
30. How would you calculate sales by region?
31. How would you analyze customer segments?
32. How do you calculate Profit Margin correctly?
33. Why should percentages not always be averaged?
34. How do you calculate Average Order Value?
35. How would you identify loss-making products?
36. How would you analyze the impact of discounts?
37. What is the difference between correlation and causation?
38. How would you create a management KPI report?
39. What is the difference between an observation and an insight?
40. How do you convert analysis results into business recommendations?

---

# 84. Completion Checklist

Before moving to Data Visualization, you should be able to:

- [ ] Select single columns
- [ ] Select multiple columns
- [ ] Filter numerical data
- [ ] Filter categorical data
- [ ] Filter using AND conditions
- [ ] Filter using OR conditions
- [ ] Use `isin()`
- [ ] Use `between()`
- [ ] Filter missing values
- [ ] Use `loc[]`
- [ ] Use `iloc[]`
- [ ] Explain `loc[]` vs `iloc[]`
- [ ] Sort ascending
- [ ] Sort descending
- [ ] Sort using multiple columns
- [ ] Use `nlargest()`
- [ ] Use `nsmallest()`
- [ ] Use `query()`
- [ ] Create calculated columns
- [ ] Calculate Cost
- [ ] Calculate Profit Margin
- [ ] Calculate Average Selling Price
- [ ] Explain `groupby()`
- [ ] Explain Split-Apply-Combine
- [ ] Group data by one column
- [ ] Group data by multiple columns
- [ ] Use `sum()`
- [ ] Use `mean()`
- [ ] Use `median()`
- [ ] Use `min()`
- [ ] Use `max()`
- [ ] Use `count()`
- [ ] Use `nunique()`
- [ ] Use `agg()`
- [ ] Use named aggregations
- [ ] Use `reset_index()`
- [ ] Explain `count()` vs `size()`
- [ ] Create Pivot Tables
- [ ] Use `fill_value`
- [ ] Create Pivot Tables with multiple values
- [ ] Create Pivot Tables with totals
- [ ] Create Crosstabs
- [ ] Create percentage Crosstabs
- [ ] Explain Pivot Table vs Crosstab
- [ ] Analyze top-selling products
- [ ] Analyze least profitable products
- [ ] Analyze sales by region
- [ ] Analyze profit by region
- [ ] Analyze customer segments
- [ ] Analyze categories
- [ ] Analyze sub-categories
- [ ] Identify loss-making products
- [ ] Analyze discount patterns
- [ ] Analyze monthly performance
- [ ] Analyze yearly performance
- [ ] Calculate Total Sales
- [ ] Calculate Total Profit
- [ ] Calculate Profit Margin correctly
- [ ] Calculate Total Orders correctly
- [ ] Calculate Unique Customers
- [ ] Calculate Average Order Value
- [ ] Create regional management reports
- [ ] Create product management reports
- [ ] Identify business opportunities
- [ ] Identify underperforming areas
- [ ] Explain observation vs insight
- [ ] Create business recommendations
- [ ] Avoid unsupported causal claims
- [ ] Export management reports

---

# Final Outcome

After completing Data Analysis with Pandas, you should be able to filter and sort business data, use `query()`, `loc[]`, and `iloc[]`, create calculated columns, perform GroupBy analysis and aggregations, create Pivot Tables and Crosstabs, calculate business KPIs correctly, identify top-selling and least profitable products, analyze regional and customer segment performance, identify business opportunities and underperforming areas, and convert Pandas analysis results into management reports, business insights, and actionable recommendations.