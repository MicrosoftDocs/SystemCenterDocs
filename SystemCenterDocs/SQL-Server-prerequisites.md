---
title: SQL Server prerequisites
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7671bca6-c2dc-4e04-8ec0-1bba7f31fa34
---
# SQL Server prerequisites
Before you deploy DPM to protect SQL Server do the following:

1.  Review the [release notes](http://technet.microsoft.com/en-us/library/jj860394.aspx) and The [Unsupported scenarios in DPM](assetId:///3e0cd491-3757-4727-90db-eca0c3e6f7fc) for any SQL Server issues.

2.  Verify the support for SQL Server versions in the [Support Matrix for DPM Protection](assetId:///52bed83a-f484-4925-af77-377073737fc4).

3.  Note the following:

    -   If you have a database with files on a remote file share, protection will fail with Error ID 104. DPM does not support protection for SQL Server data on a remote file share.

    -   DPM cannot protect databases that are stored on remote SMB shares.

    -   Ensure that the availability group replicas are configured as read\-only.

    -   You must explicitly add the system account NTAuthority\\System to the Sysadmin group on SQL Server.

    -   When you perform an alternate location recovery for a partially contained database, you must ensure that the target SQL instance has the Contained Databases feature enabled.

## Protect SQL Server with AlwaysOn enabled
SQL Server 2012 introduces a new high availability feature, named AlwaysOn. You can add your databases to Availability Groups, which are basically containers for databases that are configured for failover. System Center 2012 SP1 DPM supports protection of databases that are part of Availability Groups. The salient features of the DPM support for the AlwaysOn feature are:

-   DPM detects Availability Groups when running inquiry at protection group creation.

-   DPM detects a failover and continues protection of the database.

-   DPM supports multi\-site cluster configurations for an instance of SQL Server.

When you protect databases that use the AlwaysOn feature, DPM has the following limitations:

-   DPM will honor the backup policy for availability groups that is set in SQL Server based on the backup preferences, as follows:

    -   Prefer secondary—Backups should occur on a secondary replica except when the primary replica is the only replica online. If there are multiple secondary replicas available then the node with the highest backup priority will be selected for backup. In the case that only primary replica is available then backup should occur on the primary replica.

    -   Secondary only—Backup shouldn’t be performed on the primary replica. If the primary replica is the only one online, the backup shouldn’t occur.

    -   Primary—Backups should always occur on the primary replica.

    -   Any Replica—Backups can happen on any of the availability replicas in the availability group. The node to be backed up from will be based on the backup priorities for each of the nodes.

-   Note the following:

    -   Backups can happen from any readable replica i.e. primary, synchronous secondary, asynchronous secondary.

    -   If any replica is excluded from backup, for example Exclude Replica is enabled or is marked as not readable, then that replica will not be selected for backup under any of the options.

    -   If multiple replicas are available and readable then the node with the highest backup priority will be selected for backup.

    -   If the backup fails on the selected node then the backup operation fails.

    -   Recovery to the original location is not supported.

