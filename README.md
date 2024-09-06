# Data Cleaning Project in SQL

This project demonstrates various data cleaning techniques using SQL to prepare a Nashville Housing dataset for analysis. The goal is to standardize, normalize, and refine the data to ensure accuracy and completeness.

## Standardizing the Date Format

- **Purpose:**
  - Ensure that all dates in the dataset are in a consistent format. This is crucial for reliable analysis, sorting, filtering, and joining with other datasets that may use date fields.

- **Method:**
  - Use the SQL `CONVERT` function to change the `SaleDate` field to a standard date format.
  - If the direct update fails due to data type constraints, a new column (`SaleDateConverted`) is created to store the formatted date values.

- **Note:**
  - Ensure that the `SaleDate` field is of the correct data type (`Date` or `Datetime`). The data may contain inconsistencies or formatting issues that need additional handling.

## Populating Missing Property Address Data

- **Purpose:**
  - Fill in missing values in the `PropertyAddress` field to improve data completeness and accuracy. Missing address data can negatively affect analyses that rely on location-based metrics or mapping.

- **Method:**
  - Use SQL `JOIN` to find and replace null values in `PropertyAddress` by matching `ParcelID` between records.
  - The `ISNULL` function is used to substitute missing values with available data from related records.

- **Note:**
  - Ensuring that all property addresses are correctly populated helps maintain the integrity of location-based analyses.

## Breaking Out Address into Individual Columns

- **Purpose:**
  - Separate the `PropertyAddress` into individual columns for street address, city, and state to allow for more granular analysis and filtering.

- **Method:**
  - Use SQL string functions (`SUBSTRING` and `CHARINDEX`) to extract and populate `PropertySplitAddress`, `PropertySplitCity`, and other columns.
  - Similar logic is applied to `OwnerAddress` to break it into `OwnerSplitAddress`, `OwnerSplitCity`, and `OwnerSplitState`.

- **Note:**
  - This step helps in geospatial analysis, creating visualizations, and ensuring more accessible data manipulation.

## Changing Y/N to Yes/No in "Sold As Vacant" Field

- **Purpose:**
  - Convert ambiguous binary indicators (`Y`/`N`) in the `SoldAsVacant` field to more meaningful values (`Yes`/`No`).

- **Method:**
  - Use a `CASE` statement to update all instances where `SoldAsVacant` is `Y` to `Yes` and `N` to `No`.

- **Note:**
  - Improves data readability and consistency for users and downstream systems.

## Removing Duplicates

- **Purpose:**
  - Identify and remove duplicate records to ensure data accuracy and avoid double-counting in analyses.

- **Method:**
  - Use a Common Table Expression (CTE) with the `ROW_NUMBER` window function to identify duplicate rows based on key fields (`ParcelID`, `PropertyAddress`, `SalePrice`, etc.).
  - Select only unique records for further analysis.

- **Note:**
  - Removing duplicates ensures the dataset remains accurate and reliable for analytical purposes.

## Deleting Unused Columns

- **Purpose:**
  - Remove unnecessary columns that do not contribute to the analysis to optimize the dataset.

- **Method:**
  - Use the `ALTER TABLE` command to drop columns that are redundant or unused, such as `OwnerAddress`, `TaxDistrict`, and `SaleDate`.

- **Note:**
  - Cleaning up the dataset by removing unused columns makes the data easier to understand and work with.

## Importing Data Using OPENROWSET and BULK INSERT

- **Purpose:**
  - Demonstrate advanced data import methods using `OPENROWSET` and `BULK INSERT` to bring data from external files into SQL Server.

- **Method:**
  - Configure the SQL Server appropriately to use these methods.
  - Use `BULK INSERT` for importing CSV files directly.
  - Use `OPENROWSET` to read data from external data sources, like Excel files.

- **Note:**
  - This step requires appropriate server configuration and is more suitable for advanced users who need to import large datasets efficiently.
