# Using Events and Notification

## Introduction

The Oracle Cloud Infrastructure Notifications service broadcasts messages  to distributed components through a publish-subscribe pattern, delivering secure, highly reliable, low latency and durable messages for applications hosted on Oracle Cloud Infrastructure and externally.

The Notifications service enables you to set up communication channels for publishing messages using topics  and subscriptions . When a message is published to a topic, the Notifications service sends the message to all of the topic's subscriptions.
In this lab we will verify notifications when a compute instance is launched and deleted.

## **Step 1:** Sign in to OCI Console and configure Notification and Event

1. Sign in using your tenant name, user name and password. Use the login option under **Oracle Cloud Infrastructure**.

    ![](images/Grafana_015.PNG " ")

2. First we will create a Notification topic and subscribe to this topic. Click the **Navigation Menu** in the upper left, navigate to **Developer Services**, and select **Notifications**.

	![](https://raw.githubusercontent.com/oracle/learning-library/master/common/images/console/developer-application-notification.png " ")

3. Click **Create Topic** and fill out the dialog box:

      - **Name**: Provide a name
      - **Description**: Provide a description

4. Click **Create**.


5. Once the topic state changes to **Active**, Click the topic Name. Click **Create Subscription** and fill out the dialog box:

      - **PROTOCOL**: Email
      - **EMAIL**: Provide your email id

6. Click **Create**.

7. Subscription details screen will be displayed with subscription status showing **Pending**.

8. Check the email account you specified and click the verification link for this subscription. Switch back to OCI console window and verify the subscription status changed to **Active**. You may need to refresh your browser.

9. You are now subscribed to a Notification topic. Next we will configure Events that will publish messages to this Notification topic.

10. From OCI Services menu, under **Application Integration**, click **Events Service**.

11. Click **Create Rule**, Fill out the dialog box:

    - **DISPLAY NAME** : Provide a name
    - **DESCRIPTION** : Provide a description

    Under **Rule Conditions**

    - Ensure **Event Type** is selected
    - **SERVICE NAME**: Compute
    - **EVENT TYPE** : Choose these 4 Types from the drop down menu. **Instance-Launch Begin**, **Instance-Launch End**, **Instance-Terminate Begin**, **Instance-Terminate End**

    Under **Actions**

    - **ACTION TYPE**: Notifications
    - **NOTIFICATIONS COMPARTMENT**: Choose your compartment
    - **TOPIC**: Choose the topic created earlier

12. Click **Create Rule**.

    ![](images/Events_002.PNG " ")


We have now configured Notification service and tied events to it with a specific compartment. When a new compute instance is launched or terminated an email notification will be sent to the email address specified.

## **Step 2:** Create VCN

1. From the OCI Services menu, under **Networking**, click **Virtual Cloud Networks**. Select the compartment assigned to you from drop down menu on left part of the screen under Networking and click **Start VCN Wizard**.

    **NOTE:** Ensure the correct Compartment is selected under COMPARTMENT list.

2. Click **VCN with Internet Connectivity** and click **Start VCN Wizard**.

3. Fill out the dialog box:

       - **VCN NAME**: Provide a name
       - **COMPARTMENT**: Ensure your compartment is selected
       - **VCN CIDR BLOCK**: Provide a CIDR block (10.0.0.0/16)
       - **PUBLIC SUBNET CIDR BLOCK**: Provide a CIDR block (10.0.1.0/24)
       - **PRIVATE SUBNET CIDR BLOCK**: Provide a CIDR block (10.0.2.0/24)
       - Click **Next**

4. Verify all the information and  Click **Create**.

5. This will create a VCN with following components.

    *VCN, Public subnet, Private subnet, Internet gateway (IG), NAT gateway (NAT), Service gateway (SG)*

6. Click **View Virtual Cloud Network** to display your VCN details.


## **Step 3:** Create compute instance and verify notification

1. From OCI services menu, Click **Instances** under **Compute**.

2. Click **Create Instance**. Fill out the dialog box:

      - **Name your instance**: Enter a name
      - **Choose an operating system or image source**: For the image, we recommend using the Latest Oracle Linux available.
      - **Availability Domain**: Select availability domain
      - **Instance Type**: Select Virtual Machine
      - **Instance Shape**: Select VM shape

      **Under Configure Networking**
      - **Virtual cloud network compartment**: Select your compartment
      - **Virtual cloud network**: Choose the VCN
      - **Subnet Compartment:** Choose your compartment.
      - **Subnet:** Choose the Public Subnet under **Public Subnets**
      - **Use network security groups to control traffic** : Leave un-checked
      - **Assign a public IP address**: Check this option

    ![](images/RESERVEDIP_HOL0011.PNG " ")

    - **Boot Volume:** Leave the default
    - **Add SSH Keys:** Leave empty

3. Click **Create**.

    **NOTE:** If 'Service limit' error is displayed choose a different shape from VM.Standard2.1, VM.Standard.E2.1, VM.Standard1.1, VM.Standard.B1.1  OR choose a different AD.

    ![](images/RESERVEDIP_HOL0011.PNG " ")

4. Switch to your email account and verify an event indicating compute instance launch was received.

5. Wait for Instance to be in **Running** state.

6. Switch to your email account and verify an event indicating compute instance create was received.

## **Step 4:** Delete the resources

1. Switch to  OCI console window.

2. If your Compute instance is not displayed, From OCI services menu Click **Instances** under **Compute**.

3. Locate first compute instance, Click Action icon and then **Terminate**.

    ![](images/RESERVEDIP_HOL0016.PNG " ")

4. Make sure Permanently delete the attached Boot Volume is checked, Click **Terminate Instance**. Wait for instance to fully Terminate.

    ![](images/RESERVEDIP_HOL0017.PNG " ")

5. Switch to your email account and verify an event indicating compute instance terminate was received.

6. Once the compute instance is fully terminated another email notification will arrive.

7. From OCI services menu Click **Virtual Cloud Networks** under Networking, list of all VCNs will appear.

7. Locate your VCN , Click Action icon and then **Terminate**. Click **Terminate All** in the Confirmation window. Click **Close** once VCN is deleted.

    ![](images/RESERVEDIP_HOL0018.PNG " ")

8. From OCI Services menu, under **Application Integration**, click **Notifications**. Click your Topic name.

9. Click **Delete**.

10. From OCI Services menu, under **Application Integration**, click **Event Service**.

11. Click your Rule name and Click **Delete**. In the dialog box type **DELETE** and click **Delete**.

## Acknowledgements
*Congratulations! You have successfully completed the lab.*

- **Author** - Flavio Pereira, Larry Beausoleil
- **Adapted by** -  Yaisah Granillo, Cloud Solution Engineer
- **Contributors** - Kamryn Vinson, QA Engineer Lead Intern, Arabella Yao, Product Manager Intern, DB Product Management
- **Last Updated By/Date** - Tom McGinn, August 2020

