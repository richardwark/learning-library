# Cleaning Up After the Workshop

## Introduction

Now that you have completed the workshop, you may want to remove the artifacts left behind in your Oracle Cloud trial account. This guide will show you how to remove everything that you created during the workshop. Note that compute instances and load balancers left running in your Oracle Cloud trial account will continue to consume trial credits until they are terminated.

## Need Help?
Please submit feedback or ask for help using our [LiveLabs Support Forum](https://community.oracle.com/tech/developers/categories/livelabsdiscussions). Please click the **Log In** button and login using your Oracle Account. Click the **Ask A Question** button to the left to start a *New Discussion* or *Ask a Question*.  Please include your workshop name and lab name.  You can also include screenshots and attach files.  Engage directly with the author of the workshop.

If you do not have an Oracle Account, click [here](https://profile.oracle.com/myprofile/account/create-account.jspx) to create one.
# Remove All Deployed and Installed Workshop Components

## Clean up Oracle Cloud Account

### **STEP 1**: Delete Instances

- As documented in the other labs, connect into your Oracle Cloud Account, and go to the Cloud Console.
- From the Cloud Console, select **Compute > Images** from the top menu option

  ![](images/manualcleanup/pic01.png)

- We will now delete the three instances created by the Workshop. Delete each of the following three images by clicking in the **three dots** to the right of the image, then select **Terminate**

  ![](images/manualcleanup/pic03.png)

- Ensure the **Permanently delete** box is checked, and click on **Terminate Instance**.

  ![](images/manualcleanup/pic04.png)

- Repeat the previous steps to delete the other two instances, and wait until the instances show **Terminated**.

### **STEP 2**: Delete Load Balancers

  ![](images/manualcleanup/pic05.png)

- From the top menu bar, click on **Networking > Load Balancers**

  ![](images/manualcleanup/pic06.png)

- Click on the **three dots** next to the First load balancer in the list, and click on **Terminate**

  ![](images/manualcleanup/pic07.png)

- Click on **OK**

  ![](images/manualcleanup/pic08.png)

- **Repeat the steps** for the remaining Load Balancers until all used by the workshop have been removed.

  ![](images/manualcleanup/pic09.png)

### **STEP 3**: Delete the Virtual Network

- Using the top menu bar, go to **Networking > Virtual Cloud Networks**.

  ![](images/manualcleanup/pic10.png)

- Click on the **Three Dots** to the right of the Virtual Cloud Network, and click on **Terminate**.

  ![](images/manualcleanup/pic11.png)

### **STEP 4**: Delete the API Key Fingerprint

- Using the top menu bar, go to **Identity > Users**.

  ![](images/manualcleanup/pic12.png)

- Click on the **User's Name**.

  ![](images/manualcleanup/pic13.png)

- From the **API Key** section, click on the **Delete** button to the right of the **Fingerprint** you created during this workshop. Confirm the delete by clicking on **OK** in the popup dialog box.

  ![](images/manualcleanup/pic14.png)
