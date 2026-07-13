# Strings

## 1. Introduction

A string is a sequence of characters used to store text data.

```python
customer_name = "Manoj Kumar"
product_name = "Laptop"
city = "Hyderabad"
```

Strings are extremely important in Data Analytics because real-world datasets contain text columns such as:

- Customer Names
- Product Names
- Categories
- Cities
- States
- Email Addresses
- Order IDs

The most important string concepts for Data Analysts are:

- Indexing
- Slicing
- String Methods
- `replace()`
- `split()`
- `join()`
- `strip()`
- f-Strings

---

# 2. Creating Strings

Strings can be created using single or double quotes.

```python
company = "Reliance Retail"

city = 'Hyderabad'
```

Both are valid.

---

# 3. String Indexing

Indexing allows access to individual characters.

```python
company = "Amazon"
```

Index positions:

```text
A  m  a  z  o  n
0  1  2  3  4  5
```

Access the first character:

```python
print(company[0])
```

Output:

```text
A
```

Access another character:

```python
print(company[3])
```

Output:

```text
z
```

---

# 4. Negative Indexing

Negative indexing accesses characters from the end.

```python
company = "Amazon"
```

```text
 A   m   a   z   o   n
-6  -5  -4  -3  -2  -1
```

Get the last character:

```python
print(company[-1])
```

Output:

```text
n
```

---

# 5. String Slicing

Slicing extracts part of a string.

Syntax:

```python
string[start:stop]
```

Example:

```python
order_id = "ORD-2026-1001"

print(order_id[0:3])
```

Output:

```text
ORD
```

Important:

The `stop` position is excluded.

---

# 6. Slicing Shortcuts

From beginning:

```python
text[:5]
```

From a position to the end:

```python
text[5:]
```

Complete string:

```python
text[:]
```

Example:

```python
customer = "Manoj Kumar"

print(customer[:5])
```

Output:

```text
Manoj
```

---

# 7. Slicing with Step

Syntax:

```python
string[start:stop:step]
```

Example:

```python
text = "Python"

print(text[::2])
```

Output:

```text
Pto
```

Reverse a string:

```python
print(text[::-1])
```

Output:

```text
nohtyP
```

---

# 8. String Immutability

Strings are immutable.

This means an existing string cannot be changed directly.

Wrong:

```python
company = "Amazon"

company[0] = "a"
```

This causes an error.

Instead, create a new string:

```python
company = "Amazon"

company = company.lower()
```

---

# 9. len()

`len()` returns the number of characters.

```python
customer_name = "Manoj Kumar"

print(len(customer_name))
```

Output:

```text
11
```

Spaces are also counted.

---

# 10. upper()

Converts text to uppercase.

```python
company = "amazon"

print(company.upper())
```

Output:

```text
AMAZON
```

Data Analyst use case:

```python
category = "electronics"

category = category.upper()

print(category)
```

---

# 11. lower()

Converts text to lowercase.

```python
email = "MANOJ@GMAIL.COM"

email = email.lower()

print(email)
```

Output:

```text
manoj@gmail.com
```

Useful for standardizing email addresses and categories.

---

# 12. title()

Converts the first letter of every word to uppercase.

```python
customer_name = "manoj kumar"

customer_name = customer_name.title()

print(customer_name)
```

Output:

```text
Manoj Kumar
```

Useful for cleaning customer names.

---

# 13. capitalize()

Converts only the first character to uppercase.

```python
text = "business analytics"

print(text.capitalize())
```

Output:

```text
Business analytics
```

---

# 14. strip()

`strip()` removes unnecessary spaces from the beginning and end.

Messy data:

```python
customer_name = "   Manoj Kumar   "
```

Clean data:

```python
customer_name = customer_name.strip()

print(customer_name)
```

Output:

```text
Manoj Kumar
```

This is one of the most important string methods for data cleaning.

---

# 15. lstrip() and rstrip()

Remove spaces from one side.

```python
text = "   Python   "
```

Remove left spaces:

```python
text.lstrip()
```

Remove right spaces:

```python
text.rstrip()
```

For most data cleaning tasks:

```python
strip()
```

is used more frequently.

---

# 16. replace()

`replace()` replaces existing text with new text.

Syntax:

```python
string.replace(old, new)
```

Example:

```python
category = "Home Appliances"

category = category.replace(" ", "_")

print(category)
```

Output:

```text
Home_Appliances
```

---

# 17. Standardizing Product Categories

Messy category:

```python
category = "Mobile Phones"
```

Standardize:

```python
category = category.replace("Mobile Phones", "Mobiles")

print(category)
```

Output:

```text
Mobiles
```

---

# 18. Method Chaining

Multiple string methods can be applied together.

