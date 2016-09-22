---
title: Deploy SQL Server for VMM high availability
description: This article explains how to set up SQL Server as highly available in a VMM deployment
author:  rayne-wiselman
ms-author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---
# Deploy SQL Server for VMM high availability

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes the steps for deploying a highly available SQL Server database for System Center 2016 - Virtual Machine Manager (VMM). You set up a SQL Server cluster, configure the SQL Server VMM database with AlwaysOn availability groups.



## Before you start

Read the [planning information](../plan/plan-ha-deployment.md) for a highly available VMM deployment. It includes prerequisites and issues you should be aware of.


## Set up availability groups

[SQL Server AlwaysOn availability groups](https://msdn.microsoft.com/en-us/library/ff877884.aspx) support failover environments for a discrete set of user databases (availability databases). Each set of availability databases is hosted by an availability replica. To set up an availability group you'll need to deploy a Windows Server Failover Clustering (WSFC) cluster to host the availability replica, and enable AlwaysOn on the cluster nodes. You can then add the VMM SQL Server database as an availability database.

- [Learn more](https://msdn.microsoft.com/en-us/library/ff878487.aspx) about AlwaysOn prerequisites
- [Learn more](https://msdn.microsoft.com/en-us/library/ff929171.aspx) about setting up a WSFC for AlwaysOn availability groups
- [Learn more](https://msdn.microsoft.com/en-us/library/ff878265.aspx) about setting up an availability group



## Configure the VMM database with AlwaysOn Availability Groups

1. On the VMM server, stop the VMM service. For a cluster, in Failover Cluster Manager, stop the VMM role.
2. Connect to the machine that hosts the VMM database, and in SQL Server Management Studio, right-click the VMM database > **Properties**. In **Options**, set the **Recovery model** for the database to **Full**.
3. Right-click the VMM database > **Tasks** > **Back Up** and take a backup of the database.
5. In SQL Server Management Studio > **AlwaysOn High Availability** > right-click the availability group name > **Add Database**.
6. In **Add Database to Availability Group** > **Select Databases**, select the VMM database.
7. In **Select Data Synchronization**, leave the **Full** default.
8. In **Connect to Replicas** > **Connect**, specify permissions for the availability group destination.
9. Prerequisites are checked in **Validation**. In **Summary**, when you click **Next** AlwaysOn availability support will be initiated for the VMM database. The VMM database is copied and from this point AlwaysOn will keep the VMM database synchronized between the SQL Server AlwaysOn cluster nodes.
10. Restart the VMM service or cluster role. The VMM server should be able to connect to the SQL Server.
11. VMM credentials are only stored for the main SQL Server, so you'll need to create a new login on the secondary node of the SQL Server cluster, with the following characteristics:

-   The login name is identical to the VMM service account name.
-   The login has the user mapping to the VMM database.
-   The login is configured with the database owner credentials.

## Run a failover

To check that AlwaysOn is working as expected for the VMM database, run a failover from the primary to secondary node in the SQL Server cluster.

1.  In SQL Server Management Studio, right-click the availability group on the secondary server > **Failover**.
2. In **Fail Over Availability Group** > **Select New Primary Replica**, select the secondary server.
3. In **Summary**, click **Finish**.
4. Now move it back by initiating a failover to the secondary node computer that is running SQL Server, and verify that you can restart the VMM service (scvmmservice).
5. Repeat the last two steps for every secondary node in the cluster that is running SQL Server.
6.  If this is a high availability VMM setup, continue to install other high availability VMM nodes.
