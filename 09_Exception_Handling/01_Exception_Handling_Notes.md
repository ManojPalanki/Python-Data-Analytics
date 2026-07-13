# Exception Handling

## 1. Introduction

Exception handling allows Python programs to handle errors without immediately stopping execution.

Real-world business data is rarely perfect. A Data Analyst may encounter:

- Missing sales values
- Invalid numbers
- Missing files
- Division by zero
- Incorrect user input
- Corrupted or incomplete data

Without exception handling, one bad value can stop an entire reporting workflow.

The main concepts are:

- `try`
- `except`
- `else`
- `finally`
- `raise`
- Custom Exceptions

---

# 2. What Is an Exception?

An exception is an error that occurs while a Python program is running.

Example:

```python
revenue = 100000

orders = 0

average_order_value = revenue / orders
```

This causes:

```text
ZeroDivisionError
```

The program stops because division by zero is not allowed.

---

# 3. Common Exceptions for Data Analysts

| Exception | Cause |
|---|---|
| `ValueError` | Invalid value conversion |
| `TypeError` | Operation on incompatible data types |
| `ZeroDivisionError` | Division by zero |
| `FileNotFoundError` | File does not exist |
| `KeyError` | Dictionary key does not exist |
| `IndexError` | List index does not exist |

You do not need to memorize every Python exception. Understand these common ones first.

---

# 4. try and except

The basic exception-handling structure is:

```python
try:
    code_that_may_fail

except:
    code_to_handle_error
```

Example:

```python
try:

    revenue = 100000

    orders = 0

    average_order_value = revenue / orders

except:

    print("Unable to calculate Average Order Value")
```

Instead of crashing, the program handles the error.

---

# 5. Handling Specific Exceptions

Avoid using a generic `except` when you know which error may occur.

Better:

```python
try:

    revenue = 100000

    orders = 0

    average_order_value = revenue / orders

except ZeroDivisionError:

    print("Orders cannot be zero")
```

This makes the code easier to understand and debug.

---

# 6. Handling Invalid Numbers

Suppose sales data is stored as text:

```python
sales = "850000"
```

Convert it:

```python
sales = float(sales)
```

But invalid data may exist:

```python
sales = "Not Available"
```

This causes:

```text
ValueError
```

Handle it:

```python
try:

    sales = "Not Available"

    sales = float(sales)

except ValueError:

    print("Invalid Sales Value")
```

---

# 7. Data Analyst Example — Missing Sales Values

```python
sales_value = None

try:

    sales = float(sales_value)

except (TypeError, ValueError):

    sales = 0

print(f"Sales: ₹{sales:,.2f}")
```

This handles both:

- Missing values
- Invalid numeric values

---

# 8. Handling Multiple Exceptions

Multiple exceptions can be handled separately.

```python
try:

    revenue = float(input("Enter Revenue: "))

    orders = int(input("Enter Orders: "))

    average_order_value = revenue / orders


except ValueError:

    print("Enter valid numeric values")


except ZeroDivisionError:

    print("Orders cannot be zero")
```

This allows different errors to receive different responses.

---

# 9. Handling Multiple Exceptions Together

Exceptions can also be grouped.

```python
try:

    sales = float(None)

except (TypeError, ValueError):

    print("Invalid or Missing Sales Value")
```

Use this when multiple exceptions require the same handling logic.

---

# 10. else Block

The `else` block executes only when no exception occurs.

Syntax:

```python
try:
    code

except:
    handle_error

else:
    execute_if_successful
```

Example:

```python
try:

    revenue = 850000

    orders = 1700

    average_order_value = revenue / orders


except ZeroDivisionError:

    print("Orders cannot be zero")


else:

    print(
        f"Average Order Value: ₹{average_order_value:,.2f}"
    )
```

---

# 11. finally Block

The `finally` block always executes.

It runs whether an exception occurs or not.

```python
try:

    revenue = 850000

    orders = 0

    average_order_value = revenue / orders


except ZeroDivisionError:

    print("Orders cannot be zero")


finally:

    print("KPI calculation process completed")
```

Output:

```text
Orders cannot be zero

KPI calculation process completed
```

---

# 12. try, except, else, finally

Complete structure:

```python
try:

    code_that_may_fail


except SomeError:

    handle_the_error


else:

    run_if_no_error


finally:

    always_run_this_code
```

Remember:

```text
try
→ Attempt the operation

except
→ Handle the error

else
→ Run when no error occurs

finally
→ Always execute
```

---

# 13. Handling Missing Files

A common Data Analyst problem is a missing dataset.

```python
try:

    with open("sales.csv", "r") as file:

        data = file.read()


except FileNotFoundError:

    print("Sales file was not found")
```

