---
title: Install Service Manager on a single computer (minimum configuration)
description: This article helps you to evaluate Service Manager when you want to install it on one computer.
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
ms.assetid: 08c888e1-57cb-4f94-8b9e-041a54204c09
---

# Install Service Manager on a single computer (minimum configuration)

>Applies To: System Center 2016 - Service Manager

If you want to evaluate System Center - Service Manager and you have a minimal amount of hardware available, install Service Manager on one computer. A sample single\-computer configuration is shown in figure&nbsp;1. This configuration will not support a production environment, and no scalability or performance estimates are provided. Because you cannot install both the Service Manager management server and the data warehouse management server on the same computer, use Hyper\-V to create a virtual computer to host the data warehouse management server. For more information about the hardware requirements for Hyper\-V, see [Hyper\-V Server&nbsp;2016 system requirements](https://technet.microsoft.com/en-us/hyper-v-server-docs/).  

 To install Service Manager on a single computer, start with a physical computer that is running Windows&nbsp;Server&nbsp;2016 and Hyper\-V, and make sure that the CPU on the physical computer is compatible with Hyper\-V. Of the 8&nbsp;gigabytes \(GB\) of RAM on the host computer, 3&nbsp;GB is used for the virtual computer that hosts the data warehouse management server. Make sure that at least 200&nbsp;GB of free space is available on the hard disk drive.  

 **Figure 1: Single\-computer installation in which you use a physical computer that is running Windows&nbsp;Server&nbsp;2016 and Hyper\-V**  

 ![Minimum Configuration for Service Manager](../media/deploy-minimumconfiguration.png)  

 If your organization's best practice guidelines do not allow you to install applications on a Hyper\-V host, you can create a second virtual computer to host the Service Manager management server, the Service Manager database, and the data warehouse databases. Use the following procedures to install Service Manager on a single computer.  

## Install Service Manager

To install System Center - Service Manager on a single computer, you install the Service Manager management server, database, and console on the computer. Then, you install the data warehouse on a virtual machine on the same computer.  

 During Setup, you will be prompted to provide credentials for the following accounts:  

-   Management group administrator  

-   Service Manager account  

-   Workflow account  

 For more information about the permissions that these accounts require, see "Accounts Required During Setup" in the [Planning Guide for System Center - Service Manager](../../scsm/plan-sm.md). Before you start, make sure that Microsoft SQL&nbsp;Server&nbsp;2016 is installed on the computer.  

### To install the Service Manager management server, database, and console  

1.  Log on to the physical computer by using an account that has administrative credentials.  

2.  On the Service Manager installation media, double\-click the **Setup.exe** file.  

3.  On the **Microsoft System Center 2016** page, click **Service Manager management server**.  

4.  On the **Product registration** page, type information in the boxes. In the **Product key** boxes, type the product key that you received with Service Manager, or alternatively, select **Install as an evaluation edition \(180 day trial\)**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  

5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which the Service Manager management server will be installed.  

6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.  

     If the prerequisite checker determines that the Microsoft Report Viewer Redistributable has not been installed, click **Install Microsoft Report Viewer Redistributable**. After the Microsoft Report Viewer Redistributable 2008 \(KB971119\) Setup Wizard completes, click **Check prerequisites again**.  

7.  On the **Configure the Service Manager database** page, Service Manager checks the current computer to see if an instance of SQL&nbsp;Server exists. By default, if an instance is found, Service Manager creates a new database in the existing instance. If an instance is displayed, click **Next**.  

    > [!IMPORTANT]  
    >  A warning message appears if you are using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\). Support for multiple languages in Service Manager is not possible when you are using the default collation. If later you decide to support multiple languages using a different collation, you have to reinstall SQL&nbsp;Server. See [Planning Guide for System Center - Service Manager](../../scsm/plan-sm.md).  

8.  On the **Configure the Service Manager management group** page, complete these steps:  

    1.  In the **Management group name** box, type a unique name for the management group.  

        > [!IMPORTANT]  
        >  Management group names must be unique. Do not use the same management group name when you deploy a Service Manager management server and a Service Manager data warehouse management server. Furthermore, do not use the management group name that is used for Operations Manager.  

    2.  Click **Browse**, enter the user account or group to which you want to give Service Manager administrative credentials, and then click **Next**.  

9. On the **Configure the account for Service Manager services** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a "The credentials were accepted" message, click **Next**.  

10. On the **Configure the Service Manager workflow account** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a "The credentials were accepted" message, click **Next**.  

11. On the **Diagnostic and usage data** page, indicate your preference for sharing your Service Manager diagnostic and usage data with Microsoft. As an option, click **Privacy statement for System Center Service Manager**, and then click **Next**.  

12. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Click **Next**.  

13. On the **Installation summary** page, click **Install**.  

14. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**. For more information about backing up the encryption key, see [Completing Deployment by Backing Up the Encryption Key](deploy-completing-deployment-by-backing-up-the-encryption-key.md).  

### To install the data warehouse  

1.  Log on to the virtual machine by using an account that has administrative credentials.  

2.  On the Service Manager installation media, double\-click the **Setup.exe** file.  

3.  On the **Microsoft System Center 2016** page, click **Service Manager data warehouse management server**.  

