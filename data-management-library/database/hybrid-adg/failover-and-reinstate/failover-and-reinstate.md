# Failover and Reinstate

## Introduction
A failover is an unplanned event that assumes the primary database is lost. The standby database is converted to a primary database immediately. A failover might result in some data loss when you use **Maximum Performance** protection mode. After a failover the old primary database must be reinstated as a physical standby which is made simpler with flashback database and Data Guard broker enabled. To execute a failover and reinstatement execute the following commands in Data Guard Broker. 

Estimated Lab Time: 30 minutes

### Objectives

-   Setup the current primary database flashback on 
-   Failover 
-   Reinstate the previous primary database

### Prerequisites

This lab assumes you have already completed the following labs:

- Deploy Active Data Guard with LVM or ASM
- Test with Active Data Guard

## **STEP 1:** Setup the Current Primary Database Flashback

In the previous lab, you have done the Data Guard switch over. Now, the current primary database is the DBCS and the current standby database in the on-premise database.

1. From the Cloud side. Check the flashback status of the current primary database

    ```
    [oracle@dbstby ~]$ sqlplus / as sysdba

    SQL*Plus: Release 19.0.0.0.0 - Production on Wed Feb 5 05:31:25 2020
    Version 19.10.0.0.0

    Copyright (c) 1982, 2019, Oracle.  All rights reserved.
    ```


    Connected to:
    Oracle Database 19c EE Extreme Perf Release 19.0.0.0.0 - Production
    Version 19.10.0.0.0
    
    SQL> select open_mode,database_role,flashback_on from v$database;
    
    OPEN_MODE	     DATABASE_ROLE    FLASHBACK_ON
    -------------------- ---------------- ------------------
    READ WRITE	     PRIMARY	      NO
    
    SQL> 
    ```

2. If the flashback is not enabled you need to setup database flashback on, otherwise you won't be able to reinstate the primary after the failover.

    ```
    SQL> shutdown immediate;
    Database closed.
    Database dismounted.
    ORACLE instance shut down.
    SQL> startup mount;
    ORACLE instance started.

    Total System Global Area 1.6106E+10 bytes
    Fixed Size		    9154008 bytes
    Variable Size		 2080374784 bytes
    Database Buffers	 1.3992E+10 bytes
    Redo Buffers		   24399872 bytes
    Database mounted.
    SQL> alter database flashback on;

    Database altered.

    SQL> alter database open;

    Database altered.

    SQL> alter pluggable database all open;

    Pluggable database altered.

    SQL> select open_mode,database_role,flashback_on from v$database;

    OPEN_MODE	     DATABASE_ROLE    FLASHBACK_ON
    -------------------- ---------------- ------------------
    READ WRITE	     PRIMARY	      YES

    SQL> exit
    Disconnected from Oracle Database 19c EE Extreme Perf Release 19.0.0.0.0 - Production
    Version 19.10.0.0.0
    [oracle@dbstby ~]$ 
    ```

## **STEP 2:** Failover

1. Connect with DGMGRL, validate the primary and standby database

    ```
    [oracle@dbstby ~]$ dgmgrl sys/Ora_DB4U@orcl
    DGMGRL for Linux: Release 19.0.0.0.0 - Production on Wed Feb 5 05:41:24 2020
    Version 19.10.0.0.0

    Copyright (c) 1982, 2019, Oracle and/or its affiliates.  All rights reserved.

    Welcome to DGMGRL, type "help" for information.
    Connected to "ORCL"
    Connected as SYSDBA.
    DGMGRL> show configuration

    Configuration - adgconfig

      Protection Mode: MaxPerformance
      Members:
      orcl_nrt1d4 - Primary database
        orcl        - Physical standby database 

    Fast-Start Failover:  Disabled

    Configuration Status:
    SUCCESS   (status updated 18 seconds ago)

    DGMGRL> validate database orcl_nrt1d4

      Database Role:    Primary database

      Ready for Switchover:  Yes

      Managed by Clusterware:
        orcl_nrt187:  NO             
        Validating static connect identifier for the primary database orcl_nrt187...
        The static connect identifier allows for a connection to database "orcl_nrt187".

    DGMGRL> validate database orcl

      Database Role:     Physical standby database
      Primary Database:  orcl_nrt1d4

      Ready for Switchover:  Yes
      Ready for Failover:    Yes (Primary Running)

      Managed by Clusterware:
        orcl_nrt1d4:  NO             
        orcl       :  NO             
        Validating static connect identifier for the primary database orcl_nrt1d4...
        The static connect identifier allows for a connection to database "orcl_nrt1d4".

      Log Files Cleared:
        orcl_nrt187 Standby Redo Log Files:  Cleared
        orcl Online Redo Log Files:          Not Cleared
        orcl Standby Redo Log Files:         Available

    DGMGRL>  
    ```

2. Failover to current standby.

    ```
    DGMGRL> failover to orcl
    Performing failover NOW, please wait...
    Failover succeeded, new primary is "orcl"
    DGMGRL> show configuration

    Configuration - adgconfig

      Protection Mode: MaxPerformance
      Members:
      orcl        - Primary database
        orcl_nrt1d4 - Physical standby database (disabled)
          ORA-16661: the standby database needs to be reinstated

    Fast-Start Failover:  Disabled

    Configuration Status:
    SUCCESS   (status updated 13 seconds ago)

    DGMGRL> 
    ```

  Now, the primary is the on-premise database, and the standby database is disabled, which needs to be reinstated.

## **STEP 3:** Reinstate the Previous Primary Database

1. Connect to the cloud side(the previous primary), replace `ORCL_nrt1d4` with your previous primary db unique name. Shutdown the database and startup mount before reinstating. 

    ```
    DGMGRL> <copy>connect sys/Ora_DB4U@orcl_nrt1d4</copy>
    Connected to "ORCL_nrt1d4"
    Connected as SYSDBA.
    
    DGMGRL> <copy>shutdown immediate</copy>
    Database closed.
    Database dismounted.
    ORACLE instance shut down.
    Connected to an idle instance.
    
    DGMGRL> <copy>startup mount</copy>
    Connected to "ORCL_nrt1d4"
    ORACLE instance started.
    Database mounted.
    DGMGRL> 
    ```



2. Connect to the new primary side, reinstate the standby database, replace `ORCL_nrt1d4` with your previous primary db unique name.

    ```
    DGMGRL> <copy>connect sys/Ora_DB4U@orcl</copy>
    Connected to "ORCL"
    Connected as SYSDBA.
    
    DGMGRL> <copy>reinstate database orcl_nrt1d4</copy>
    Reinstating database "orcl_nrt1d4", please wait...
    Reinstatement of database "orcl_nrt1d4" succeeded
    
    DGMGRL> <copy>show configuration</copy>
    
    Configuration - adgconfig
    
      Protection Mode: MaxPerformance
      Members:
      orcl        - Primary database
        orcl_nrt1d4 - Physical standby database 
    
    Fast-Start Failover:  Disabled
    
    Configuration Status:
    SUCCESS   (status updated 21 seconds ago)
    
    DGMGRL> 
    ```

3. Check the status of the new standby database

    ```
    [oracle@dbstby ~]$ sqlplus / as sysdba

    SQL*Plus: Release 19.0.0.0.0 - Production on Wed Feb 5 05:53:48 2020
    Version 19.10.0.0.0

    Copyright (c) 1982, 2019, Oracle.  All rights reserved.
    Connected to:
    Oracle Database 19c EE Extreme Perf Release 19.0.0.0.0 - Production
    Version 19.10.0.0.0
    
    SQL> select open_mode,database_role from v$database;
    
    OPEN_MODE	     DATABASE_ROLE
    -------------------- ----------------
    READ ONLY WITH APPLY PHYSICAL STANDBY
    
    SQL> 
    ```



Congratulations, you have successfully completed the workshop!

## Acknowledgements
* **Author** - Minqiao Wang, DB Product Management
* **Last Updated By/Date** - Minqiao Wang, Mar 2021


