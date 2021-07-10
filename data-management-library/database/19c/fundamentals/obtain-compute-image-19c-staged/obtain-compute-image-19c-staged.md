# Obtain a Compute Image with Staged Oracle Database 19c Installer Files

## Introduction
Use Resource Manager in Oracle Cloud Infrastructure (OCI) to quickly deploy a compute instance with the private **workshop-staged** image in Oracle Cloud Marketplace. The image has the Oracle Database 19c installer files staged on it and has a noVNC desktop, which provides an easy-to-use browser user interface. On the desktop, there are shortcuts to a terminal window and a Firefox browser.

Begin by creating and applying a stack in Resource Manager. A stack is a collection of Oracle Cloud Infrastructure resources corresponding to a given Terraform configuration. A Terraform configuration is a set of one or more TF files written in HashiCorp Configuration Language (HCL) that specify the Oracle Cloud Infrastructure resources to create. The Terraform configuration that you use here loads a custom image stored in Oracle Cloud Marketplace and creates a virtual cloud network (VCN). After your compute instance is created, you can log into it via a browser.

Oracle highly recommends that you create a new VCN when creating the stack, which is the default, to ensure you have all of the proper connectivity required to access your compute instance and run the applications. If you choose to use one of your own existing VCNs, be sure that your VCN has a public subnet and a routing table configured with an Internet Gateway. Your VCN also requires several ingress security rules, which is covered in STEP 1. If you accept the default to create a new VCN when creating the stack, then you can skip STEP 1.

> **Note**: If you are working in the LiveLabs environment, you can skip STEP 1 and STEP 2 because they are already done for you.

Estimated Lab Time: 30 minutes

### Objectives

Learn how to do the following:

- Add security rules to your existing VCN
- Create and apply a stack in Resource Manager
- Connect to your compute instance from a browser and set up your desktop


### Prerequisites

Before you start, be sure that you have done the following:

- Obtained an Oracle Cloud account
- Signed in to Oracle Cloud Infrastructure
- Created SSH keys in Cloud Shell

## **STEP 1**: Add security rules to your existing VCN

Configure ingress rules in your VCN's default security list to allow traffic on port 22 for SSH connections, traffic on ports 1521 to 1524 for the database listeners, and traffic on port 6080 for HTTP connections to the noVNC browser interface.

> **Note**: If you plan to let the terraform script create a new VCN for you (recommended), you can skip this step and proceed to STEP 2. If you are working in the LiveLabs environment, you can skip this step and STEP 2 and proceed to STEP 3.

1. From the navigation menu in Oracle Cloud Infrastructure, select **Networking**, and then **Virtual Cloud Networks**.

2. Select your VCN.

3. Under **Resources**, select **Security Lists**.

4. Click the default security list.

5. For each port number/port number range (22, 1521-1524, 6080), click **Add Ingress Rule**. For **Source CIDR**, enter **0.0.0.0/0**. For **Destination port range**, enter the port number. Click **Add Ingress Rule**.

## **STEP 2**: Create and apply a stack in Resource Manager

> **Note**: If you are working in the LiveLabs environment, you can skip this step and proceed to STEP 3.

1. Download [19cnf-workshop-staged.zip](https://objectstorage.eu-frankfurt-1.oraclecloud.com/p/8ymA1czX8XRytfobEBedr8guxJfPwZ9gRUH2PZjbk2AeQBnFHMM06si6NSitFeqY/n/frmwj0cqbupb/b/19cNewFeatures/o/19cnf-workshop-staged.zip) to a directory on your local computer. This ZIP file contains the terraform script that you use with Resource Manager.

2. On the home page in Oracle Cloud Infrastructure, click **Create a stack**. The **Create Stack** page is displayed.

  ![Create a stack tile on the home page](images/create-a-stack.png)

    The **Create Stack - Stack Information** page is displayed.

3. Select **My Configuration**.

4. In the **Stack Configuration** area, select **.Zip file**, click **Browse**, select the ZIP file that you just downloaded, and then click **Open**.

  ![Stack Information](images/stack-information-page.png "Stack Information page")

5. For **Name**, leave the default stack name as is.

6. For **Description**, leave the default description for the stack as is.

7. Select your compartment to store the stack.

8. Click **Next**. The **Configure Variables** page is displayed.

9. In the **Instance** section, make sure the appropriate region is selected.

10. Select your compartment.

11. Select an availability domain.

12. Select **Paste SSH Key**, and then paste the contents of your public key into the box. Be sure that there are no carriage returns. The key should be all on one line.

  ![Instance Configuration](images/instance-configuration.png "Instance Configuration")

13. In the **Network** section, choose one of the following options:

    - **Option 1 (Recommended)**: Leave the default settings as is to create a new VCN.

    ![Network Configuration](images/network-configuration.png "Network Configuration")

    - **Option 2**: Select **Use existing VCN** and select an existing VCN and subnet in your tenancy. You may need to select different compartments to locate these items. Your VCN needs to have a public subnet and a routing table configured with an Internet Gateway. It also requires the ingress security rules specified in STEP 1 above.

14. Click **Next**.

15. On the **Review** page, verify that the information is correct.

  ![Review page](images/review-page.png "Review page")

16. In the **Run Apply on the created stack** section, select **Run Apply** to immediately provision the resources.

  ![Run Apply section](images/run-apply-section.png "Run Apply Section")

17. Click **Create**.

    Resource Manager starts provisioning your compute instance. The **Job Details** page is displayed. You can monitor the progress of the job by viewing the details in the log. The job is finished when the state reads **Succeeded**.

  ![Job Details page](images/job-details-page.png "Job Details page")

18. Scroll down in the log to the last line. This line contains the URL to access your compute instance via a browser. For example, your URL looks similar to the one below, with your own public IP address. Copy the URL (don't include `remote_desktop =`) to the clipboard because you need it in STEP 3.

    ```
    remote_desktop = http://public-ip-address:6080/index.html?password=s0TGCvFfk9&resize=scale&autoconnect=true&quality=9&reconnect=true
    ```


## **STEP 3**: Connect to your compute instance via a browser and set up your desktop

> **Note**: If you are working in the LiveLabs tenancy, you are provided the URL to your compute instance.

1. In a browser, enter the URL to your workshop-staged compute instance.

   You are automatically logged into your compute instance and presented with a user-friendly desktop. On the desktop, you can find shortcuts to Firefox and a terminal window. The "Install Oracle Database 19c with Automatic Root Script Execution" lab instructions are displayed in Firefox.

    ![noVNC Desktop](images/noVNC-desktop.png "noVNC Desktop")

2. To enable full screen display: Click the small gray tab on the middle-left side of your screen to open the control bar. Next, click the **Fullscreen** icon (6th button down).

    ![Small Grey Tab](images/small-grey-tab.png "Small Grey Tab")

    ![Full Screen](images/full-screen.png "Full Screen")

3. If the workshop guide is not open on the desktop: Double-click the Firefox icon on the desktop to open Firefox. On the Firefox toolbar, click **Workshop Guides** and then select **Oracle Database 19c New Features**.



## Learn More

- [Resource Manager](https://docs.oracle.com/en-us/iaas/Content/ResourceManager/Concepts/landing.htm#ResourceManager)
- [Video about Resource Manager](https://youtu.be/udJdVCz5HYs)
- [Oracle Cloud Marketplace](https://cloudmarketplace.oracle.com/marketplace/en_US/homePage.jspx)

## Acknowledgements

- **Author**- Jody Glover, Principal User Assistance Developer, Database Development
- **Last Updated By/Date** - Jody Glover, Database team, July 9 2021