4.  On the **Product registration** page, type information in the boxes. In the **Product key** boxes, type the product key you received with Service Manager, or as an alternative, select **Install as an evaluation edition \(180 day trial**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  

5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which the Service Manager data warehouse management server will be installed.  

6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.  

7.  On the **Configure data warehouse databases** page, in the **Database server** box, type the computer name of the physical computer that will host the data warehouse databases, the SQL server port, and Database name for all three data warehouse databases, then click **Next**.  

    > [!IMPORTANT]  
    >  A warning message appears if you are using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\). Support for multiple languages in Service Manager is not possible when you are using the default collation. If later you decide to support multiple languages using a different collation, you have to reinstall SQL Server. For more information, see [Planning Guide for System Center - Service Manager](../../scsm/plan-sm.md).  

8.  On the **Configure additional data warehouse datamarts** page, Service Manager will check the current computer to see if an instance of SQL&nbsp;Server exists. By default, if an instance is found, Service Manager creates a new database in the existing instance. If an instance appears, click **Next**.  

9. On the **Configure the data warehouse management group** page, complete these steps:  

    1.  In the **Management group name** box, type a unique name for the group.  

        > [!IMPORTANT]  
        >  Management group names must be unique. Do not use the same management group name when you deploy a Service Manager management server and a Service Manager data warehouse management server. Furthermore, do not use the management group name that is used for Operations Manager.  

    2.  Click **Browse**, enter the user account or group to which you want to give Service Manager administrative credentials, and then click **Next**.  

10. On the **Configure the reporting server for the data warehouse** page, Service Manager will use the existing computer if SQL Server Reporting Services \(SSRS\) is present. Accept the defaults, and then click **Next**.  

    > [!NOTE]  
    >  The URL that you are presented with might not be in the form of a fully qualified domain name \(FQDN\). If the URL as presented cannot be resolved in your environment, configure SQL Server Reporting URLs so that the FQDN is listed in the **Web service URL** field. For more information, see [How to: Configure a URL \(Reporting Services Configuration\)](http://go.microsoft.com/fwlink/p/?LinkId=230712).  

11. On the **Configure the account for Service Manager services** page, select a domain account; click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a "The credentials were accepted" message, click **Next**.  

12. On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a "The credentials were accepted" message, click **Next**.  

13. On the **Configure Analysis Service for OLAP cubes** page, click **Next**.  

14. On the **Configure Analysis Services credential** page, select a domain account; click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. After you receive a "The credentials were accepted" message, click **Next**.  

    > [!NOTE]  
    >  The account that you specify here must have administrator rights on the computer that hosts SSRS.  

15. On the **Diagnostic and usage data** page, indicate your preference for sharing your Service Manager diagnostic and usage data with Microsoft. As an option, click **Privacy statement for System Center Service Manager**, and then click **Next**.  

16. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates. Select **Initiate machine wide Automatic update** if you want Windows Update to check for updates. Click **Next**.  

17. On the **Installation summary** page, click **Install**.  

18. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**. For more information about backing up the encryption key, see [Completing Deployment by Backing Up the Encryption Key](deploy-completing-deployment-by-backing-up-the-encryption-key.md).


## Validate the single-computer installation

You can use the following procedures to validate the single\-computer installation of System Center - Service Manager.  

### To validate the Service Manager management server installation  

1.  On the physical computer that hosts the Service Manager management server, verify that the Program Files\\Microsoft System Center 2016\\Service Manager\\ folder exists.  

2.  Run **services.msc**, and then verify that the following services are installed, that they have a status of **Started**, and that the startup type is **Automatic**:  

    -   **System Center Data Access Service**  
    -   **Microsoft Monitoring Agent**  
    -   **System Center Management Configuration**  

### To validate the Service Manager console installation  

1.  On the physical computer, click **Start**, click **All Programs**, click **Microsoft System Center**, and then click **Service Manager Console**.  

2.  The first time that you run the Service Manager console, the **Connect to Service Manager Server** dialog box appears. In the **Server name** box, enter the computer name of the server that hosts the Service Manager management server.  

3.  The Service Manager console successfully connects to the Service Manager management server and starts.  

### To validate the data warehouse management server installation  

-   On the virtual machine, run **services.msc**, and verify that the following services are installed:  

    -   **System Center Data Access Service**  
    -   **Microsoft Monitoring Agent**  
    -   **System Center Management Configuration**  

### To validate the Service Manager database  

1.  On the physical computer, click **Start**, click **All Programs**, click **Microsoft SQL Server&nbsp;2016**, and then click **SQL Server Management Studio**.  

2.  In the **Connect to Server** dialog box, follow these steps:  

    1.  In the **Server Type** list, select **Database Engine**.  

    2.  In the **Server Name** list, select the name of the computer that hosts the Service Manager database.  

    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  

3.  In the **Object Explorer** pane, expand **Databases**.  

4.  Verify that the **ServiceManager** database is listed.  

5.  Exit Microsoft SQL Server Management Studio.  

### To validate the data warehouse installation  

1.  On the physical computer that hosts the data warehouse databases, click **Start**, click **All Programs**, click **Microsoft SQL&nbsp;Server&nbsp;2016**, and then click **SQL&nbsp;Server Management Studio**.  

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

# Next steps

- Review [Install Service Manager on two computers](deploy-installing-service-manager-on-two-computers.md) to install Service Manager on two computers. This scenario is useful for testing Service Manager in a lab environment.
