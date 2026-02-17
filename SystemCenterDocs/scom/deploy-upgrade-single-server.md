---
title: Upgrade a single-server Management Group
description: This article describes how to upgrade a single-server management group to the newest release of Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency.5, engagement-fy23, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
ms.assetid: 2f41a8e5-3ec1-4279-8c06-5e59ff27ef3d
---

# Upgrade a single-server management group

When you upgrade a single-server management group, all the features that are installed on the server are upgraded. Before you begin the upgrade process, ensure that your server meets the minimum supported configurations. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

Follow these steps to upgrade a single-server management group:

1. Sign in to the server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group, a member of the SQL Server sysadmin fixed server role, and a local administrator on the computer.

2. On the Operations Manager media, run **Setup.exe**, and select **Install**.

   > [!NOTE]
   > The **Getting Started** page displays information about what will be upgraded. Select **Next** to proceed with the upgrade.

3. On the **Getting Started, Please read the license terms page**, read the Microsoft Software License Terms, select **I have read, understood, and agree with the license terms**, and then select **Next**.

4. On the **Select installation location** page, accept the default value, enter a new location or browse to one. Then select **Next**.

::: moniker range="<=sc-om-2022"
   > [!NOTE]
   > For System Center 2016 - Operations Manager, the default path is C:\Program Files\Microsoft System Center 2016\Operations Manager. For all later releases (2019 and 2022), the default path is C:\Program Files\Microsoft System Center\Operations Manager.
::: moniker-end

::: moniker range="sc-om-2025"
   > [!NOTE]
   > For System Center 2025 - Operations Manager, the default path is C:\Program Files\Microsoft System Center\Operations Manager.
::: moniker-end

5. On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and select **Verify prerequisites again** to recheck the system.

   > [!NOTE]
   > Microsoft SQL Server Full Text Search must be enabled on the SQL Server hosting the OperationsManager and OperationsManagerDW databases.

6. If the Prerequisites checker doesn't return any other errors or warnings that must be addressed, select **Next**.

7. On the **Configuration, Configure Operations Manager accounts** page, enter the domain account or Local System credentials for the System Center Configuration and Data Access service accounts, and select **Next**.

   > [!IMPORTANT]
   > If you receive a message about using the wrong version of the SQL Server, or experience a problem with the SQL Server Windows Management Instrumentation (WMI) provider, you can resolve this. Open a Command Prompt window by using the **Run as administrator** option. Then run the following command; replace the *\<path>* placeholder with the location of Microsoft SQL Server:
   >
   > **mofcomp.exe \<path>\Microsoft SQL Server\100\Shared\sqlmgmproviderxpsp2up.mof**

8. When the **Ready to Upgrade** page appears, review the upgrade summary, and select **Upgrade**.

## Upgrade a single-server management group from the command prompt

Follow these steps to upgrade a single-server management group from the command prompt:

1. Sign in to the server with an account that is a member of the Operations Manager Administrators role for your Operations Manager management group, a member of the SQL Server sysadmin fixed server role, and a local administrator on the computer.

2. Open an elevated command prompt by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager Setup.exe file is located.

    > [!IMPORTANT]
    > Use the `/WebConsoleUseSSL` parameter only if your website has Secure Sockets Layer (SSL) activated. For a default web installation, specify **Default Web Site** for the `/WebSiteName` parameter.

    > [!IMPORTANT]
    > The following commands assume that you specified the Local System for the Data Access service `(/UseLocalSystemDASAccount)`. To specify a domain\user name for these accounts, you must provide the following parameters instead:`/DASAccountUser: <domain\username> /DASAccountPassword: <password>`

4. Run the following command.

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

    After you've upgraded your single-server management group, you can upgrade the agents.

## Verify the upgrade

### Confirm the health of the management server

Follow these steps to confirm the health of the management server:

1. In the Operations console, in the navigation pane, select **Administration**.

2. Under **Device Management**, select **Management Servers**. In the results pane, you should see the management server that you installed with a green check mark in the Health State column.

## Next steps

To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).
