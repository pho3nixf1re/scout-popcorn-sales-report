# Popcorn Sales Reports

This project analyzes and allocates popcorn fundraiser sales among scouts based
on shift participation.

## Project Overview

The notebook processes popcorn sales data and calculates each scout's share
based on:
- **Sales Date**: Uses the "Date Taken" field as the authoritative sales date
- **Shift Matching**: Matches sales to shifts by date and time
- **Equal Split**: Divides shift sales equally among all scouts present during
  that shift
- **Pack Percentage**: Applies the Pack's 35% share to calculate amounts owed to
  scouts

## Inputs

The following CSV files are required in the `data/` directory. The files
are derived from the Trail's End sales and shift reports. The raw files are in
xlsx format and must be exported to CSV. Delete any extraneous header rows
such as the report title and spacing rows. Only include the headers as the first
row.

### shifts.csv
Contains scout shift assignments at various sites.

**Columns:**
- `Date` - Shift date (YYYY-MM-DD format)
- `Site Name` - Location name (e.g., "Lowe's", "Bass Pro Shops")
- `Address Line 1` - Site address
- `Shift` - Time slot in format "HH:MM AM/PM - HH:MM AM/PM US/Central"
- `Scout Name` - Scout's name
- `Scout Code` - Unique scout identifier
- `Scout Email` - Scout's email address
- `Scout Phone` - Scout's phone number

**Notes:**
- Rows with blank scout fields indicate assigned shifts with no scouts present
- Multiple scouts can be assigned to the same shift

### sales.csv
Contains all sales transactions including storefront, online, and wagon sales.

**Key Columns:**
- `Order Number` - Unique transaction ID
- `Scout` - Scout who made the sale
- `Scout Code` - Unique scout identifier
- `Total Order Amount` - Sale amount in dollars (format: "$XX.XX")
- `Sale Type` - Type of sale: "Storefront", "Wagon", "Online", etc.
- `Date Taken` - Date of sale (YYYY-MM-DD format, **authoritative date field**)
- `Shift` - Time slot (format: "HH:MM:SS AM/PM - HH:MM:SS AM/PM")
- `Site Name` - Location where sale occurred
- Additional customer information fields

**Notes:**
- The notebook filters to include only "Storefront" sales
- Non-storefront sales (Online, Wagon) are excluded from allocation

## Environment Setup

See dev container for a portable development environment. Otherwise here are the
requirements for local setup.

### Prerequisites
- Python 3.11+
- pip (Python package manager)

### Local Installation

1. **Clone or download the repository**

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the notebook:**
   ```bash
   jupyter notebook popcorn_sales_allocation.ipynb
   ```

### Docker / Dev Container

For a portable containerized environment:

1. **Install Docker** on your system and the **Dev Containers** extension in VS
   Code

2. **Open the project in VS Code** and select "Reopen in Container" from the
   command palette

3. **The dev container will:**
   - Automatically install all dependencies
   - Set up Python 3.11 environment
   - Configure Jupyter port forwarding (port 8888)
   - Install Python and Jupyter VS Code extensions

## Usage

1. Open the notebook in Jupyter
2. Run the **Configuration cell** (cell 2) which displays interactive text input widgets:
   - **Shifts file**: Path or URL to shifts.csv (default: `data-example/shifts.csv`)
   - **Sales file**: Path or URL to sales.csv (default: `data-example/sales.csv`)
   - Edit these values directly in the text boxes before continuing
3. Run remaining cells sequentially to:
   - Load and clean shift data
   - Load and clean sales data
   - Match sales to shifts
   - Calculate per-scout allocation
   - Apply the 35% Pack share
4. Final output displays as CSV format for easy copying

### Acceptable Input Values

The configuration widgets accept:
- **Local paths**: `data/shifts.csv`, `data-example/shifts.csv`, or absolute paths like `C:/path/to/shifts.csv` (Windows) or `/home/user/path/to/shifts.csv` (Linux/Mac).
- **URLs**: `https://example.com/popcorn/shifts.csv` (any HTTP/HTTPS URL).
- Mixed sources are supported (e.g., local shifts file with remote sales file).

## Output

The notebook generates:
- `scout_totals` - Total allocated sales per scout (100% of shift share)
- `scout_totals_pct` - Amount owed per scout (35% of shift share for Pack)

The final output is displayed in CSV format for easy copying and exporting.

## Project Structure

```
.
├── popcorn_sales_allocation.ipynb  # Main analysis notebook
├── data/                           # Input CSV files (not in version control)
│   ├── .gitkeep                    # Preserves folder structure in git
│   ├── shifts.csv                  # Your production data
│   └── sales.csv                   # Your production data
├── data-example/                   # Example data for testing
│   ├── shifts.csv                  # Sample shifts data
│   ├── sales.csv                   # Sample sales data
│   └── README.md                   # Example data documentation
├── requirements.txt                # Python dependencies
├── README.md                       # This file
├── .gitignore                      # Files excluded from git
└── .devcontainer/                  # Dev container configuration
    └── devcontainer.json
```

## Notes

- All date comparisons use the Date Taken field from sales data as
  authoritative.
- Shift times are normalized by removing timezone information and seconds for
  matching purposes.

## Dependencies

See `requirements.txt` for pinned versions for `pip`.
