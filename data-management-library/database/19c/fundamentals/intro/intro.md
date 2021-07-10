# Introduction

## About Oracle Database 19c

Oracle Database 19c provides the most advanced SQL engine on the planet. It complies with the latest ISO SQL standard, making it not only the most comprehensive database but also the most open one. It supports highly sophisticated analytics alongside and with no impact on OLTP workloads, eliminating the need to develop and orchestrate complex, fragile, and inconsistent data movement between different specialized data stores. Oracle’s SQL engine ships with integrated machine learning algorithms and allows developers to easily apply them on the data directly, hence moving the computation to the data—rather than having to pull the data out of the database and perform the calculation within the application. Using this capability, developers can create real-time prediction models directly on the data itself and act on insights more quickly and easily than ever before.

[](youtube:LcsPSJrZDrI)

Oracle Database 19c supports fully consistent data with ACID transaction guarantees and consistent queries. This greatly simplifies application development compared to NoSQL stores. Native JSON support makes up a cornerstone for flexible schema support and Internet of Things (IoT)workloads, enabling developers to simply load JSON documents into the database natively and analyze them later on, with the full power of Oracle SQL. Oracle’s PL/SQL engine is yet another powerful tool for bringing computations to the data and providing an easy and standardized interface to them via simple SQL function or procedure calls. Interfaces such as REST allow for easy communication and integration with Oracle Database. These can be created automatically on top of tables, as well as stored procedures, giving developers the flexibility on how and what data to expose to consuming services.

Extend this with the move to autonomy provided by Oracle Autonomous Database, a self-driving, self-securing, and self-repairing approach where the database itself decides on the steps to perform for the best of the user's workload or data. Machine learning algorithms are used to help the database to decide how to tune a workload, how to secure the data, and how to take countermeasures to preserve the agreed-on SLA levels.

With the Oracle Autonomous Database, developers can fully concentrate on the applications they write and the business’s requirements, rather than having to think about the data tier. And to make this even easier the Oracle Autonomous Database environment can be provisioned in minutes with a few simple clicks or an API call to the Oracle Cloud.

## About the Oracle Database 19c New Features Workshop

This workshop lets you try out many of the Oracle Database 19c new features, including general, security, performance, Big Data and Data Warehouse, and diagnose-ability enhancements. When you reserve this workshop in the LiveLabs tenancy, you are provided two Linux compute instances named workshop-staged and workshop-installed. One instance has the Oracle Database 19c installer files staged on it; the other has Oracle Database 19c already installed. Both compute instances have a noVNC desktop, which provides an easy-to-use interface.

To obtain your compute instances, you need to create SSH keys for yourself. When you reserve this workshop in the LiveLabs tenancy, you are asked to provide your public SSH key on the registration page. For help on generating SSH keys, see the lab called Generate SSH Keys. If you are working in your own tenancy, whether free or paid, you are guided through the steps to create the two compute instances using Resource Manager.

All labs are independent of each other, so you don't need to do them in any particular order.

### Cleaning Up PDBs at the beginning of each lab

The workshop-installed compute instance consists of three container databases (ORCL, CDB1, and CDB2). You only use CDB1 and CDB2. CDB1 contains one pluggable database (PDB1). CDB2 doesn't contain any pluggable database.

If you need to reset CDB1 back to its original state, you can run the `/home/oracle/labs/19cnf/cleanup_PDBs.sh` shell script. This script drops all PDBs that may have been created during the labs, and re-creates `PDB1` in CDB1. Enter the following command to run the script.

```nohighlighting
$ <copy>/home/oracle/labs/19cnf/cleanup_PDBs.sh</copy>
...
$
```

In case you need to recreate `CDB1` and `PDB1`, run the `/home/oracle/labs/19cnf/recreate_CDB1.sh` shell script.

```nohighlighting
$ <copy>/home/oracle/labs/19cnf/recreate_ORCL.sh</copy>
...
$
```

## Copying and pasting text

The instructions include a lot of code that you need to enter into a terminal window. Rather than enter the code manually, which often takes a long time and is prone to errors, you can copy and paste code. There are several ways to do so.

With the lab instructions displayed on your compute instance's desktop, it's easy to copy text directly from the lab and paste text into any application using the **Copy** and **Paste** options on the speed menu. You can also use **Ctrl+C** to copy text, and click the middle mouse button to paste text. Some instructions in the labs may include a Copy button.

If you need to copy and paste text from your local computer to the compute instance:

1. Click the **Clipboard** icon on the control bar (5th button down). In the **Clipboard** dialog box, paste some copied text, for example, "This text was copied from my local computer".

    ![Clipboard](images/clipboard.png "Clipboard")

2. Open the application into which you want to paste the text, for example, a terminal window.

3. Paste the text using your mouse controls (middle button or context menu option). It's important that you open the Clipboard dialog box and paste your text into it before you open the application into which you want to paste the text. Otherwise, the Paste option on the context menu may be grayed out.





## General Database Overall Enhancements

The following new features in Oracle Database 19c are covered in the labs:

- Install Oracle Database 19c using automatic root script execution
- Clone a PDB by using DBCA in silent mode
- Relocate a PDB by using DBCA in silent mode
- Duplicate a CDB by using DBCA in silent mode
- Decrease the transportable tablespace (TTS) import and export time
- Omit the column encryption attribute during import
- Use RMAN to connect to a PDB to use the recovery catalog
- Explore automatic deletion of flashback logs
