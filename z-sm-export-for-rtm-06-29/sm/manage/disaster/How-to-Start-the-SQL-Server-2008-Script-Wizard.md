---
title: How to Start the SQL Server 2008 Script Wizard
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d66205ea-8470-4994-9ce2-ebb08d404c02
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Start the SQL Server 2008 Script Wizard
You can use the following procedure as part of your disaster recovery preparation steps for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] to generate a script to capture SQL Server logon permissions and object\-level permissions. You perform this procedure on the computer that hosts SQL Server Reporting Services \(SSRS\) and on the computers that host the following [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and data warehouse databases:  
  
-   DWDataMart  
  
-   DWRepository  
  
-   DWStagingAndConfig  
  
-   ServiceManager  
  
-   ReportServer  
  
### To start the SQL Server Script Wizard  
  
1.  Using an account with Administrator privileges, log on to the computer that hosts the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] or data warehouse database.  
  
2.  On the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.  
  
3.  In the **Connect to Server** dialog box, do the following:  
  
    1.  In the **Server Type** list, select **Database Engine**.  
  
    2.  In the **Server Name** list, select the server and the instance for your Server Manager database. For example, select **computer\\INSTANCE1**.  
  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
4.  In the **Object Explorer** pane, expand **Databases**.  
  
5.  Right\-click the database name, point to **Tasks**, and then click **Generate Scripts**. For this example, right\-click **ServiceManager**, point to **Tasks**, and then click **Generate Scripts**.  
  
6.  In the **Script Wizard** dialog box, do the following:  
  
    1.  On the **Welcome to the Generate SQL Server Scripts Wizard** page, click **Next**.  
  
    2.  On the **Select Database** page, select the database for which you are generating the script. In this example, select **ServiceManager**, and then click **Next**.  
  
    3.  On the **Choose Script Options** page, set all True\/False entries to **False**. In the **General** area, set **Script Logins** and **Script Object\-Level Permissions** to **True**, and then click **Next**.  
  
    4.  On the **Choose Object Types** page, click **Select All**, and then click **Next**.  
  
    5.  On the **Choose Assemblies** page, click **Select All**, and then click **Next**.  
  
    6.  On the **Choose Database Roles** page, click **Select All**, and then click **Next**.  
  
    7.  On the **Choose Schemas** page, click **Select All**, and then click **Next**.  
  
    8.  On the **Choose Stored Procedures** page, click **Select All**, and then click **Next**.  
  
    9. On the **Choose Tables** page, click **Select All**, and then click **Next**.  
  
    10. On the **Choose User\-Defined Table Types** page, click **Select All**, and then click **Next**.  
  
    11. On the **Choose User\-Defined Functions** page, click **Select All**, and then click **Next**.  
  
    12. On the **Choose Users** page, click **Select All**, and then click **Next**.  
  
    13. On the **Choose Views** page, click **Select All**, and then click **Next**.  
  
    14. On the **Choose XML Schema Collections** page, click **Select All**, and then click **Next**.  
  
    15. On the **Choose full text catalogs** page, click **Select All**, and then click **Next**.  
  
    16. On the **Output Option** page, select **Script to file**, and in **File name**, type a location and file name for the script \(for example, type **C:\\Backup\\ServiceManagerDatabaseScript.sql**\), and then click **Next**.  
  
    17. On the **Script Wizard Summary** page, click **Finish**.  
  
    18. On the **Generate Script Progress** page, make sure that **Success** appears, and then click **Close**.  
  
7.  Save the script file that you just created on a separate physical computer, usually at the same location where you are saving your [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] encryption keys.  
  
8.  Run this same procedure on each of the three data warehouse databases and SSRS.  
  
9. If you need to restore a database, use these scripts to restore permissions to the new server.