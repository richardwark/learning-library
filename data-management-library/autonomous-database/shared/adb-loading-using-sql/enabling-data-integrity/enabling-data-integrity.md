﻿
# Enabling Data Integrity

## Background

Autonomous Data Warehouse supports the ability to define constraints against your data that enforce logical and business rules. In the example below, we are going to add a unique constraint and ensure that there are no empty rows in our data table.

A unique constraint designates a column (it could also be a group of columns) as a unique key. To satisfy a unique constraint, no two rows in the table can have the same value for the unique key. The second step is to combine this concept with the NOT NULL constraint that was included in the definition of our data table to derive a **PRIMART KEY**. The concept of a primary key concept is a key part of an efficient relational database. Without the primary key, along with the closely related concept of a foreign key, relational databases would simply not work. A primary key provides us with a fast and efficient way to uniquely identify each row in a table.   

## STEP 1 - Adding Constraints

1. Run the following command in the SQL worksheet to enable a data integrity check on the fact table:

    ```
    <copy>CREATE UNIQUE INDEX idx_msf_order_num ON MOVIE_SALES_FACT(order_num);
    ALTER TABLE movie_sales_fact ADD primary KEY (order_num) USING INDEX idx_msf_order_num;</copy>
    ```
    **NOTE:**  These two statement may take a 1-2 minutes to complete.

## STEP 2 - Testing that the New Constraint Works

1. Check the value of total sales in the `movie_sales_fact` table:

    ```
    <copy>SELECT SUM(actual_price) FROM movie_sales_fact;</copy>
    ```
    **NOTE:** This should return a value of **$160,365,556.83**.

2. Now let's try to reload sales data for January 2018 using the following command: 

    ```
    <copy>BEGIN
    DBMS_CLOUD.COPY_DATA (
    table_name => 'MOVIE_SALES_FACT',
    file_uri_list => 'https://objectstorage.uk-london-1.oraclecloud.com/n/adwc4pm/b/data_library/o/d801_movie_sales_fact_m-201801.csv',
    format => '{"type":"csv","skipheaders":"1"}'
    );
    END;
    /</copy>
    ```

3. This time, the data load process will fail with the following error message in the script output window that indicates the duplicate records have been rejected: (ORA-20000: ORA-00001: unique constraint (ADMIN.SYS_C0022901) violated...):

    ![Error message showing duplicates](images/data-loading-lab3-step2-substep-3.png)

    **NOTE:** The data integrity checking does not depend on the name of the source data file. You could use a different filename (i.e. a filename that has not been used before) and you would get the same result - an error message indicating the data file contains records that have already been loaded.

4. Check the value of total sales in the `movie_sales_fact` table:

    ```
    <copy>SELECT SUM(actual_price) FROM movie_sales_fact;</copy>
    ```

    **NOTE:** This should return the same value as shown in step 1 - $160,365,556.83.

We can now show that our sales data is factually correct - our data set contains no duplicate records. Note that other non-Oracle cloud data warehouse vendors do not have this important feature, and with them you would need to implement your own data auditing features to ensure your data sets are factually correct.

Please *proceed to the next lab*.

## **Acknowledgements**

- **Author** - Keith Laker, ADB Product Management
- **Adapted for Cloud by** - Richard Green, Principal Developer, Database User Assistance
- **Last Updated By/Date** - Richard Green, June 2021
