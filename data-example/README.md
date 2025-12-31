# Example Data

This folder contains minimal example data files to demonstrate how the popcorn
sales allocation notebook works.

## Files

- **shifts.csv** - Scout shift assignments for Sept 13, 2025
- **sales.csv** - Corresponding storefront sales for those shifts

## How to Use

This example data is the **default data source** for the notebook. When you run
the configuration cell, the input widgets are pre-populated with:
- Shifts file: `data-example/shifts.csv`
- Sales file: `data-example/sales.csv`

Simply run the notebook as-is to analyze this example data, or modify the file
paths in the configuration cell to use different data sources.

## Example Results

With this example data, you should see:
- **Jordan T**: $100 total share → $35.00 (35%)
- **Alex M**: $82.50 total share → $28.87 (35%)
- **Casey L**: $27.50 total share → $9.62 (35%)
