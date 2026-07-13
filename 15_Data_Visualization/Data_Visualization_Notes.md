# Data Visualization

## 1. Introduction

Data Visualization is the process of converting data and analysis results into charts that make patterns, trends, comparisons, and business insights easier to understand.

For a Data Analyst, the goal is not to create beautiful charts.

The goal is:

```text
Business Question
    ↓
Analyze Data
    ↓
Choose Correct Chart
    ↓
Create Clear Visualization
    ↓
Interpret the Result
    ↓
Communicate Business Insight
```

The most important topics are:

- Matplotlib
- Line Charts
- Bar Charts
- Horizontal Bar Charts
- Histograms
- Scatter Plots
- Pie Charts
- Labels
- Titles
- Legends
- Figure Size
- Grid
- Chart Formatting
- Monthly Sales Trends
- Regional Performance
- Product Revenue
- Customer Distribution
- Profit Trends
- Executive-Ready Charts

---

# 2. Import Matplotlib

```python
import matplotlib.pyplot as plt
```

Common convention:

```text
matplotlib.pyplot
→
plt
```

---

# 3. Basic Visualization Workflow

```text
1. Understand the Business Question

2. Prepare and Analyze the Data

3. Select the Correct Chart

4. Create the Visualization

5. Add Title and Labels

6. Improve Readability

7. Interpret the Chart

8. Communicate the Business Insight
```

Never create a chart without knowing:

```text
What business question does this chart answer?
```

---

# 4. Basic Chart Structure

```python
plt.figure(figsize=(10, 6))

plt.plot(x, y)

plt.title("Chart Title")

plt.xlabel("X-Axis")

plt.ylabel("Y-Axis")

plt.show()
```

---

# 5. figure()

Use:

```python
plt.figure()
```

to create a figure.

Example:

```python
plt.figure(
    figsize=(10, 6)
)
```

`figsize` controls chart size.

```text
(10, 6)

10 → Width

6 → Height
```

---

# 6. Line Chart

Use a Line Chart to show:

```text
Trends Over Time
```

Common business use cases:

- Monthly Sales
- Yearly Revenue
- Daily Orders
- Profit Trends
- Customer Growth

Example:

```python
months = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May"
]

sales = [
    100000,
    120000,
    115000,
    150000,
    170000
]

plt.figure(
    figsize=(10, 6)
)

plt.plot(
    months,
    sales
)

plt.title(
    "Monthly Sales Trend"
)

plt.xlabel(
    "Month"
)

plt.ylabel(
    "Sales"
)

plt.show()
```

---

# 7. Line Chart with Markers

```python
plt.plot(
    months,
    sales,
    marker="o"
)
```

Markers make individual data points easier to identify.

---

# 8. Line Chart from Pandas DataFrame

Suppose:

```python
monthly_sales = (
    df.groupby(
        "order_month"
    )["sales"]
    .sum()
    .reset_index()
)
```

Create chart:

```python
plt.figure(
    figsize=(10, 6)
)

plt.plot(
    monthly_sales[
        "order_month"
    ].astype(str),

    monthly_sales[
        "sales"
    ],

    marker="o"
)

plt.title(
    "Monthly Sales Trend"
)

plt.xlabel(
    "Month"
)

plt.ylabel(
    "Total Sales"
)

plt.xticks(
    rotation=45
)

plt.tight_layout()

plt.show()
```

---

# 9. Bar Chart

Use a Bar Chart to compare:

```text
Different Categories
```

Common business use cases:

- Sales by Region
- Profit by Category
- Revenue by Product
- Orders by Segment
- Customers by State

Example:

```python
regions = [
    "North",
    "South",
    "East",
    "West"
]

sales = [
    500000,
    750000,
    600000,
    900000
]

plt.figure(
    figsize=(10, 6)
)

plt.bar(
    regions,
    sales
)

plt.title(
    "Sales by Region"
)

plt.xlabel(
    "Region"
)

plt.ylabel(
    "Total Sales"
)

plt.show()
```

---

# 10. Bar Chart from Pandas DataFrame

Prepare data:

```python
regional_sales = (
    df.groupby(
        "region"
    )["sales"]
    .sum()
    .reset_index()
)
```

