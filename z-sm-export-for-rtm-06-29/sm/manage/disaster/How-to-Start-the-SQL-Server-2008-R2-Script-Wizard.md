---
title: How to Start the SQL Server 2008 R2 Script Wizard
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 661a47c3-d228-4af0-806d-9f67a5a2f443
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
# How to Start the SQL Server 2008 R2 Script Wizard
You can use the following procedure as part of your disaster recovery preparation steps for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] to generate a script to capture SQL Server logon permissions and object\-level permissions. You perform this procedure on the computer that hosts SQL Server Reporting Services \(SSRS\) and on the computers that host the following Service Manager and data warehouse databases:  
  
-   DWDataMart  
  
-   DWRepository  
  
-   DWStagingAndConfig  
  
-   ServiceManager  
  
-   ReportServer  
  
### To start the SQL Server Script Wizard  
  
1.  Using an account with Administrator privileges, log on to the computer that hosts the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] or data warehouse database.  
  
2.  On the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008 R2**, and then click **SQL Server Management Studio**.  
  
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