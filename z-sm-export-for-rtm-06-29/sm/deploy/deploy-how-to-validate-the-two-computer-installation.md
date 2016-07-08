---
title: How to Validate the Two-Computer Installation
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54fa37fb-1a2c-4d5c-b25f-041782b77215


















---
# How to Validate the Two-Computer Installation
You can use the following procedures to validate the two\-computer installation of System Center 2012 - Service Manager. In these procedures, the *first computer* is the computer on which you installed the Service Manager management server, the Service Manager database, and Service Manager console. The *second computer* is the computer that hosts the data warehouse management server and the data warehouse databases.  
  
### To validate the Service Manager management server installation  
  
-   On the first computer, verify that the Program Files\\Microsoft System Center\\Service Manager 2012 folder exists.  
  
-   Run **services.msc**, and then verify that the following services are installed, that they have a status of **Started**, and that the startup type is **Automatic**:  
  
    -   System Center Data Access Service  
  
    -   System Center Management Configuration  
  
### To validate the Service Manager console installation  
  
1.  On the first computer, click **Start**, click **All Programs**, click **Microsoft System Center**, and then click **Service Manager Console**.  
  
2.  The first time that you run the Service Manager console, the **Connect to Service Manager Server** dialog box appears. In the **Server name** box, enter the computer name of the server that hosts the Service Manager management server.  
  
3.  The Service Manager console successfully connects to the Service Manager management server.  
  
### To validate the data warehouse management server installation  
  
-   On the second computer, run **services.msc**, and verify that the following services are installed:  
  
    -   System Center Data Access Service  
  
    -   System Center Management Configuration  
  
### To validate the Service Manager database  
  
1.  On the first computer, click **Start**, click **All Programs**, click **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, complete these steps:  
  
    1.  In the **Server Name** list, type the computer name for the computer that hosts the Service Manager database. In this example, type **localhost**.  
  
    2.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**.  
  
4.  Verify that the **ServiceManager** database is listed.  
  
5.  Exit Microsoft SQL Server Management Studio.  
  
### To validate the data warehouse installation  
  
1.  On the second computer, click **Start**, click **All Programs**, click **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, complete these steps:  
  
    1.  In the **Server Name** list, type the computer name for the computer that hosts the Service Manager data warehouse database. In this example, type **localhost**.  
  
    2.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**.  
  
4.  Verify that the **DWDataMart**, **DWRepository**, and **DWStagingAndConfig** databases are listed.  
  
5.  In the **Object Explorer** pane, click **Connect**, and then click **Analysis Services**.  
  
6.  In the **Server Name** list, type the computer name for the computer hosting the Service Manager data warehouse database. In this example, type **localhost**.  
  
7.  In the **Object Explorer** pane, expand the new entry for Analysis Services, and then expand **Databases**.  
  
8.  Verify that the **DWASDataBase** database is listed.  
  
9. Exit Microsoft SQL Server Management Studio.