Create chart:

```python
plt.figure(
    figsize=(10, 6)
)

plt.bar(
    regional_sales[
        "region"
    ],

    regional_sales[
        "sales"
    ]
)

plt.title(
    "Regional Sales Performance"
)

plt.xlabel(
    "Region"
)

plt.ylabel(
    "Total Sales"
)

plt.tight_layout()

plt.show()
```

---

# 11. Horizontal Bar Chart

Use:

```python
plt.barh()
```

Horizontal Bar Charts are useful when:

- Category names are long
- Product names are long
- Ranking Top-N products
- Comparing many categories

Example:

```python
plt.figure(
    figsize=(10, 6)
)

plt.barh(
    regional_sales[
        "region"
    ],

    regional_sales[
        "sales"
    ]
)

plt.title(
    "Regional Sales Performance"
)

plt.xlabel(
    "Total Sales"
)

plt.ylabel(
    "Region"
)

plt.show()
```

---

# 12. Top 10 Products Chart

Prepare data:

```python
top_products = (
    df.groupby(
        "product_name"
    )["sales"]
    .sum()
    .nlargest(10)
    .sort_values()
)
```

Create chart:

```python
plt.figure(
    figsize=(10, 6)
)

plt.barh(
    top_products.index,
    top_products.values
)

plt.title(
    "Top 10 Products by Sales"
)

plt.xlabel(
    "Total Sales"
)

plt.ylabel(
    "Product"
)

plt.tight_layout()

plt.show()
```

Horizontal Bar Charts are usually better for product rankings.

---

# 13. Histogram

Use a Histogram to understand:

```text
Distribution of Numerical Data
```

Common business use cases:

- Sales Distribution
- Profit Distribution
- Customer Age Distribution
- Order Value Distribution
- Delivery Time Distribution

Example:

```python
plt.figure(
    figsize=(10, 6)
)

plt.hist(
    df["sales"],
    bins=20
)

plt.title(
    "Sales Distribution"
)

plt.xlabel(
    "Sales"
)

plt.ylabel(
    "Frequency"
)

plt.show()
```

---

# 14. Understanding bins

```python
plt.hist(
    df["sales"],
    bins=20
)
```

`bins` controls the number of intervals used to divide the data.

Too few bins:

```text
May Hide Important Patterns
```

Too many bins:

```text
May Make the Chart Noisy
```

Choose bins based on the dataset and analysis purpose.

---

# 15. Scatter Plot

Use a Scatter Plot to analyze:

```text
Relationship Between Two Numerical Variables
```

Common business use cases:

- Sales vs Profit
- Discount vs Profit
- Advertising Spend vs Revenue
- Customer Age vs Spending
- Quantity vs Sales

Example:

```python
plt.figure(
    figsize=(10, 6)
)

plt.scatter(
    df["sales"],
    df["profit"]
)

plt.title(
    "Sales vs Profit"
)

plt.xlabel(
    "Sales"
)

plt.ylabel(
    "Profit"
)

plt.show()
```

---

# 16. Scatter Plot Business Interpretation

A Scatter Plot may help identify:

```text
Positive Relationship

Negative Relationship

No Clear Relationship

Clusters

Outliers
```

Example business question:

```text
Do higher sales generally produce higher profits?
```

Another:

```text
Are higher discounts associated with lower profits?
```

---

# 17. Discount vs Profit Scatter Plot

```python
plt.figure(
    figsize=(10, 6)
)

plt.scatter(
    df["discount"],
    df["profit"]
)

plt.title(
    "Discount vs Profit"
)

plt.xlabel(
    "Discount"
)

plt.ylabel(
    "Profit"
)

plt.show()
```

Important:

```text
A Scatter Plot Can Show Association

It Does Not Automatically Prove Causation
```

---

# 18. Pie Chart

Use a Pie Chart to show:

```text
Part-to-Whole Relationships
```

Example:

```python
category_sales = (
    df.groupby(
        "category"
    )["sales"]
    .sum()
)
```

Create chart:

```python
plt.figure(
    figsize=(8, 8)
)

plt.pie(
    category_sales.values,

    labels=category_sales.index,

    autopct="%1.1f%%"
)

plt.title(
    "Sales Distribution by Category"
)

plt.show()
```

