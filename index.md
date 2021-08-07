## SQL - CAST and REPLACE - Converting string price to decimal

Database: SQLite

Thanks to https://sqliteonline.com/ which offers us a platform to explore SQL.

The page is written to answer queries around converting string prices to decimals for calculations / analytics. In general a price column should never have a string data type but due to the existing source database design data engineers / analysts face some challenges during transformations.
So, let us get into action.

Below is the sample table definition created with only two columns orderid and price. Our focus will be on price primarily which has been intentionally defined as varchar with length 10.

![image](https://user-images.githubusercontent.com/83854194/128607082-531b12ff-3e99-4531-89b5-d6af545d14f3.png)

The table is populated with 5 records below and notice the currency ("$") before the value. For this example we consider that all orders placed are in single currency. For the scenario where we have the orders placed in different currencies the best approach is to first convert the price to a common currency and then perform CAST / REPLACE.

![image](https://user-images.githubusercontent.com/83854194/128607153-ffb96643-414c-4ca4-8cfe-7611a733e666.png)

Now, let us assume you need the sum of the column "price". This is not straight forward considering the type is varchar(10).
CAST and REPLACE to the rescue,
- CAST has the potential to convert data types
- REPLACE, as the name suggests, helps with replacing sub-strings with the value we need

Applying the functions, we get the output below showing SUM of the price column.

![image](https://user-images.githubusercontent.com/83854194/128607430-834f6909-ddfc-4d17-b50e-3d5a17416371.png)

Let us break this down,
- the inner function REPLACE(<column name>, <sub-string to replace>, <what to replace with?>) is used to replace $ with empty. After this operation, the data type of the column is still varchar
- the outer function CAST(<column name> AS <to-be data type>) is used to convert the type. After this operation, the varchar price is converted to decimal of length 15 and 2 decimal places

And we got the expected outcome :)
