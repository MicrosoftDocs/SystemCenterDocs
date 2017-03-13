---
title: Back up Service Manager databases
description: Describes how you can back up Service Manager databases.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68f6b035-4085-4348-8247-3b31ae85f125
---

# Back up System Center 2016 - Service Manager databases

>Applies To: System Center 2016 - Service Manager

There are up to eight databases in a System Center 2016 - Service Manager environment:  

-   ServiceManager  

-   DWDataMart  

-   DWRepository  

-   DWStagingAndConfig  

-   ReportServer  

-   Analyst  

-   OMDWDataMart  

-   CMDWDataMart  

 The first four databases in this list need to connect and exchange data with the Service Manager and data warehouse management servers. Data is encrypted during these exchanges. On the management servers, the encryption keys are backed up and restored as necessary, as explained in this guide. For more information about the encryption keys on the management servers, see [Backing Up Service Manager Management Servers](disaster-backing-up-service-manager-management-servers.md). For the servers that host databases, the encryption keys are stored in the databases themselves.  

 If a computer that hosts a database fails, all you need for recovery is the ability to restore the databases, which include the encryption keys, to a computer with the same name as the original computer. Your disaster recovery strategy for the Service Manager databases should be based on procedures for general SQL&nbsp;Server disaster recovery. For more information, see [Planning for Disaster Recovery](http://go.microsoft.com/fwlink/p/?LinkID=131016).  

 As part of your disaster recovery preparation, you run a script to capture the Security log to preserve user role information for each database. After you deploy Service Manager and, if necessary, run the Data Warehouse Registration Wizard, you use the SQL&nbsp;Server Script Wizard to create a script that captures SQL&nbsp;Server logon permissions and object\-level permissions. Then, if you need to restore a new server for the Service Manager databases, you can use this script to recreate the necessary logon permissions and object\-level permissions.  

## Enable common language runtime on SQL&nbsp;Server  
 During installation of the Service Manager database, Service Manager Setup enables common language runtime \(CLR\) on the computer that is running SQL&nbsp;Server. If you restore a Service Manager database to another computer running SQL&nbsp;Server, you must enable CLR manually. For more information, see [Enabling CLR Integration](http://go.microsoft.com/fwlink/p/?LinkId=217932).  

## Start the SQL Server Script wizard

You can use the following procedure as part of your disaster recovery preparation steps for Service Manager to generate a script to capture SQL&nbsp;Server logon permissions and object\-level permissions. You perform this procedure on the computer that hosts SQL&nbsp;Server Reporting Services \(SSRS\) and on the computers that host the following Service Manager and data warehouse databases:  

-   DWDataMart  

-   DWRepository  

-   DWStagingAndConfig  

-   ServiceManager  

-   ReportServer  

### To start the SQL&nbsp;Server Script wizard  

1.  Using an account with Administrator privileges, log on to the computer that hosts the Service Manager or data warehouse database.  

2.  On the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft&nbsp;SQL&nbsp;Server&nbsp;2008&nbsp;R2**, and then click **SQL&nbsp;Server Management Studio**.  

3.  In the **Connect to Server** dialog box, do the following:  

    1.  In the **Server Type** list, select **Database Engine**.  

    2.  In the **Server Name** list, select the server and the instance for your Service Manager database. For example, select **computer\\INSTANCE1**.  

    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  

4.  In the **Object Explorer** pane, expand **Databases**.  

5.  Right\-click the database name, point to **Tasks**, and then click **Generate Scripts**. For this example, right\-click **ServiceManager**, point to **Tasks**, and then click **Generate Scripts**.  

6.  In the Generate and Publish Scripts Wizard, do the following:  

    1.  On the **Introduction** page, click **Next**.  

    2.  On the **Choose Objects** page, select **Select specific database objects**, and then click **Select All**.  

    3.  In the database objects list, expand **Tables**.  

    4.  Clear the check box for the following tables:  

        -   **dbo.STG\_Collation**  

        -   **dbo.STG\_Locale**  

        -   **dbo.STG\_MTD\_ConverisonLog**  

    5.  Scroll up to the top of the list, and then collapse **Tables**.  

    6.  Expand **Stored Procedures**.  

    7.  Clear the check box for the following stored procedures:  

        -   **dbo.STG\_DTS\_ConvertToUnicode**  

        -   **dbo.STG\_DTS\_CreateClonedTable**  

        -   **dbo.STG\_DTS\_InsertSQL**  

        -   **dbo.STG\_DTS\_ValidateConversion**  

    8.  Click **Next**.  

    9. On the **Set Scripting Options** page, select **Save scripts**, select **Save to file**, select **Single file**, specify a file location in **File name**, and then click **Next**.  

    10. On the **Summary** page, click **Next**.  

    11. When the script is complete, on the **Save or Publish Scripts** page, click **Finish**.  

7.  If you need to restore a database, use this script to set permissions.
