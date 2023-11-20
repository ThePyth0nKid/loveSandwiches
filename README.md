# Python Google Sheets Sales Data Project

## Project Overview
This Python project leverages the `gspread` module to interact with Google Sheets. It focuses on managing and analyzing sales data in a spreadsheet named "love_sandwiches". The script allows users to edit and analyze sales data through a simple command-line interface.

## Main Functions and Code

### get_sales_data()
Get sales figures input from the user.Run a while loop to collect a valid string of data from the user via the terminal, which must be a string of 6 numbers separated by commas. The loop will repeatedly request data, until it is valid.

```python
def get_sales_data():
    while True:
        print("Please enter sales data from the last market.")
        print("Data should be six numbers, separated by commas.")
        print("Example: 10,20,30,40,50,60\n")

        # Further code...
```
### validate_data()
Inside the try, converts all string values into integers. Raises ValueError if strings cannot be converted into int, or if there aren't exactly 6 values.

```python
def validate_data(values):
    try:
        [int(value) for value in values]
        if len(values) != 6:
            raise ValueError(
                f"Exactly 6 values required, you provided {len(values)}"
            )
    except ValueError as e:
        print(f"Invalid data: {e}, please try again.\n")
        return False

    # Further code...
```
### update_worksheet()
Receives a list of integers to be inserted into a worksheet. Update the relevant worksheet with the data provided

```python
def update_worksheet(data, worksheet):
    print(f"Updating {worksheet} worksheet...\n")
    worksheet_to_update = SHEET.worksheet(worksheet)
    worksheet_to_update.append_row(data)
    print(f"{worksheet} worksheet updated successfully\n")

    # Further code...
```
### calculate_surplus_data()
Compare sales with stock and calculate the surplus for each item type.

```python
def calculate_surplus_data(sales_row):
    """
    The surplus is defined as the sales figure subtracted from the stock:
    - Positive surplus indicates waste
    - Negative surplus indicates extra made when stock was sold out.
    """
    print("Calculating surplus data...\n")
    stock = SHEET.worksheet("stock").get_all_values()
    stock_row = stock[-1]
    surplus_data = []
    for stock, sales in zip(stock_row, sales_row):
        surplus = int(stock) - sales
        surplus_data.append(surplus)

    return surplus_data
```
### get_last_5_entries_sales ()
Collects columns of data from sales worksheet, collecting the last 5 entries for each sandwich and returns the data as a list of lists.

```python
def get_last_5_entries_sales():
    sales = SHEET.worksheet("sales")
    columns = []
    for ind in range(1, 7):
        column = sales.col_values(ind)
        columns.append(column[-5:])

    return columns
```

### main()
Run all program functions.

```python
def main():
    data = get_sales_data()
    sales_data = [int(num) for num in data]
    update_worksheet(sales_data, "sales")
    new_surplus_data = calculate_surplus_data(sales_data)
    update_worksheet(new_surplus_data, "surplus")


print("Welcome to Love Sandwiches Data Automation")
main()
```

