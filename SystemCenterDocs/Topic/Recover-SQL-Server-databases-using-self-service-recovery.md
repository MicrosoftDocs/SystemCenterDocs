---
title: Recover SQL Server databases using self-service recovery
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2d71cff-810f-42de-813f-70479a5009e2
---
# Recover SQL Server databases using self-service recovery
The Self\-Service Recovery Tool \(SSRT\) for [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] enables end\-users who have permissions to recover SQL Server databases that are backed up by the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server, without any intervention from the DPM administrator. Note the following prerequisites:

-   The user must be configured as a DPM self\-service user. For more information see [Configure self-service recovery of SQL Server databases](../Topic/Configure-self-service-recovery-of-SQL-Server-databases.md).

-   The user needs .NET Framework 3.5 on their client computers.

-   To install SSRT the user needs administrator privileges on their local computer.

-   You can find the DPM SSRT client application installer on the DPM product DVD, in the DpmSqlEURInstaller folder

Install the SSRT on client computers that belong to the self\-service users, and then use the following procedures to run the SSRT.

### Run the tool

1.  On the Start menu, or using search, open the DPM Self\-Service Recovery Tool.

2.  In the DPM SSRT console, click **Connect to DPM Server**. Specify the name of the server.

3.  Ensure you’re connected to the DPM server that backs up the SQL Server database you want to recover. Then click **New Recovery Job** to start the Recovery Wizard.

The Recovery Wizard guides you through the process of recovering SQL Server databases. This wizard changes dynamically, depending on the type of recovery you select.

### Run the Recovery Wizard

1.  On the Welcome page, click Next

2.  On the Specify Database Details page, specifying the SQL Server instance name, and the name of database that you want to recover.

    Note that if you’re using availability groups, provide the group name instead of the SQL Server instance name and leave the database name empty. Specify the group name in the format AGNAME.ClusternameFQDN\\AGNAME, where AGNAME is the name of the availability group.

3.  On the Specify Recovery Point page, select the recovery point you want to use to recover the database. Available recovery points are indicated in bold on the calendar. Select the date, and then the time for that date.

4.  On the Select Recovery Type page specify the type of recovery you want to perform, as follows:

    -   **Recover to any instance of SQL Server**—Select to recover to any instance on either the same SQL Server or a different one.

    -   **Copy to a network folder**—Recover the database files to a network folder. Note that you can only copy to a network folder from a recovery point that was created from an express full backup.

5.  If you’re recovering to a SQL Server, on the Specify Alternate Recovery Location page, specify details of the SQL Server to which you want to recover the database.

6.  If you’re recovering to a network folder, on the Specify Destination page, specify the details of the destination server if you want to recover to a network folder.

7.  If you’re recovering to a SQL Server, on the Specify Database State page, specify how you want to perform the recovery:

    -   **Leave database operational**—Perform a full recovery and leave the database ready to use

    -   **Leave database non\-operational but able to restore additional transaction logs**—Recover the database but leave it non\-operational

    -   **Copy SQL transaction logs between the selected recovery point and the latest recovery point**—Copy transaction logs for the database restoring state. This option if disabled if no transaction logs are available.

    -   **Copy destination**—Specify the folder path location to copy transaction logs for the database restoring state.

8.  On the Specify Recovery Options page, specify the options you want to apply to the recovered data:

    -   **Apply security settings o the destination computer**—The recovered data will have the same security settings as the destination server.

    -   **Apply the secure settings of the recovery point version**—Recovered data will retain its existing security settings.

    -   **Notification**—Send an email when recovery completes. This is only available for recovery to a network folder, and only if email notifications are enabled on the DPM server.

9. You should receive a notification that the recovery job was started successfully. On the server or location that you recovered to, verify that the files appear as expected.

