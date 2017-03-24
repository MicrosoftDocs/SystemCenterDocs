---
title: Install an additional management server
description: As part of the upgrade process, you need to install an additional Management Server in the production Service Manager management group.
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
ms.assetid: 03747a1c-cdb9-47ce-83d1-55ee9d6c8119
---

# Install an additional management server in the production Service Manager management group

>Applies To: System Center 2016 - Service Manager

The following procedure shows how to install an additional management server. You must deploy the initial Service Manager management server and Service Manager Database before deploying an additional management server.  

> [!TIP]  
>  You must be a member of the Service Manager Administrators user role in order to install an additional Service Manager management server.  

When you install a secondary management server, data retention settings are reset. Before you install a secondary management server, make a note of data retention settings. After you have installed the additional management server, adjust the data retention settings to their original values.  

### To install an additional management server  

1.  By using an account that has administrator rights and that is also a member of the Service Manager Management group administrators, log on to the computer that will host the additional Service Manager Management server.  

2.  On the System Center 2016 - Service Manager installation media, double\-click Setup.exe.  

3.  On the **Microsoft System Center 2016 Service Manager** page, click **Install a Service Manager Management server**.  

4.  On the **Product registration** page, type information in the boxes. In the **Product key** boxes, type the product key you received with Service Manager, or alternatively, select **Install as an evaluation edition \(180 day trial\)?**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  

5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location where the additional Service Manager Management server will be installed.  

6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.  

    1.  If the prerequisite checker determines that the Microsoft Report Viewer Redistributable has not been installed, click **Install Microsoft Report Viewer Redistributable**. After the **Microsoft Report Viewer Redistributable 2008 \(KB971119\) Setup** wizard completes, click **Check perquisites again**.  

7.  On the **Configure the Service Manager Database** page, in the **Database server** box, type the name of the computer that hosts the Service Manager database that you used for your initial Service Manager Management server, and then press TAB. When the name of the instance displays in the **SQL Server instance** box, click **Use an existing database**. For example, type **Computer 2** in the **Database server** box.  

8.  Click the **Database** list, select the database name for the Service Manager database \(the default name is ServiceManager\), and then click **Next**.  

9. On the **Configure the Service Manager Management group** page, verify that the management group name and management group administrators boxes have been populated. Click **Next**.  

10. On the **Configure the Account for Service Manager Services** page, click **Domain account**, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a **The credentials were accepted** message, click **Next**. For example, enter the account information for the domain user SM\_Acct, and then click **Next**.  

    > [!NOTE]  
    >  The user name and password you provide here must be the same ones used for the Service Manager account on the data warehouse management server.  

11. On the **Diagnostic and usage data** page, indicate your preference for sharing your Service Manager diagnostic and usage data with Microsoft. As an option, click **Privacy statement for System Center Service Manager**, and then click **Next**.

12. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates, and then click **Next**.  

13. On the **Installation summary** page, click **Install**.  

14. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**.

## Next steps

- Review [Copy customized workflow assembly files before you upgrade](upgrade-how-to-copy-the-workflow-assembly-files.md).
