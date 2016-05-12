---
title: How to Restore the Service Manager Database in the Lab Environment
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: acc6c46d-3377-47ce-9c94-ce20997d376f
---
# How to Restore the Service Manager Database in the Lab Environment
Use the following procedure to restore the production [!INCLUDE[smshort](Token/smshort_md.md)] database using Microsoft SQL Server 2008 R2.

### To restore the Service Manager database

1.  After connecting to the appropriate instance of the Microsoft SQL Server Database Engine, in Object Explorer, click the server name to expand the server tree.

2.  Expand **Databases**, and depending on the database, either select a user database or expand **System Databases** and select a system database.

3.  Right\-click the database, point to **Tasks**, and then click **Restore**. The Back Up Database dialog box appears.

4.  Click **Database**, which opens the **Restore Database** dialog box

5.  On the **General** page, the name of the restoring database appears in the **To database** list box. To create a new database, enter its name in the list box.

6.  In the **To a point in time** text box, either retain the default \(Most recent possible\) or select a specific date and time by clicking the browse button which opens the **Point in Time Restore** dialog box. For more information, see [How to: Restore to a Point in Time \(SQL Server Management Studio\)](http://go.microsoft.com/fwlink/p/?LinkId=236006).

7.  To specify the source and location of the backup sets to restore, click either **From database** or **From device**.

8.  In the **Select the backup sets to restore** grid, select the backups to restore. For more information see [Restore Database \(General Page\)](http://go.microsoft.com/fwlink/p/?LinkId=236009).

9. To view or select the advanced options, click **Options** in the **Select a page pane**.

10. In the **Restore options** panel, choose one of the following options most appropriate for your situation:

    -   Overwrite the existing database

    -   Preserve the replication settings

    -   Prompt before restoring each backup

    -   Restrict access to the restored database

    For more information, see [Restore Database \(Options Page\)](http://go.microsoft.com/fwlink/p/?LinkId=236010)

11. Optionally, you can restore the database to a new location by specifying a new restore destination for each file in **Restore the database files as**. For more information see [Restore Database \(Options Page\)](http://go.microsoft.com/fwlink/p/?LinkId=236010).

12. In the **Recovery state** panel, select one of the following options most appropriate for your environment:

    -   **Leave the database ready to use by rolling back the uncommitted transactions. Additional transaction logs cannot be restored. \(RESTORE WITH RECOVERY\)**

        > [!NOTE]
        > Choose this option only if you are restoring all of the necessary backups at this time.

    -   **Leave the database non\-operational, and do not roll back the uncommitted transactions. Additional transaction logs can be restored. \(RESTORE WITH NORECOVERY\)**

    -   **Leave the database in read\-only mode. Undo uncommitted transactions, but save the undo actions in a standby file so that recovery effects can be reverted. \(RESTORE WITH STANDBY\)**

    For more information see [Restore Database \(Options Page\)](http://go.microsoft.com/fwlink/p/?LinkId=236010).


