---
ms.assetid: 5523da23-09d3-4b34-b7a9-af2dbde9e64b
title: Manage mirrored SQL servers
description: This article provides information about how to manage mirrored SQL servers in System Center DPM.
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  evansma
ms.date:  04/08/2021
ms.topic:  article
ms.prod:  system-center
ms.technology: data-protection-manager
MonikerRange: sc-dpm-2019||sc-dpm-2016
---

# Manage mirrored SQL servers

System Center – Data Protection Manager (DPM) protects SQL Server databases and clusters that use SQL Server mirroring technology. This support does not translate into any major changes in the procedure to protect or recover SQL Server databases in DPM.

 following sections will call out any changes in procedure.

## Before you begin

Before you protect a mirrored SQL Server database, make sure that you meet the following prerequisites:

- Install agents on both the partners of the mirror.
- Do not mirror the database on the same computer.

## Protect a mirrored SQL server database

The procedure to protect a mirrored database is the same as to [protect a SQL Server database](#back-up-sql-server.md).

When you select a mirrored database to add to the protection group in the  **Create New Protection Group**  wizard, DPM automatically detects that the database is mirrored and displays the mirror details on the  **Select Group Members**  page.

## Protect a mirrored SQL Server cluster

DPM also supports protection of mirrored SQL server clusters. The procedure to protect SQL server clusters that are mirrored is the same as to protect a mirrored SQL server database.

> [!NOTE]
> DPM agents must be installed on all the computers in the cluster.

DPM protects the following configurations:

- Principal is clustered, mirror is not.
- Principal is not clustered, mirror is.
- Both principal and mirror are clustered.

## Common scenarios

### A protected SQL Server database gets mirrored

At the time of backup, DPM detects that the database was mirrored, and raises an alert. You need to remove protection (with retain data) for the database, and then re protect it.

> [!NOTE]
> DPM maintains a single replica for the mirror.

### A mirror is broken

When the mirror is broken for a mirrored SQL Server database that is currently protected by DPM, backups fail with alerts. Remove protection (with retain data) for the SQL Server database and re protect it.

### Principal partner in a mirror fails over and fails back before the next backup

This scenario does not affect protection, because DPM is not informed about the failover, unless a backup of the mirror is in progress.

### Principal partner fails and the mirror server takes over

When DPM detects that the mirror is the principal partner, it stops the back-up job, and it performs a consistency check on the database that failed over after 30 minutes.

> [!NOTE]
> During these 30 minutes if the database fails back to the original principal, DPM  detects this, and  resumes protection after performing a consistency check.

If you try to back up the mirrored database before the scheduled consistency check (after 30 minutes), an alert indicating that a consistency check is required is created on the DPM Monitor tab, and the back-up will not start until a consistency check is done. To start the backup immediately, do a consistency check and retry the backup.

### One protected database is made the mirror of another protected database

If one SQL Server database that is protected by DPM is made the mirror of another protected database, protection  fails for both partners of the mirror. To continue protection, you must protect the principal partner.

### Recover a mirrored SQL Server database

When you recover a mirrored SQL Server database, always use the  **Recover to alternate location**  option. Even if you want to recover the database to the original location, use the alternate location option and provide the path to either of the partners of the mirror.

## Unsupported scenarios

DPM does not support the following scenarios for mirrored SQL Server databases:

- If the database is mirrored on the same server.
- If the SQL Server mirroring session uses an explicitly configured IP address.

## Next steps
