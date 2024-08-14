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

# Phase B: Create tables

# Task 5: Create the dimension table MyDimDate

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

# Task 6: Create the dimension table MyDimProduct

Create the MyDimProduct table using the CREATE statement below:

          CREATE TABLE MyDimProduct (
                       productid INT PRIMARY KEY,
                       productname VARCHAR(255)
          );
          
![image](https://github.com/user-attachments/assets/c8bc7a39-9a69-47c3-b69c-7209de01d200)

# Task 7: Create the dimension table MyDimCustomerSegment

Create the MyDimCustomerSegment table using the CREATE statement below:

          CREATE TABLE MyDimCustomerSegment (
                      segmentid INT PRIMARY KEY,
                      segmentname VARCHAR(255)
          );
          
![image](https://github.com/user-attachments/assets/fe5277b2-4e96-4d94-a36f-24252555f06f)

# Task 8: Create the fact table MyFactSales

          CREATE TABLE MyFactSales (
                      salesid INT PRIMARY KEY,
                      productid INT,
                      quantitysold INT,
                      priceperunit DECIMAL (10, 2),
                      segmentid INT,
                      dateid INT
            );

![image](https://github.com/user-attachments/assets/861e8b9f-beeb-4a0c-bf3d-eaf1cc316c31)

# Phase 3 - Load data into the data warehouse

After the initial schema design, you were informed that data could not be collected in the format initially planned due to operational issues. This means that the previous tables (MyDimDate, MyDimProduct, MyDimCustomerSegment, MyFactSales) in the Practice database and their associated attributes are no longer applicable to the current design. The company has now provided data in CSV files according to the new design.

You will need to load the data provided by the company in CSV format. First, create a new database named PracProj. Then, create the tables DimDate, DimProduct, DimCustomerSegment, and FactSales as per the new schema. Follow the instructions in the lab to run the new scripts and load the data from the CSV files into the appropriate tables.

# Task 9: create a new database named PracProj

1. In the left tree-view, right-click on Databases> Create > Database.

![image](https://github.com/user-attachments/assets/5fdc2ff1-98d9-4c02-9573-94551be1a9bb)

6. In the Database box, type PracProj as the name for your new database, and then click Save. Proceed to Task 10.

![image](https://github.com/user-attachments/assets/c1976cf4-1b64-4649-ad29-04f72a003df4)


          
