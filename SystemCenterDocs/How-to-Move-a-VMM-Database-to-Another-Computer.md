---
title: How to Move a VMM Database to Another Computer
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02bb189f-bd3b-420b-93cf-3c14e234f551
---
# How to Move a VMM Database to Another Computer
You might want to move the [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] database for one or more of the following reasons:

-   You want to use a different computer than the one you currently use for the VMM database. For example, you might want to use a new computer with a newer version of SQL Server for the VMM database. Make sure you choose a supported version of SQL Server.

    For an in\-place upgrade of SQL Server, the procedures in this topic are not necessary \(because the database will not move\). Make sure no jobs are running when you perform the upgrade, or jobs may fail and may need to be restarted manually. For procedures, see the SQL Server documentation, for example, [Upgrade to SQL Server 2014](https://msdn.microsoft.com/en-us/library/bb677622(v=sql.120).aspx).

-   You are upgrading VMM and the VMM database is using a version of SQL Server that is not supported for the upgrade.

-   The VMM database is installed on the same computer as the VMM management server, and you plan to upgrade to a high availability VMM management server.

Use the following procedures to collect information about the VMM database and installation settings, and to move the VMM database.

### To collect information about the VMM database and VMM installation settings

1.  In VMM, open the **Settings** workspace.

2.  In the **Settings** pane, expand **General**, and then double\-click **Database Connection**. Record the information you see.

3.  Open Server Manager.

4.  Click **Tools** and then click **Services**.

5.  In the list of services, right\-click **System Center Virtual Machine Manager** \(don't confuse this with the service whose name ends in "Agent"\), and then click **Properties**.

6.  Click the **Log On** tab, and then record the account information you see.

    This account was assigned as the service account when VMM was previously installed. It might be a local account or a domain account.

7.  If the account you recorded in the previous step is the **Local System** account, or you already know whether it is a local account or a domain account, skip this step. Otherwise, click **Tools > Computer Management**, expand **Local Users and Groups**, and then click **Users**. If the account you recorded is listed under Users \(or is the **Local System** account\), it is a local account. If not, it is a domain account.

8.  Review your records for information about whether you are using distributed key management, or whether encryption keys are being stored locally on the VMM management server. For more information, see [Choosing Service Account and Distributed Key Management Settings During an Upgrade](./Choosing-Service-Account-and-Distributed-Key-Management-Settings-During-an-Upgrade.md).

9. If you are moving the VMM database but not upgrading VMM, also review your records about which Update Rollups, if any, have been applied to VMM.

### To move a VMM database

1.  Back up your existing VMM database by using tools that are available in SQL Server.

2.  Copy the database backup to a computer that is running a supported version of SQL Server.

3.  Use the tools in SQL Server to restore the database.

4.  If you are upgrading VMM, continue the upgrade as described in [Performing a VMM Upgrade](./Performing-a-VMM-Upgrade.md), and skip the remainder of this procedure.

    If you are not upgrading, go on to the next step.

5.  If you are moving the VMM database but not upgrading VMM, close all connections to the VMM management server, then uninstall and re\-install VMM. When you uninstall, make sure that on the **Database options** page, you click **Retain database**. When you re\-install, use the same settings that you used for the original installation, but on the **Database configuration** page, do the following:

    -   Specify the name of the computer where the VMM database is now located.

        If your database is configured with AlwaysOn Availability Groups, enter the name of the availability group listener.

    -   Specify the port to use for communication with the computer where the VMM database is now located, if all of the following conditions are true:

        -   SQL Server is running on a remote computer.

        -   The SQL Server Browser service is not started on that remote computer.

        -   SQL Server is not using default port 1433.

        Otherwise, leave the **Port** box empty.

    -   Select or type the name of the instance of SQL Server to use. If you are moving a database that was configured with AlwaysOn Availability Groups, leave the text box for the instance of SQL Server empty.

    -   Select **Existing Database**, and then select the database.

    -   You can check **Use the following credentials** and specify any account that has access to the database \(it doesn't have to be the same account that you used for the earlier installation\). Or, if the account that you're logged on with has access to the database, you can leave **Use the following credentials** unchecked, and VMM will use that account when making the initial connection to the database.

    After following the previous instructions, finish re\-installing with the settings that you used for the original installation.

6.  If you are moving the VMM database but not upgrading VMM, after you finish installing, be sure to re\-apply the same Update Rollups that you had previously applied.

    This step ensures that the VMM software will continue to interpret data in the VMM database in exactly the same way as it did before you uninstalled and re\-installed VMM.

    As a best practice, if you also want to apply additional, newer Update Rollups, first confirm that VMM works as expected \(to confirm that the VMM database has been successfully moved\) before applying those Update Rollups.

For more information about moving a SQL Server database, see [Copying Databases with Backup and Restore](http://technet.microsoft.com/library/ms190436.aspx).

## See Also
[Planning an Upgrade of Virtual Machine Manager](./Planning-an-Upgrade-of-Virtual-Machine-Manager.md)


