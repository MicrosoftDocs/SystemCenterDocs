---
title: Deploy additional Service Manager management servers
description: Deploy additional Service Manager management servers to load-balance additional Service Manager consoles or to support your disaster recovery strategy.
ms.custom: intro-deployment, UpdateFrequency3, engagement-fy23, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: install-set-up-deploy
ms.assetid: 80e03b05-c500-4b96-8ca0-4193e9cc07b1
---

# Deploy additional Service Manager management servers



You can deploy additional Service Manager management servers to load-balance additional Service Manager consoles or as part of your disaster recovery strategy.  

 This section describes how you can install additional Service Manager management servers. The additional Service Manager management servers can improve performance in a high-use environment.  

## Management servers

You create a management server when you select **Service Manager management server** in the Service Manager Setup Wizard. The initial Service Manager management server hosts data access, workflow services, and authorization services.  

### Initial and additional management servers

When you run Setup for the first time, you install the initial Service Manager management server and define the management group for your installation. The initial management server handles all of the workflows in your Service Manager environment. Any additional Service Manager management servers that you deploy are used to load-balance additional Service Manager console connections. With this release of Service Manager, we recommend that you deploy an additional Service Manager management server for every 40 to 50 Service Manager consoles that you intend to deploy.  

To associate your additional Service Manager management servers with the initial Service Manager management server and management group, you must specify the Service Manager database that you used for your initial Service Manager management server.  

## Disjointed namespace considerations

If you're installing an additional management server in an environment with a disjointed namespace, see [Deployment considerations with a disjointed namespace](disjointed-namespaces.md).  

## Install an additional management server

The following procedure shows how to install an additional management server in System Center - Service Manager. You must deploy the initial Service Manager management server and Service Manager database before deploying an additional management server.  

> [!NOTE]  
> You must be a member of the Service Manager Administrators user role to install an additional Service Manager management server.  

To install an additional management server, follow these steps:

1. By using an account that has administrator rights and that is also a member of the Service Manager management group administrators, sign in to the computer that will host the additional Service Manager management server.  

2. On the System Center - Service Manager installation media, double-click the **Setup.exe** file.  

3. On the **Service Manager Setup Wizard** page, select **Service Manager management server**.  

4. On the **Product registration** page, enter the information in the boxes. In the **Product key** boxes, enter the product key you received with Service Manager, or as an alternative, select **Install as an evaluation edition (180 day trial)?**. Read the Microsoft Software License Terms, and, if applicable, select **I have read, understood, and agree with the terms of the license agreement**, and select **Next**.  

5. On the **Installation location** page, verify that sufficient free disk space is available, and select **Next**. If necessary, select **Browse** to change the location where the additional Service Manager management server will be installed.  

6. On the **System check results** page, ensure that the prerequisite check passed or at least passed with warnings, and select **Next**.  

     If the prerequisite checker determines that the Microsoft Report Viewer Redistributable hasn't been installed, select **Install Microsoft Report Viewer Redistributable**. After the Microsoft Report Viewer Redistributable 2008 (KB971119) Setup Wizard completes, select **Check perquisites again**.  

7. On the **Configure the Service Manager database** page, in the **Database server** box, enter the name of the computer that hosts the Service Manager database that you used for your initial Service Manager management server, and then press the Tab key. When the name of the instance appears in the **SQL Server instance** box, select **Use an existing database**. For example, enter **Computer 2** in the **Database server** box.  

8. Select the **Database** list, select the database name for the Service Manager database (the default name is **ServiceManager**), and select **Next**.  

9. On the **Configure the Service Manager management group** page, verify that the management group name and management group administrators boxes have been populated. Select **Next**.  

10. On the **Diagnostic and usage data** page, indicate your preference for sharing your Service Manager diagnostic and usage data with Microsoft. As an option, select **Privacy statement for System Center Service Manager**, and select **Next**.  

11. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, select **Tell me more about the program**, and select **Next**.  

12. On the **Use Microsoft Update to help keep your computer secure and up-to-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Select **Next**.  

13. On the **Installation summary** page, select **Install**.  

14. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and select **Close**. For more information about backing up the encryption key, see [Complete deployment by backing up the encryption key](encryption-key.md).

## Next steps

To perform additional steps when you deploy either an additional Service Manager management server or Self-Service Portal in an environment with a disjointed namespace, review [Deployment considerations with a disjointed namespace](disjointed-namespaces.md).
