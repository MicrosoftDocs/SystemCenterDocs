---
title: Restore and synchronize the DPM database with DPMSync
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4baee8f0-1855-4fc5-ab22-d0613a4aa3b8
---
# Restore and synchronize the DPM database with DPMSync
**DpmSync** is a command\-line tool that enables you to synchronize the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database with the state of the disks in the storage pool and with the installed protection agents. The DpmSync tool restores the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database, synchronizes the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database with the replicas in the storage pool, restores the Report database, and reallocates missing replicas.

**DpmSync Syntax**

DpmSync **–RestoreDb –DbLoc location –InstanceName server\\instance**\]

DpmSync **\-Sync**

DpmSync **\-ReallocateReplica**

DpmSync **\-DataCopied**

**Parameters**

|Parameter|Description|
|-------------|---------------|
|**\-RestoreDb**|Restores a [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database from a specified location.|
|**\-Sync**|Synchronizes restored databases.<br /><br />You must run DpmSync –Sync after you restore the databases.<br /><br />After you run DpmSync –Sync, some replicas may still be marked as missing.|
|**\-DbLoc** *location*|Identifies the location of backup of [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database.|
|**\-InstanceName** *server\\instance*|Instance to which DPMDB must be restored.|
|**\-ReallocateReplica**|Reallocates all missing replica volumes without synchronization.|
|**\-DataCopied**|Indicates that you have completed loading data into the newly allocated replica volumes.<br /><br />This is applicable for client computers only.|

**Example 1:** To restore the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database from local backup media on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server. 
Run the following command:

**DpmSync –RestoreDb \-DbLoc G:\\DPM\\Backups\\2005\\November\\DPMDB.bak**

After you restore the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database, to synchronize the databases, you run the following command:

**DpmSync \-Sync**

After you restore and synchronize the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database and before you restore the replica, you run the following command to reallocate disk space for the replica:

**DpmSync \-ReallocateReplica**

**Example 2:** To restore the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database from a remote database. 
Run the following command on the remote computer:

**DpmSync –RestoreDb \-DbLoc G:\\DPM\\Backups\\2005\\November\\DPMDB.bak –InstanceName contoso\\ms$dpm**

After you restore the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database, to synchronize the databases, you run the following command on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server:

**DpmSync \-Sync**

After you restore and synchronize the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database and before you restore the replica, you run the following command on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server to reallocate disk space for the replica:

**DpmSync \-ReallocateReplica**

**Example 3:** To move a [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database from the local [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server to a remote SQL server.

The following steps illustrate the use of DPMSync in moving a [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database \(DPMDB\) from the local [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server \(DPMServer1\) to a remote SQL server \(DPMRemoteSQL\).

|||
|-|-|
|1.|Run the following command: **DPMBackup –db**. <br />This will create the file DPMDB.bak at **\\Program Files\\Microsoft DPM\\DPM\\volumes\\Shadowcopy\\Database Backups**. Store this backup in a secure location.|
|2.|Uninstall [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] from DPMServer1 and choose to retain data.|
|3.|Delete DPMDB. You have to do this in order to reinstall [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)].|
|4.|Install [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] on DPMServer1 with the remote SQL Server instance installed on DPMRemoteSQL.|
|5.|Run the following command on DPMRemoteSQL **dpmsync –restoredb –dbloc** *<dbbackuplocation>* **–instancename***<instancename>*, where dbbackuplocation is the location of the backup taken in step 1 and instancename is the name of the remote SQL Server instance.|
|6.|Now run the following command on DPMServer1 Dpmsync –sync|