The program handles the missing file instead of immediately crashing.

---

# 14. File Processing with finally

```python
try:

    with open("sales.csv", "r") as file:

        data = file.read()

        print("Sales file loaded successfully")


except FileNotFoundError:

    print("Sales file was not found")


finally:

    print("File processing attempt completed")
```

---

# 15. Handling Division by Zero

Suppose:

```python
revenue = 850000

orders = 0
```

Calculate AOV safely:

```python
try:

    average_order_value = revenue / orders


except ZeroDivisionError:

    average_order_value = 0

    print("Warning: Orders are zero")


print(
    f"Average Order Value: ₹{average_order_value:,.2f}"
)
```

---

# 16. Handling Invalid Customer Data

```python
customer_age = "Unknown"

try:

    customer_age = int(customer_age)


except ValueError:

    customer_age = None

    print("Invalid Customer Age")
```

---

# 17. Handling Missing Dictionary Keys

Consider:

```python
business_data = {
    "Revenue": 850000,
    "Profit": 230000
}
```

This causes an error:

```python
print(business_data["Orders"])
```

Handle it:

```python
try:

    orders = business_data["Orders"]


except KeyError:

    orders = 0

    print("Orders KPI is missing")
```

For simple dictionary lookups, this is often cleaner:

```python
orders = business_data.get("Orders", 0)
```

Do not use exception handling when a simpler solution already exists.

---

# 18. Handling Invalid List Index

```python
monthly_sales = [
    850000,
    920000,
    780000
]

try:

    print(monthly_sales[10])


except IndexError:

    print("Requested sales month does not exist")
```

---

# 19. raise Statement

`raise` allows you to intentionally create an exception.

Example:

```python
sales = -50000

if sales < 0:

    raise ValueError("Sales cannot be negative")
```

Output:

```text
ValueError: Sales cannot be negative
```

---

# 20. Why Use raise?

Python may consider some data technically valid even when it violates business rules.

Example:

```python
profit_margin = 150
```

Python accepts this number.

But your business requirement may say:

```text
Profit Margin must be between -100 and 100.
```

Use `raise`:

```python
if profit_margin < -100 or profit_margin > 100:

    raise ValueError(
        "Profit Margin is outside the valid range"
    )
```

`raise` is useful for enforcing business rules.

---

# 21. Validate Sales Data Using raise

```python
def validate_sales(sales):

    if sales is None:

        raise ValueError(
            "Sales value cannot be missing"
        )

    if sales < 0:

        raise ValueError(
            "Sales value cannot be negative"
        )

    return sales
```

Use:

```python
sales = validate_sales(850000)

print(sales)
```

---

# 22. Handling a Raised Exception

```python
def validate_sales(sales):

    if sales is None:

        raise ValueError(
            "Sales value cannot be missing"
        )

    if sales < 0:

        raise ValueError(
            "Sales cannot be negative"
        )

    return sales


try:

    sales = validate_sales(-50000)


except ValueError as error:

    print(f"Data Validation Error: {error}")
```

---

# 23. Capturing Exception Messages

Use:

```python
except ValueError as error:
```

Example:

```python
try:

    sales = float("Invalid")


except ValueError as error:

    print(f"Error: {error}")
```

The variable:

```text
error
```

contains information about what went wrong.

This is useful for debugging and logging.

---

# 24. Custom Exceptions

Custom exceptions allow you to create errors specifically for your application or business rules.

Create a custom exception:

```python
class InvalidSalesError(Exception):

    pass
```

Raise it:

```python
sales = -50000

if sales < 0:

    raise InvalidSalesError(
        "Sales cannot be negative"
    )
```

---

# 25. Custom Exception Example

```python
class InvalidSalesError(Exception):

    pass


def validate_sales(sales):

    if sales < 0:

        raise InvalidSalesError(
            "Negative sales values are not allowed"
        )

    return sales
```

Use:

```python
try:

    sales = validate_sales(-50000)


except InvalidSalesError as error:

    print(f"Sales Validation Error: {error}")
```

---

# 26. When to Use Custom Exceptions

Use custom exceptions when:

- You are building a larger application
- You need clear business-specific errors
- Different validation errors require different handling

Examples:

```text
InvalidSalesError

MissingCustomerDataError

InvalidProfitMarginError

ReportGenerationError
```

For small scripts, built-in exceptions such as `ValueError` are usually enough.

Do not create custom exceptions just to make simple code look advanced.

---

# 27. Safe Profit Margin Function

```python
def calculate_profit_margin(revenue, cost):

    try:

        profit = revenue - cost

        profit_margin = (
            profit / revenue
        ) * 100

        return profit_margin


    except ZeroDivisionError:

        return 0
```

