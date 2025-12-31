# Example Data

This folder contains minimal example data files to demonstrate how the popcorn
sales allocation notebook works.

## Files

- **shifts.csv** - Scout shift assignments for Sept 13, 2025
- **sales.csv** - Corresponding storefront sales for those shifts

## How to Use

To test the notebook with example data:

1. Copy the files from this folder to the `data/` folder:
   ```bash
   cp data-example/* data/
   ```

2. Run the notebook normally

## Example Results

With this example data, you should see:
- **Jordan T**: $100 total share → $35.00 (35%)
- **Alex M**: $82.50 total share → $28.87 (35%)
- **Casey L**: $27.50 total share → $9.62 (35%)