---

# 19. When to Use Pie Charts

Use Pie Charts only when:

- There are few categories
- Categories represent parts of a whole
- Percentage comparison is meaningful

Avoid Pie Charts when:

- There are many categories
- Values are very similar
- Precise comparison is required

In many business cases:

```text
Bar Chart > Pie Chart
```

because Bar Charts are easier to compare accurately.

---

# 20. Chart Titles

Every business chart should have a meaningful title.

Weak:

```text
Sales Chart
```

Better:

```text
Monthly Sales Performance
```

Better:

```text
Monthly Sales Trend — January to December 2026
```

Example:

```python
plt.title(
    "Monthly Sales Performance"
)
```

---

# 21. X-Axis Label

```python
plt.xlabel(
    "Month"
)
```

The label should clearly explain what the X-axis represents.

---

# 22. Y-Axis Label

```python
plt.ylabel(
    "Total Sales"
)
```

Avoid vague labels.

Weak:

```text
Value
```

Better:

```text
Total Sales
```

---

# 23. Rotate Axis Labels

Long labels may overlap.

Use:

```python
plt.xticks(
    rotation=45
)
```

Example:

```python
plt.xticks(
    rotation=45,
    ha="right"
)
```

---

# 24. Grid

Use:

```python
plt.grid()
```

Example:

```python
plt.grid(
    axis="y",
    alpha=0.3
)
```

A light grid can improve readability.

Avoid excessive grid lines.

---

# 25. Legend

Use a Legend when multiple data series appear in one chart.

Example:

```python
plt.plot(
    months,
    sales,
    label="Sales"
)

plt.plot(
    months,
    profit,
    label="Profit"
)

plt.legend()

plt.show()
```

---

# 26. Multiple Lines

Example:

```python
plt.figure(
    figsize=(10, 6)
)

plt.plot(
    monthly_performance[
        "month"
    ],

    monthly_performance[
        "sales"
    ],

    marker="o",

    label="Sales"
)

plt.plot(
    monthly_performance[
        "month"
    ],

    monthly_performance[
        "profit"
    ],

    marker="o",

    label="Profit"
)

plt.title(
    "Monthly Sales and Profit Trends"
)

plt.xlabel(
    "Month"
)

plt.ylabel(
    "Amount"
)

plt.legend()

plt.grid(
    alpha=0.3
)

plt.tight_layout()

plt.show()
```

Be careful when Sales and Profit have very different scales.

A chart with two lines is not automatically useful just because both metrics are available.

---

# 27. tight_layout()

Use:

```python
plt.tight_layout()
```

This helps prevent:

- Cut-off labels
- Overlapping titles
- Poor spacing

Example:

```python
plt.tight_layout()

plt.show()
```

---

# 28. Save Charts

Use:

```python
plt.savefig()
```

Example:

```python
plt.savefig(
    "monthly_sales.png"
)
```

Save before:

```python
plt.show()
```

Complete example:

```python
plt.figure(
    figsize=(10, 6)
)

plt.plot(
    months,
    sales
)

plt.title(
    "Monthly Sales Trend"
)

plt.tight_layout()

plt.savefig(
    "monthly_sales.png"
)

plt.show()
```

---

# 29. Save High-Quality Charts

```python
plt.savefig(
    "monthly_sales.png",
    dpi=300,
    bbox_inches="tight"
)
```

Important parameters:

```text
dpi
→ Image Resolution

bbox_inches="tight"
→ Removes Unnecessary Empty Space
```

---

# 30. Monthly Sales Visualization

Prepare data:

```python
df["order_date"] = (
    pd.to_datetime(
        df["order_date"]
    )
)

df["order_month"] = (
    df["order_date"]
    .dt.to_period("M")
)

monthly_sales = (
    df.groupby(
        "order_month"
    )["sales"]
    .sum()
    .reset_index()
)
```

Visualize:

