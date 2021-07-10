# Oracle Data Redaction

## Introduction
This workshop introduces the various features and functionality of Oracle Data Redaction. It gives the user an opportunity to learn how to configure those features in order to protect access to sensitive data by redacting them on-the-fly.

*Estimated Lab Time:* 15 minutes

*Version tested in this lab:* Oracle DB 19.10
### Video Preview
Watch a preview of "*Understanding Oracle Data Redaction (July 2020)*" [](youtube:ssy6Hov-MAs)

### Objectives
Dynamically redact sensitive data preventing it from being displayed outside the application

### Prerequisites
This lab assumes you have:
- A Free Tier, Paid or LiveLabs Oracle Cloud account
- SSH Private Key to access the host via SSH
- You have completed:
    - Lab: Generate SSH Keys (*Free-tier* and *Paid Tenants* only)
    - Lab: Prepare Setup (*Free-tier* and *Paid Tenants* only)
    - Lab: Environment Setup
    - Lab: Initialize Environment

### Lab Timing (estimated)
| Step No. | Feature | Approx. Time |
|--|------------------------------------------------------------|-------------|
| 1 | Create a basic Data Redaction policy | 5 minutes |
| 2 | Contextualize an existing Data Redaction policy | 5 minutes |
| 3 | (Optional) Drop the Data Redaction policy | <5 minutes |

## **STEP 1**: Create a basic Data Redaction policy

1. Open a SSH session on your **DBSec-Lab VM as *oracle* user**

      ````
      <copy>sudo su - oracle</copy>
      ````

2. Go to the scripts directory

      ````
      <copy>cd $DBSEC_LABS/data-redaction</copy>
      ````

3. First, let's view the data before we redact it

      ````
      <copy>./dr_query_employee_data.sh</copy>
      ````

   ![](./images/dr-001.png " ")

4. Create the redaction policy `PROTECT_EMPLOYEES` for the `DEMO_HR_EMPLOYEES` table to (**FULL**) redact data on column **SIN** for all queries (**Expression "1=1"**)

      ````
      <copy>./dr_redact_for_all.sh</copy>
      ````

   ![](./images/dr-002.png " ")

5. Re-run the query to see the redacted data

      ````
      <copy>./dr_query_employee_data.sh</copy>
      ````

   ![](./images/dr-003.png " ")

## **STEP 2**: Contextualize an existing Data Redaction policy

1. Now, modify the redaction policy to only redact non-Glassfish queries (**Expression with "Rule Set"**)

      ````
      <copy>./dr_redact_nonapp_queries.sh</copy>
      ````

   ![](./images/dr-004.png " ")

2. Add additional columns (**SSN** and **NINO**) to the redaction policy

      ````
      <copy>./dr_add_redacted_columns.sh</copy>
      ````

   ![](./images/dr-005.png " ")

3. Run the query to see the redact data again

      ````
      <copy>./dr_query_employee_data.sh</copy>
      ````

   ![](./images/dr-006.png " ")

## **STEP 3**: (Optional) Drop the Data Redaction policy

1. When you are finished with the lab, you can drop the redaction policy

      ````
      <copy>./dr_drop_redaction_policy.sh</copy>
      ````

   ![](./images/dr-007.png " ")

2. Check that all data are now not redacted

      ````
      <copy>./dr_query_employee_data.sh</copy>
      ````

   ![](./images/dr-001.png " ")

You may now [proceed to the next lab](#next)..

## **Appendix**: About the Product
### **Overview**
Hard-coded within the Oracle Database core product, this features is part of the *Advanced Security Option (ASO)*

Data Redaction enables you to mask (redact) data that is returned from queries issued by applications. We can also talk about Dynamic Data Masking.

You can redact column data by using one of the following methods:

- **Full redaction**
You redact all of the contents of the column data. The redacted value that is returned to the querying user depends on the data type of the column. For example, columns of the NUMBER data type are redacted with a zero (0) and character data types are redacted with a blank space.

- **Partial redaction**
You redact a portion of the column data. For example, you can redact most of a Social Security number with asterisks (*), except for the last 4 digits.

- **Regular expressions**
You can use regular expressions in both full and partial redaction. This enables you to redact data based on a search pattern for the data. For example, you can use regular expressions to redact specific phone numbers or email addresses in your data.

- **Random redaction**
The redacted data presented to the querying user appears as randomly generated values each time it is displayed, depending on the data type of the column.

- **No redaction**
This option enables you to test the internal operation of your redaction policies, with no effect on the results of queries against tables with policies defined on them. You can use this option to test the redaction policy definitions before applying them to a production environment.

Data Redaction performs the redaction at runtime, that is, the moment that the user tries to view the data. This functionality is ideally suited for dynamic production systems in which data constantly changes. While the data is being redacted, Oracle Database is able to process all of the data normally and to preserve the back-end referential integrity constraints. Data redaction can help you to comply with industry regulations such as Payment Card Industry Data Security Standard (PCI DSS) and the Sarbanes-Oxley Act.

   ![](./images/aso-concept-dr.png " ")

### **Benefits of Using Oracle Data Redaction**
- You have different styles of redaction from which to choose
- Because the data is redacted at runtime, Data Redaction is well suited to environments in which data is constantly changing
- You can create the Data Redaction policies in one central location and easily manage them from there
- The Data Redaction policies enable you to create a wide variety of function conditions based on `SYS_CONTEXT` values, which can be used at runtime to decide when the Data Redaction policies will apply to the results of the application user's query

## Want to Learn More?
Technical Documentation: [Data Redaction 19c](https://docs.oracle.com/en/database/oracle/oracle-database/19/asoag/asopart1.html)

## Acknowledgements
- **Author** - Hakim Loumi, Database Security PM
- **Contributors** - Rene Fontcha
- **Last Updated By/Date** - Hakim Loumi, Database Security PM - May 2021
