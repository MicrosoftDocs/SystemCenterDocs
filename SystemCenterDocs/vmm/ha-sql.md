---
ms.assetid: a6ab9340-decc-4f90-bb5b-4f0901737fc6
title: Deploy SQL Server for VMM high availability
description: This article explains how to set up SQL Server as highly available in a VMM deployment
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 02/19/2021
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
ms.custom: intro-deployment
---
# Deploy SQL Server for VMM high availability

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

This article describes the steps for deploying a highly available SQL Server database for System Center - Virtual Machine Manager (VMM). You set up a SQL Server cluster, and configure the SQL Server VMM database with Always On Availability Groups.

## Before you start

Read the [planning information](plan-ha-install.md) for a highly available VMM deployment. It includes prerequisites and issues you should be aware of.

## Set up availability groups

[SQL Server Always On availability groups](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) support failover environments for a discrete set of user databases (availability databases). Each set of availability databases is hosted by an availability replica. To set up an availability group, you must deploy a Windows Server Failover Clustering (WSFC) cluster to host the availability replica, and enable Always On on the cluster nodes. You can then add the VMM SQL Server database as an availability database.

- [Learn more](/sql/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability) about Always On prerequisites
- [Learn more](/sql/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server) about setting up a WSFC for Always On availability groups
- [Learn more](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server) about setting up an availability group

## Configure the VMM database with Always On Availability Groups

1. On the VMM server, stop the VMM service. For a cluster, in Failover Cluster Manager, stop the VMM role.
1. Connect to the machine that hosts the VMM database, and in SQL Server Management Studio, right-click the VMM database > **Properties**. In **Options**, set the **Recovery model** for the database to **Full**.
1. Right-click the VMM database > **Tasks** > **Back Up** and take a backup of the database.
1. In SQL Server Management Studio > **Always On High Availability** > right-click the availability group name > **Add Database**.
1. In **Add Database to Availability Group** > **Select Databases**, select the VMM database.
1. In **Select Data Synchronization**, leave the **Full** default.
1. In **Connect to Replicas** > **Connect**, specify permissions for the availability group destination.
1. Prerequisites are checked in **Validation**. In **Summary**, when you select **Next** Always On availability support is initiated for the VMM database. The VMM database is copied and from this point Always On keeps the VMM database synchronized between the SQL Server Always On cluster nodes.
1. Change VMM connection string in the path *HKLM\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings\Sql\ConnectionString* from *Server* to *SQLListenerName*. Also, update the following:

   - *HKLM\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings\Sql\MachineName* with *SQLListenerName*
   - *HKLM\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings\Sql\InstanceName* with *SQLListenerName*.
   - *HKLM\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager  Server\Settings\Sql\MachineFQDN* with *SQLListenerFQDN*.

1. Restart the VMM service or cluster role. The VMM server should be able to connect to the SQL Server.
1. VMM credentials are only stored for the main SQL Server, so you need to create a new login on the secondary node of the SQL Server cluster, with the following characteristics:
    - The login name is identical to the VMM service account name.
    - The login has the user mapping to the VMM database.
    - The login is configured with the database owner credentials.

## Run a failover

To check that Always On is working as expected for the VMM database, run a failover from the primary to secondary node in the SQL Server cluster.

1. In SQL Server Management Studio, right-click the availability group on the secondary server > **Failover**.
1. In **Fail Over Availability Group** > **Select New Primary Replica**, select the secondary server.
1. In **Summary**, select **Finish**.
1. Now move it back by initiating a failover to the secondary node computer that is running SQL Server, and verify that you can restart the VMM service (scvmmservice).
1. Repeat the last two steps for every secondary node in the cluster that is running SQL Server.
1. If this is a high availability VMM setup, continue to install other high availability VMM nodes.

>[!NOTE]
>
> If you're experiencing high latency or timeout errors in a multi-subnet scenario, change the VMM connection string in the path *HKLM\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings\Sql\ConnectionString*, add MultiSubnetFailover=True, and restart the VMM service.