```python
plt.figure(
    figsize=(12, 6)
)

plt.plot(
    monthly_sales[
        "order_month"
    ].astype(str),

    monthly_sales[
        "sales"
    ],

    marker="o"
)

plt.title(
    "Monthly Sales Trend"
)

plt.xlabel(
    "Month"
)

plt.ylabel(
    "Total Sales"
)

plt.xticks(
    rotation=45
)

plt.grid(
    alpha=0.3
)

plt.tight_layout()

plt.show()
```

---

# 31. Regional Performance Visualization

Prepare data:

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
        )
    )
    .reset_index()
)
```

Visualize:

```python
plt.figure(
    figsize=(10, 6)
)

plt.bar(
    regional_performance[
        "region"
    ],

    regional_performance[
        "total_sales"
    ]
)

plt.title(
    "Regional Sales Performance"
)

plt.xlabel(
    "Region"
)

plt.ylabel(
    "Total Sales"
)

plt.tight_layout()

plt.show()
```

---

# 32. Product Revenue Visualization

Prepare data:

```python
product_revenue = (
    df.groupby(
        "product_name"
    )["sales"]
    .sum()
    .nlargest(10)
    .sort_values()
)
```

Visualize:

```python
plt.figure(
    figsize=(12, 7)
)

plt.barh(
    product_revenue.index,
    product_revenue.values
)

plt.title(
    "Top 10 Products by Revenue"
)

plt.xlabel(
    "Total Revenue"
)

plt.ylabel(
    "Product"
)

plt.tight_layout()

plt.show()
```

---

# 33. Customer Distribution Visualization

Prepare data:

```python
customer_distribution = (
    df.groupby(
        "segment"
    )["customer_id"]
    .nunique()
)
```

Visualize:

```python
plt.figure(
    figsize=(8, 6)
)

plt.bar(
    customer_distribution.index,
    customer_distribution.values
)

plt.title(
    "Customer Distribution by Segment"
)

plt.xlabel(
    "Customer Segment"
)

plt.ylabel(
    "Unique Customers"
)

plt.tight_layout()

plt.show()
```

---

# 34. Profit Trend Visualization

Prepare data:

```python
monthly_profit = (
    df.groupby(
        "order_month"
    )["profit"]
    .sum()
    .reset_index()
)
```

Visualize:

```python
plt.figure(
    figsize=(12, 6)
)

plt.plot(
    monthly_profit[
        "order_month"
    ].astype(str),

    monthly_profit[
        "profit"
    ],

    marker="o"
)

plt.title(
    "Monthly Profit Trend"
)

plt.xlabel(
    "Month"
)

plt.ylabel(
    "Total Profit"
)

plt.xticks(
    rotation=45
)

plt.grid(
    alpha=0.3
)

plt.tight_layout()

plt.show()
```

---

# 35. Profit by Category

Prepare:

```python
category_profit = (
    df.groupby(
        "category"
    )["profit"]
    .sum()
    .sort_values(
        ascending=False
    )
)
```

Visualize:

```python
plt.figure(
    figsize=(10, 6)
)

plt.bar(
    category_profit.index,
    category_profit.values
)

plt.title(
    "Profit Performance by Category"
)

plt.xlabel(
    "Category"
)

plt.ylabel(
    "Total Profit"
)

plt.tight_layout()

plt.show()
```

---

# 36. Sales Distribution Visualization

```python
plt.figure(
    figsize=(10, 6)
)

plt.hist(
    df["sales"],
    bins=30
)

plt.title(
    "Distribution of Sales Values"
)

plt.xlabel(
    "Sales"
)

plt.ylabel(
    "Frequency"
)

plt.tight_layout()

plt.show()
```

This helps identify:

- Typical Sales Values
- Skewed Data
- Extreme Values
- Possible Outliers

---

# 37. Sales vs Profit Visualization

```python
plt.figure(
    figsize=(10, 6)
)

plt.scatter(
    df["sales"],
    df["profit"]
)

plt.title(
    "Relationship Between Sales and Profit"
)

plt.xlabel(
    "Sales"
)

plt.ylabel(
    "Profit"
)

plt.grid(
    alpha=0.3
)

plt.tight_layout()

plt.show()
```

---

# 38. Adding Value Labels to Bar Charts

Prepare data:

```python
regional_sales = (
    df.groupby(
        "region"
    )["sales"]
    .sum()
    .reset_index()
)
```

Create chart:

```python
plt.figure(
    figsize=(10, 6)
)

