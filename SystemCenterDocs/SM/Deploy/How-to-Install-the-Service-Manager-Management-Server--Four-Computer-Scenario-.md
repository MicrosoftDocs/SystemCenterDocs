---
title: How to Install the Service Manager Management Server (Four-Computer Scenario)
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f420b9b-c3ca-424c-9b35-520807ab40a7
---
# How to Install the Service Manager Management Server (Four-Computer Scenario)
The following procedure describes how to install the [!INCLUDE[scsm_threshold_1](../../Token/scsm_threshold_1_md.md)] management server, the [!INCLUDE[smshort12](../../Token/smshort12_md.md)] database, the data warehouse management server, data warehouse databases, and the [!INCLUDE[smcons](../../Token/smcons_md.md)] in a four\-computer topology. You start the deployment process by installing the [!INCLUDE[smshort12](../../Token/smshort12_md.md)] management server and the [!INCLUDE[smcons](../../Token/smcons_md.md)] on one computer and the [!INCLUDE[smshort12](../../Token/smshort12_md.md)] database on a second computer. Before you start, make sure that Microsoft SQL Server 2008 is installed on the computer that will host the [!INCLUDE[smshort12](../../Token/smshort12_md.md)] database.

During Setup, you will be prompted to provide credentials for the following accounts:

-   Management group administrator

-   [!INCLUDE[smshort12](../../Token/smshort12_md.md)] services account

-   [!INCLUDE[smshort12](../../Token/smshort12_md.md)] workflow account

For more information about the permissions that these accounts require, see "Accounts Required During Setup" in the [Planning Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209672).

### To install the Service Manager management server, Service Manager database, and console

1.  Log on to the computer that will host the [!INCLUDE[smshort12](../../Token/smshort12_md.md)] management server by using an account that has administrative rights.

2.  On the System Center Service Manager installation media, double\-click the **Setup.exe** file.

3.  On the **Service Manager Setup Wizard** page, click **Service Manager management server**.

4.  On the **Product registration** page, in the **Product key** boxes, type the product key that you received with [!INCLUDE[smshort12](../../Token/smshort12_md.md)], or as an alternative, select **Install as an evaluation edition \(180 day trial\)**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

5.  On the **Installation location** page, verify that sufficient free disk space is available. If necessary, click **Browse** to change the location of where the [!INCLUDE[smshort12](../../Token/smshort12_md.md)] management server will be installed. Click **Next**.

6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings.

    If the prerequisite checker determines that the Microsoft Report Viewer Redistributable has not been installed, click **Install Microsoft Report Viewer Redistributable**. After the Microsoft Report Viewer Redistributable 2008 \(KB971119\) Setup Wizard completes, click **Check prerequisites again**. Click **Next**.

7.  On the **Configure the Service Manager database** page, in the **Database server** field, type the name of the computer that will host the [!INCLUDE[smshort12](../../Token/smshort12_md.md)] database, and press the TAB key. Ensure that **SQL Server instance** box is set to the desired SQL Server instance and that **Create a new database** is selected, and then click **Next**. For example, type **Computer 2** in the **Database server** box.

    > [!IMPORTANT]
    > A warning message appears if you are using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\). Support for multiple languages in Service Manager is not possible when you are using the default collation. If later you decide to support multiple languages using a different collation, you have to reinstall SQL Server. See "Microsoft SQL Server 2008 with SP1" in the [Planning Guide for Service Manager for System Center 2012](http://go.microsoft.com/fwlink/p/?LinkID=209672).

8.  On the **Configure the Service Manager management group** page, complete these steps:

    1.  In the **Management group name** box, type a unique name for the group name.

        > [!IMPORTANT]
        > Management group names must be unique. Do not use the same management group name even when you are deploying a [!INCLUDE[smshort12](../../Token/smshort12_md.md)] management server and a [!INCLUDE[smshort12](../../Token/smshort12_md.md)] data warehouse management server. Furthermore, do not use the management group name that is used for Operations Manager.

    2.  In the **Management group administrators** areas, click **Browse**, enter the user or group that you want to be the [!INCLUDE[smshort12](../../Token/smshort12_md.md)] administrator, and then click **Next**. For example, select the group Woodgrove\\SM\_Admins.

9. On the **Configure the account for Service Manager services** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.

10. On the **Configure the Service Manager workflow account** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.

11. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click **Tell me more about the program**, and then click **Next**.

12. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for [!INCLUDE[smshort12](../../Token/smshort12_md.md)] updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Click **Next**.

13. On the **Installation summary** page, click **Install**.

14. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**. For more information about backing up the encryption key, see [Completing Deployment by Backing Up the Encryption Key](assetId:///dbb276a9-7df5-4cd9-ae75-9099aabcaa93).