```python
customer_name = "   manoj kumar   "

customer_name = customer_name.strip().title()

print(customer_name)
```

Output:

```text
Manoj Kumar
```

Execution:

```text
Original Data
      ↓
strip()
      ↓
Remove Extra Spaces
      ↓
title()
      ↓
Standardize Name
```

Method chaining is extremely useful for data cleaning.

---

# 19. split()

`split()` converts a string into separate values.

Example:

```python
customer_name = "Manoj Kumar"

name_parts = customer_name.split()

print(name_parts)
```

Output:

```python
["Manoj", "Kumar"]
```

---

# 20. Extract First and Last Name

```python
customer_name = "Manoj Kumar"

name_parts = customer_name.split()

first_name = name_parts[0]

last_name = name_parts[1]

print(first_name)

print(last_name)
```

---

# 21. Split Using a Separator

Consider:

```python
location = "Hyderabad-Telangana"
```

Split using `-`:

```python
location_parts = location.split("-")

print(location_parts)
```

Output:

```text
["Hyderabad", "Telangana"]
```

---

# 22. Extract City and State

```python
location = "Hyderabad,Telangana"

city, state = location.split(",")

print(city)

print(state)
```

Output:

```text
Hyderabad
Telangana
```

This is useful when one column contains multiple pieces of information.

---

# 23. join()

`join()` combines multiple strings into one string.

```python
words = ["Python", "Data", "Analytics"]

result = " ".join(words)

print(result)
```

Output:

```text
Python Data Analytics
```

---

# 24. Joining with Different Separators

Using comma:

```python
",".join(["Laptop", "Mobile", "Tablet"])
```

Output:

```text
Laptop,Mobile,Tablet
```

Using hyphen:

```python
"-".join(["2026", "07", "13"])
```

Output:

```text
2026-07-13
```

---

# 25. split() vs join()

| Method | Purpose |
|---|---|
| `split()` | String → Multiple Values |
| `join()` | Multiple Strings → Single String |

Example:

```python
text = "Python Data Analytics"

words = text.split()
```

Result:

```text
["Python", "Data", "Analytics"]
```

Join again:

```python
result = " ".join(words)
```

Result:

```text
Python Data Analytics
```

---

# 26. startswith()

Checks whether a string starts with specific text.

```python
order_id = "ORD-2026-1001"

print(order_id.startswith("ORD"))
```

Output:

```text
True
```

Useful for validating IDs.

---

# 27. endswith()

Checks whether a string ends with specific text.

```python
file_name = "sales_report.csv"

print(file_name.endswith(".csv"))
```

Output:

```text
True
```

Useful later when processing files.

---

# 28. Finding Text

Use the `in` operator to check whether text exists.

```python
product = "Apple iPhone 15"

print("iPhone" in product)
```

Output:

```text
True
```

Data Analyst example:

```python
email = "customer@gmail.com"

if "@gmail.com" in email:

    print("Gmail Customer")
```

---

# 29. count()

Counts how many times a value appears.

```python
text = "Data Analytics and Data Science"

print(text.count("Data"))
```

Output:

```text
2
```

---

# 30. find()

Returns the position of text.

```python
email = "manoj@gmail.com"

print(email.find("@"))
```

Output:

```text
5
```

If the value is not found:

```text
-1
```

---

# 31. f-Strings

f-Strings are used to insert variables inside strings.

```python
company = "ShopKart India"

revenue = 850000

print(f"Company: {company}")

print(f"Revenue: {revenue}")
```

---

# 32. Formatting Numbers with f-Strings

```python
revenue = 850000

print(f"Revenue: ₹{revenue:,.2f}")
```

Output:

```text
Revenue: ₹850,000.00
```

---

# 33. Formatting Percentages

```python
profit_margin = 27.19452

print(f"Profit Margin: {profit_margin:.2f}%")
```

Output:

```text
Profit Margin: 27.19%
```

---

# 34. Expressions Inside f-Strings

```python
revenue = 850000

cost = 620000

print(f"Profit: ₹{revenue - cost:,.2f}")
```

Output:

```text
Profit: ₹230,000.00
```

---

# 35. Creating Report Titles

```python
company_name = "ShopKart India"

report_month = "July 2026"

report_title = f"{company_name.upper()} - SALES REPORT - {report_month.upper()}"

print(report_title)
```

Output:

```text
SHOPKART INDIA - SALES REPORT - JULY 2026
```

---

# 36. Data Cleaning Example — Customer Name

Messy data:

```python
customer_name = "   mANOJ kUMAR   "
```

Clean:

```python
customer_name = customer_name.strip().title()

print(customer_name)
```

Output:

```text
Manoj Kumar
```

---

