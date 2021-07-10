﻿
# Loading Movie Sales Data

## Introduction

To help us do some financial analysis, the IT Team at MovieStream has created a data extract for us from the MovieStream operational systems. The quarter-end closing process takes a few days, so some of our data contains an early snapshot of our company's financial trading data. We can expect a second set of files a bit later, which will contain the final updates and corrections that reflect the closed-status of the accounts.

### Overview Of The Data Loading Process

Autonomous Data Warehouse provides different ways to load data depending on your needs: a way to load data on a regular basis and a way to load one-off files. In this lab, we will explore how you can quickly and easily initially populate a new data warehouse using a simple script, which you can then amend and use to load new data on an on-going basis. Later in this lab, we will load a set of data files containing just updates and corrections - in many cases with this type of sales analysis you will get an initial file to load containing a "draft" view or soft-close view of the latest sales data. A "final", verified sales data set is often then published later in the month after all the sales transactions have been processed and correctly booked. This is the scenario we are using in this workshop.

### What About Data Quality In Your Autonomous Data Warehouse?

In the real world, it is highly likely that our data files will be imperfect - that is, they will contain formatting errors, have duplicate records, and so on. Therefore, in the next lab we will review how Autonomous Data Warehouse can enforce business rules to ensure our data warehouse only contains structurally correct and valid data. In this lab, we are going to assume that our data loading files are perfectly formatted and only contain valid records. 

### Where Are My Data Files Stored?

Autonomous Data Warehouse makes it easy to load data files from many different locations: your local computer, other databases, and object stores such as Oracle OCI Object Storage, Amazon S3, Microsoft Azure Blob Storage and many others.

### What is Oracle Cloud Infrastructure (OCI) Object Storage?

