---
title: Install Service Manager on two computers
description: To evaluate Service Manager, you can install the Service Manager management server and data warehouse management server on two computers.
ms.custom: intro-installation, UpdateFrequency2, engagement-fy24
ms.service: system-center
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 03/19/2025
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95b4f9e4-e6f3-4d04-9b11-aeba6bea22ec
---

# Install Service Manager on two computers

If you want to evaluate System Center - Service Manager and its reporting capabilities in a lab environment, we recommend that you install the Service Manager management server and data warehouse management server on two computers. The first computer hosts the Service Manager management server and the Service Manager database. The second computer hosts the data warehouse management server and the data warehouse databases. This deployment topology is shown in figure&nbsp;1.  

 **Figure 1: An installation on two physical computers**  

 ![Screenshot showing Two - computer installation for Service Manager.](./media/install-two-computers/deploy-service_manager_deployment_simple.png)  

> [!IMPORTANT]  
> Service Manager doesn't support case-sensitive instance names. Setup will display a warning if you attempt to install Service Manager on a case\-sensitive instance of Microsoft SQL&nbsp;Server.  


::: moniker range=">=sc-sm-2019"

[!INCLUDE [validation-service-manager.md](../includes/validation-service-manager.md)]

::: moniker-end

## Install the Service Manager management server, Service Manager database, and console

As the first step in the two-computer installation process, install the Service Manager management server, the Service Manager database, and the Service Manager console on one of the two computers.  

 During setup, you'll be prompted to provide credentials for the following accounts:  

- Management group administrator  
- Service Manager services account  
- Service Manager workflow account  

For more information about the permissions that these accounts require, see [Account required during Setup](prepare-deploy.md).  

### Install the Service Manager management server, Service Manager database, and console

1. Sign in to the computer that will host the Service Manager management server by using an account that has administrative rights.  

2. On the Service Manager installation media, double-click the **Setup.exe** file.  

3. On the **Service Manager Setup Wizard** page, select **Service Manager management server**.  

