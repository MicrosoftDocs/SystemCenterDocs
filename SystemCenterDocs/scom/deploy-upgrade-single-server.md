---
title: How to Upgrade a Single Server Management Group to System Center 2016 - Operations Manager
description: This article describes how to upgrade a single server management group to Operations Manager 2016.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 01/26/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 2f41a8e5-3ec1-4279-8c06-5e59ff27ef3d
---

# How to upgrade a single server management group to System Center 2016 - Operations Manager

>Applies To: System Center 2016 - Operations Manager

When you upgrade a single server management group to System Center 2016 - Operations Manager, all features that are installed on the server are upgraded. Before you begin the upgrade process, make sure that your server meets the minimum supported configurations. For more information, see [System Requirements for System Center 2016 - Operations Manager](/system-center/orchestrator/system-requirements).

### To upgrade a single server management group

1.  Log on to the server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group, a member of the SQL Server sysadmin fixed server role, and a local administrator on the computer.

2.  On the Operations Manager media, run **Setup.exe**, and then click **Install**.

    > [!NOTE]
    > The **Getting Started** page displays information about what will be upgraded. Click **Next** to proceed with the upgrade.

3.  On the **Getting Started, Please read the license terms page**, read the Microsoft Software License Terms, click **I have read, understood, and agree with the license terms**, and then click **Next**.

4.  On the **Select installation location** page, accept the default value of **C:\Program Files\Microsoft System Center 2016\Operations Manager**, or type in a new location or browse to one. Then click **Next**.

5.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify prerequisites again** to recheck the system.

    > [!NOTE]
    > Microsoft SQL Server Full Text Search must be enabled on the SQL Server hosting the OperationsManager and OperationsManagerDW databases.

6.  If the Prerequisites checker does not return any other errors or warnings that have to be addressed, click **Next**.

7.  On the **Configuration, Configure Operations Manager accounts** page, enter the domain account or Local System credentials for the System Center Data Access service account, and then click **Next**.

    > [!IMPORTANT]
    > If you receive a message about using the wrong version of SQL Server, or experience      a problem with the SQL Server Windows Management Instrumentation (WMI) provider,        you can resolve this. Open a Command Prompt window by using the **Run as administrator** option. Then run the following command, replace the *\<path>* placeholder with the location of Microsoft SQL Server:
        >
        > **mofcomp.exe \<path>\Microsoft SQL Server\100\Shared\sqlmgmproviderxpsp2up.mof**

8.  When the **Ready to Upgrade** page appears, review the upgrade summary, and then click **Upgrade**.

### To upgrade a single server management group from the Command Prompt 

1.  Log on to the server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group, a member of the SQL Server sysadmin fixed server role, and a local administrator on the computer.

2.  Open an elevated Command Prompt by using the **Run as Administrator** option.

3.  Change the path to where the Operations Manager Setup.exe file is located.

    > [!IMPORTANT]
    > Use the `/WebConsoleUseSSL` parameter only if your website has Secure Sockets Layer (SSL) activated. For a default web installation, specify **Default Web Site** for the `/WebSiteName` parameter.

    > [!IMPORTANT]
    > The following commands assume that you specified the Local System for the Data Access service `(/UseLocalSystemDASAccount`). To specify a domain\user name for these accounts, you must provide the following parameters instead:`/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

4.  Run the following command.

    ```
    setup.exe /silent /install
    /components:OMServer,OMConsole,OMWebConsole,OMReporting
    /ManagementGroupName: "<ManagementGroupName>"
    /SqlServerInstance: <server\instance>
    /SqlServerInstance: <SQL server instance port number>
    /DatabaseName: <OperationalDatabaseName>
    /DWSqlServerInstance: <server\instance>
    /DWSqlInstancePort: <SQL server instance port number>
    /DWDatabaseName: <DWDatabaseName>
    /UseLocalSystemActionAccount /UseLocalSystemDASAccount
    /DatareaderUser: <domain\username>
    /DatareaderPassword: <password>
    /DataWriterUser: <domain\username>
    /DataWriterPassword: <password>
    /AcceptEndUserLicenseAgreement: [0|1]
    /WebSiteName: "<WebSiteName>" [/WebConsoleUseSSL]
    /WebConsoleAuthorizationMode: [Mixed|Network]
    /SRSInstance: <server\instance>
    /SendODRReports: [0|1]
    /EnableErrorReporting: [Never|Queued|Always]
    /SendCEIPReports: [0|1]
    /UseMicrosoftUpdate: [0|1]
    ```

    > [!TIP]
    > If you want to upgrade a specific component, you can add `/components: <component name1> [<, component name2>][ <, component name3>]`

    After you have upgraded your single-server management group, you can upgrade the agents.

## Verifying the upgrade

### To confirm the health of the management server


1. In the Operations console, select the Administration workspace.

2. Under Device Management select Management Servers. In the results pane, you should see the management server that you just installed with a green check mark in the Health State column.

## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center 2016 - Operations Manager](deploy-upgrade-post-tasks.md).
