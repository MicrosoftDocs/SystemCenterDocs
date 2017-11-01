---
ms.assetid: a6ab9340-decc-4f90-bb5b-4f0901737fc6
title: Deploy SQL Server for VMM high availability
description: This article explains how to set up SQL Server as highly available in a VMM deployment
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/01/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---
# Deploy SQL Server for VMM high availability

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes the steps for deploying a highly available SQL Server database for System Center 2016 - Virtual Machine Manager (VMM). You set up a SQL Server cluster, configure the SQL Server VMM database with Always On Availability Groups.

## Before you start

Read the [planning information](plan-ha-install.md) for a highly available VMM deployment. It includes prerequisites and issues you should be aware of.

## Set up availability groups

[SQL Server Always On availability groups](https://msdn.microsoft.com/en-us/library/ff877884.aspx) support failover environments for a discrete set of user databases (availability databases). Each set of availability databases is hosted by an availability replica. To set up an availability group you must deploy a Windows Server Failover Clustering (WSFC) cluster to host the availability replica, and enable Always On on the cluster nodes. You can then add the VMM SQL Server database as an availability database.

- [Learn more](https://msdn.microsoft.com/en-us/library/ff878487.aspx) about Always On prerequisites
- [Learn more](https://msdn.microsoft.com/en-us/library/ff929171.aspx) about setting up a WSFC for Always On availability groups
- [Learn more](https://msdn.microsoft.com/en-us/library/ff878265.aspx) about setting up an availability group

## Configure the VMM database with Always On Availability Groups

1. On the VMM server, stop the VMM service. For a cluster, in Failover Cluster Manager, stop the VMM role.
1. Connect to the machine that hosts the VMM database, and in SQL Server Management Studio, right-click the VMM database > **Properties**. In **Options**, set the **Recovery model** for the database to **Full**.
1. Right-click the VMM database > **Tasks** > **Back Up** and take a backup of the database.
1. In SQL Server Management Studio > **Always On High Availability** > right-click the availability group name > **Add Database**.
1. In **Add Database to Availability Group** > **Select Databases**, select the VMM database.
1. In **Select Data Synchronization**, leave the **Full** default.
1. In **Connect to Replicas** > **Connect**, specify permissions for the availability group destination.
1. Prerequisites are checked in **Validation**. In **Summary**, when you click **Next** Always On availability support is initiated for the VMM database. The VMM database is copied and from this point Always On keeps the VMM database synchronized between the SQL Server Always On cluster nodes.
1. Restart the VMM service or cluster role. The VMM server should be able to connect to the SQL Server.
1. VMM credentials are only stored for the main SQL Server, so you need to create a new login on the secondary node of the SQL Server cluster, with the following characteristics:
    - The login name is identical to the VMM service account name.
    - The login has the user mapping to the VMM database.
    - The login is configured with the database owner credentials.

## Run a failover

To check that Always On is working as expected for the VMM database, run a failover from the primary to secondary node in the SQL Server cluster.

1. In SQL Server Management Studio, right-click the availability group on the secondary server > **Failover**.
1. In **Fail Over Availability Group** > **Select New Primary Replica**, select the secondary server.
1. In **Summary**, click **Finish**.
1. Now move it back by initiating a failover to the secondary node computer that is running SQL Server, and verify that you can restart the VMM service (scvmmservice).
1. Repeat the last two steps for every secondary node in the cluster that is running SQL Server.
1. If this is a high availability VMM setup, continue to install other high availability VMM nodes.
