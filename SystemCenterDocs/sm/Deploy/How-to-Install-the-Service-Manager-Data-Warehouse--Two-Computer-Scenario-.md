---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Install the Service Manager Data Warehouse  Two Computer Scenario 
ms.technology:  service-manager
ms.assetid:  e4ecbde0-c51b-4511-b3b4-c84bc2bcd141
---

# How to Install the Service Manager Data Warehouse (Two-Computer Scenario)
As the second step in the two-computer installation process for System Center 2016 Technical Preview - Service Manager, deploy the data warehouse management server and the data warehouse databases on the second computer. During Setup, you will be prompted to provide credentials for the following accounts:

-   Management group administrator

-   Service Manager services account

-   Reporting account

For more information about the permissions that these accounts require, see "Accounts Required During Setup" in the [Planning Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209672). Before you start, make sure that Microsoft SQL Server Reporting Services (SSRS) is installed in the default instance of Microsoft SQL Server.

### To install a data warehouse management server and data warehouse databases

-   Log on to the computer by using an account that has administrative rights.

-   On the Service Manager installation media, double-click the **Setup.exe** file.

-   On the **Service Manager Setup Wizard** page, click **Service Manager data warehouse management server**.

-   On the **Product registration** page, type information in the boxes. In the **Product key** boxes, type the product key that you received with Service Manager, or as an alternative, select **Install as an evaluation edition (180 day trial**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

-   On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which the Service Manager data warehouse management server will be installed.

-   On the **System check results** page, make sure that prerequisites passed or at least passed with warnings, and then click **Next**.

-   On the **Configure data warehouse databases** page, Service Manager checks the computer you are using to see if it can host the data warehouse databases. For this configuration, confirm that the database server is the computer on which you are installing the data warehouse management server, and then click **Next**.

    > [!IMPORTANT]
    > A warning message appears if you are using the default collation (SQL_Latin1_General_CP1_CI_AS). Support for multiple languages in Service Manager is not possible when you are using the default collation. If later you decide to support multiple languages using a different collation, you have to re-install SQL Server. See “Microsoft SQL Server 2008 with SP1” in the [Planning Guide for System Center 2012 - Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209672).

-   On the **Configure additional data warehouse datamarts** page, Service Manager checks the current computer to see if an instance of SQL Server exists. By default, if an instance is found, Service Manager creates a new database in the existing instance. If an instance appears, click **Next**.

-   On the **Configure the data warehouse management group** page, complete these steps:

    1.  In the **Management group name** box, type a unique name for the group.

        > [!IMPORTANT]
        > Management group names must be unique. Do not use the same management group name when you deploy a Service Manager management server and a Service Manager data warehouse management server. Furthermore, do not use the management group name that is used for Operations Manager.

    2.  Click **Browse**, enter the user account or group to which you want to give Service Manager administrative rights, and then click **Next**.

-   On the **Configure the reporting server for the data warehouse** page, Service Manager will use the existing computer if SQL Server Reporting Services is present. Accept the defaults, and then click **Next**.

    > [!NOTE]
    > The URL that you are presented with might not be in the form of a fully qualified domain name (FQDN). If the URL as presented cannot be resolved in your environment, configure SQL Server Reporting URLs so that the FQDN is listed in the **Web service URL** field. For more information see [How to: Configure a URL (Reporting Services Configuration)](http://go.microsoft.com/fwlink/p/?LinkId=230712).

-   On the **Configure the account for Service Manager services** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.

-   On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.

-   On the **Configure Analysis Service for OLAP cubes** page, click **Next**.

-   On the **Configure Analysis Services credential** page, select a domain account; click **Domain account** specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.

    > [!NOTE]
    > The account that you specify here must have administrator rights on the computer hosting SSRS.

-   On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click **Tell me more about the program**, and then click **Next**.

-   On the **Use Microsoft Update to help keep your computer secure and up-to-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Click **Next**.

-   On the **Installation summary** page, click **Install**.

-   On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**.

