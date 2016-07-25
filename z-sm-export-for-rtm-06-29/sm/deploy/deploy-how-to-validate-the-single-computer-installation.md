---
title: How to Validate the Single-Computer Installation
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e53368f-77f9-456a-964c-989d6e797990


















---
# How to Validate the Single-Computer Installation
You can use the following procedures to validate the single\-computer installation of System Center 2012 - Service Manager.  
  
### To validate the Service Manager management server installation  
  
1.  On the physical computer that hosts the Service Manager management server, verify that the Program Files\\Microsoft System Center 2012\\Service Manager\\ folder exists.  
  
2.  Run **services.msc**, and then verify that the following services are installed, that they have a status of **Started**, and that the startup type is **Automatic**:  
  
    -   **System Center Data Access Service**  
  
    -   **System Center Management**  
  
        > [!NOTE]  
        >  For System Center 2012 R2 Service Manager, the System Center Management service was renamed to Microsoft Monitoring Agent.  
  
    -   **System Center Management Configuration**  
  
### To validate the Service Manager console installation  
  
1.  On the physical computer, click **Start**, click **All Programs**, click **Microsoft System Center**, and then click **Service Manager Console**.  
  
2.  The first time that you run the Service Manager console, the **Connect to Service Manager Server** dialog box appears. In the **Server name** box, enter the computer name of the server that hosts the Service Manager management server.  
  
3.  The Service Manager console successfully connects to the Service Manager management server and starts.  
  
### To validate the data warehouse management server installation  
  
-   On the virtual machine, run **services.msc**, and verify that the following services are installed:  
  
    -   **System Center Data Access Service**  
  
    -   **System Center Management**  
  
        > [!NOTE]  
        >  For System Center 2012 R2 Service Manager, the System Center Management service was renamed to Microsoft Monitoring Agent.  
  
    -   **System Center Management Configuration**  
  
### To validate the Service Manager database  
  
1.  On the physical computer, click **Start**, click **All Programs**, click **Microsoft SQL Server&nbsp;2008**, and then click **SQL Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, follow these steps:  
  
    1.  In the **Server Type** list, select **Database Engine**.  
  
    2.  In the **Server Name** list, select the name of the computer that hosts the Service Manager database.  
  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**.  
  
4.  Verify that the **ServiceManager** database is listed.  
  
5.  Exit Microsoft SQL Server Management Studio.  
  
### To validate the data warehouse installation  
  
1.  On the physical computer that hosts the data warehouse databases, click **Start**, click **All Programs**, click **Microsoft SQL&nbsp;Server&nbsp;2008**, and then click **SQL&nbsp;Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, complete these steps:  
  
    1.  In the **Server Name** list, type the computer name of the computer hosting Service Manager data warehouse databases. For this example, type **localhost**.  
  
    2.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**.  
  
4.  Verify that the **DWDataMart**, **DWRepository**, and **DWStagingAndConfig** databases are listed.  
  
5.  In the **Object Explorer** pane, click **Connect**, and then click **Analysis Services**.  
  
6.  In the **Server Name** list, type the computer name for the computer hosting the Service Manager data warehouse database. In this example, type **localhost**.  
  
7.  In the **Object Explorer** pane, expand the new entry for Analysis Services, and then expand **Databases**.  
  
8.  Verify that the **DWASDataBase** database is listed.  
  
9. Exit Microsoft SQL&nbsp;Server Management Studio.