bars = plt.bar(
    regional_sales[
        "region"
    ],

    regional_sales[
        "sales"
    ]
)

plt.bar_label(
    bars,
    fmt="%.0f"
)

plt.title(
    "Regional Sales Performance"
)

plt.xlabel(
    "Region"
)

plt.ylabel(
    "Total Sales"
)

plt.tight_layout()

plt.show()
```

---

# 39. Currency Formatting

Import:

```python
from matplotlib.ticker import FuncFormatter
```

Create formatter:

```python
def currency_formatter(
    value,
    position
):

    return f"₹{value:,.0f}"
```

Apply:

```python
plt.gca().yaxis.set_major_formatter(
    FuncFormatter(
        currency_formatter
    )
)
```

Complete example:

```python
from matplotlib.ticker import FuncFormatter


def currency_formatter(
    value,
    position
):

    return f"₹{value:,.0f}"


plt.figure(
    figsize=(10, 6)
)

plt.bar(
    regional_sales[
        "region"
    ],

    regional_sales[
        "sales"
    ]
)

plt.gca().yaxis.set_major_formatter(
    FuncFormatter(
        currency_formatter
    )
)

plt.title(
    "Regional Sales Performance"
)

plt.xlabel(
    "Region"
)

plt.ylabel(
    "Total Sales"
)

plt.tight_layout()

plt.show()
```

---

# 40. Chart Selection Guide

| Business Question | Recommended Chart |
|---|---|
| How are sales changing over time? | Line Chart |
| Which region has the highest sales? | Bar Chart |
| Which products generate the most revenue? | Horizontal Bar Chart |
| What is the distribution of order values? | Histogram |
| Is there a relationship between sales and profit? | Scatter Plot |
| What percentage of sales comes from each category? | Pie Chart or Bar Chart |
| Which products are underperforming? | Horizontal Bar Chart |
| How are profits changing monthly? | Line Chart |
| How many customers belong to each segment? | Bar Chart |

---

# 41. Choosing the Correct Chart

## Line Chart

Use for:

```text
Time Trends
```

## Bar Chart

Use for:

```text
Category Comparisons
```

## Horizontal Bar Chart

Use for:

```text
Rankings and Long Category Names
```

## Histogram

Use for:

```text
Numerical Distributions
```

## Scatter Plot

Use for:

```text
Relationships Between Numerical Variables
```

## Pie Chart

Use for:

```text
Simple Part-to-Whole Comparisons
```

---

# 42. Executive-Ready Charts

An executive-ready chart should:

- Answer one clear business question
- Have a meaningful title
- Use the correct chart type
- Have readable labels
- Avoid unnecessary clutter
- Highlight important information
- Use appropriate units
- Be understandable quickly
- Support business decisions

The goal is:

```text
Decision-Making

Not Decoration
```

---

# 43. Weak vs Strong Chart Titles

Weak:

```text
Sales
```

Better:

```text
Monthly Sales Trend
```

Strong:

```text
Monthly Sales Declined During Q3 Before Recovering in Q4
```

A strong title can communicate the key finding.

---

# 44. Avoid Chart Junk

Do not add unnecessary:

- 3D Effects
- Excessive Grid Lines
- Too Many Colors
- Decorative Backgrounds
- Unnecessary Legends
- Too Many Data Labels
- Unreadable Text
- Excessive Categories

Simple charts are usually more effective.

---

# 45. Weekly Business Review Charts

A weekly business review may contain:

```text
1. Overall KPI Summary

2. Weekly or Monthly Sales Trend

3. Profit Trend

4. Regional Performance

5. Category Performance

6. Top Products

7. Underperforming Products

8. Customer Segment Performance

9. Key Business Insights

10. Recommended Actions
```

---

# 46. Executive Business Review Example

```python
import pandas as pd

import matplotlib.pyplot as plt


# LOAD DATA

df = pd.read_csv(
    "cleaned_sales_data.csv"
)


# DATE CONVERSION

df["order_date"] = (
    pd.to_datetime(
        df["order_date"]
    )
)


# CREATE MONTH

