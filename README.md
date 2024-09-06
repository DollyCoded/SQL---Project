# Nashville Housing Data Cleaning Project

This project focuses on cleaning and transforming a dataset of Nashville housing data using SQL. The aim is to standardize the data format, handle missing values, split addresses into components, normalize field values, and remove duplicates to prepare the dataset for further analysis.

## Key Data Cleaning Steps

### 1. Standardizing the Date Format

- **Purpose:** Ensure all dates are in a consistent format to facilitate analysis.
- **Method:** Use the `CONVERT` function to change the `SaleDate` field to a standard date format.
- **Fallback:** If the direct update fails, add a new column (`SaleDateConverted`) and store the converted date values there.

### 2. Populating Missing Property Address Data

- **Purpose:** Fill in missing values in the `PropertyAddress` field using existing data.
- **Method:** Perform a self-join on the `ParcelID` to find matching records with non-null addresses and update the missing addresses accordingly.

### 3. Breaking Out Address into Individual Columns

- **Purpose:** Split the `PropertyAddress` and `OwnerAddress` fields into separate components such as Address, City, and State.
- **Method:** Use string manipulation functions (`SUBSTRING` and `PARSENAME`) to extract individual components and create new columns (`PropertySplitAddress`, `PropertySplitCity`, `OwnerSplitAddress`, `OwnerSplitCity`, `OwnerSplitState`).

### 4. Normalizing Boolean Fields

- **Purpose:** Standardize the values in the `SoldAsVacant` field from 'Y'/'N' to 'Yes'/'No'.
- **Method:** Apply a `CASE` statement to transform the field values accordingly.

### 5. Removing Duplicate Records

- **Purpose:** Identify and remove duplicate records to ensure data quality.
- **Method:** Use a Common Table Expression (CTE) with the `ROW_NUMBER` window function to assign a row number to each record, partitioned by key fields (`ParcelID`, `PropertyAddress`, `SalePrice`, `SaleDate`, `LegalReference`). Delete records with a row number greater than 1.

### 6. Deleting Unused Columns

- **Purpose:** Clean up the dataset by removing columns that are no longer necessary for analysis.
- **Method:** Use the `ALTER TABLE` statement to drop redundant columns such as `OwnerAddress`, `TaxDistrict`, `PropertyAddress`, and `SaleDate`.

## Additional Steps for Data Import

### Importing Data using `OPENROWSET` and `BULK INSERT`

- **Purpose:** Load data from external files (like CSV or Excel) directly into the SQL database.
- **Method:** Configure the SQL server to allow `OPENROWSET` and `BULK INSERT`. Utilize these commands to import data from specified file paths.
- **Note:** Proper server configuration is required, including setting permissions and enabling necessary options.

## Summary

This project demonstrates various SQL data cleaning techniques, such as standardizing date formats, handling missing data, splitting address fields, normalizing field values, and removing duplicates. The cleaned dataset is now ready for more detailed analysis, such as property sales trends, market evaluations, and other real estate insights.

## Next Steps

- Use the cleaned dataset for analysis and visualization in tools like Power BI or Tableau.
- Explore further optimization and automation of data cleaning processes using advanced SQL features or other ETL tools.
- Share insights and findings based on the cleaned dataset to stakeholders or in reports.

## Resources

- [SQL Documentation](https://docs.microsoft.com/en-us/sql/)
- [SQL Server Functions](https://docs.microsoft.com/en-us/sql/t-sql/functions/)
