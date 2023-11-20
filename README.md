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