df["order_month"] = (
    df["order_date"]
    .dt.to_period("M")
)


# MONTHLY SALES

monthly_sales = (
    df.groupby(
        "order_month"
    )["sales"]
    .sum()
    .reset_index()
)


# REGIONAL SALES

regional_sales = (
    df.groupby(
        "region"
    )["sales"]
    .sum()
    .sort_values(
        ascending=False
    )
)


# TOP PRODUCTS

top_products = (
    df.groupby(
        "product_name"
    )["sales"]
    .sum()
    .nlargest(10)
    .sort_values()
)


# CUSTOMER DISTRIBUTION

customer_distribution = (
    df.groupby(
        "segment"
    )["customer_id"]
    .nunique()
)


# MONTHLY SALES CHART

plt.figure(
    figsize=(12, 6)
)

plt.plot(
    monthly_sales[
        "order_month"
    ].astype(str),

    monthly_sales[
        "sales"
    ],

    marker="o"
)

plt.title(
    "Monthly Sales Trend"
)

plt.xlabel(
    "Month"
)

plt.ylabel(
    "Total Sales"
)

plt.xticks(
    rotation=45
)

plt.grid(
    alpha=0.3
)

plt.tight_layout()

plt.show()


# REGIONAL SALES CHART

plt.figure(
    figsize=(10, 6)
)

plt.bar(
    regional_sales.index,
    regional_sales.values
)

plt.title(
    "Regional Sales Performance"
)

plt.xlabel(
    "Region"
)

plt.ylabel(
    "Total Sales"
)

plt.tight_layout()

plt.show()


# TOP PRODUCTS CHART

plt.figure(
    figsize=(12, 7)
)

plt.barh(
    top_products.index,
    top_products.values
)

plt.title(
    "Top 10 Products by Sales"
)

plt.xlabel(
    "Total Sales"
)

plt.ylabel(
    "Product"
)

plt.tight_layout()

plt.show()


# CUSTOMER DISTRIBUTION CHART

plt.figure(
    figsize=(8, 6)
)

plt.bar(
    customer_distribution.index,
    customer_distribution.values
)

plt.title(
    "Customer Distribution by Segment"
)

plt.xlabel(
    "Segment"
)

plt.ylabel(
    "Unique Customers"
)

plt.tight_layout()

plt.show()
```

---

# 47. Visualization Business Insight Structure

After creating a chart, explain:

```text
1. What Happened?

2. Where Did It Happen?

3. How Significant Is It?

4. Why Might It Have Happened?

5. What Should the Business Investigate or Do Next?
```

Example:

```text
Finding:

The West region generated the highest sales.

Comparison:

West sales were significantly higher than East region sales.

Business Meaning:

The West region is currently the strongest revenue contributor.

Investigation:

Analyze whether performance is driven by customer volume, larger order values, specific products, or discounting.

Recommendation:

Identify successful products and sales strategies from the West region that may be applicable to underperforming regions.
```

---

# 48. Common Beginner Errors

## Using the Wrong Chart

Wrong:

```text
Line Chart for Product Categories
```

Better:

```text
Bar Chart
```

---

## Creating Charts Before Analyzing Data

Wrong:

```text
Raw Data
    ↓
Chart
```

Better:

```text
Raw Data
    ↓
Clean
    ↓
Analyze
    ↓
Aggregate
    ↓
Visualize
    ↓
Interpret
```

---

## Missing Titles and Labels

Weak:

```python
plt.bar(
    regions,
    sales
)

plt.show()
```

Better:

```python
plt.bar(
    regions,
    sales
)

plt.title(
    "Regional Sales Performance"
)

plt.xlabel(
    "Region"
)

plt.ylabel(
    "Total Sales"
)

plt.show()
```

---

## Too Many Categories

Showing 100 products in one Bar Chart is usually useless.

Better:

```text
Top 10 Products

