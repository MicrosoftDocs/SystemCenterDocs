---
title: How to Install an Additional Management Server
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24e7b034-b009-40f1-9987-16665516ac54
 

















---
# How to Install an Additional Management Server
The following procedure shows how to install an additional management server in System Center 2012 - Service Manager. You must deploy the initial Service Manager management server and Service Manager database before deploying an additional management server.  
  
> [!NOTE]  
>  You must be a member of the Service Manager Administrators user role to install an additional Service Manager management server.  
  
### To install an additional management server  
  
1.  By using an account that has administrator rights and that is also a member of the Service Manager management group administrators, log on to the computer that will host the additional Service Manager management server.  
  
2.  On the System Center 2012 - Service Manager installation media, double\-click the **Setup.exe** file.  
  
3.  On the **Service Manager Setup Wizard** page, click **Service Manager management server**.  
  
4.  On the **Product registration** page, type information in the boxes. In the **Product key** boxes, type the product key you received with Service Manager, or as an alternative, select **Install as an evaluation edition \(180 day trial\)?**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  
  
5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location where the additional Service Manager management server will be installed.  
  
6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.  
  
     If the prerequisite checker determines that the Microsoft Report Viewer Redistributable has not been installed, click **Install Microsoft Report Viewer Redistributable**. After the Microsoft Report Viewer Redistributable 2008 \(KB971119\) Setup Wizard completes, click **Check perquisites again**.  
  
7.  On the **Configure the Service Manager database** page, in the **Database server** box, type the name of the computer that hosts the Service Manager database that you used for your initial Service Manager management server, and then press the TAB key. When the name of the instance appears in the **SQL Server instance** box, click **Use an existing database**. For example, type **Computer 2** in the **Database server** box.  
  
8.  Click the **Database** list, select the database name for the Service Manager database \(the default name is **ServiceManager**\), and then click **Next**.  
  
9. On the **Configure the Service Manager management group** page, verify that the management group name and management group administrators boxes have been populated. Click **Next**.  
  
10. On the **Configure the account for Service Manager services** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**. For example, enter the account information for the domain user SM\_Acct, and then click **Next**.  
  
11. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click **Tell me more about the program**, and then click **Next**.  
  
12. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Click **Next**.  
  
13. On the **Installation summary** page, click **Install**.  
  
14. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**. For more information about backing up the encryption key, see [Completing Deployment by Backing Up the Encryption Key](../../../sm/deploy/deploy-guide/Completing-Deployment-by-Backing-Up-the-Encryption-Key.md).
