---
title: How to Install an Audit Collection Services (ACS) Collector and Database
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d281902-d6b9-4cf9-9b89-fb79e761f4f5
---
# How to Install an Audit Collection Services (ACS) Collector and Database
Use the following procedures in [!INCLUDE[om12long](./Token/om12long_md.md)] to install an Audit Collection Services \(ACS\) collector and database and to start the service for the ACS collector computer. Both procedures are performed on the computer that is designated as your ACS collector.

The ACS database runs on a supported version of Microsoft SQL Server. The Audit Collection Services Collector Setup wizard creates the ACS database on an existing installation of Microsoft SQL Server. To complete the installation procedure, you must be a member of the local Administrators group on both the ACS collector and the ACS database computers as well as a database administrator on the ACS database. As a best practice for security, consider using Run As to perform this procedure.

For information about system requirements and best practices for performance, see [Collecting Security Events Using Audit Collection Services in Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=207797) and [Audit Collection Services Capacity Planning](http://go.microsoft.com/fwlink/p/?LinkID=238721) in the Operations Guide.

### To install an ACS collector and an ACS database

1.  Log on to the server by using an account that has local administrative credentials.

2.  On the [!INCLUDE[om12short](./Token/om12short_md.md)] installation media, run **Setup.exe**, and then click **Audit collection services**.

    For monitoring UNIX and Linux computers, click **Audit collection services for UNIX\/Linux**.

    The **Audit Collection Services Collector Setup** wizard opens.

3.  On the **Welcome** page, click **Next**.

4.  On the **License Agreement** page, read the licensing terms, click **I accept the agreement**, and then click **Next**.

5.  On the **Database Installation Options** page, click **Create a new database**, and then click **Next**.

6.  On the **Data Source** page, in the **Data source name** box, type a name that you want to use as the Open Database Connectivity \(ODBC\) data source name for your ACS database. By default, this name is **OpsMgrAC**. Click **Next**.

7.  On the **Database** page, if the database is on a separate server than the ACS collector, click **Remote Database Server**, and then type the computer name of the database server that will host the database for this installation of ACS. Otherwise, click **Database server running locally**.

8.  In the **Database server instance name** field, type the name of the database that will be created for ACS. If you leave this field blank, the default name is used. In the **Database** name field, the default database name of **OperationsManagerAC** is automatically entered. You can select the text and type in a different name or leave the default name. Click **Next**.

    > [!NOTE]
    > To display a list of SQL Server Instances, on the database computer click **Start**, point to **Programs** and open **SQL Server** \(the appropriate version of SQL Server is dependent on the version of [!INCLUDE[om12short](./Token/om12short_md.md)] – see [System Requirements for System Center 2012 – Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=219650)\), and then click **SQL Server Management Studio**. On the **Server name** list, click **Browse for more** and then expand **Database Engine**. All databases are listed as server name\\database name.

9. On the **Database Authentication** page, select one of the authentication methods. If the ACS collector and the ACS database are members of the same domain, you can select **Windows authentication**, otherwise select **SQL authentication**, and then click **Next**.

    > [!NOTE]
    > If you select **SQL authentication** and click **Next**, the **Database Credentials** page displays. In the **SQL login name** box, enter the name of the user account that has access to the SQL Server and the password for that account in the **SQL password** box, and then click **Next**.

10. On the **Database Creation Options** page, click **Use SQL Server's default data and log file directories** to use SQL Server's default folders. Otherwise, click **Specify directories** and enter the full path, including drive letter, to the location you want for the ACS database and log file, for example C:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data. Click **Next**.

11. On the **Event Retention Schedule** page, click **Local hour of day to perform daily database maintenance**. Choose a time when the number of expected security events is low. During the database maintenance period, database performance will be impacted. In the **Number of days to retain events** box type the number of days ACS should keep events in the ACS database before the events are removed during database grooming. The default value is 14 days. Click **Next**.

12. On the **ACS Stored Timestamp Format** page, choose **Local** or **Universal Coordinated Time**, formerly known to as Greenwich Mean Time, and then click **Next**

13. The **Summary** page displays a list of actions that the installation program will perform to install ACS. Review the list, and then click **Next** to begin the installation.

    > [!NOTE]
    > If a **SQL server login** dialog box displays and the database authentication is set to **Windows authentication**, click the correct database and verify that the **Use Trusted Connection** check box is checked. Otherwise click to remove the check and enter the SQL login name and password. Click **OK**.

14. When the installation is complete, click **Finish**.

## See Also
[Deploying ACS and ACS Reporting](assetId:///acbe8dba-82f5-447b-a01c-9abb337e378c)
[How to Install Audit Collection Services \(ACS\)](assetId:///7686cf46-0792-4057-8d47-920063fc8928)
[How to Deploy ACS on a Secondary Management Server](assetId:///d1b8064f-01dd-4c54-94c4-b64f61b994d5)
[How to Deploy ACS Reporting](assetId:///8a06a7bd-78b8-442a-ba7f-2b7027018f55)


