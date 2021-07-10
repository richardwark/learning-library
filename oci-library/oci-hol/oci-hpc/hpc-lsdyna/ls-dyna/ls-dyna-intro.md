# LS_DYNA Introduction

LS-DYNA is a general-purpose finite element program capable of simulating complex real world problems. It is used by the automobile, aerospace, construction, military, manufacturing, and bioengineering industries. [LS-DYNA Website](https://www.lstc.com/products/ls-dyna)

This Runbook will take you through the process of deploying an LS Dyna cluster on Oracle Cloud with low latency networking between the compute nodes. Running LS Dyna on Oracle Cloud is quite straightforward, follow along this guide for all the tips and tricks.


![](images/3cars.jpg)

## **Architecture**
The architecture for this runbook is as follow, we have one small machine (bastion) that you will connect into. The compute nodes will be on a separate private network linked with RDMA RoCE v2 networking. The bastion will be accesible through SSH from anyone with the key (or VNC if you decide to enable it). Compute nodes will only be accessible through the bastion inside the network. This is made possible with 1 Virtual Cloud Network with 2 subnets, one public and one private.

### Baseline Infrastructure

Cluster Networks are supported in the following regions. In each case, we recommend using the baseline reference architecture and then adjusting it, as required, to meet your specific requirements:

* VCN
    * Public Subnet, Security List, Route Table
    * Private Subnet, Security List, Route Table
    * Internet Gateway
    * NAT Gateway

* Compute Nodes
* Bastion Host in a Public Subnet
* HPC Compute Nodes in Private Subnet

![](images/images.png)

The above baseline infrastructure provides the following specifications:

* Networking
    * 1 x 100 Gbps RDMA over converged ethernet (ROCE) v2
    * Latency as low as 1.5 µs
* HPC Compute Nodes (BM.HPC2.36)
    * 6.4 TB Local NVME SSD storage per node
    * 36 cores per node
    * 384 GB memory per node

## Optional Infrastructure

### Storage

On top of the NVME SSD storage that comes with the HPC shape, you can also attach block volumes at 32k IOPS per volume, backed by Oracle’s highest performance SLA. If you are using our solutions to launch the infrastructure, an nfs-share is installed by default on the NVME SSD storage in /mnt. You can also install your own parallel file system on top of either the NVME SSD storage or block storage, depending on your performance requirements.

### Visualizer Node
You can create a visualizer node, such as a GPU VM or BM machine, depending on your requirements. This visualizer node can be your bastion host or else it can be separate. Depending on the security requirements for the workload, the visualizer node can be placed in the private or public subnet.


## Acknowledgements
* **Author** - High Performance Compute Team
* **Contributors** -  Chris Iwicki, Harrison Dvoor, Gloria Lee, Selene Song, Bre Mendonca, Samrat Khosla
* **Last Updated By/Date** - Samrat Khosla, October 2020