Use:

```python
margin = calculate_profit_margin(0, 50000)

print(f"Profit Margin: {margin:.2f}%")
```

---

# 28. Better KPI Validation

A stronger approach is to validate the data before calculation.

```python
def calculate_profit_margin(revenue, cost):

    if revenue <= 0:

        raise ValueError(
            "Revenue must be greater than zero"
        )

    profit = revenue - cost

    return (profit / revenue) * 100
```

Handle the exception:

```python
try:

    margin = calculate_profit_margin(
        0,
        50000
    )


except ValueError as error:

    print(f"KPI Error: {error}")
```

This is often better than silently returning incorrect or misleading values.

---

# 29. Safe Sales Data Processing

```python
sales_data = [
    "850000",
    "920000",
    None,
    "Invalid",
    "780000"
]

cleaned_sales = []

for sales in sales_data:

    try:

        sales = float(sales)

        cleaned_sales.append(sales)


    except (TypeError, ValueError):

        print(
            f"Skipping Invalid Sales Value: {sales}"
        )
```

Display:

```python
print(cleaned_sales)
```

Output:

```text
[850000.0, 920000.0, 780000.0]
```

This is an important Data Analyst pattern:

```text
Read Value
    ↓
Attempt Conversion
    ↓
Valid?
 ↙       ↘
Yes       No
 ↓         ↓
Process   Handle / Skip
```

---

# 30. Safe File Processing Workflow

```python
import csv


try:

    with open("sales.csv", "r") as file:

        reader = csv.DictReader(file)

        total_sales = 0


        for row in reader:

            try:

                sales = float(row["Sales"])

                total_sales += sales


            except (ValueError, TypeError):

                print(
                    f"Skipping Invalid Row: {row}"
                )


except FileNotFoundError:

    print("Error: sales.csv was not found")


else:

    print(
        f"Total Sales: ₹{total_sales:,.2f}"
    )


finally:

    print("Sales processing completed")
```

This handles:

- Missing files
- Invalid sales values
- Incomplete data
- Successful report calculation
- Process completion

---

# 31. Real-World Automated Reporting Scenario

## Business Requirement

An automated sales report should:

- Load a sales file
- Handle a missing file
- Handle missing sales values
- Handle invalid numbers
- Prevent division by zero
- Skip bad records
- Calculate business KPIs
- Complete the reporting process without unnecessary crashes

---

# 32. Automated Report with Exception Handling

```python
import csv


total_sales = 0

total_orders = 0

valid_records = 0

invalid_records = 0


try:

    with open("sales.csv", "r") as file:

        reader = csv.DictReader(file)


        for row in reader:

            try:

                sales = float(row["Sales"])

                orders = int(row["Orders"])


                if sales < 0:

                    raise ValueError(
                        "Negative sales value"
                    )


                if orders < 0:

                    raise ValueError(
                        "Negative order count"
                    )


                total_sales += sales

                total_orders += orders

                valid_records += 1


            except (
                ValueError,
                TypeError,
                KeyError
            ) as error:

                invalid_records += 1

                print(
                    f"Skipping Invalid Record: {error}"
                )


except FileNotFoundError:

    print(
        "Report Failed: sales.csv was not found"
    )


else:

    try:

        average_order_value = (
            total_sales / total_orders
        )


    except ZeroDivisionError:

        average_order_value = 0


    print("=" * 55)

    print("AUTOMATED SALES REPORT")

    print("=" * 55)

    print(
        f"Total Sales: ₹{total_sales:,.2f}"
    )

    print(
        f"Total Orders: {total_orders}"
    )

    print(
        f"Average Order Value: ₹{average_order_value:,.2f}"
    )

    print(
        f"Valid Records: {valid_records}"
    )

    print(
        f"Invalid Records: {invalid_records}"
    )

    print("=" * 55)


finally:

    print("Report processing completed")
```

---

# 33. Do Not Overuse Exception Handling

Bad practice:

```python
try:

    result = 10 + 20

except:

    print("Error")
```

There is no realistic reason for this calculation to fail.

Use exception handling for operations that can reasonably fail:

- File access
- User input
- Data type conversion
- External data
- Division
- Business validation

Exception handling should solve real problems, not wrap every line of code.

---

# 34. Avoid Bare except

Avoid:

```python
try:

    sales = float(value)

except:

    print("Error")
```

This catches every exception and can hide real programming bugs.

Prefer:

```python
try:

    sales = float(value)

except (TypeError, ValueError):

    print("Invalid Sales Value")
```

Catch the exceptions you actually expect.

---

# 35. Do Not Silently Ignore Errors

Avoid:

```python
try:

    sales = float(value)

except ValueError:

    pass
```

