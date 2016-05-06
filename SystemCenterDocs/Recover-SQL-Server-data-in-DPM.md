---
title: Recover SQL Server data in DPM
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0bc5ce4e-8bdb-4417-8854-ff7875bd5e7c
---
# Recover SQL Server data in DPM
You can recover SQL Server data as follows:

-   Recover the database to its original location

-   Recover the database with a new name to its original location or to a different instance of SQL Server

-   Recover the database to a different instance of SQL Server

-   Copy the database to a network folder

-   Copy the database to tape

Note that you can’t recover a system database to a different instance of SQL Server.

## Recover a database

1.  In [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Administrator Console, click **Recovery** on the navigation bar.

2.  Using the browse functionality, select the database to recover.

3.  On the calendar, click any date in bold to obtain the recovery points available for that date. The **Recovery time** menu lists the time for each available recovery point.

4.  On the **Recovery time** menu, select the recovery point you want to use.

5.  In the **Actions** pane, click **Recover**.

    The Recovery Wizard starts.

6.  On the **Review recovery selection** page, click **Next**.

7.  Select where you want to recover the database. Note that: **Recover to original SQL Server location**, and then click **Next**.

    -

    -   If you select **Recover to any SQL instance** on the **Specify recovery destination** page, enter the path to recover the database to. You can specify a new name for the recovered database. Note that this option isn’t available with the **Latest** recovery point. You can’t recover a newer version SQL Server database to an older version SQL Server instance.

    -   If you select **Copy to a network folder** and the recovery point that you selected wasn’t created from an express full backup, you’ll be presented with new recovery point choices.

    -   If you select **Copy to tape** and the recovery point that you selected wasn’t created from an express full backup, you’ll be presented with new recovery point choices. For the tape option you’ll select the tape library you want to use for recovery.

8.  If you selected a recovery point other than **Latest**, on the **Specify Database State** page, select **Leave database operational**.

9. Specify recovery options for network bandwidth usage throttling, SAN\-based recovery, and e\-mail notifications, and then click **Next**.

10. On the **Summary** page, review the recovery settings, and then click **Recover**.

## Recover a SQL and allow additional log backups
DPM uses SQL Server functionality to recover a database so that all uncommitted transactions are rolled back. The recovery process opens the transaction log to identify uncommitted transactions. Uncommitted transactions are undone by being rolled back, unless they hold locks that prevent other transactions from viewing transactionally inconsistent data. This step is called the undo or rollback, phase.In some circumstances, the SQL Server administrator might need the database to be restored in a mode that allows log backups to be selectively played back. In DPM you can can recover a database and leave it in a restoring state in which additional log backups can be applied to the database.

#### To recover a database without transaction roll back

1.  In [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Administrator Console, click **Recovery** on the navigation bar.

2.  Using the browse functionality, select the database to recover.

3.  On the calendar, click any date in bold to obtain the recovery points available for that date. The **Recovery time** menu lists the time for each available recovery point.

4.  On the **Recovery time** menu, select the recovery point you want to use. You can select any recovery point except **Latest**.

5.  In the **Actions** pane, click **Recover**.

    The Recovery Wizard starts.

6.  On the **Review recovery selection** page, click **Next**.

7.  Select **Recover to original SQL Server location** or **Recover to any SQL instance**, and then click **Next**.

8.  If you select **Recover to any SQL instance**, on the **Specify recovery destination** page, specify the instance of SQL Server to which the database should be recovered.

9. On the **Specify Database State** page, select **Leave database non\-operational but able to restore additional transaction logs**.

10. Select **Copy SQL transaction logs between the selected recovery point and latest available recovery point**, specify a copy destination for the transaction logs, and then click **Next**.

    [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] must have Write permission for the copy destination for the transaction logs.

11. Specify recovery options for network bandwidth usage throttling, SAN\-based recovery, and e\-mail notifications, and then click **Next**.

12. On the **Summary** page, review the recovery settings, and then click **Recover**.

13. Use the Restore Transact\-SQL command with the HeaderOnly argument to retrieve the header information for the transaction logs. The header contains information that allows the log backup sequences to be correctly ordered.

14. Use the Restore command with the Log argument to apply the desired logs to the database in the right order.

    For more information on the Restore command, see [RESTORE Arguments \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=104665).


