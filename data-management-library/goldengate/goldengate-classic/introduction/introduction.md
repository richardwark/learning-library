# Introduction

## About Oracle GoldenGate Classic
Oracle GoldenGate offers high-performance, fault-tolerant, easy-to-use, and flexible real- time data streaming platform for big data environments. It easily extends customers' real-time data integration architectures to big data systems without impacting the performance of the source systems and enables timely business insight for better decision making. This workshop focuses on **GoldenGate Real Time Data Capture** demonstrating four scenarios that you can use (both on-premise and in the cloud) to capture real time data changes from your sources.

**Workshop Architecture**
  ![](./images/image200_1.png " ")

### Prerequisites
* An Oracle Free Tier, Always Free, Paid or LiveLabs Cloud Account

### Lab Overview

- **Lab: GoldenGate Classic Configuration** -
    In this lab we will install GoldenGate for Big Data in the GG Target Home. Follow the steps below to install GG, or optionally you can select “I” from the Lab Menu below to auto-install GG.

- **Lab: Replication from mySQL Relational Database to Oracle Relational Database using GoldenGate** -
    This lab is intended to give you familiarity with how to configure GG for database to database replication. If you are already familiar with GG, you can choose to skip this lab.

- **Lab: Replication from Oracle Relational Database to mySQL Relational Database using GoldenGate** -
    This lab is intended to give you familiarity with how to configure GG for database to database replication. If you are already familiar with GG, you can choose to skip this lab.

- **Lab: Active - Active HA Replication from Relational to Relational** -
    In this lab we will load data in MySQL database *ggsource*, GG extract process *extmysql* will capture the changes from MySQL's binary logs and wrote them to the local trail file. The pump process *pmphadop* will route the data from the local trail (on the source) to the remote trail (on the target). The replicat
    process *rhive* will read the trail file, create the Hive tables, write the data and the schema files (avsc) to the HDFS target directory for Hive: `/user/ggtarget/hive/data/*` and `/user/ggtarget/hive/schema/*`

- **Lab: Replication Column Conversion and GoldenGate** -
    In this lab we will load data in MySQL database *ggsource*, GG extract process *extmysql* will In this lab we will load data in MySQL database *ggsource*, GG extract process *extmysql* will capture the changes from MySQL's binary logs and write them to the local trail file. The pump process *pmphadop* will route the data from the local trail (on the source) to the remote trail (on the target). The replicat process *rhbase* will read the remote trail files, create the HBase tables and write the data to those tables.

- **Lab: PostgreSQL and GoldenGate Replication** -
- In this lab we will configure and load data into PostgreSQL database

## Learn More

* [GoldenGate](https://www.oracle.com/middleware/data-integration/goldengate/")
* [GoldenGate with PostgreSQL](https://docs.oracle.com/en/middleware/goldengate/core/19.1/gghdb/using-oracle-goldengate-postgresql.html/")

## Acknowledgements
* **Author** - Brian Elliott, Data Integration Team, Oracle, November 2020
* **Contributors** - Madhu Kumar, Rene Fontcha
* **Last Updated By/Date** - Rene Fontcha, LiveLabs Platform Lead, NA Technology, November 2020


