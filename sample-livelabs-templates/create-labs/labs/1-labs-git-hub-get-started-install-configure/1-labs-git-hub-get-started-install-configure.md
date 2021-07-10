#  Get Started with Git and Set up the GitHub Environment

## Introduction

In this lab, you will learn how to create a GitHub Account and associate it with your Oracle email account, set up the GitHub Development Environment, and install GitHub Desktop.

### Objectives
* Submit a workshop in LiveLabs.
* Create a GitHub Account.
* Associate your GitHub account with your Oracle email account.
* Set up the GitHub Environment.
* Install GitHub Desktop Client.

### What Do You Need?

* Familiarity with HTML is helpful.
* Access to the LiveLabs Workshop Management System

## **STEP 1:** Submit a workshop to the LiveLabs Workshop Management System
Before getting started, we recommend you submit your workshop to the LWMS. 	Submitting a workshop tells the Oracle ecosystem you are working on a workshop and submits your idea to the Workshop Council.  We urge you not to delay this step.  There are hundreds of workshops already, this step is important to helps us preserve the quality and integrity of the workshop catalog

1.  Login to Corporate VPN
2.  Go to http://bit.ly/oraclelivelabs.  This is only available to Oracle Employees at this time.
3.  Click **Submit a New LiveLab**
4.  Fill in the required fields including the abstract *thoroughly*.  Failure to do so will prevent your workshop from being approved.
5.  Click **Submit**
6.  We recommend you don't start working on your workshop until your workshop has been approved by a council member.

Once your workshop is submitted, it will be sent to the workshop council.  The workshop council will approve your workshop or ask for more details.  Once approved, you will be entered into the workflow and given additional steps to progress through to production.

## **STEP 2:** Download and Install the latest version of Git (Optional Step)
  **Note**: For UA Developers, Oracle recommends the usage of the GitHub Desktop client because of its simple and user friendly user interface, and it is much easier than using the Git command line. Therefore, this is an optional Step.

