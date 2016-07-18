---
title: How to Validate the Four-Computer Installation
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c69ae206-b4e6-4bb2-a543-5613a5827d0e
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
# How to Validate the Four-Computer Installation
The procedures in this topic describe how to validate the four\-computer installation of [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
## Step 1: Validate the Installation of the Management Server and Database  
  
#### To validate a Service Manager management server installation  
  
1.  On the computer hosting the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, verify that a Program Files\\Microsoft System Center 2012\\Service Manager folder exists.  
  
2.  Run **services.msc**, and then verify that the following services are installed, that they have the status of **Started**, and that the startup type is **Automatic**:  
  
    -   System Center Data Access Service  
  
    -   System Center Management  
  
        > [!NOTE]  
        >  For [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)], the System Center Management service was renamed to Microsoft Monitoring Agent.  
  
    -   System Center Management Configuration  
  
#### To validate the Service Manager console installation  
  
1.  On the first computer, click **Start**, click **All Programs**, click **Microsoft System Center**, and then click **Service Manager Console**.  
  
2.  The first time that you run the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], the **Connect to Service Manager Server** dialog box appears. In the **Server name** box, enter the computer name of the server that is hosting the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server.  
  
3.  The [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] successfully connects to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server.  
  
#### To validate the Service Manager database  
  
1.  On the computer hosting the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, click **Start**, click **All Programs**, click **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, select the following:  
  
    1.  In the **Server Type** list, select **Database Engine**.  
  
    2.  In the **Server Name** list, select the server name for your [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database. For example, select **Computer 2**.  
  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**.  
  
4.  Verify that the **ServiceManager** database is listed.  
  
5.  Exit **Microsoft SQL Server Management Studio**.  
  
## Step 2: Validate the Installation of the Data Warehouse Management Server and Database  
  
#### To validate a data warehouse management server installation  
  
-   On the computer hosting the data warehouse management server \(the server you ran Setup on\), run **services.msc**, and verify that the following services have been installed:  
  
    -   System Center Data Access Service  
  
    -   System Center Management  
  
        > [!NOTE]  
        >  For [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)], the System Center Management service was renamed to Microsoft Monitoring Agent.  
  
    -   System Center Management Configuration  
  
#### To validate data warehouse databases  
  
1.  On the computer hosting the data warehouse management databases, click **Start**, click **All Programs**, click **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, select the following:  
  
    1.  In the **Server Type** list, select **Database Engine**.  
  
    2.  In the **Server Name** list, select the server and instance for your [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse database. For example, select **Computer 4**.  
  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**.  
  
4.  Verify that the **DWStagingAndConfig** and **DWRepository** databases are listed.  
  
5.  On the computer hosting SQL Server Reporting Services \(SSRS\), click **Start**, click **All Programs**, click **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.  
  
6.  In the **Connect to Server** dialog box, select the following:  
  
    1.  In the **Server Type** list, select **Database Engine**.  
  
    2.  In the **Server Name** list, select the server and instance for your [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse database. For example, select **Computer 4**.  
  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
7.  In the **Object Explorer** pane, expand **Databases**.  
  
8.  Verify that the **DWDataMart** database is listed.  
  
9. In the **Object Explorer** pane, click **Connect**, and then click **Analysis Services**.  
  
10. In the **Server Name** list, type the computer name for the computer hosting the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse database. In this example, type **localhost**.  
  
11. In the **Object Explorer** pane, expand the new entry for Analysis Services, and then expand **Databases**.  
  
12. Verify that the **DWASDataBase** database is listed.  
  
13. Exit Microsoft SQL Server Management Studio.