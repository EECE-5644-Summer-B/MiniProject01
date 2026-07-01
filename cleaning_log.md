# Cleaning Log

## Dropped Rows

The original data set had several errors in the original `Description`, `UnitPrice`, and `CustomerID` fields. We handled these in the following ways:
- Rows with invalid `Description` values (e.g., transactions with no description) were dropped. Because these rows comprised such a small section of the data set, were correlated with other errors including invalid `UnitPrice` and `CustomerID` fields, and irrevocably destroyed useful market information, the decision was made to to remove these data from the set.
- Rows with `UnitPrice` fields were very strongly correlated with malformed entries, and constituted a negligible percentage of total transactions, and so were similarly dropped.
- Due to containing largely redundant information, the `StockCode` column was dropped.

## Kept Rows

- The biggest decision in this data set was the handling of rows with invalid or missing `CustomerID` fields, as they comprised nearly a quarter of the total data set. Though missing information as to exactly whom we sold their associated items, the `Description` and `Country` fields for the vast majority of such entries were intact, and thus these entries still provided useful market information, even though we were unable to recover the exact customers. Hence, so as to not sacrifice this useful data for a marginal increase in information breadth, the decision was made to keep all such entries and convert them to a sentinel value of `0.0`.
- Rows with invalid or missing `Country` entries were similarly kep, as they still provide information of per-item revenue and general trends.

## Changed Entries

In order to unify the format of the table, the following changes were made:
- All column titles were changed to snake case.
- All `Description` entries were changed to title case.
- All `InvoiceDate` fields were changed to ISO-8601 format.
- All `Country` entries were changed to long-format official names.

## Added Entries

In order to facilitate analysis, the following entries were added:
- To easily gauge revenue generation, the `Quantity` and `UnitPrice` columns were combined and merged into the database as a `Revenue` column.
- To more easily analyze market trends, the `Country` column was consolidated into a broader `Region` column following ISO-3166 and merged into the database.
