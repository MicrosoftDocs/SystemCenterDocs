---
title: Recover a backed up DPM server
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13e3605e-373f-425f-8eb0-14d571e26791
---
# Recover a backed up DPM server
If a primary server fails you can switch protection to the secondary server. After you’ve switched protection, you can perform recovery functions from the secondary server.

## Switch protection to the secondary server

1.  In the **Protection** area of the DPM Administrator Console Go to the Protection work area, right\-click the protection group for which you want to switch protection.

2.  Select **Switch Disaster Protection** from the context menu.

3.  Run a consistency check. After switching protection, the replica will appear as inconsistent until the check runs.

You can switch protection in Windows Powershell using the Start –DPMSwitchProtection cmdlet.

To switch protection back perform the same procedure. You’ll begin to see **Agent Ownership Required** alerts on the primary server. Click **Take Ownership** in the alert to give the primary server ownership of the protection agent.

## Recover a DPM server
When you recover a primary [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server, you’ll need to reestablish protection for the computers that were previously protected by the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server. Note that:

-   You can’t restore recovery points for data sources protected by the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server.

-   When you recover database files, ensure that the restore location on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server is secure.

#### Recover a DPM database

1.  Uninstall [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)], selecting the option **Retain disk\-based recovery points**. Then restart the computer.

2.  Delete the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database using SQL Server Management Studio.

3.  Install [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] and restart the computer.

4.  On the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server, create a restore folder for the files.

5.  Insert the tape with the latest backup of the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database into the tape library.

6.  In the **Management** tab of [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Administrator Console, open **Libraries** and click **Rescan** on the **Actions** pane

7.  Insert the tape with the latest backup of the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database in the tape drive\/library. You can identify this tape from the last tape management report.

8.  Select the library from the list and click **Inventory libraries…**. Perform a detailed inventory from the **Actions** pane.

9. Select the imported tape from the list and click **Recatalog imported tape** on the **Actions** pane.

10. In the **Recovery** tab select the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database in the **External Tapes** node. Click **Recover** on the **Actions** pane and using the Recovery Wizard, recover the database to a network folder \(the folder you created earlier\).

11. Run [DPMSync](http://go.microsoft.com/fwlink/?LinkId=255172) to attach the database to [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)]: DPMSync –RestoreDB –DBLoc*location of folder created in Step 6\\name of DPMDB*. DPMSync takes the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] service offline and attaches the backed up database to SQL Server.

12. Then run DpmSync \-sync

To recover a [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] replica, first run DpmSync to reallocate it. DpmSync marks the replica as manual replica creation pending. You can only recover the replica when it has this status. If a replica recovery fails, the replica status changes to inconsistent, which prevents repeated recovery attempts. If failure occurs stop protection of the data source using the delete replica option, add the data source to a protection group again using the manual replica creation option, and then retry the replica recovery. If this fails retrying the recovery will always fail because the replica will now be marked with invalid status.

#### Recover replicas after recovering the database

1.  Run **DpmSync \-reallocateReplica**. This command reformats any replicas that are missing and marks them as "manual replica creation pending."

2.  Manually create the replica from either the secondary [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server or a tape backup of the data source corresponding to each of the replicas. If you use a secondary server the **Restore to replica** option is enabled in the **Recovery task** area. For tape backups, use the management shell with the **RestoreToReplica** option.

3.  Perform a consistency check to continue protection.

After you rebuild a primary [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server, you must reestablish protection of the computers that were protected by the primary server, as follows:

#### Reestablish protection

1.  On the protected computer run the following at the command prompt:

    **Setdpmserver.exe <***primary DPM server name***>**

2.  Open Computer Management and perform the following steps:

    1.  Select **Local Users and Groups**.  Verify that the primary server, in the format of *Domain*\/*Name*, is a member of the following groups:

    2.  Distribute COM Users

        DPMRADCOMTrustedMachines

        DPMRADmTrustedMachines

    3.  If the primary server isn’t not listed in any of the groups, manually add the server in the format of *Domain*\/*Name*.

If protection fails after completing the steps, do the following:

1.  In Administrative Tools, open Component Services. Expand **Computers**, expand **My Computer**, and then click **DCOM Config**.

2.  In the results pane, right\-click **DPM RA Service**. Click **Properties** > **Security**.

3.  In the **Launch and Activation Permissions** area, click **Edit**, and then do one of the following:

    -   If the primary server is listed, the Access Control List \(ACL\) entry might be incorrect. Remove the entry, and then add the primary server with full permissions.

    -   If the primary server is not listed, add the primary server with full permissions.


