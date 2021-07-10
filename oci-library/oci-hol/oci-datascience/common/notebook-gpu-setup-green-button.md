# Create a Notebook Session Running on a VM with A GPU

## Introduction

Data Science notebook sessions are interactive coding environments for building and training models. Notebook sessions provide access to a JupyterLab serverless environment that is managed by the Data Science service. All notebook sessions run in the Data Science service tenancy.

A notebook session is associated with a compute instance, VCN, subnet, and block storage. There are two block storage drives that are associated with a notebook session. There is a boot volume that is initialized each time the notebook session is activated. Any data on the boot volume is lost when the notebook session is deactivated or terminated. There is an additional block storage that is persisted when a notebook session is deactivated, but it is not persisted when a notebook session is terminated. This block volume is mounted in the ``/home/datascience`` directory and it is where the JupyterLab notebooks, data files, installed custom software, and other files should be stored.

When a notebook session is activated or created, the compute instance shape, block storage, VCN, and subnet are configured. These resources can only be changed by deactivating a notebook session, and then changing the configuration while activating the notebook session again. The size of the block storage can only be increased.

*Estimated Lab Time*: 15 minutes

### Objectives
In this lab, you:
* Use the Console to create a Data Science notebook session running on a virtual machine with a GPU
* Use the Console to open the Data Science notebook session

### Prerequisites

* A tenancy that is configured to work with the Data Science service.
* A configured project, VCN, and subnet.
* An account that has permission to create a Data Science notebook session.

## **STEP 1:** Creating a Notebook Session

1. [Login to the OCI Console](https://www.oracle.com/cloud/sign-in.html).
1. Click the **Navigation Menu** in the upper left, navigate to **Analytics & AI**, and select **Data Science**. 
	
	![](https://raw.githubusercontent.com/oracle/learning-library/master/common/images/console/analytics-ml-datascience.png " ")

1. Select the compartment for the project.
1. Click the name of the project to contain the notebook session.
    ![](./../speed-up-ds-with-the-ads-sdk/images/select-project.png)

1. Click **Create Notebook Session**.
    ![](./../speed-up-ds-with-the-ads-sdk/images/create-notebook.png)

1. Confirm that the compartment that is selected is the compartment that is assigned to your account. The **Workshop Details** section at the top of the instructions page lists the compartment. If the compartment is different, change it to the one listed in the **Workshop Details** section.
1. (Optional, but recommended) Enter a unique name for the notebook session (limit of 255 characters). If you do not provide a name, a name is automatically generated for you.
1. Select the VM shape **VM.GPU2.1**. This VM shape has one NVIDIA P100 (Pascal) GPU card (16GB of memory), 12 OCPUs, and 72 GB of CPU memory. The [GPU Shapes](https://docs.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm#vmshapes__vm-gpu) page has details on the specifications for GPU shapes.
1. Enter the block volume in GB. The suggested size is 100 Gb or larger.
1. Confirm that the compartment for the VCN is the same as the one that is listed in the **Workshop Details** section at the top of the instructions page. If not, change it to that compartment.
1. Confirm that the VCN is the one assigned to your account. It should be prefix with the same code as the compartment. For example, if your compartment is ``LL####-COMPARTMENT`` the VCN must be ``LL####-VCN``.
1. Confirm that the compartment for the subnet is the same as the one that is listed in the **Workshop Details** section at the top of the instructions page. If not, change it to that compartment.
1. Confirm that the subnet is the one assigned to your account. It should be prefix with the same code as the compartment. For example, if your compartment is ``LL####-COMPARTMENT`` the subnet must be ``LL####-Subnet-Private``.
1. (Optional) Add tags to the notebook session by selecting a tag namespace, then entering the key and the value. You can add more tags to the compartment by clicking **+Additional Tags**, see [Working with Resource Tags](https://docs.cloud.oracle.com/iaas/Content/General/Concepts/resourcetags.htm#workingtags).
1. (Optional) View the details for your notebook session immediately after creation by selecting **VIEW DETAIL PAGE ON CLICKING CREATE.**.
1. Click **Create**.
    ![](./../accelerate-ds-rapids-gpu/images/gpu-notebook-modal.png)

    While the notebook session is being created, you can navigate away from the current page.
    ![](./../speed-up-ds-with-the-ads-sdk/images/creating-ns.png)

## **STEP 2:** Opening a Notebook Session

Once the notebook session has been created the notebook session page shows the notebook in an **Active** or **Inactive** state. To open the notebook:

1. [Login to the OCI Console](https://www.oracle.com/cloud/sign-in.html).
1. Open the navigation menu.
1. Under **Data and AI**, select **Data Science**, and then click **Projects**.
    ![](./../speed-up-ds-with-the-ads-sdk/images/select-projects.png)

1. Select the compartment for the project.
1. Click the name of the project to contain the notebook session. This will open the Projects page.
    ![](./../speed-up-ds-with-the-ads-sdk/images/select-project.png)

1. Click the name of the notebook session. This will open the Notebook Session page.
    ![](./../speed-up-ds-with-the-ads-sdk/images/click-ns.png)

1. If the notebook is in an **Active** state, then click **Open**.
    ![](./../speed-up-ds-with-the-ads-sdk/images/click-open.png)

1. If the notebook is in an **Inactive** state, then:
    1. Click **Activate** to open the **Activate Notebook Session** dialog with the configuration from the last time the notebook session was activated or created.
    1. Select a VM shape. The [Compute Shapes](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm) page has details on the specifications. In this lab, it is suggested a VM.Standard2.4 or larger is used.
    1. Enter the block volume in GB. The suggested size is 100 Gb or larger. The size of the block storage can be increased, but not decreased.
    1. Confirm that the compartment for the VCN is the same as the one that is listed in the **Workshop Details** section at the top of the instructions page. If not, change it to that compartment.
    1. Confirm that the VCN is the one assigned to your account. It should be prefix with the same code as the compartment. For example, if your compartment is ``LL####-COMPARTMENT`` the VCN must be ``LL####-VCN``.
    1. Confirm that the compartment for the subnet is the same as the one that is listed in the **Workshop Details** section at the top of the instructions page. If not, change it to that compartment.
    1. Confirm that the subnet is the one assigned to your account. It should be prefix with the same code as the compartment. For example, if your compartment is ``LL####-COMPARTMENT`` the subnet must be ``LL####-Subnet-Private``.
    1. Click **Activate** and the notebook session status changes to **Updating**.
    1. When the notebook session status changes to **Active**, click **Open**

You can *proceed to the next lab*.

## Acknowledgements

* **Author**: [John Peach](https://www.linkedin.com/in/jpeach/), Principal Data Scientist
* **Last Updated By/Date**:
    * * [Jean-Rene Gauthier](https://www.linkedin.com/in/jr-gauthier/), Sr. Principal Product Data Scientist, January 2021

