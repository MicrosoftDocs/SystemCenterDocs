---
title: How to Install the Service Manager Data Warehouse (Four-Computer Scenario)
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef24bc6b-17ec-4cb3-8de8-35ca0cc7d5a7
---
# How to Install the Service Manager Data Warehouse (Four-Computer Scenario)
To start deployment of the System Center 2016 Technical Preview \- Service Manager data warehouse and data warehouse databases, install the data warehouse management server on one computer \(for example, computer 3\), and all of the data warehouse databases on another computer \(for example, computer 4\).

During Setup, you will be prompted to provide credentials for the following accounts:

-   Management group administrator

-   Service Manager services account

-   Reporting account

-   Analysis Services account

For more information about the permissions that these accounts require, see "Accounts Required During Setup" in the [Planning Guide for Service Manager for System Center 2012](http://go.microsoft.com/fwlink/p/?LinkID=209672).

The data warehouse databases include the following three databases: DWStagingAndConfig, DWRepository, and DWDataMart. The first two databases, DWStagingAndConfig and DWRepository, must reside on the same instance of Microsoft SQL Server. The DWDataMart database can reside on a separate instance of SQL Server. The optional OMDWDataMart and CMDWDataMart databases can reside together or separately on their own instances of Microsoft SQL Server.

### To install a data warehouse management server

1.  Because, in this scenario, the computer that hosts SQL Server Reporting Services \(SSRS\) is not the same computer that hosts the data warehouse management server, you have to prepare the computer that will remotely host SSRS for Service Manager. See [Manual Steps to Configure the Remote SQL Server Reporting Services](Manual-Steps-to-Configure-the-Remote-SQL-Server-Reporting-Services.md) before continuing with this procedure.

2.  Log on to the computer that will host the data warehouse management server by using an account that has administrator rights. For example, run Setup on Computer 3.

3.  On the System Center Service Manager installation media, double\-click the **Setup.exe** file.

4.  On the **Service Manager Setup Wizard** page, click **Service Manager data warehouse management server**.

5.  On the **Product registration** page, in the **Product key** boxes, type the product key that you received with Service Manager, or as an alternative, select **Install as an evaluation edition \(180 day trial\)**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

6.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location where the Service Manager management server will be installed.

7.  On the **System check results** page, verify that prerequisites passed or at least passed with warnings, and then click **Next**.

8.  On the **Configure the data warehouse databases** page, click **Staging and Configuration**. In the **Database server** box, type the computer name of the computer that will host the two data warehouse databases. For example, type **Computer 4**, and then press the TAB key. Verify that **Default** appears in the **SQL Server instance** box.

    > [!IMPORTANT]
    > A warning message appears if you are using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\). Support for multiple languages in Service Manager is not possible when you are using the default collation. If later you decide to support multiple languages using a different collation, you have to reinstall SQL Server. See “Microsoft SQL Server 2008 with SP1” in the [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209672).

9. In the list of the three databases, select **Data Mart**. In the **Database server** box, type the computer name of the server that will host the Data Mart database. For example, type **Computer 4**, and then press the TAB key. When **Default** appears in the **SQL Server instance** box, click **Next**.

10. On the **Configure additional data warehouse datamarts** page, complete these steps:

    1.  Click **OM Data mart**. In the **Database server** box, type the computer name of the computer that will host the Operations Manager data mart database. For example, type **Computer 4**, and then press the TAB key.

    2.  Click **CM Data mart**. In the **Database server** box, type the computer name of the computer that will host the CM data mart database. For example, type **Computer 4**, and then press the TAB key.

    3.  Click **Next**.

11. On the **Configure the data warehouse management group** page, complete these steps:

    1.  In the **Management group name** box, type a unique name for the group name.

        > [!CAUTION]
        > Management group names must be unique. Do not use the same management group name even when deploying a Service Manager management server and a Service Manager data warehouse management server. Furthermore, do not use the management group name that is used for Operations Manager. All data warehouse management group names have the prefix DW\_.

    2.  Click **Browse**, enter the user or group that you want to be the Service Manager administrator, and then click **Next**.

        > [!NOTE]
        > The group Domain\\Administrators is not allowed as a management group administrator.

12. On the **Configure the reporting server for the data warehouse** page, follow these steps:

    1.  In the **Report server** box, enter the name of the computer that will host the reporting server. In this example, this will be the computer that hosts the data warehouse database, enter **Computer 4**, and then press the TAB key.

        > [!NOTE]
        > The URL that you are presented with might not be in the form of a fully qualified domain name \(FQDN\). If the URL as presented cannot be resolved in your environment, you will need to configure SQL Server Reporting URLs so that the FQDN is listed in the **Web service URL** field. For more information see the TechNet article [Configure a URL](http://go.microsoft.com/fwlink/p/?LinkId=230712) \(http:\/\/go.microsoft.com\/fwlink\/p\/?LinkId\=230712\).

    2.  Verify that **Default** is displayed in the **Report server instance** box.

    3.  Because you followed the procedure “Manual Steps to Configure the Remote SQL Server Reporting Services” in the [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209670) \(http:\/\/go.microsoft.com\/fwlink\/p\/?LinkID\=209670\), select the **I have taken the manual steps to configure the remote SQL Server Reporting Services as described in the Service Manager Deployment Guide** check box, and then click **Next**.

13. On the **Configure the account for Service Manager services** page, click **Domain account**, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a **The credentials were accepted** message, click **Next**.

    For example, enter the account information for the domain user SM\_Acct.

14. On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a **The credentials were accepted** message, click **Next**.

15. On the **Configure Analysis Service for OLAP cubes** page, in the **Database server** box, type the computer name of the server that will host the Analysis Services database, and then press the TAB key. When **Default** appears in the **SQL Server instance** box, click **Next**. For example, type **Computer 4** in the **Database server** box.

    > [!WARNING]
    > If you are installing SQL Server Analysis Services on a computer other than the computer hosting the data warehouse management server and there is a firewall in your environment, you must make sure that the proper firewall ports are opened. For more information, see the topic Port Assignments for Service Manager 2012 in the [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672).

16. On the **Configure Analysis Services credential** page, select a domain account, click **Domain account**, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a **The credentials were accepted** message, click **Next**.

    > [!NOTE]
    > The account you specify here must have administrator rights on the computer hosting SQL Server Analysis Services.

17. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. Optionally, click **Tell me more about the program**, and then click **Next**.

18. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates. Select **Initiate machine wide Automatic update** if you want Windows Update to check for updates. Click **Next**.

19. On the **Installation summary** page, click **Install**.

20. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**.
