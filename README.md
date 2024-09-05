# Nashville Housing Data Cleaning Project

This project involves cleaning and transforming a dataset related to Nashville housing using SQL. The goal is to standardize the data, handle missing values, split addresses into meaningful components, and remove duplicates, among other tasks.

## Skills Used

- Data Cleaning
- SQL Functions
- Joins
- Common Table Expressions (CTEs)
- String Manipulation
- Date Formatting
- Data Type Conversion
- Handling Missing Data
- Removing Duplicates
- SQL Server Specific Functions (e.g., `PARSENAME`)

## Data Overview

The dataset, `NashvilleHousing`, contains various columns related to housing sales in Nashville. The data includes fields like `SaleDate`, `PropertyAddress`, `OwnerAddress`, and `SoldAsVacant`, among others. The data cleaning steps performed below aim to ensure the data is consistent, accurate, and ready for analysis.

## Key Data Cleaning Steps

### 1. Standardizing Date Format

- **Purpose:** To standardize the format of the `SaleDate` field.
- **Method:** Use SQL's `CONVERT` function to ensure all dates are stored in a standard date format.
- **Additional Step:** If the direct update fails, a new column `SaleDateConverted` is added to store the converted dates.

### 2. Populating Missing Property Addresses

- **Purpose:** To fill in missing `PropertyAddress` fields based on the `ParcelID`.
- **Method:** Use a self-join to match records with the same `ParcelID` and update missing addresses using available data.

### 3. Splitting Address Components

- **Purpose:** To break down the `PropertyAddress` and `OwnerAddress` fields into individual components (e.g., Address, City, State).
- **Method:** Use string functions like `SUBSTRING` and `PARSENAME` to extract these components and store them in new columns (`PropertySplitAddress`, `PropertySplitCity`, `OwnerSplitAddress`, `OwnerSplitCity`, `OwnerSplitState`).

### 4. Normalizing Boolean Fields

- **Purpose:** To standardize the values in the `SoldAsVacant` field from 'Y'/'N' to 'Yes'/'No'.
- **Method:** Use a `CASE` statement to replace the values.

### 5. Removing Duplicate Records

- **Purpose:** To remove duplicate rows based on specific criteria (`ParcelID`, `PropertyAddress`, `SalePrice`, `SaleDate`, `LegalReference`).
- **Method:** Use a Common Table Expression (CTE) with the `ROW_NUMBER` window function to identify and remove duplicates.

### 6. Deleting Unused Columns

- **Purpose:** To clean up the dataset by removing columns that are no longer needed.
- **Method:** Use the `ALTER TABLE` statement to drop columns like `OwnerAddress`, `TaxDistrict`, `PropertyAddress`, and `SaleDate`.

## Additional Steps for Data Import

### Importing Data using `OPENROWSET` and `BULK INSERT`

- **Purpose:** To import data from external files (like a CSV or Excel file) into the SQL database.
- **Method:** Configure the server to allow `OPENROWSET` and `BULK INSERT`. Then, use these commands to load data from external files into the `NashvilleHousing` table.
- **Note:** These steps require appropriate server configuration, including setting permissions and enabling specific server options.

## Summary

This project demonstrates various SQL techniques for data cleaning and transformation, such as handling missing values, standardizing data formats, splitting strings, and removing duplicates. By the end of the project, the dataset is cleaned and ready for further analysis or reporting.

## Next Steps

- Use the cleaned data for analytical purposes, such as understanding property sales trends in Nashville.
- Integrate the cleaned dataset with visualization tools like Tableau or Power BI to create dashboards and visualizations.
- Explore advanced SQL techniques or tools to further automate and enhance the data cleaning process.
