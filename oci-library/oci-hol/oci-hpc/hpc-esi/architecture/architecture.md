# Architecture

## Introduction

The architecture for this runbook is as follow, we have one main machine (The headnode) that will start the jobs. Other machines (Compute Nodes) will be accessible from the headnode and MPI will distribute the jobs to the compute nodes. The headnode will be accesible through SSH from anyone with the key (or VNC if you decide to enable it) Compute nodes will only be accessible from inside the network. This is made possible with 1 Virtual Cloud Network with 2 subnets, one public and one private.


![](images/rocky_image.png " ")


### Objectives

In this lab:
* Showcase the different OCI components and services you will need in order to run ESI Pam-Crash on OCI
* Briefly describe the acrhitecture required for this runbook

### Prerequisites

* Some understanding of cloud and database terms is helpful
* Familiarity with Oracle Cloud Infrastructure (OCI) is helpful
* Familiarity with networking is helpful



## Acknowledgements

* **Author** - High Performance Compute Team
* **Contributors** -  Chris Iwicki, Harrison Dvoor, Gloria Lee, Selene Song, Bre Mendonca, Samrat Khosla
* **Last Updated By/Date** - Samrat Khosla, January 2021