This hides the problem completely.

Better:

```python
try:

    sales = float(value)

except ValueError:

    print(
        f"Invalid Sales Value: {value}"
    )
```

In real projects, errors may be written to logs instead of printed.

---

# 36. Most Important Concepts

## Handle Expected Errors

```python
try:
    operation()

except SpecificError:
    handle_error()
```

## Handle Invalid Numbers

```python
except (TypeError, ValueError):
```

## Handle Missing Files

```python
except FileNotFoundError:
```

## Handle Division by Zero

```python
except ZeroDivisionError:
```

## Execute Code After Success

```python
else:
```

## Always Execute Cleanup or Completion Logic

```python
finally:
```

## Enforce Business Rules

```python
raise ValueError("Invalid business data")
```

## Create Business-Specific Exceptions

```python
class InvalidSalesError(Exception):

    pass
```

---

# 37. Core Patterns to Remember

## Invalid Number Handling

```python
try:

    sales = float(value)

except (TypeError, ValueError):

    sales = 0
```

## Missing File Handling

```python
try:

    with open("sales.csv", "r") as file:

        data = file.read()

except FileNotFoundError:

    print("File Not Found")
```

## Division by Zero Handling

```python
try:

    result = revenue / orders

except ZeroDivisionError:

    result = 0
```

## Business Validation

```python
if sales < 0:

    raise ValueError(
        "Sales cannot be negative"
    )
```

## Process Valid Data and Skip Bad Data

```python
for value in data:

    try:

        value = float(value)

    except (TypeError, ValueError):

        continue
```

---

# 38. Common Beginner Errors

## Using Bare except Everywhere

Avoid:

```python
except:
```

Prefer specific exceptions:

```python
except ValueError:
```

---

## Using try for Every Line

Exception handling should be focused around code that may realistically fail.

---

## Hiding Errors with pass

Avoid silently ignoring important data-quality problems.

---

## Returning Zero for Every Error

Sometimes returning `0` creates misleading analytics results.

Depending on the business requirement, better options may be:

- `None`
- Skip the record
- Log the error
- Raise an exception
- Stop the report

The correct decision depends on the business requirement.

---

## Confusing raise and except

Remember:

```text
raise
→ Create / Trigger an Exception

except
→ Handle an Exception
```

---

# 39. Interview Questions

1. What is an exception?
2. Why is exception handling important for Data Analysts?
3. What does `try` do?
4. What does `except` do?
5. Why should you catch specific exceptions?
6. What is `ValueError`?
7. What is `TypeError`?
8. What is `ZeroDivisionError`?
9. What is `FileNotFoundError`?
10. What is the purpose of `else`?
11. What is the purpose of `finally`?
12. What is the difference between `else` and `finally`?
13. How would you handle invalid sales values?
14. How would you handle missing data files?
15. How would you prevent division-by-zero errors?
16. What does `raise` do?
17. Why would a Data Analyst use `raise`?
18. What is a custom exception?
19. When should custom exceptions be used?
20. Why should bare `except` usually be avoided?
21. Why is silently ignoring errors dangerous?
22. How would you process valid records while skipping invalid records?
23. How would you ensure an automated report handles bad data?
24. Should every error be replaced with zero? Why not?
25. How would you design a reliable sales data processing workflow?

---

# 40. Completion Checklist

Before moving to the next module, you should be able to:

- [ ] Explain exceptions
- [ ] Use `try`
- [ ] Use `except`
- [ ] Catch specific exceptions
- [ ] Handle `ValueError`
- [ ] Handle `TypeError`
- [ ] Handle `ZeroDivisionError`
- [ ] Handle `FileNotFoundError`
- [ ] Handle `KeyError`
- [ ] Handle `IndexError`
- [ ] Handle multiple exceptions
- [ ] Use `else`
- [ ] Use `finally`
- [ ] Explain `else` vs `finally`
- [ ] Handle missing sales values
- [ ] Handle invalid numeric values
- [ ] Handle missing files
- [ ] Prevent division-by-zero failures
- [ ] Capture exception messages
- [ ] Use `raise`
- [ ] Validate business rules
- [ ] Create a basic custom exception
- [ ] Explain when custom exceptions are useful
- [ ] Avoid bare `except`
- [ ] Avoid silently hiding errors
- [ ] Process valid records while skipping bad records
- [ ] Build a reliable automated reporting workflow

---

# Final Outcome

After completing Exception Handling, you should be able to handle missing sales values, invalid numbers, missing files, division-by-zero errors, and incomplete business data; enforce data-quality rules using `raise`; create basic custom exceptions; and build more reliable automated reporting workflows that handle expected data problems without unnecessary program failures.