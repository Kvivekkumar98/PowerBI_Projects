# Sales Performance Data Analysis & Dashboard

### Dashboard Link : https://github.com/Kvivekkumar98/PowerBI_Projects/blob/main/PowerBI_Dashboard_snap.JPG

## Problem Statement

A retail business faced challenges in tracking sales performance across multiple dimensions, including product brands, regions, and states. Due to manual reporting limitations, decision-makers lacked real-time insights into key metrics such as:

Total Revenue – Difficulty in analyzing revenue trends and meeting sales targets.
Product Performance – Identifying the most and least profitable brands.
Regional Sales Distribution – Understanding revenue contributions from different geographic locations.
State-wise Transactions – Visualizing transaction volume and identifying high-performing areas.


### Steps followed 

- Step 1 : Extract data from the file using Power BI Desktop, Here all our dataset are in csv files.

- Step 2 : As data needs cleaning we click on load and transform so a power query editor is opened.

  - Customer's Table.

          - Check the data type of each column header in the Customer's table.

          - Since we need the full name of the customer, select the 'First_name' and 'Last_name' columns. Then, click on 'Add Column' and choose 'Merge Columns'. Add a separator and rename the new column as 'Full_Name'.

          - To get the birth year of the customer, we need to extract the year from the birthdate. Under 'Add Column' in the 'Date' section, select 'Year' and then choose 'Year' under 'Year.

          - To determine if the customer has any children, select 'total_children' under 'Add Column' in the 'Conditional Column' section, and rename it as 'Has_children'. In the 'If' statement, choose 'total_children' for the operator, set it to 'is greater than' with a value of '0', and output 'Y', output 'N' in else.

  - Product's Table.

          - Check the data type of each column header in the Product's table.

          - To add a 'Discounted_price' column, select 'product_retail_price' and click on 'Add Column.' Under the 'Standard' section, click on 'Percentage' and enter a value of 90 to apply the discount. Then, under the 'Transform' tab, use the 'Round' section to round the result to 2 decimal places.

  - Stores Table.

          - Check the data type of each column header in the Stores table.

  - Regions Table.

          - Check the data type of each column header in the Regions table.

  - Calender Table.

          - Check the data type of each column header in the Calender table.

          - Select the 'Date' column, then under the 'Add Column' tab in the 'Date' section, choose 'Week' and select 'Start of Week'.

          - Select the 'Date' column, then under the 'Add Column' tab in the 'Date' section, choose 'Day' and select 'Name of the Day'.

          - Select the 'Date' column, then under the 'Add Column' tab in the 'Date' section, choose 'Month' and select 'Start of Month'.

          - Select the 'Date' column, then under the 'Add Column' tab in the 'Date' section, choose 'Month' and select 'Name of Month'.

          - Select the 'Date' column, then under the 'Add Column' tab in the 'Date' section, choose 'Quarter' and select 'Quarter of Year'.

          - Select the 'Date' column, then under the 'Add Column' tab in the 'Date' section, choose 'Year' and select 'Year'.

 - Returns Table.

          - Check the data type of each column header in the Returns table.

 - Transactions Table.

          - In 'New Source,' click on 'More.' From the options, select 'Folder' and click on 'Connect.' In the folder path field, enter the path of the folder and then click on 'Combine & Transform Data.

          - Check the data type of each column header in the Transactions table.

- Step 3 : After transforming all the data, click on 'Close & Apply' to load the entire dataset into Power BI.
- Step 4 : To maintain the relationship between tables, we use modeling in Power BI.

  - In the Model view, create a new relationship between the 'Customer' and 'Transaction' tables by using 'Customer ID' as the common field, and then connect the tables. This forms a one-to-many relationship.

  - In the Model view, create a new relationship between the 'Products' and 'Transaction' tables by using 'Product ID' as the common field, with 'Product ID' as the primary key in the 'Products' table and as the foreign key in the 'Transaction' table. This forms a one-to-many relationship.

  - In the Model view, create a new relationship between the 'Stores' and 'Transaction' tables by using 'Store ID' as the common field, with 'Store ID' as the primary key in the 'Stores' table and as the foreign key in the 'Transaction' table which forms a one-to-many relationship.

  - In the Model view, create a new relationship between the 'Calendar' and 'Transaction' tables. 'Date' as the primary key in the 'Calendar' table and 'Transaction Date' as the foreign key in the 'Transaction' table. This forms a one-to-many relationship.

  - In the Model view, create a new relationship between the 'Products' and 'Returns' tables by using 'Product ID' as the common field. This forms a one-to-many relationship.

  - In the Model view, create a new relationship between the 'Stores' and 'Returns' tables by using 'Store ID' as the common field. This forms a one-to-many relationship.

  - In the Model view, create a new relationship between the 'Calendar' and 'Returns' tables. 'Date' as the primary key in the 'Calendar' table and 'Return Date' as the foreign key in the 'Transaction' table. This forms a one-to-many relationship.

  - In the Model view, create a new relationship between the 'Regions' and 'Stores' tables. 'Store ID' as the primary key in the 'Regions' table and as the foreign key in the 'Stores' table. This forms a one-to-many relationship.

 - Step 5 : New measure was created to find  the 'Quantity_Sold',
 
 Following DAX expression was written to find 'Quantity_Sold',
 
         Quantity_Sold = SUM(Transactions[quantity])

 - Step 6 : New measure was created to find  the 'Quantity_Returned',
 
 Following DAX expression was written to find 'Quantity_Returned',
 
         'Quantity_Returned' = SUM(Returns[quantity])

 - Step 7 : New measure was created to find  the 'Quantity_Returned',
 
 Following DAX expression was written to find 'Total_Transactions',
 
         'Total_Transactions' = COUNTA(Transactions[transaction_date])

 - Step 8 : New measure was created to find  the 'Total_Returns',
 
 Following DAX expression was written to find 'Total_Returns',
 
         'Total_Returns' = COUNTA(Returns[Return_date])
