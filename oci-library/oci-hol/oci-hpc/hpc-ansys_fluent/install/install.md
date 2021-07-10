# Install ANSYS Fluent

## Introduction

In this lab, you will install ANSYS Fluent.

Estimated Lab Time: 25 minutes

### Objectives

In this lab:
* We will walk you through the different steps on how to install the ANSYS Fluent Software (including it's specific libraries and binaries) on OCI

### Prerequisites

* Download the FLUENT installer from the ANSYS website
* Familiarity with Oracle Cloud Infrastructure (OCI) is helpful
* Familiarity with networking is helpful

## **STEP 1**: Adding specific libraries

***If you used the CFD Ready Cluster from marketplace, this step is not needed***

1. There are a couple of libraries that need to be added to the Oracle Linux image on all the compute nodes.

    ```
    <copy>
    sudo yum -y install libGLU libXrender.x86_64 libXtst.x86_64 motif-2.3.4-14.el7_5.x86_64 mesa-libGLU-9.0.0-4.el7 x86_64  mesa-libGLU mesa-libGL motif axel fontconfig freetype freetype-devel fontconfig-devel libXext libXrender-devel.x86_64 libXrender.x86_64 mesa-libGL.x86_64
    </copy>
    ```

## **STEP 2**: Download the binaries

You can download the FLUENT installer from the ANSYS website and push it to your machine using scp.

```
<copy>
scp /path/own/machine/FLUID_version.zip opc@1.1.1.1:/home/opc/
</copy>    
```

Another possibility is to upload the installer into object storage.

1. In the main menu of the console, select Object Storage.
2. Choose the correct region on the top right
3. Select the correct compartment on the left-hand side
4. Create a bucket if you do not have one already created
5. In the bucket, select upload object and specify the path of the installer.
6. Select the 3 dots on the right-hand side of the installer object and select Create Pre-Authenticated Request
7. If you lose the URL, you cannot get it back, but you can regenerate a new Pre-Authenticated Request
8. Download the installer form object storage with

    ```
    <copy>
    wget PAR_URL
    </copy>
    ```

9. Untar or unzip the installer depending on your version

    ```
    <copy>
    tar -xf installer.tgz
    unzip installer.tgz
    </copy>
    ```
## **STEP 3**: Install

1. Launch the installer on a shared location. By default, an HPC cluster has a NFS-share or a Gluster-share mounted on all the compute nodes. Add the IP address to access the license server.

    ```
    <copy>
    mkdir /mnt/nfs-share/install/fluent
    sudo ./INSTALL -silent -install_dir "/mnt/nfs-share/install/fluent" -fluent -licserverinfo 2325:1055:IP
    </copy>    
    ```

    **NOTE: There is a known problem when running the ANSYS installer that it can hang. When you see RSS is disabled, feel free to exit using CTRL-C**

2. Finally, you can add fluent to your path like this

    ```
    <copy> 
    export PATH=$SHARE_DIR/applications/ansys_inc/v$VERS/fluent/bin:$PATH
    echo export PATH=$SHARE_DIR/applications/ansys_inc/v$VERS/fluent/bin:'$PATH' | sudo tee /etc/profile.d/ansys.sh
    </copy> 
    ```


## Acknowledgements
* **Author** - High Performance Compute Team
* **Contributors** -  Chris Iwicki, Harrison Dvoor, Gloria Lee, Selene Song, Bre Mendonca, Samrat Khosla
* **Last Updated By/Date** - Samrat Khosla, October 2020

