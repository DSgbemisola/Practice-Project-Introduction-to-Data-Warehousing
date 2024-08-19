# Practice-Project-Introduction-to-Data-Warehousing

This comprehensive hands-on lab is designed to provide hands-on experience in designing and implementing a data warehouse. 

# Senerio

You are a data engineer hired by a consumer electronics retail company. The company sells various electronic products through its online and offline channels across major cities in the United States. They operate multiple stores and warehouses to manage their inventory and sales operations. The company wants to create a data warehouse to analyze its sales performance and inventory management and aim to generate reports, such as:

Total sales revenue per year per city
Total sales revenue per month per city
Total sales revenue per quarter per city
Total sales revenue per year per product category
Total sales revenue per product category per city
Total sales revenue per product category per store

# Software used in the lab

In this lab, you will use PostgreSQL Database. PostgreSQL is a Relational Database Management System (RDBMS) designed to store, manipulate, and retrieve data efficiently.

![image](https://github.com/user-attachments/assets/4903573c-45dc-407d-985e-8d66dd6927f2)

# Learning objectives

After completing this lab, you will be able to:

Develop dimension and fact tables to organize and structure data effectively for analysis
Employ SQL queries to create and load data into dimension and fact tables
Create materialized views to optimize query performance.

# About the Dataset

The dataset you would be using in this assignment is not a real-life dataset. It was programmatically created for this project purpose.

# Phase 1: Design a data warehouse

![image](https://github.com/user-attachments/assets/011c96ca-2c24-4fa6-8358-3e6e94f3cf30)

# Task 1: Design the dimension table MyDimDateTask 1 - Design the dimension table MyDimDate

Write down the fields in the MyDimDate table in any text editor, one field per line. The company is looking at a granularity of day, which means they would like to have the ability to generate the report on a yearly, monthly, daily, and weekday basis.

Here is a partial list of fields to serve as an example:

dateid
month
monthname
…

- Solution
Fields in MyDimDate table:

dateid
year
month
monthname
day
weekday
weekdayname

The table will have a unique identifier (dateid) for each date entry. Other fields such as year, month, monthname, day, weekday, and weekdayname will provide detailed information about each date, allowing for flexible reporting options based on different time intervals.

# Task 2: Design the dimension table MyDimProduct

Write down the fields in the MyDimProduct table in any text editor, one field per line.

- Solution:
In this task, you will design the dimension table MyDimProduct to store product-related information.

Fields in MyDimProduct table:

productid
productname
The table will have a unique identifier (productid) for each product entry. The field productname will store the name or description of the product. This table will facilitate analysis and reporting based on different products sold.

# Task 3: Design the dimension table MyDimCustomerSegment
Write down the fields in the MyDimCustomerSegment table in any text editor, one field per line.

- Solution:
In this task, you will design the dimension table MyDimCustomerSegment to store customer segment-related information.

Fields in DimCustomerSegment table:

segmentid
segmentname

# Task 4: Design the fact table MyFactSales

Write down the fields in the MyFactSales table in any text editor, one field per line.

- Solution:
In this task, you will design the fact table MyFactSales to store sales-related information.

Fields in FactSales table:

salesid
productid
quantitysold
priceperunit
segmentid
dateid

The fact table FactSales will store information about each sales transaction, including the unique identifier (salesid), product identifier (productid), quantity sold (quantitysold), price per unit (priceperunit), customer segment identifier (segmentid) and date identifier (dateid). This table will serve as the central repository for sales data and enable analysis and reporting on various dimensions.

# Phase 2: Create schema for data warehouse on PostgreSQL
Open pgAdmin and create a database named Practice, then create the following tables.

# Task 5: Create a database

1. Open the pgAdmin Graphical User Interface
   
2. Once the pgAdmin GUI opens, click on the Servers tab on the left side of the page. You will be prompted to enter a password.
   
![image](https://github.com/user-attachments/assets/51aa4680-d798-48e5-98f6-5bfd5aa7772b)

3. Input your password, then click OK.

![image](https://github.com/user-attachments/assets/8d7f2d64-b412-49af-9558-67acbbcbb576)

4. You will then be able to access the pgAdmin GUI tool.

5. In the left tree-view, right-click on Databases> Create > Database.

![image](https://github.com/user-attachments/assets/5fdc2ff1-98d9-4c02-9573-94551be1a9bb)

6. In the Database box, type Practice as the name for your new database, and then click Save. Proceed to Task 6.

![image](https://github.com/user-attachments/assets/c1976cf4-1b64-4649-ad29-04f72a003df4)

# Task 6: Create tables

Create the MyDimDate table using the CREATE statement below:

          CREATE TABLE MyDimDate (
                      dateid INT PRIMARY KEY,
                      year INT,
                      month INT,
                      monthname VARCHAR(20),
                      day INT,
                      weekday INT,
                      weekdayname VARCHAR(20)
          );

![image](https://github.com/user-attachments/assets/c3c9ba7a-31ec-47cc-9cf7-4ba96da6dcee)

# Task 7: Create the dimension table MyDimProduct

Create the MyDimProduct table using the CREATE statement below:

          CREATE TABLE MyDimProduct (
                       productid INT PRIMARY KEY,
                       productname VARCHAR(255)
          );
          
![image](https://github.com/user-attachments/assets/c8bc7a39-9a69-47c3-b69c-7209de01d200)

# Task 8: Create the dimension table MyDimCustomerSegment

Create the MyDimCustomerSegment table using the CREATE statement below:

          CREATE TABLE MyDimCustomerSegment (
                      segmentid INT PRIMARY KEY,
                      segmentname VARCHAR(255)
          );
          
![image](https://github.com/user-attachments/assets/fe5277b2-4e96-4d94-a36f-24252555f06f)

# Task 9: Create the fact table MyFactSales

Create the MyFactSales table using the CREATE statement below:

          CREATE TABLE MyFactSales (
                      salesid INT PRIMARY KEY,
                      productid INT,
                      quantitysold INT,
                      priceperunit DECIMAL (10, 2),
                      segmentid INT,
                      dateid INT
            );

![image](https://github.com/user-attachments/assets/861e8b9f-beeb-4a0c-bf3d-eaf1cc316c31)

# Phase 3: Load data into the data warehouse

After the initial schema design, you were informed that data could not be collected in the format initially planned due to operational issues. This means that the previous tables (MyDimDate, MyDimProduct, MyDimCustomerSegment, MyFactSales) in the Practice database and their associated attributes are no longer applicable to the current design. The company has now provided data in CSV files according to the new design.

You will need to load the data provided by the company in CSV format. First, create a new database named PracProj. Then, create the tables DimDate, DimProduct, DimCustomerSegment, and FactSales as per the new schema. Follow the instructions in the lab to run the new scripts and load the data from the CSV files into the appropriate tables.

# Task 10: create a new database named PracProj

1. In the left tree-view, right-click on Databases> Create > Database.

![image](https://github.com/user-attachments/assets/5fdc2ff1-98d9-4c02-9573-94551be1a9bb)

6. In the Database box, type PracProj as the name for your new database, and then click Save. Proceed to Task 10.

![image](https://github.com/user-attachments/assets/c1c11d86-d128-49a3-8e17-c9f7c8fe5ddb)

# Task 11: Create tables

-STEP 1: Create the DimDate table

Create the DimDate table using the CREATE statement below:

         CREATE TABLE DimDate (
                      Dateid INT PRIMARY KEY,
                      date DATE NOT NULL,
                      Year INT NOT NULL,
                      Quarter INT NOT NULL,
                      QuarterName VARCHAR(2) NOT NULL,
                      Month INT NOT NULL,
                      Monthname VARCHAR(255) NOT NULL,
                      Day INT NOT NULL,
                      Weekday INT NOT NULL,
                      WeekdayName VARCHAR(255) NOT NULL
         );

- STEP 2: Download the data from https://drive.google.com/file/d/1imF3b128WfkR_L7efgVoPKiCD4DNeF09/view?usp=sharing

- STEP 3: Load data into DimDate table.
  
- STEP 4: Use the import tool in pgAdmin to load your CSV file into the table

Navigate to the DimDate table in pgAdmin, right-click it, select “Import/Export Data”.

Choose “Import”, select your CSV file, and follow the prompts to import the data.

-STEP 5: View the first 5 rows of the dataset using the query statement below:

         SELECT * FROM DimDate 
         LIMIT 5;

![image](https://github.com/user-attachments/assets/2f4c1096-b305-4237-aac3-ef8b9c4496b2)

# Task 12: Load data into the dimension table DimProduct

- STEP 1: Create the DimProduct table

  Create the DimProduct table using the CREATE statement below:

           CREATE TABLE DimProduct (
                        Productid INT PRIMARY KEY,
                        Producttype VARCHAR(255) NOT NULL
           );

- STEP 2: Download the DimProduct data from https://drive.google.com/file/d/1VovKm9Y58ZTZZ1Rmm-p9E-XBj5G4A980/view?usp=sharing

- STEP 3: Load data into DimProduct table.
  
- STEP 4: Use the import tool in pgAdmin to load your CSV file into the table

Navigate to the DimProduct table in pgAdmin, right-click it, select “Import/Export Data”.

Choose “Import”, select your CSV file, and follow the prompts to import the data.

-STEP 5: View the first 5 rows of the dataset using the query statement below:

         SELECT * FROM DimProduct
         LIMIT 5;
         
# Task 13: Load data into the dimension table DimCustomerSegment

- STEP 1: Create the DimCustomerSegment table

  Create the DimCustomerSegment table using the CREATE statement below:

           CREATE TABLE DimCustomerSegment (
                      Segmentid INT PRIMARY KEY,
                      City VARCHAR(255) NOT NULL
           );

- STEP 2: Download the DimCustomerSegment data from https://drive.google.com/file/d/19pT_kQuksppC_4pwxRcV2_LShm2oOtbI/view?usp=sharing

- STEP 3: Load data into DimCustomerSegment table.
  
- STEP 4: Use the import tool in pgAdmin to load your CSV file into the table

Navigate to the DimCustomerSegment table in pgAdmin, right-click it, select “Import/Export Data”.

Choose “Import”, select your CSV file, and follow the prompts to import the data.

- STEP 5: View the first 5 rows of the dataset using the query statement below:

         SELECT * FROM DimCustomerSegment
         LIMIT 5;

![image](https://github.com/user-attachments/assets/d55303b1-e4b4-4295-9375-101dba830907)

# Task 14: Load data into the fact table FactSales

- STEP 1: Create the FactSales table

  Create the FactSales table using the CREATE statement below:

           CREATE TABLE FactSales (
                       Salesid VARCHAR(255) PRIMARY KEY,
                       Dateid INT NOT NULL,
                       Productid INT NOT NULL,
                       Segmentid INT NOT NULL,
                       Price_PerUnit DECIMAL(10, 2) NOT NULL,
                       QuantitySold INT NOT NULL,
                       FOREIGN KEY (Dateid) REFERENCES DimDate(Dateid),
                       FOREIGN KEY (Productid) REFERENCES DimProduct(Productid),
                       FOREIGN KEY (Segmentid) REFERENCES DimCustomerSegment(Segmentid)
            );

- STEP 2: Download the FactSales data from https://drive.google.com/file/d/1o1oU1jW3bUH3WK5IiCGSWQ53FjLpsiGI/view?usp=sharing
  
- STEP 3: Load data into FactSales table.
  
- STEP 4: Use the import tool in pgAdmin to load your CSV file into the table

Navigate to the FactSales table in pgAdmin, right-click it, select “Import/Export Data”.

Choose “Import”, select your CSV file, and follow the prompts to import the data.

- STEP 5: View the first 5 rows of the dataset using the query statement below:

         SELECT * FROM FactSales
         LIMIT 5;

![image](https://github.com/user-attachments/assets/f6712464-e7ae-4cb9-8226-2fa9b53a0f52)

# Phase 4: Writing aggregation queries and creating materialized view

# Task 15: Create a grouping sets query

Create a grouping sets query using the columns productid, producttype, total sales.

The following query statement was used to create a grouping sets query using the columns productid, producttype, total sales.

         SELECT
          p.Productid,
          p.Producttype,
          SUM(f.Price_PerUnit * f.QuantitySold) AS TotalSales
         FROM
          FactSales f
         INNER JOIN
          DimProduct p ON f.Productid = p.Productid
         GROUP BY GROUPING SETS (
          (p.Productid, p.Producttype),
          p.Productid,
          p.Producttype,
          ()
            )
         ORDER BY
          p.Productid,
          p.Producttype;

![image](https://github.com/user-attachments/assets/991f5695-8e85-4912-a318-7aade46f7add)

- Explanation of query statement

  In this query:

   I joined FactSales 'f' with DimProduct 'p' on their productid to correlate each sale with its product type.

   I used GROUPING SETS to specify the different levels of aggregation:

   By both Productid and Producttype
   By Productid alone
   By Producttype alone
   And a grand total with (), which doesn't group by any column and hence returns the sum for all sales.

I calculated TotalSales by multiplying the Price_PerUnit by QuantitySold for each sale.

The ORDER BY clause ensures the results are ordered by productid and then by producttype.

# Task 16: Create a rollup query

Create a rollup query using the columns year, city, productid, and total sales. 

The following query statement was used to create a rollup query using the columns year, city, productid, and total sales. 
      
          SELECT
             d.Year,
             cs.City,
             p.Productid,
          SUM(f.Price_PerUnit * f.QuantitySold) AS TotalSales 
         FROM
          FactSales f
         JOIN
          DimDate d ON f.Dateid = d.Dateid
         JOIN
          DimProduct p ON f.Productid = p.Productid
         JOIN
          DimCustomerSegment cs ON f.Segmentid = cs.Segmentid
         GROUP BY ROLLUP (d.Year, cs.City, p.Productid)
         ORDER BY
          d.Year DESC,
          cs.City,
          p.Productid;

![image](https://github.com/user-attachments/assets/f08176ff-8ed0-407e-990b-9d47489fd6e2)

- Explanation of the query statement

This query performs the following operations:

Joins FactSales with DimDate on Dateid, DimProduct on Productid, and DimCustomerSegment on Segmentid.
Selects the year from DimDate, the city from DimCustomerSegment, and the product ID from DimProduct.
Calculates total sales by multiplying the price per unit by the quantity sold for each sales entry.
Groups the results using the ROLLUP function to create a grouping set that includes all combinations of year, city, and productid, along with their respective subtotals and a grand total for all sales.
The ORDER BY clause ensures the results are first ordered by year in descending order, then by city and product ID.

# Task 17: Create a cube query

Create a cube query using the columns year, city, productid, and average sales.
         
The following query statement was used to create a cube query using the columns year, city, productid, and average sales.

          SELECT
             d.Year,
             cs.City,
             p.Productid,
          AVG(f.Price_PerUnit * f.QuantitySold) AS AverageSales
         FROM
          FactSales f
         INNER JOIN
          DimDate d ON f.Dateid = d.Dateid
         INNER JOIN
          DimProduct p ON f.Productid = p.Productid
         INNER JOIN
          DimCustomerSegment cs ON f.Segmentid = cs.Segmentid
         GROUP BY CUBE (d.Year, cs.City, p.Productid);

![image](https://github.com/user-attachments/assets/815102ff-d6d0-46af-a023-1436841388af)

- Explanation of the query

In this query:

The CUBE clause is used in the GROUP BY to create subtotals for all combinations of year, city, and productid in addition to the grand total across all groups.

AVG(f.Price_PerUnit * f.QuantitySold) calculates the average sales, factoring in both the price per unit and the quantity sold.

INNER JOIN is used to join the FactSales table with the dimension tables DimDate, DimProduct, and DimCustomerSegment.

# Task 18: Create a materialized view

Create an materialized view named max_sales using the columns city, productid, producttype, and max sales.

The following query statement was used to create an materialized view named max_sales using the columns city, productid, producttype, and max sales.

            CREATE MATERIALIZED VIEW max_sales AS
            SELECT
             cs.City,
             p.Productid,
             p.Producttype,
             MAX(f.Price_PerUnit * f.QuantitySold) AS MaxSales
            FROM
             FactSales f
            JOIN
             DimProduct p ON f.Productid = p.Productid
            JOIN
             DimCustomerSegment cs ON f.Segmentid = cs.Segmentid
            GROUP BY
             cs.City,
             p.Productid,
             p.Producttype
            WITH DATA;

![image](https://github.com/user-attachments/assets/d3fdeffd-f516-4d48-b9dc-2b770db1fb17)

- Explanation of the query:

This query statement creates the materialized view and populate it with the current data from the joined tables. 
The WITH DATA clause tells PostgreSQL to fill the view with the query results immediately. 
However, to create the view without filling it with data, I used WITH NO DATA.

To update the materialized view with the latest data, we use the REFRESH MATERIALIZED VIEW command:

# Task 19: View the new materialized view data

To view the new materialized view data, the command below was used:

         REFRESH MATERIALIZED VIEW max_sales; 

Right-clicking the new materialized view, I navigated to the "view/edit data" option, selected "First 100 Rows" to have the output as shown below:

![image](https://github.com/user-attachments/assets/7f709244-e072-44fa-98d7-83facf28b39c)

          