To install Git:
1. Install Git for your operating system from the [Git download site] (https://git-scm.com/downloads).
2. Click the required option under **Downloads** (**Windows** in this example) and save the installer file.
3. Browse to the downloaded location and double-click the file to launch the installer.
4. Click **Yes** in the **User Account Control** dialog box.
5. Click **Next** in the **GNU General Public License** dialog box.
6. Under **Choose the default behavior of `git pull`**, leave the selected **Default (fast-forward or merge)** option as is and click **Next**.
7. In the **Configuring experimental options** dialog box, click **Install**.

## **STEP 3:** Create and Set Up Your GitHub Account

In this Step, you will create and set up your GitHub account.

1. Create a free GitHub Account here: [GitHub Web UI](https://github.com/) if you don't have one.
    ![](./images/git-download-install-create-account.png " ")
2.  If this is a new account, use your Oracle email ID to register.

    **Note**: Do not create a secondary new account to join GitHub. Ensure that your GitHub account is associated to your @oracle.com email ID.
3. Go to [GitHub Settings](https://github.com/settings/profile) and configure the following:
    *   Set your Name as it appears in your Aria employee page.
    *   Add your Profile Picture.
4. Click **Account** to add your user name in the **Enter a user name** dialog. For example, achepuri, LauranSerhal etc.
5. Set up a 2 Factor Authentication here: [GitHub Security](https://github.com/settings/security).
    ![](./images/git-2-factor-authentication.png " ")

## **STEP 4:** Install GitHub Desktop
The GitHub Desktop application is a UI client for Windows and Mac that simplifies the complex set of GitHub command line arguments. GitHub Desktop is a fast and easy way to contribute to projects and it simplifies your development workflow. It is much easier than using Git command line.

To setup the GitHub Development Environment and install **GitHub Desktop**:

1. Download and install **GitHub Desktop** from [GitHub Desktop](https://desktop.github.com/).

2. When the software is successfully installed, open the **GitHub Desktop**.

  ![](./images/git-hub-desktop-login-screen.png " ")


3. Click **File > Options > Sign in**, enter your GitHub **Username** or **email address**, **Password**, and then click **Sign in**.
  You will receive an authentication code to your cell phone. Enter this code in the **Authentication code** field in the **Sign in** dialog box.

  **Note**: The authentication code is valid only for a few seconds.

    You are now logged in to **GitHub Desktop**.
    ![](./images/get-started-git-hub-desktop.png " ")

## **STEP 5:** Fork the learning-library Repository on Your GitHub Account
  We create workshops and labs in the **learning-library** repository of the **oracle** project. You must fork the learning-library repository to create a duplicate personal copy of the repository on your GitHub account. You own the forked repository and you can edit its contents without affecting the parent repository.

  For example, if a user named achepuri forks the learning-library repository in the oracle project, a duplicate repository [achepuri/learning-library](https://github.com/achepuri/learning-library) is created.

  To fork the **learning-library** repository:
1. Log in to the [GitHub Web UI](http://github.com), using your GitHub account.
2. Navigate to the [oracle/learning-library repository](https://github.com/oracle/learning-library).
3. Click **Fork** to display the following message: **How are you planning to use this fork?**.
  ![](./images/get-started-git-hub-webUI-fork.png " ")
4. Select the option that indicates your local repository.
In the following example, user achepuri has forked the **learning-library** repository.

![](./images/get-started-git-hub-webui-forked-library.png " ")

In the next Step, you will clone this forked repository.

## **STEP 6:** Clone the Forked Repository
A clone is a copy of your forked repository that lives on your local computer instead of on [GitHub Web UI](http://github.com). When you clone your forked repository, you can edit the files in your preferred editor, such as **Atom** editor, and use the **GitHub Desktop** client to keep track of your changes without having to be online.

To clone the forked repository:
1. Open your **GitHub Desktop** application and log in using your GitHub account.
2. Click **File > Clone repository** to display the **Clone a repository** dialog box.

    ![](./images/git-hub-desktop-clone-repository.png " ")

3. Select your own repository such as **your account/learning-library** from **Your repositories**. In this example, there is only one repository displayed named **achepuri/learning-library**. Under **Local path**, select the local path on your machine where the repository is going to be cloned (copied). This is where the project files get copied to your local file system. In this example, the local path is **C:\Users\achepuri.ORADEV\Documents\GitHub**.  

    ![](./images/git-hub-desktop-clone-repository_dialog.png " ")

4. Click **Clone**.

  The **learning-library** repository files appear in the local path you just specified. You can now start working on your labs and workshops!

  ![](./images/git-hub-my-cloned-repository.png " ")

  **Note**: The local cloned repository is connected to the remote fork version. You can push your local changes to the remote fork version when you are online to keep them in sync.

  **Important Note**: The **create-labs** folder (shown in the above screen) and its contents are internal to this "**Creating Labs and Workshops**" workshop. This folder is not available at the production. This means that when you fork the **oracle\learning-library** repository to your fork, such as **your account\learning-library**, you will not find the **create-labs** folder, and thereby it will not be available in your cloned repository as well.

  When you make a clone, you can create your own project folder, edit the files in your preferred editor, such as **Atom**, and use **GitHub Desktop client** to keep track of your changes without having to be online.

  The repository you cloned is still connected to the remote version (your fork) so that you can push your local changes to the remote to keep them synced when you're online.

5. You can also use Github Desktop to Synchronize the changes that you have made in your local file system to the forked content on your github repo, more details on using Github Desktop in Lab 4 of this workshop and also on Otube [Working with GitHub Desktop](https://otube.oracle.com/media/t/1_bxj0cfqf).

![](./images/github-desktop-sync.png " ")

You may now [proceed to the next lab](#next).

## Want to Learn More?

* [Setting Up Environment](https://otube.oracle.com/media/Setting+Up+GitHub/0_93stcjpb)
* [Download and Install Git for Windows and Mac](https://git-scm.com/download/win)
* [Using GitHub Desktop to merge, commit and make pull requests](https://otube.oracle.com/media/t/1_bxj0cfqf)


## Acknowledgements

* **Author:**
    * Anuradha Chepuri, Principal User Assistance Developer, Oracle GoldenGate
* **Contributors:**
    * Lauran Serhal, Principal User Assistance Developer, Oracle Database and Big Data User Assistance

* **Reviewed by:**  
    * Aslam Khan, Senior User Assistance Manager, ODI, OGG, EDQ
    * Tom McGinn, Database and Database Cloud Service Senior Principal Product Manager, DB Development - Documentation


* **Last Updated By/Date:** Madhusudhan Rao, February 2021