Bottom 10 Products
```

---

## Using Pie Charts for Everything

Pie Charts are frequently overused.

For accurate category comparison:

```text
Prefer Bar Charts
```

---

## Ignoring Sort Order

Weak:

```text
Random Category Order
```

Better:

```text
Highest to Lowest
```

Sorting makes comparison easier.

---

## Reporting Charts Without Insights

Weak:

```text
Here is the regional sales chart.
```

Better:

```text
West generates the highest sales, but profitability analysis is required before concluding that it is the strongest-performing region.
```

---

## Claiming Causation

Weak:

```text
Discounts caused losses.
```

Better:

```text
Higher discounts appear to be associated with lower profits and require further investigation.
```

---

# 49. Interview Questions

1. What is Data Visualization?
2. Why is Data Visualization important for Data Analysts?
3. What is Matplotlib?
4. How do you import Matplotlib?
5. What does `plt.figure()` do?
6. What is `figsize`?
7. When should you use a Line Chart?
8. When should you use a Bar Chart?
9. When should you use a Horizontal Bar Chart?
10. When should you use a Histogram?
11. When should you use a Scatter Plot?
12. When should you use a Pie Chart?
13. Why are Bar Charts often better than Pie Charts?
14. What does `bins` mean in a Histogram?
15. What information can a Scatter Plot show?
16. Can a Scatter Plot prove causation?
17. How do you add a chart title?
18. How do you add X-axis and Y-axis labels?
19. How do you rotate axis labels?
20. What does `plt.legend()` do?
21. What does `plt.grid()` do?
22. What does `plt.tight_layout()` do?
23. How do you save a chart?
24. What does `dpi` mean?
25. How would you visualize monthly sales?
26. How would you visualize regional performance?
27. How would you visualize the Top 10 products?
28. How would you visualize customer distribution?
29. How would you visualize profit trends?
30. How would you analyze Sales vs Profit?
31. How do you add value labels to a Bar Chart?
32. How do you format chart values as currency?
33. What makes a chart executive-ready?
34. What is chart junk?
35. How do you choose the correct chart?
36. Why should charts answer business questions?
37. What charts would you include in a weekly business review?
38. What is the difference between a chart observation and a business insight?
39. Why is sorting important in Bar Charts?
40. How do you convert a visualization into a business recommendation?

---

# 50. Completion Checklist

Before moving to Advanced Pandas, you should be able to:

- [ ] Import Matplotlib
- [ ] Create a figure
- [ ] Set figure size
- [ ] Create Line Charts
- [ ] Add markers to Line Charts
- [ ] Create Bar Charts
- [ ] Create Horizontal Bar Charts
- [ ] Create Histograms
- [ ] Understand `bins`
- [ ] Create Scatter Plots
- [ ] Create Pie Charts
- [ ] Explain when to avoid Pie Charts
- [ ] Add chart titles
- [ ] Add X-axis labels
- [ ] Add Y-axis labels
- [ ] Rotate axis labels
- [ ] Add grids
- [ ] Add legends
- [ ] Create charts with multiple lines
- [ ] Use `tight_layout()`
- [ ] Save charts
- [ ] Save high-resolution charts
- [ ] Visualize monthly sales
- [ ] Visualize regional performance
- [ ] Visualize product revenue
- [ ] Visualize customer distribution
- [ ] Visualize profit trends
- [ ] Visualize category profitability
- [ ] Visualize numerical distributions
- [ ] Analyze relationships with Scatter Plots
- [ ] Add values to Bar Charts
- [ ] Format currency values
- [ ] Choose the correct chart
- [ ] Create executive-ready charts
- [ ] Avoid chart junk
- [ ] Create weekly business review charts
- [ ] Interpret visualizations
- [ ] Convert observations into insights
- [ ] Create business recommendations
- [ ] Avoid unsupported causal claims

---

# Final Outcome

After completing Data Visualization, you should be able to use Matplotlib to create Line Charts, Bar Charts, Horizontal Bar Charts, Histograms, Scatter Plots, and Pie Charts; add meaningful titles, labels, legends, grids, and formatting; visualize monthly sales, regional performance, product revenue, customer distribution, and profit trends; save high-quality charts; choose the correct visualization for different business questions; and create clear, executive-ready charts for weekly business review meetings.

The goal is not:

```text
Create More Charts
```

The goal is:

```text
Business Question
    ↓
Correct Analysis
    ↓
Correct Chart
    ↓
Clear Communication
    ↓
Business Insight
    ↓
Actionable Recommendation
```