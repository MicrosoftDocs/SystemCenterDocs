---
title: Recover SharePoint data
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4408908-3cf8-477f-a6ad-26bdf40ab7aa
---
# Recover SharePoint data
You can recover SharePoint data as follows:

-   Recover to the original location

-   Recover to an alternate location. Note that you can’t perform a full farm recovery to a new location.

-   Copy the data to a network folder

-   Copy the data to tape

## Before you begin
Note that to recover a farm:

-   If you protected a SharePoint server as a SQL Server database, you can recover SharePoint data by selecting the SQL Server database in the Recovery Wizard.

-   Note the following to recover a farm:

    -   The front\-end Web servers should be configured the same as they were when the recovery point was created.

    -   The farm structure must be created on the front\-end Web server; the farm data will be recovered to the existing structure.

    -   The instances of SQL Server are configured with the same names as when the recovery point was created.

    -   The instances of SQL Server are configured with the same drive configuration as when the recovery point was created.

    -   The recovery farm must have all service packs, language packs, and patches installed on the primary farm.

    -   Don’t directly try to recover the Central Administration content database or the configuration database because this could cause data corruption in the SharePoint farm.

    -   The recovery point time for SharePoint data displayed on the **Browse** tab may differ from the time displayed on the **Search** tab. The **Browse** tab displays the backup time for the farm, while the **Search** tab lists the correct recovery point time for sites, documents, and folders.

## Recover data
There a couple of possible scenarios for farm recovery:

-   A farm configuration exists as it did at the time of taking the backup. In this case, you will be restoring to a functioning farm.

-   The Configuration database is corrupt and the servers in the farm are down.

#### Restore data to a functioning farm

1.  In [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Administrator Console, click **Recovery** on the navigation bar.

2.  In the **Protected data** pane, expand the server that contains the farm you want to recover, and then click **All Protected SharePoint Data**.The farm displays in the **Recoverable** item pane as server name\\farm name.

3.  On the calendar, click any date in bold to obtain the recovery points available for that date. The **Recovery time** menu lists the time for each available recovery point.

4.  On the **Recovery time** menu, select the recovery point you want to use.

5.  In the **Actions** pane, click **Recover**.

    The Recovery Wizard starts.

6.  On the **Review recovery selection** page, click **Next**.

7.  Select where you want to recover the database. Note that:

    -   You can’t recover an entire farm to an alternate location.

    -   If you select **Copy to a network folder** and the recovery point that you selected wasn’t created from an express full backup, you’ll be presented with new recovery point choices.

    -   If you select **Copy to tape** and the recovery point that you selected wasn’t created from an express full backup, you’ll be presented with new recovery point choices. For the tape option you’ll select the tape library you want to use for recovery.

8.  Specify recovery options for network bandwidth usage throttling, SAN\-based recovery, and e\-mail notifications, and then click **Next**.

9. On the **Summary** page, review the recovery settings, and then click **Recover**.

#### Restore data to a non\-functioning farm

1.  Create a new farm that uses the same instance of SQL Server and the same front\-end Web server as the original protected farm.

2.  On the front\-end Web server that DPM uses to recover farm data, run the following command at the command prompt:`ConfigureSharePoint-EnableSharePointProtection`

3.  In [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Administrator Console, click **Recovery** on the navigation bar.

4.  In the **Protected data** pane, expand the server that contains the farm you want to recover, and then click **All Protected SharePoint Data**.The farm displays in the **Recoverable** item pane as server name\\farm name.

5.  On the calendar, click any date in bold to obtain the recovery points available for that date. The **Recovery time** menu lists the time for each available recovery point.

6.  On the **Recovery time** menu, select the recovery point you want to use.

7.  In the **Actions** pane, click **Recover**.

    The Recovery Wizard starts.

8.  On the **Review recovery selection** page, click **Next**.

9. Select where you want to recover the database. Note that:

    -   You can’t recover an entire farm to an alternate location.

    -   If you select **Copy to a network folder** and the recovery point that you selected wasn’t created from an express full backup, you’ll be presented with new recovery point choices.

    -   If you select **Copy to tape** and the recovery point that you selected wasn’t created from an express full backup, you’ll be presented with new recovery point choices. For the tape option you’ll select the tape library you want to use for recovery.

10. Specify recovery options for network bandwidth usage throttling, SAN\-based recovery, and e\-mail notifications, and then click **Next**.

11. On the **Summary** page, review the recovery settings, and then click **Recover**.

12. On the main front\-end Web server for the server farm, run the SharePoint Products and Technologies Configuration Wizard and disconnect the front\-end Web server from the farm.