Snap of new calculated column ,

![Image](https://github.com/user-attachments/assets/a4b0ae2d-dcbb-4465-a43e-80fe1c72d596)

 - Step 9 : New measure was created to find  the 'All_Transactions',
 
 Following DAX expression was written to find 'Total_Returns',
 
         'All_Transactions' = CALCULATE([Total_Transactions], ALL(Transactions))

 - Step 10 : New measure was created to find  the 'All_Retruns',
 
 Following DAX expression was written to find 'All_Retruns',
 
         'All_Retruns' = CALCULATE([Total_Returns], ALL(Returns))

 - Step 11 : New measure was created to find  the 'Total_Revenue',
 
 Following DAX expression was written to find 'Total_Revenue',
 
         'Total_Revenue' = SUMX(Transactions, Transactions[quantity]*RELATED(Products[product_retail_price]))
Snap of new calculated column ,

![Image](https://github.com/user-attachments/assets/9d46e989-8eb6-4f05-9a18-59e24b3e22c4)

 - Step 12 : New measure was created to find  the 'Total_Cost',
 
 Following DAX expression was written to find 'Total_Cost',
 
         'Total_Cost' = SUMX(Transactions, Transactions[quantity]*RELATED(Products[product_cost]))

 - Step 13 : New measure was created to find  the 'Total_Profit',
 
 Following DAX expression was written to find 'Total_Profit',
 
         'Total_Profit' = [Total_Revenue]-[Total_Cost]
Snap of new calculated column ,

![Image](https://github.com/user-attachments/assets/bf435120-69ee-4fa5-881c-e4d84f8dd330)

 - Step 14 : New measure was created to find  the 'Profit_Margin' it has to convert into percentage by using %,
 
 Following DAX expression was written to find 'Profit_Margin',
 
         'Profit_Margin' = [Total_Profit]/ [Total_Revenue]

 - Step 15 : New measure was created to find  the 'Unique_Products',
 
 Following DAX expression was written to find 'Unique_Products',
 
         'Unique_Products' = DISTINCTCOUNT(Products[products_id])

 - Step 16 : New measure was created to find  the 'YTD_Revenue',
 
 Following DAX expression was written to find 'YTD_Revenue',
 
         'YTD_Revenue' = CALCULATE([Total_Revenue],DATESYTD(Calendar[date]))

 - Step 17 : New measure was created to find  the 'Previous_Month_Transactions',
 
 Following DAX expression was written to find 'Previous_Month_Transactions',
 
         'Previous_Month_Transactions' = CALCULATE([Total_Transactions],PREVIOUSMONTH(Calendar[date]))

 - Step 18 : New measure was created to find  the 'Previous_Month_Transactions',
 
 Following DAX expression was written to find 'Previous_Month_Transactions',
 
         'Previous_Month_Transactions' = CALCULATE([Total_Transactions],PREVIOUSMONTH(Calendar[date]))

 - Step 19 : New measure was created to find  the 'Previous_Month_Revenue',
 
 Following DAX expression was written to find 'Previous_Month_Revenue',
 
         'Previous_Month_Revenue' = CALCULATE([Total_Revenue],PREVIOUSMONTH(Calendar[date]))

 - Step 20 : New measure was created to find  the 'Previous_Month_Profit',
 
 Following DAX expression was written to find 'Previous_Month_Profit',
 
         'Previous_Month_Profit' = CALCULATE([Total_Profit],PREVIOUSMONTH(Calendar[date]))

 - Step 21 : New measure was created to find  the 'Previous_Month_Returns',
 
 Following DAX expression was written to find 'Previous_Month_Returns',
 
         'Previous_Month_Returns' = CALCULATE([Quantity_Returned],PREVIOUSMONTH(Calendar[date]))

 
 # Report Snapshot (Power BI DESKTOP)

 
![Image](https://github.com/user-attachments/assets/e9db0620-8bdd-4562-a38a-eae6d6660e85)
