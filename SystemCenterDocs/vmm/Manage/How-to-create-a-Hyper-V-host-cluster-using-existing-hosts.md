---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to create a Hyper V host cluster using existing hosts
ms.technology:  virtual-machine-manager
ms.assetid:  1e15b87e-f46d-4285-bc6e-eace2d078a95
---

# How to create a Hyper-V host cluster using existing hosts

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager



You can create a Hyper-v host cluster in the VMM fabric using the VMM console.  

 
    
    
## Add the cluster
1.  In the VMM console click **Fabric** > **Create** > **Hyper-V Cluster** to open the Create Hyper-V Cluster wizard.

2.  In **General** specify a cluster name and choose the host group in which the existing Hyper-V hosts are located.
3. In **Resource Type** select the Run As account that you'll use to create the cluster. he account that you use must have administrative permissions on the servers that will become cluster nodes, and must belong to the same domain as the Hyper-V hosts that you want to cluster. Also, the account requires **Create Computer objects** permission in the container that is used for Computer accounts in the domain. Ensure that **Existing Windows servers** is selected, and if you don't need support from Microsoft for this cluster, you can select **Skip cluster validation**. 
4.  In **Nodes** select the Hyper-V host servers that you want to include in the cluster. You can select multiple hosts by using the CTRL key, or a range by using SHIFT.
5. In IP address (if it appears) type in the IP address you want to use for the cluster.
6. In **Storage** select the data disks you want the cluster to use. The list of available disks includes the logical units associated with the host group that you selected at the beginning of the wizard.

    -   If you assigned storage out-of-band, disks that are not managed by VMM are displayed and selected as available disks, with the check box next to each disk dimmed and unavailable.
     -   If you are using a third-party clustered file system (CFS) solution, make sure you are aware which disks are CFS disks. Do not select those disks for the cluster. If you do, cluster creation will fail. If you are using a third-party clustered file system (CFS) solution, make sure you are aware which disks are CFS disks. Do not select those disks for the cluster. If you do, cluster creation will fail.
       -   If the number of selected hosts for the cluster is even, the smallest disk that is larger than 500 megabytes (MB) is automatically chosen as the witness disk and is unavailable for selection.

7. In **Virtual Switches** you can select the logical networks to use when VMM automatically create virtual switches on the Hyper-V nodes. the external virtual switches on destination Hyper-V nodes. VMM will automatically create the virtual switches on all the Hyper-V nodes.
8. On the **Summary** page, confirm the settings and then click **Finish**. You can monitor the cluster status on the **Jobs** page. After the job finishes  you can verify cluster information by right-clicking **Properties** > **Status** tab on the cluster. You can also right-click the cluster and click **Validate Cluster**. 
 

Here's what VMM does after you create the cluster:

1.  Validates that all hosts meet the prerequisites, such as required operating system and domain membership

2.  Enables the Failover Clustering feature on each host

3.  Unmasks the selected storage logical units to each host

4.  Runs the cluster validation process

5.  Creates the cluster with quorum settings, configures any cluster static IP settings that you specified, and enables Cluster Shared Volumes (CSV)

6.  For each logical unit that is designated as a CSV, assigns the logical unit as a CSV on the cluster