# 37. Data Cleaning Example — Product Category

Messy data:

```python
product_category = "   MOBILE PHONES   "
```

Clean:

```python
product_category = product_category.strip().lower().replace(
    "mobile phones",
    "mobiles"
)

print(product_category)
```

Output:

```text
mobiles
```

---

# 38. Data Cleaning Example — Location

Messy data:

```python
location = "   Hyderabad,Telangana   "
```

Clean and extract:

```python
location = location.strip()

city, state = location.split(",")

city = city.strip().title()

state = state.strip().title()

print(f"City: {city}")

print(f"State: {state}")
```

---

# 39. Complete Customer Data Cleaning Example

```python
customer_name = "   mANOJ kUMAR   "

product_category = "  MOBILE PHONES  "

location = "  hyderabad,telangana  "


# Clean Customer Name

customer_name = customer_name.strip().title()


# Clean Product Category

product_category = (
    product_category
    .strip()
    .lower()
    .replace("mobile phones", "mobiles")
)


# Extract and Clean Location

location = location.strip()

city, state = location.split(",")

city = city.strip().title()

state = state.strip().title()


# Clean Data Report

print("=" * 50)

print("CLEANED CUSTOMER DATA")

print("=" * 50)

print(f"Customer Name:    {customer_name}")

print(f"Product Category: {product_category}")

print(f"City:             {city}")

print(f"State:            {state}")

print("=" * 50)
```

---

# 40. Most Important String Methods

| Method | Purpose |
|---|---|
| `upper()` | Convert to uppercase |
| `lower()` | Convert to lowercase |
| `title()` | Capitalize each word |
| `strip()` | Remove extra spaces |
| `replace()` | Replace text |
| `split()` | Separate text |
| `join()` | Combine strings |
| `startswith()` | Check beginning |
| `endswith()` | Check ending |
| `count()` | Count occurrences |
| `find()` | Find position |

Do not waste time memorizing every Python string method.

Master these methods first because they cover most beginner-level data cleaning requirements.

---

# 41. Core Patterns to Remember

## Clean Customer Names

```python
customer_name.strip().title()
```

## Standardize Categories

```python
category.strip().lower()
```

## Replace Incorrect Values

```python
category.replace("old_value", "new_value")
```

## Extract Information

```python
city, state = location.split(",")
```

## Combine Strings

```python
" ".join(words)
```

## Create Business Reports

```python
f"Revenue: ₹{revenue:,.2f}"
```

---

# 42. Common Beginner Errors

## Forgetting Strings Are Immutable

Wrong assumption:

```python
customer_name.strip()
```

This does not modify the original variable permanently.

Correct:

```python
customer_name = customer_name.strip()
```

---

## Incorrect Index

```python
text = "Python"

print(text[10])
```

This causes:

```text
IndexError
```

because the index does not exist.

---

## Forgetting split() Returns Multiple Values

```python
location = "Hyderabad,Telangana"

result = location.split(",")
```

`result` contains:

```text
["Hyderabad", "Telangana"]
```

---

## Confusing split() and join()

Remember:

```text
split() → Break Apart

join() → Combine Together
```

---

# 43. Interview Questions

1. What is a string?
2. What is string indexing?
3. What is negative indexing?
4. What is string slicing?
5. Why are strings immutable?
6. What does `strip()` do?
7. What is the difference between `lower()` and `title()`?
8. How does `replace()` work?
9. What does `split()` return?
10. What is the difference between `split()` and `join()`?
11. How would you extract city and state from one string?
12. How would you clean inconsistent customer names?
13. What are f-Strings?
14. How do you format numbers to two decimal places?
15. How would you standardize messy product categories?

---

# 44. Completion Checklist

Before moving to the next module, you should be able to:

- [ ] Create strings
- [ ] Use positive indexing
- [ ] Use negative indexing
- [ ] Slice strings
- [ ] Explain string immutability
- [ ] Use `len()`
- [ ] Use `upper()`
- [ ] Use `lower()`
- [ ] Use `title()`
- [ ] Use `strip()`
- [ ] Use `replace()`
- [ ] Use method chaining
- [ ] Use `split()`
- [ ] Extract city and state
- [ ] Use `join()`
- [ ] Use `startswith()`
- [ ] Use `endswith()`
- [ ] Search for text using `in`
- [ ] Use f-Strings
- [ ] Format numbers and percentages
- [ ] Clean messy customer names
- [ ] Standardize product categories
- [ ] Create formatted business reports

---

# Final Outcome

After completing Strings, you should be able to clean and standardize text data, remove extra spaces, correct inconsistent customer and product information, extract information from combined text fields, join multiple text values, validate text patterns, and create professional business report outputs using f-Strings.