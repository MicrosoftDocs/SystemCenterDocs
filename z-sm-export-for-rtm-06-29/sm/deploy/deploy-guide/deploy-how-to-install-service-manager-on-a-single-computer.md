---
title: How to Install Service Manager on a Single Computer
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0fc3af5-d400-4a98-adf8-f76aaf890cf0
translation.priority.ht: 
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
# How to Install Service Manager on a Single Computer
To install [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] on a single computer, you install the Service Manager management server, database, and console on the computer. Then, you install the data warehouse on a virtual machine on the same computer.  
  
 During Setup, you will be prompted to provide credentials for the following accounts:  
  
-   Management group administrator  
  
-   Service Manager account  
  
-   Workflow account  
  
 For more information about the permissions that these accounts require, see "Accounts Required During Setup" in the [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209672). Before you start, make sure that Microsoft SQL Server 2008 is installed on the computer.  
  
### To install the Service Manager management server, database, and console  
  
1.  Log on to the physical computer by using an account that has administrative credentials.  
  
2.  On the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation media, double\-click the **Setup.exe** file.  
  
3.  On the **Microsoft System Center 2012** page, click **Service Manager management server**.  
  
4.  On the **Product registration** page, type information in the boxes. In the **Product key** boxes, type the product key that you received with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], or alternatively, select **Install as an evaluation edition \(180 day trial\)**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  
  
5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server will be installed.  
  
6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.  
  
     If the prerequisite checker determines that the Microsoft Report Viewer Redistributable has not been installed, click **Install Microsoft Report Viewer Redistributable**. After the Microsoft Report Viewer Redistributable 2008 \(KB971119\) Setup Wizard completes, click **Check prerequisites again**.  
  
7.  On the **Configure the Service Manager database** page, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] checks the current computer to see if an instance of SQL Server exists. By default, if an instance is found, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] creates a new database in the existing instance. If an instance is displayed, click **Next**.  
  
    > [!IMPORTANT]  
    >  A warning message appears if you are using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\). Support for multiple languages in Service Manager is not possible when you are using the default collation. If later you decide to support multiple languages using a different collation, you have to reinstall SQL Server. See “Microsoft SQL Server 2008 with SP1” in the [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209672).  
  
8.  On the **Configure the Service Manager management group** page, complete these steps:  
  
    1.  In the **Management group name** box, type a unique name for the management group.  
  
        > [!IMPORTANT]  
        >  Management group names must be unique. Do not use the same management group name when you deploy a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse management server. Furthermore, do not use the management group name that is used for Operations Manager.  
  
    2.  Click **Browse**, enter the user account or group to which you want to give [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] administrative credentials, and then click **Next**.  
  
9. On the **Configure the account for Service Manager services** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.  
  
10. On the **Configure the Service Manager workflow account** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.  
  
11. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click **Tell me more about the program**, and then click **Next**.  
  
12. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Click **Next**.  
  
13. On the **Installation summary** page, click **Install**.  
  
14. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**. For more information about backing up the encryption key, see [Completing Deployment by Backing Up the Encryption Key](../../../sm/deploy/deploy-guide/Completing-Deployment-by-Backing-Up-the-Encryption-Key.md).  
  
### To install the data warehouse  
  
1.  Log on to the virtual machine by using an account that has administrative credentials.  
  
2.  On the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation media, double\-click the **Setup.exe** file.  
  
3.  On the **Microsoft System Center 2012** page, click **Service Manager data warehouse management server**.  
  
4.  On the **Product registration** page, type information in the boxes. In the **Product key** boxes, type the product key you received with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], or as an alternative, select **Install as an evaluation edition \(180 day trial**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  
  
5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse management server will be installed.  
  
6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.  
  
7.  On the **Configure data warehouse databases** page, in the **Database server** box, type the computer name of the physical computer that will host the data warehouse databases, and then press the TAB key. When **Default** is displayed in the **SQL Server instance** box, click **Next**.  
  
    > [!IMPORTANT]  
    >  A warning message appears if you are using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\). Support for multiple languages in Service Manager is not possible when you are using the default collation. If later you decide to support multiple languages using a different collation, you have to reinstall SQL Server. For more information, see “Microsoft SQL Server 2008 with SP1” in the [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209672).  
  
8.  On the **Configure additional data warehouse datamarts** page, Service Manager will check the current computer to see if an instance of SQL Server exists. By default, if an instance is found, Service Manager creates a new database in the existing instance. If an instance appears, click **Next**.  
  
9. On the **Configure the data warehouse management group** page, complete these steps:  
  
    1.  In the **Management group name** box, type a unique name for the group.  
  
        > [!IMPORTANT]  
        >  Management group names must be unique. Do not use the same management group name when you deploy a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse management server. Furthermore, do not use the management group name that is used for Operations Manager.  
  
    2.  Click **Browse**, enter the user account or group to which you want to give [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] administrative credentials, and then click **Next**.  
  
10. On the **Configure the reporting server for the data warehouse** page, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] will use the existing computer if SQL Server Reporting Services \(SSRS\) is present. Accept the defaults, and then click **Next**.  
  
    > [!NOTE]  
    >  The URL that you are presented with might not be in the form of a fully qualified domain name \(FQDN\). If the URL as presented cannot be resolved in your environment, configure SQL Server Reporting URLs so that the FQDN is listed in the **Web service URL** field. For more information, see [How to: Configure a URL \(Reporting Services Configuration\)](http://go.microsoft.com/fwlink/p/?LinkId=230712).  
  
11. On the **Configure the account for Service Manager services** page, select a domain account; click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.  
  
12. On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.  
  
13. On the **Configure Analysis Service for OLAP cubes** page, click **Next**.  
  
14. On the **Configure Analysis Services credential** page, select a domain account; click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.  
  
    > [!NOTE]  
    >  The account that you specify here must have administrator rights on the computer that hosts SSRS.  
  
15. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click **Tell me more about the program**, and then click **Next**.  
  
16. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] updates. Select **Initiate machine wide Automatic update** if you want Windows Update to check for updates. Click **Next**.  
  
17. On the **Installation summary** page, click **Install**.  
  
18. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**. For more information about backing up the encryption key, see [Completing Deployment by Backing Up the Encryption Key](../../../sm/deploy/deploy-guide/Completing-Deployment-by-Backing-Up-the-Encryption-Key.md).