The OCI Object Storage service is an internet-scale, high-performance storage platform that offers reliable and cost-efficient data durability. The Object Storage service can store an unlimited amount of unstructured data of any content type, including analytic data and rich content, like images and videos. For more information, [see here](https://docs.oracle.com/en-us/iaas/Content/Object/Concepts/objectstorageoverview.htm).

A wide range of file formats are supported including Excel, comma-separated, tab delimited, AVRO, parquet, and so on. There are separate data loading wizards to support each of the different data locations scenarios within the Database Actions Data Loading feature. We will cover using the built-in data loading wizard later in this workshop.

For this data loading scenario, we will access data files that have been stored in a  **public bucket**  in Oracle's OCI **Object Storage**.

**Note** -  *all the data files for this workshop are located in a public bucket in our UK (London) data center. All timings for data loading in this workshop assume an ADW instance also running in the UK (London) data center. If this is not the case then your timings for specific steps may vary because the data files and ADW instance are not co-located in the same data center*.

## STEP 1 - Launching SQL Worksheet 

During this part of the workshop, we will use the SQL Worksheet application that is built-in to our data warehouse environment. 

1. From your cloud console page, click the **Tools** tab, then click the **Open Database Actions** button:

    ![Click the Open Database Actions button.](images/3054194717.png)

2. On the login screen, enter the username **ADMIN**, then click the blue **Next** button.

3. Enter the admin password you set up when provisioning the ADW instance.

4. In the **Development** section of the Database Actions page, click the **SQL** card to open a new SQL worksheet:

    ![Click the SQL card.](images/3054194715.png)

    This will open up a new window that should look something like the screenshot below:

    ![Screenshot of initial SQL Worksheet](images/3054194690.png)


## STEP 2 - Creating A New Table

1. Below is the script to help you create the sales fact table, **"MOVIE\_SALES\_FACT"**. Simply copy and paste this code into your SQL Worksheet (**NOTE** the first column in the CREATE TABLE definition includes a NOT NULL clause which ensures that each row we load has an order number. There is more on this concept in the lab covering data integrity): 


    ```
    <copy>CREATE TABLE MOVIE_SALES_FACT
    (ORDER_NUM NUMBER(38,0) NOT NULL,
    DAY DATE,
    DAY_NUM_OF_WEEK NUMBER(38,0),
    DAY_NAME VARCHAR2(26),
    MONTH VARCHAR2(12),
    MONTH_NUM_OF_YEAR NUMBER(38,0),
    MONTH_NAME VARCHAR2(26),
    QUARTER_NAME VARCHAR2(26),
    QUARTER_NUM_OF_YEAR NUMBER(38,0),
    YEAR NUMBER(38,0),
    CUSTOMER_ID NUMBER(38,0),
    USERNAME VARCHAR2(26),
    CUSTOMER_NAME VARCHAR2(250),
    STREET_ADDRESS VARCHAR2(250),
    POSTAL_CODE VARCHAR2(26),
    CITY_ID NUMBER(38,0),
    CITY VARCHAR2(128),
    STATE_PROVINCE_ID NUMBER(38,0),
    STATE_PROVINCE VARCHAR2(128),
    COUNTRY_ID NUMBER(38,0),
    COUNTRY VARCHAR2(126),
    COUNTRY_CODE VARCHAR2(26),
    CONTINENT VARCHAR2(128),
    SEGMENT_NAME VARCHAR2(26),
    SEGMENT_DESCRIPTION VARCHAR2(128),
    CREDIT_BALANCE NUMBER(38,0),
    EDUCATION VARCHAR2(128),
    EMAIL VARCHAR2(128),
    FULL_TIME VARCHAR2(26),
    GENDER VARCHAR2(26),
    HOUSEHOLD_SIZE NUMBER(38,0),
    HOUSEHOLD_SIZE_BAND VARCHAR2(26),
    WORK_EXPERIENCE NUMBER(38,0),
    WORK_EXPERIENCE_BAND VARCHAR2(26),
    INSUFF_FUNDS_INCIDENTS NUMBER(38,0),
    JOB_TYPE VARCHAR2(26),
    LATE_MORT_RENT_PMTS NUMBER(38,0),
    MARITAL_STATUS VARCHAR2(26),
    MORTGAGE_AMT NUMBER(38,0),
    NUM_CARS NUMBER(38,0),
    NUM_MORTGAGES NUMBER(38,0),
    PET VARCHAR2(26),
    PROMOTION_RESPONSE NUMBER(38,0),
    RENT_OWN VARCHAR2(26),
    YEARS_CURRENT_EMPLOYER NUMBER(38,0),
    YEARS_CURRENT_EMPLOYER_BAND VARCHAR2(26),
    YEARS_CUSTOMER NUMBER(38,0),
    YEARS_CUSTOMER_BAND VARCHAR2(26),
    YEARS_RESIDENCE NUMBER(38,0),
    YEARS_RESIDENCE_BAND VARCHAR2(26),
    AGE NUMBER(38,0),
    AGE_BAND VARCHAR2(26),
    COMMUTE_DISTANCE NUMBER(38,0),
    COMMUTE_DISTANCE_BAND VARCHAR2(26),
    INCOME NUMBER(38,0),
    INCOME_BAND VARCHAR2(26),
    MOVIE_ID NUMBER(38,0),
    SEARCH_GENRE VARCHAR2(26),
    TITLE VARCHAR2(4000),
    GENRE VARCHAR2(26),
    SKU NUMBER(38,0),
    LIST_PRICE NUMBER(38,2),
    APP VARCHAR2(26),
    DEVICE VARCHAR2(26),
    OS VARCHAR2(26),
    PAYMENT_METHOD VARCHAR2(26),
    DISCOUNT_TYPE VARCHAR2(26),
    DISCOUNT_PERCENT NUMBER(38,1),
    ACTUAL_PRICE NUMBER(38,2),
    QUANTITY_SOLD NUMBER(38,0));</copy>
    ```

2. To run the above `CREATE TABLE` command, we need to click the green circular **Run Statement** icon in the main menu bar:

    ![Click the Run Statement icon.](images/3054194713.png)

3. This will result in the table being created. The output panel at the bottom of the screen will show the table was created:

    ![Output panel shows the table was created.](images/3054194712.png)

4.  Now refresh the Navigator panel on the left side of the screen, using the icon that has two rotating arrows:

    ![The icon to click to refresh the Navigator panel](images/3054194688.png)

    ![Navigator panel showing the created table](images/3054194689.png)

Now we are ready to start loading the sales data.

## STEP 3 - Loading Sales Data

### Background

All the MovieStream data files for this workshop are stored in a public bucket in the OCI Object Storage. For this initial data load into our new data warehouse, we will use a script to import sales data for 2018 to 2020 - this will give you some insight into how to create your own scripts to automate your own data loading processes. There are 35 separate data files for the sales data stored in the public bucket. We can either load each file individually, or we can bulk load all the files in one step. If we wanted to load a single month, then we could use the following approach:

Let's say that we were going to load data for January 2018; then the filename in the public bucket for that file would be *movie\_sales\_fact-2018**01**.csv*. This filename is passed into the built-in data load procedure (which is called DBMS\_CLOUD.COPY\_DATA) as a parameter (**Note**: *you do not need to run the command below at this stage!*):

<pre><code>
    BEGIN
    DBMS_CLOUD.COPY_DATA(
    table_name => 'MOVIE_SALES_FACT',
    file_uri_list => 'https://objectstorage.uk-london-1.oraclecloud.com/n/adwc4pm/b/data_library/o/d801_movie_sales_fact_m-201801.csv',
    format =>  '{"type":"csv","skipheaders":"1"}'
    );
    END;
    /
</code></pre>

Let's quickly review some of the key parts of the above command.

**What is DBMS\_CLOUD.COPY\_DATA?**

This is the procedure that loads data into your Autonomous Data Warehouse tables from files in the Cloud. The procedure takes a number of arguments:

**table\_name =>** name of the target table on the database. Note that the target table needs to be created before you run COPY\_DATA. In this case, the target table is the one we created a few steps back (MOVIE\_SALES\_FACT).

**file\_uri\_list =>** comma-delimited list of source file URIs. You can use wildcards in the file names in your URIs. The character "*" can be used as the wildcard for multiple characters, the character "?" can be used as the wildcard for a single character. In this case, the `COPY_DATA` procedure will load all the CSV files where the filename contains the string movie\_sales\_fact-201801.csv.

 **format =>** options describing the format of the source csv files. For the list of the options and how to specify the values, see [DBMS_CLOUD Package Format Options](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/format-options.html#GUID-08C44CDA-7C81-481A-BA0A-F7346473B703).

To load the data for February, March, April, May, and so on, we could simply change the filename in the file\_uri\_list parameter.  **BUT** this would mean having to create a very long script containing multiple instances of the DBMS\_CLOUD.COPY\_DATA procedure! 

A smarter and more efficient way to load all the data for 2018 to 2020 is to let Autonomous Data Warehouse manage the loading of all the files by using a wildcard string in the file\_uri\_list parameter as shown below.

1. The first step in this workshop allows us to manage the resources we are going to use to load our sales data. You will notice that when you open SQL Worksheet, it automatically defaults to using the LOW consumer group - this is shown in the top right section of your worksheet.

    ![LOW consumer group shown in worksheet](images/3054194710.png)

**NOTE**: For more information about how to use consumer groups to manage concurrency and prioritization of user requests in Autonomous Data Warehouse, please click the following link: [Manage Concurrency and Priorities on Autonomous Database](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/manage-priorities.html#GUID-19175472-D200-445F-897A-F39801B0E953).

2. Change the consumer group, by simply clicking the downward pointing arrow next to the word LOW, and from the pulldown menu select the word **HIGH**.

    ![Select the HIGH consumer group from the pulldown menu.](images/3054194709.png)

3. To load all the data for 2018-2020, use the following code:

    ```
    <copy>BEGIN
    DBMS_CLOUD.COPY_DATA (table_name => 'MOVIE_SALES_FACT',
    file_uri_list => 'https://objectstorage.uk-london-1.oraclecloud.com/n/adwc4pm/b/data_library/o/d801_movie_sales_fact_m-*.csv',
    format =>  '{"type":"csv","skipheaders":"1"}'
    );
    END;
    /</copy>
    ```

    **NOTE:** If you want to clear the previous `CREATE TABLE` statement from your worksheet window, then simply click the trashcan icon in the menu:

    ![Click the trashcan icon in menu](images/3054194708.png)

4. Then paste the SQL command above into the worksheet and run the command:

    ![SQL command pasted into the worksheet](images/data-loading-lab2-step3-substep4.png)

5.  While the procedure is executing and loading your data, you will see a small cog spinning in the bottom left corner of your browser window:

    ![Cog spins while procedure is executing](images/3054194706.png)

6.  With 8 OCPUs, this data load process should take around 4 minutes to load 35 months’ worth of movie sales data. Once all the data has been loaded, the following message will appear in the status window, indicating that the procedure completed successfully:

    ![Message indicating the procedure completed successfully](images/3054194705.png)

7.  To check the status of the data load, we can query a metadata table (USER\_LOAD\_OPERATIONS) that tracks all our data load jobs. Copy and paste the SQL query below into the worksheet and run the query:

    ```
    <copy>SELECT
    start_time,
    update_time,
    substr(to_char(update_time-start_time, 'hh24:mi:ss'),11) as duration,
    status,
    table_name,
    rows_loaded,
    logfile_table,
    badfile_table
    FROM user_load_operations
    WHERE table_name = 'MOVIE_SALES_FACT'
    ORDER BY 1 DESC, 2 DESC
    FETCH FIRST 1 ROWS ONLY;</copy>
    ```

    ![Query to show result of data load](images/3054194687.png)

    You should see from the column headed rows_loaded that 97,890,562 rows were loaded from the csv files that were located in our Object Storage bucket.

8. Now let's confirm that information by finding out how many rows are actually in our fact table:

    ```
    <copy>SELECT COUNT(*) FROM movie_sales_fact;</copy>
    ```

9. Running the above query should return the value 97,890,562 records, as shown below in the Query Result window:

    ![Query result window showing number of rows in table](images/3054194703.png)

10. If you refresh the navigator panel again, you will see that we have two additional new files: 1) a bad records table and 2) a log table.

    **NOTE:** Your filenames will be slightly different than those shown below in terms of the numeric identifier within each filename:

    ![Two new files showing in Navigator panel](images/3054194702.png)

11. If we check the table containing information about the bad records, this query should return zero rows:

    ```
    <copy>SELECT COUNT(*) FROM copy$1_bad;</copy>
    ```
    **NOTE**: Amend the above query to match the table name shown in your Navigator panel!

12. We can check how many data files were processed by querying the log file as follows:

    ```
    <copy>SELECT *
    FROM copy$1_log
    WHERE RECORD LIKE '%Data File%'ORDER BY 1;</copy>
    ```

13. This should return a list of 35 entries as shown below:

    ![List of 35 entries](images/3054194701.png)

Please *proceed to the next lab*.

## **Acknowledgements**

- **Author** - Keith Laker, ADB Product Management
- **Adapted for Cloud by** - Richard Green, Principal Developer, Database User Assistance
- **Last Updated By/Date** - Richard Green, June 2021
