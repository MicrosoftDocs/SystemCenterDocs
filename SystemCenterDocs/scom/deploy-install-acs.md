---
ms.assetid: ed1c51df-2507-4f34-b051-04540896ac17
title: How to Install an Audit Collection Services ACS Collector and Database
description: This article describes how to install the Operations Manager Audit Collector and ACS database.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to install an Audit Collection Services (ACS) collector and database

>Applies To: System Center 2016 - Operations Manager

Use the following procedures to install an Audit Collection Services (ACS) collector and database and to start the service for the ACS collector computer. Both procedures are performed on the computer that is designated as your ACS collector.

The ACS database runs on a supported version of Microsoft SQL Server. The Audit Collection Services Collector Setup wizard creates the ACS database on an existing installation of Microsoft SQL Server. To complete the installation procedure, you must be a member of the local Administrators group on both the ACS collector and the ACS database computers as well as a database administrator on the ACS database. As a best practice for security, consider using Run As to perform this procedure.

## To install an ACS collector and an ACS database

1.  Log on to the server by using an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Audit collection services**.

    For monitoring UNIX and Linux computers, click **Audit collection services for UNIX/Linux**.

    The **Audit Collection Services Collector Setup** wizard opens.

3.  On the **Welcome** page, click **Next**.

4.  On the **License Agreement** page, read the licensing terms, click **I accept the agreement**, and then click **Next**.

5.  On the **Database Installation Options** page, click **Create a new database**, and then click **Next**.

6.  On the **Data Source** page, in the **Data source name** box, type a name that you want to use as the Open Database Connectivity (ODBC) data source name for your ACS database. By default, this name is **OpsMgrAC**. Click **Next**.

7.  On the **Database** page, if the database is on a separate server than the ACS collector, click **Remote Database Server**, and then type the computer name of the database server that will host the database for this installation of ACS. Otherwise, click **Database server running locally**.

8.  In the **Database server instance name** field, type the name of the database that will be created for ACS. If you leave this field blank, the default name is used. In the **Database** name field, the default database name of **OperationsManagerAC** is automatically entered. You can select the text and type in a different name or leave the default name. Click **Next**.

    > [!NOTE]
    > To display a list of SQL Server Instances, on the database computer click **Start**, point to **Programs** and open **SQL Server** (the appropriate version of SQL Server is dependent on the version of Operations Manager - see [System Requirements for System Center 2012 - Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=219650)), and then click **SQL Server Management Studio**. On the **Server name** list, click **Browse for more** and then expand **Database Engine**. All databases are listed as server name\database name.

9. On the **Database Authentication** page, select one of the authentication methods. If the ACS collector and the ACS database are members of the same domain, you can select **Windows authentication**, otherwise select **SQL authentication**, and then click **Next**.

    > [!NOTE]
    > If you select **SQL authentication** and click **Next**, the **Database Credentials** page displays. In the **SQL login name** box, enter the name of the user account that has access to the SQL Server and the password for that account in the **SQL password** box, and then click **Next**.

10. On the **Database Creation Options** page, click **Use SQL Server's default data and log file directories** to use SQL Server's default folders. Otherwise, click **Specify directories** and enter the full path, including drive letter, to the location you want for the ACS database and log file, for example C:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Data. Click **Next**.

11. On the **Event Retention Schedule** page, click **Local hour of day to perform daily database maintenance**. Choose a time when the number of expected security events is low. During the database maintenance period, database performance will be impacted. In the **Number of days to retain events** box type the number of days ACS should keep events in the ACS database before the events are removed during database grooming. The default value is 14 days. Click **Next**.

12. On the **ACS Stored Timestamp Format** page, choose **Local** or **Universal Coordinated Time**, formerly known to as Greenwich Mean Time, and then click **Next**

13. The **Summary** page displays a list of actions that the installation program will perform to install ACS. Review the list, and then click **Next** to begin the installation.

    > [!NOTE]
    > If a **SQL server login** dialog box displays and the database authentication is set to **Windows authentication**, click the correct database and verify that the **Use Trusted Connection** check box is checked. Otherwise click to remove the check and enter the SQL login name and password. Click **OK**.

14. When the installation is complete, click **Finish**.

## To deploy ACS reporting

1.  Log on to the server that will be used to host ACS reporting as a user that is an administrator of the SSRS instance.

2.  Create a temporary folder, such as **C:\acs**.

3.  On your installation media, go to **\ReportModels\acs** and copy the directory contents to the temporary installation folder.

    There are two folders (**Models** and **Reports**) and a file named **UploadAuditReports.cmd**.

4.  On your installation media, go to **\SupportTools** and copy the file **ReportingConfig.exe** into the temporary **acs** folder.

5.  Open a Command Prompt window by using the **Run as Administrator** option, and then change directories to the temporary **acs** folder.

6.  Run the following command.
    `UploadAuditReports "<AuditDBServer\Instance>" "<Reporting Server URL>" "<path of the copied acs folder>"`
    For example: `UploadAuditReports "myAuditDbServer\Instance1" "http://myReportServer/ReportServer$instance1" "C:\acs"`

    This example creates a new data source called **Db Audit**, uploads the reporting models **Audit.smdl** and **Audit5.smdl**, and uploads all reports in the **acs\reports** directory.

    > [!NOTE]
    > The reporting server URL needs the reporting server virtual directory (`ReportingServer_<InstanceName>`) instead of the reporting manager directory (`Reports_<InstanceName>`).

7.  Open Internet Explorer and enter the following address to view the **SQL Reporting Services Home** page. `http://<yourReportingServerName>/Reports_<InstanceName>`

8.  Click **Audit Reports** in the body of the page and then click **Show Details** in the upper right part of the page.

9. Click the **Db Audit** data source.

10. In the **Connect Using** section, select **Windows Integrated Security** and click **Apply**.

## Next steps

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  