4. On the **Product registration** page, enter information in the boxes. In the **Product key** boxes, enter the product key that you received with Service Manager, or as an alternative, select **Install as an evaluation edition (180 day trial**. Read the Microsoft Software License Terms, and, if applicable, select **I have read, understood, and agree with the terms of the license agreement**, and select **Next**.  

5. On the **Installation location** page, verify that sufficient free disk space is available, and select **Next**. If necessary, select **Browse** to change the location in which the Service Manager management server will be installed.  

6. On the **System check results** page, ensure that the prerequisite check passed or at least passed with warnings, and select **Next**.  

     If the prerequisite checker determines that the Microsoft Report Viewer Redistributable hasn't been installed, select **Install Microsoft Report Viewer Redistributable**. After the Microsoft Report Viewer Redistributable 2008 (KB971119) Setup Wizard completes, select **Check prerequisites again**.  

7. On the **Configure the Service Manager database** page, Service Manager will check the current computer to see if an instance of SQL Server exists. By default, if an instance is found, Service Manager creates a new database in the existing instance. If an instance appears, select **Next**.  

    > [!IMPORTANT]  
    > A warning message appears if you're using the default collation (SQL_Latin1_General_CP1_CI_AS). Support for multiple languages in Service Manager isn't possible when you're using the default collation. If later you decide to support multiple languages using a different collation, you have to reinstall SQL Server. See the [Planning Guide for System Center - Service Manager](plan-sm.md).  

8. On the **Configure the Service Manager management group** page, complete these steps:  

    1. In the **Management group name** box, enter a unique name for the management group.  

        > [!IMPORTANT]  
        > Management group names must be unique. Don't use the same management group name when you deploy a Service Manager management server and a Service Manager data warehouse management server. Furthermore, don't use the management group name that is used for Operations Manager.  

    2. Select **Browse**, enter the user account or group to which you want to give Service Manager administrative rights, and select **Next**.  

9. On the **Configure the account for Service Manager services** page, select **Domain account**; specify the user name, password, and domain for the account; and select **Test Credentials**. After you receive a **The credentials were accepted** message, select **Next**.  

10. On the **Configure the Service Manager workflow account** page, select **Domain account**; specify the user name, password, and domain for the account; and select **Test Credentials**. After you receive a **The credentials were accepted** message, select **Next**.  

11. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, select **Tell me more about the program**, and select **Next**.  

12. On the **Use Microsoft Update to help keep your computer secure and up-to-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Select **Next**.  

13. On the **Installation summary** page, select **Install**.  

14. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and select **Close**. For more information about backing up the encryption key, see [Back up the encryption Key](encryption-key.md).

## Install the Service Manager data warehouse (two-computer scenario)

As the second step in the two\-computer installation process for System Center - Service Manager, deploy the data warehouse management server and the data warehouse databases on the second computer. During Setup, you'll be prompted to provide credentials for the following accounts:  

- Management group administrator  
- Service Manager services account  
- Reporting account  

For more information about the permissions that these accounts require, see [Accounts Required During Setup](prepare-deploy.md). Before you start, ensure that Microsoft SQL&nbsp;Server Reporting Services \(SSRS\) is installed in the default instance of Microsoft SQL&nbsp;Server.  

### Install a data warehouse management server and data warehouse databases  

1. Sign in to the computer by using an account that has administrative rights.  

2. On the Service Manager installation media, double\-click the **Setup.exe** file.  

3. On the **Service Manager Setup Wizard** page, select **Service Manager data warehouse management server**.  

4. On the **Product registration** page, enter information in the boxes. In the **Product key** boxes, enter the product key that you received with Service Manager, or as an alternative, select **Install as an evaluation edition \(180 day trial**. Read the Microsoft Software License Terms, and, if applicable, select **I have read, understood, and agree with the terms of the license agreement**, and select **Next**.  

5. On the **Installation location** page, verify that sufficient free disk space is available, and select **Next**. If necessary, select **Browse** to change the location in which the Service Manager data warehouse management server will be installed.  

6. On the **System check results** page, ensure that prerequisites passed or at least passed with warnings, and select **Next**.  

7. On the **Configure data warehouse databases** page, Service Manager checks the computer you're using to see if it can host the data warehouse databases. For this configuration, confirm that the database server is the computer on which you're installing the data warehouse management server, and select **Next**.  

   > [!IMPORTANT]  
   > A warning message appears if you are using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\). Support for multiple languages in Service Manager isn't possible when you're using the default collation. If later you decide to support multiple languages using a different collation, you have to re\-install SQL Server. See [Planning Guide for System Center - Service Manager](plan-sm.md).  

8. On the **Configure additional data warehouse datamarts** page, Service Manager checks the current computer to see if an instance of SQL Server exists. By default, if an instance is found, Service Manager creates a new database in the existing instance. If an instance appears, select **Next**.  

9. On the **Configure the data warehouse management group** page, complete these steps:  

   1. In the **Management group name** box, enter a unique name for the group.  

       > [!IMPORTANT]  
       > Management group names must be unique. Don't use the same management group name when you deploy a Service Manager management server and a Service Manager data warehouse management server. Furthermore, don't use the management group name that is used for Operations Manager.  

   2. Select **Browse**, enter the user account or group to which you want to give Service Manager administrative rights, and select **Next**.  

10. On the **Configure the reporting server for the data warehouse** page, Service Manager will use the existing computer if SQL Server Reporting Services is present. Accept the defaults, and select **Next**.  

    > [!NOTE]  
    > - Manually configure the SQL Server Reporting Services even when SSRS and data warehouse management server MS are on the same machine. For detailed information, see [Manual steps to configure remote SQL Server Reporting Services](./config-remote-ssrs.md).
    > - The URL that you are presented with might not be in the form of a fully qualified domain name \(FQDN\). If the URL as presented can't be resolved in your environment, configure SQL Server Reporting URLs so that the FQDN is listed in the **Web service URL** field. For more information, see [How to: Configure a URL \(Reporting Services Configuration\)](/sql/reporting-services/install-windows/configure-a-url-ssrs-configuration-manager).  

11. On the **Configure the account for Service Manager services** page, select **Domain account**; specify the user name, password, and domain for the account; and select **Test Credentials**. After you receive a **The credentials were accepted** message, select **Next**.  

12. On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and select **Test Credentials**. After you receive a **The credentials were accepted** message, select **Next**.  

13. On the **Configure Analysis Service for OLAP cubes** page, select **Next**.  

14. On the **Configure Analysis Services credential** page, select a domain account; select **Domain account** specify the user name, password, and domain for the account; and select **Test Credentials**. After you receive a **The credentials were accepted** message, select **Next**.  

    > [!NOTE]  
    > The account that you specify here must have administrator rights on the computer hosting SSRS.  

15. On the **Diagnostic and usage data** page, indicate your preference for sharing your Service Manager diagnostic and usage data with Microsoft. As an option, select **Privacy statement for System Center Service Manager**, and select **Next**.  

16. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Select **Next**.  

17. On the **Installation summary** page, select **Install**.  

18. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and select **Close**. For more information about backing up the encryption key, see [Completing Deployment by Backing Up the Encryption Key](encryption-key.md).

After the installation, do the following:

19. Disable all the Data Warehouse jobs. To do this, open the Service Manager shell, and then run the following commands:

    ```powershell
    $DW ='DWMS Servername'

    Get-scdwjob -Computername $DW | %{disable-scdwjobschedule -Computername $DW -jobname $_.Name}
    ```

20. Make the required changes in the following PowerShell script based on the data source views in your environment, and then run the script by using elevated privileges:

    ```powershell   
    $SSAS_ServerName = "ssas servername" # - to be replaced with Analysis Service instance Name

    [System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices")
    $Server = New-Object Microsoft.AnalysisServices.Server
    $Server.Connect($SSAS_ServerName)
    $Databases = $Server.Databases
    $DWASDB = $Databases["DWASDataBase"]

    #update DWDatamart dsv. Comment the below 3 commands if DWdatamart dsv is not present 

    $DWASDB.DataSourceViews["DwDataMart"].Schema.Tables["OperatingsystemDim"].Columns["PhysicalMemory"].DataType  =  [decimal] 

    $DWASDB.DataSourceViews["DwDataMart"].Schema.Tables["LogicalDiskDim"].Columns["Size"].DataType  =  [decimal] 

    $DWASDB.DataSourceViews["DwDataMart"].Update([Microsoft.AnalysisServices.UpdateOptions]::ExpandFull) 

    #update CMDatamart dsv.Comment the below 2 commands if cmdatamart dsv is not present 

    $DWASDB.DataSourceViews["CMDataMart"].Schema.Tables["OperatingsystemDim"].Columns["PhysicalMemory"].DataType  =  [decimal] 

    $DWASDB.DataSourceViews["CMDataMart"].Update([Microsoft.AnalysisServices.UpdateOptions]::ExpandFull) 

    #update OperatingsystemDim
    $DWASDB.Dimensions["OperatingsystemDim"].Attributes["PhysicalMemory"].KeyColumns[0].DataType =  [System.Data.OleDb.OleDbType]::Double 

    $DWASDB.Dimensions["OperatingsystemDim"].Update([Microsoft.AnalysisServices.UpdateOptions]::ExpandFull + [Microsoft.AnalysisServices.UpdateOptions]::AlterDependents)
    #update LogicalDiskDim 

    $DWASDB.Dimensions["LogicalDiskDim"].Attributes["Size"].KeyColumns[0].DataType =  [System.Data.OleDb.OleDbType]::Double 

    $DWASDB.Dimensions["LogicalDiskDim"].Update([Microsoft.AnalysisServices.UpdateOptions]::ExpandFull + [Microsoft.AnalysisServices.UpdateOptions]::AlterDependents) 

    ```

21. Enable the job schedules by running the following commands:

    ```powershell    
    $DW ='DWMS Servername'

    Get-scdwjob -Computername $DW | %{enable-scdwjobschedule -Computername $DW -jobname $_.Name}
    ```

## Next steps

- To install Service Manager on four computers, review [Install Service Manager on four computers](install-four-computers.md). This scenario is useful in a production environment, and it maximizes performance and scalability.
