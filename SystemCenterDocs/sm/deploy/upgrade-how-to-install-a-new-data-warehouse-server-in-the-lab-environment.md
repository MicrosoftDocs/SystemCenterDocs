---
title: How to Install a New Data Warehouse Server in the Lab Environment
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 239ee325-d396-4e8c-8d1e-adc7d28f3f04
---

# How to Install a New Data Warehouse Server in the Lab Environment

>Applies To: System Center 2016 - Service Manager

Use the following procedure to install a new data warehouse server in the lab environment.  

### To install a data warehouse management server and data warehouse databases  

1.  Log on to the computer by using an account that has administrative rights.  

2.  On the Service Manager installation media, double\-click the **Setup.exe** file.  

3.  On the **Microsoft System Center Service Manager 2016** page, click **Install a Service Manager data warehouse management server**.  

4.  On the **Product registration** page, type information in the boxes. In the **Product key** boxes, type the product key you received with Service Manager, or alternatively, select **Install as an evaluation edition \(180 day trial\)?.** Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  

5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which the Service Manager data warehouse management server will be installed.  

6.  On the **System check results** page, make sure that prerequisites passed or at least passed with warnings, and then click **Next**.  

7.  On the **Configure data warehouse databases** page, Service Manager checks the computer you are using to see if it can host the data warehouse databases. For this configuration, confirm that the database server is the computer on which you are installing the data warehouse management server, and then click **Next**.  

    > [!WARNING]  
    >  A warning message appears if you are using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\). Support for multiple languages in Service Manager is not possible when you are using the default collation. If later you decide to support multiple languages using a different collation, you have to re\-install SQL Server.  

8.  On the **Configure the data warehouse management group** page, follow these steps:  

    1.  In the **Management group name** box, type a unique name for the group.  

        > [!WARNING]  
        >  Management group names must be unique. Do not use the same management group name when you deploy a Service Manager management server and a Service Manager data warehouse management server. Furthermore, do not use the management group name that is used for Operations Manager.  

    2.  Click **Browse**, enter the user account or group to which you want to give Service Manager administrative rights, and then click **Next**.  

9. Service Manager will use the existing computer if SQL Server Reporting Services is present. On the **Configure the reporting server for the data warehouse** page, accept the defaults, and then click **Next**.  

10. On the **Configure the account for Service Manager services** page, click **Domain account**, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a **The credentials were accepted** message, click **Next**.  

11. On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a **The credentials were accepted** message, click **Next**.  

12. On the **Help improve System Center** page, indicate your preference for participation in the Customer Experience Improvement Program and in Error Reporting. Optionally, click **Tell me more about the program**, and then click **Next**.  

13. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates, and then click **Next**.  

14. On the **Installation summary** page, click **Install**.  

### To validate a data warehouse management server installation  

1.  On the computer hosting the data warehouse management server \(the server you ran Setup on\), run services.msc, and verify that the following services have been installed:  

    -   System Center Data Access Service  

    -   System Center Management  

    -   System Center Management configuration  

2.  On the computer hosting the data warehouse databases, click **Start**, point to **Programs**, point to **Microsoft SQL Server**, and then click **SQL Server Management Studio**.  

3.  In the **Connect to Server** dialog box, select the following:  

    1.  In the **Server Type** list, select **Database Engine**.  

    2.  In the Server Name list, select the server and instance for your Service Manager data warehouse database. For example, select **Computer 4**.  

    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  

4.  In the **Object Explorer** pane, expand **Databases**.  

5.  Verify that the **DWDataMart**, **DWRepository**, and **DWStagingAndConfig** databases are listed.
