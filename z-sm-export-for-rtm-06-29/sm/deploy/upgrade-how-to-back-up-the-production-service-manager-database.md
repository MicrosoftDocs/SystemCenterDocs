---
title: How to Back Up the Production Service Manager Database
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ebe6cb4-0352-4c71-b2a9-0a235c0102d5


















---
# How to Back Up the Production Service Manager Database
Use the following procedure to back up the production Service Manager database in Microsoft SQL Server 2008 R2.  
  
### To back up the Service Manager database  
  
1.  After connecting to the appropriate instance of the Microsoft SQL Server Database Engine, in Object Explorer, click the server name to expand the server tree.  
  
2.  Expand **Databases**, and depending on the database, either select a user database or expand **System Databases** and select a system database.  
  
3.  Right\-click the database, point to **Tasks**, and then click **Back Up**. The Back Up Database dialog box appears.  
  
4.  In the **Database** list box, verify the database name. You can optionally select a different database from the list.  
  
5.  You can perform a database backup for any recovery model \(FULL, BULK\_LOGGED, or SIMPLE\).  
  
6.  In the **Backup type** list box, select **Full**.  
  
    > [!NOTE]  
    >  After creating a full database backup, you can create a differential database backup. For more information, see [How to: Create a Differential Database Backup \(SQL Server Management Studio\)](http://go.microsoft.com/fwlink/p/?LinkId=134470).  
  
7.  Optionally, you can select **Copy Only Backup** to create a copy\-only backup. A copy\-only backup is a SQL Server backup that is independent of the sequence of conventional SQL Server backups. For more information, see [Copy\-Only Backups](http://go.microsoft.com/fwlink/p/?LinkId=236002).  
  
    > [!NOTE]  
    >  When the **Differential** option is selected, you cannot create a copy\-only backup.  
  
8.  For **Backup component**, click **Database**.  
  
9. Either accept the default backup set name suggested in the **Name** text box, or enter a different name for the backup set.  
  
10. Optionally, in the **Description** text box, enter a description of the backup set.  
  
11. Specify when the backup set will expire and can be overwritten without explicitly skipping verification of the expiration data.  
  
    > [!NOTE]  
    >  For more information about backup expiration dates, see [BACKUP \(Transact\-SQL\)](http://go.microsoft.com/fwlink/p/?LinkId=134324).  
  
12. Choose the type of backup destination by clicking **Disk** or **Tape**. To select the paths of up to 64 disk or tape drives containing a single media set, click **Add**. The selected paths are displayed in the **Backup to** list box.  
  
13. To view or select the advanced options, click **Options** in the **Select a page** pane.  
  
14. Select an Overwrite Media option, by clicking either **Back up to the existing media set** or **Back up to a new media set, and erase all existing backup sets**.  
  
15. In the Reliability section, select either **Verify backup when finished** or **Perform checksum before writing to media**, and then optionally select **Continue on checksum error**. For more information, see [Detecting and Coping with Media Errors During Backup and Restore](http://go.microsoft.com/fwlink/p/?LinkId=236004)
