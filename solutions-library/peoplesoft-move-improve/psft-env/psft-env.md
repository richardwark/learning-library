# Creating Environment in PeopleSoft

## Introduction

This lab walks you through the steps to a PeopleSoft Environment from the previously created environment template

Estimated Lab Time: 90 minutes

### Objectives

The purpose of this lab is to show you how to create a PeopleSoft Environment from an environment template in the PeopleSoft Cloud Manager.

In this lab, you will:
* Create a PeopleSoft Environment

### Prerequisites
- A PeopleSoft Cloud Manager Instance
- A PeopleSoft Environment Template 

## **STEP 1**: Creating a New PeopleSoft Environment

1. 	Navigate to Dashboard | Environments.  Click Create Environment button.

  ![](./images/e1.png "")

2. 	Provide a unique Environment Name - **WorkshopEnvironment** . Select the Template that was created in previous section – **TestWorkshop**. Click **yes** for **Pause after infra creation**.  

  ![](./images/workshop.png "")

3. Go to **Environment Attributes -> Region and Availability Domains -> Credentials**

  Give following values to the field.

  No. | Full Tier | Credentials
  --- | --------- | -----------
  1 | Gateway Administrator Password | Psft1234
  2 | Web Profile Password for user PTWEBSERVER | Psft1234
  3 | Database Connect Password | Psft1234
  4 | Weblogic Administrator Password | Psft1234
  5 | Database Administrator Password | **Psft1234#**
  6 | Database Access Password | Psft1234
  7 | Database Operator Password | Psft1234

  ![](./images/e3.png "")

  Leave the rest as default. You can also expand all sections under Environment Attributes. 

4. Scroll up and click Done on the top right to begin the environment creation process. 

  ![](./images/e4.png "")

5. Accept the license. 

  ![](./images/e5.png "")

6. Refresh the page and click on the arrow button -> Details.

  ![](./images/create1.png "")

7. Monitor the deployment logs under Dashboard -> Environments -> Environment Name -> Action Menu -> Details -> Logs

  ![](./images/cl.png "")

  You can also go to **Provision Task Status** to see detailed progress status for every step. Click on **Deployment Tasks**. If any step fails, you can change the attribute as per the error and start the process from where it failed.

    ![](./images/pts.png "")

8. Once environment creation is completed, you can click on arrow button -> Deploy to start provisioning.

  ![](./images/create2.png "")

9. Monitor the deployment logs under Dashboard -> Environments -> Environment Name -> Action Menu -> Details -> Logs

  ![](./images/e10.png "")

  You can also go to **Provision Task Status** to see detailed progress status for every step. Click on **Deployment Tasks**. If any step fails, you can change the attribute as per the error and start the process from where it failed.

    ![](./images/pts2.png "")

10. After the environment up and running, you can perform a variety of actions on the environment by using the Related Actions button corresponding to each environment. 

  Cloning is a popular feature for Cloud Manager. Trial accounts don't have enough resources to accomodate a cloned environment. Please switch to a paid account for that feature.

  ![](./images/e11.png "")

  The actions can be:

    • **Details**: Select this option to view environment details and to perform additional actions on the environment such as performing a health check, applying a PeopleTools patch, viewing logs, and managing PUM connections.

    • **Start**: Select this option to start all the instances and then all the domains within them.

    • **Stop**: Select this option to stop all domains and shutdown all the instances. In case of database, only compute database instances are shutdown.

    • **Delete**: Select this option to remove the environment.

    • **Manage Node**: Select this option to scale environment up or down.

    • **Clone Environment**: Select this option to clone an existing environment.

    • **Refresh**: Select this option to refresh the database or the database, ps app home and ps cust home.  
  This option is only available for DBaaS environments.

    • **Backup and Restore**: Select this option to backup or restore an environment.

  Login credential: 

      ```
      Username : PS
      Password: Psft1234
      ```

You may proceed to the next lab.

## Acknowledgements
* **Authors** - Rich Konopka, Peoplesoft Specialist, Megha Gajbhiye, Cloud Solutions Engineer
* **Contributor** -  Sara Lipowsky, Cloud Engineer
* **Last Updated By/Date** - Sara Lipowsky, Cloud Engineer, February 2021

