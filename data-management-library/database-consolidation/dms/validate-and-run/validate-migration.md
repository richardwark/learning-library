# Validate Migration

## Introduction

This lab walks you through the steps to validate a migration prior to running it. Before you can run a job with a migration resource in OCI Database Migration, the migration resource must be validated. The validation job will check that all associated database and GoldenGate environments are correctly set up.

Estimated Lab Time: 20 minutes

### Objectives

In this lab, you will:
* Validate a migration

### Prerequisites

* An Oracle Cloud Account - Please view this workshop's LiveLabs landing page to see which environments are supported
* This lab requires completion of the preceding labs in the Contents menu on the left.

*Note: If you have a **Free Trial** account, when your Free Trial expires your account will be converted to an **Always Free** account. You will not be able to conduct Free Tier workshops unless the Always Free environment is available. **[Click here for the Free Tier FAQ page.](https://www.oracle.com/cloud/free/faq.html)***

## **STEP 1**: Validate Migration

1. In the OCI Console Menu ![](images/hamburger.png =22x22), go to **Migration > Migrations**

  ![](images/1.png =90%x*)

2. Select **TestMigration**

  ![](images/2.png =90%x*)

3. If Migration is still being created, wait until Lifecycle State is Active

4. Press **Validate** button

  ![](images/3.png =90%x*)

5. Click on **Jobs** in left-hand **Resources** list

  ![](images/4.png)

6. Click on most recent Evaluation Job

7. Click on **Phases** in left-hand **Resources** list

  ![](images/5.png =20%x*)

8. Phases will be shown and status will be updated as phases are completed. It can take 2 minutes before the first phase is shown.
    ![](images/Pump.png =90%x*)

9. If a phase has failed, it will show with status **Failed**. In this case press **Download Log** to learn more about the reason of failure. Press **Abort** on a failed job to allow further jobs or deleting of the migration.

  ![](images/9.png =90%x*)

10. Once all phases show complete, move to the next step.

## **STEP 2**: Run Migration

  1. In the OCI Console Menu ![](images/hamburger.png =22x22), go to **Migration > Migrations**

    ![](images/1.png =90%x*)

  2. Select **TestMigration**

    ![](images/2.png =90%x*)

  3. Press **Start** to begin the Migration

![](images/done.png =90%x*)

  4. The Start Migration dialog is shown. Select the phase **Monitor Replication Lag** in the 'Require User Input After' list. This will cause the replication to run continuously until the Migration is resumed (If nothing is shown continue to number 6).

  5. Press **Start** to begin the Migration

  6. Click on **Jobs** in left-hand **Resources** list

  7. Click on most recent Evaluation Job

  8. Click on **Phases** in left-hand **Resources** list

  9. Job phases are updated as the migration progresses

  10. Wait till all the phases have completed and your screen should look the like picture below.

  ![](FD/2.png =90%x*)

  13. The migration runs the final cleanup phases and shows as **Succeeded** when finished



You may now [proceed to the next lab](#next).

## Learn More

* [Managing Migration Jobs](https://docs.oracle.com/en-us/iaas/database-migration/doc/managing-migration-jobs.html)

## Acknowledgements
* **Author** - Alex Kotopoulis, Director, Product Management
* **Contributors** -  Kiana McDaniel, Hanna Rakhsha, Killian, Lynch, Solution Engineers, Austin Specialist Hub
* **Last Updated By/Date** - Killian Lynch, Kiana McDaniel, Hanna Rakhsha, Solution Engineers, July 2021
