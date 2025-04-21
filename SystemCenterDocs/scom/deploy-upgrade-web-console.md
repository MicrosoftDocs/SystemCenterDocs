---
ms.assetid: ac2e1b48-2f24-44c1-8d06-9405b2db9c26
title: Upgrade a Web Console
description: This article describes how to upgrade a Web console to the latest release of System Center Operations Manager.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/21/2025
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
monikerRange: 'sc-om-2016'
ms.subservice: operations-manager
ms.topic: how-to
---

# Upgrade a Web console

This article describes how to upgrade a Web console to the latest release of System Center Operations Manager. Before you begin the upgrade process, ensure that your server meets the minimum supported configurations for System Center Operations Manager. For more information, see [System Requirements for System Center Operations Manager](./system-requirements.md).

> [!NOTE]
> When you upgrade the web console, any customizations that were made to the web.config file after the web console was installed will be reset. Make a backup copy before proceeding.  

If you made changes after you set up your web console to either enable or disable Secure Sockets Layer (SSL), the SSL settings will be reset during upgrade. To resolve the issue, you must make changes to the registry key before you upgrade the web console, as follows:

### Set the registry to enable or disable SSL on the Web console server

To set the registry to enable or disable SSL, follow the steps:

1. Sign in to the web console with an account that has local administrator rights, and on the desktop, select **Start**, and then select **Run**.

2. Enter **regedit**, and select **OK**. The Registry Editor starts.

    > [!CAUTION]
    > Incorrectly editing the registry can severely damage your system. Before you make changes to the registry, you should back up any valued data that is on the computer.

3. Navigate to the **HKey_Local_Machine\Software\Microsoft\System Center Operations Manager\12\Setup\WebConsole\\** key.

4. To enable SSL, set the following:

    HTTP_GET_ENABLED=0

    BINDING_CONFIGURATION=DefaultHttpsBinding

5. To disable SSL, set the following:

    HTTP_GET_ENABLED=1

    BINDING_CONFIGURATION=DefaultHttpBinding

### Upgrade the Web console server

To upgrade the Web console server, follow the steps:

1. Sign in to the computer that hosts the web console server with an Operations Manager Administrators role account for your Operations Manager management group.

2. On the Operations Manager source media, run **Setup.exe**, and select **Install**.

    > [!NOTE]
    > The **Getting Started** page displays information about what will be upgraded. Select **Next** to proceed with the upgrade.

3. On the **Getting Started, Please read the license terms page**, read the Microsoft Software License Terms, select **I have read, understood, and agree with the license terms**, and select **Next**.

4. On the **Select installation location** page, accept the default value, enter a new location, or browse to one. Then select **Next**.

    > [!NOTE]
    > For System Center 2016 - Operations Manager, the default path is C:\Program Files\Microsoft System Center 2016\Operations Manager. For all the later releases (2019 and 2022), the default path is C:\Program Files\Microsoft System Center\Operations Manager.
    >

5. On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and select **Verify Prerequisites Again** to recheck the system.

6. If the Prerequisites checker doesn't return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Select **Next**.

7. When the **Ready to Upgrade** page appears, review the upgrade summary, and select **Upgrade**.

### Upgrade the Web console server from the Command Prompt

To upgrade the Web console server from the Command Prompt, follow the steps:

1. Sign in to the computer that hosts the web console server with an Operations Manager Administrators role account for your Operations Manager management group.

2. Open a Command Prompt by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager Setup.exe file is located, and run the following command.

    > [!IMPORTANT]
    > Use the `/WebConsoleUseSSL` parameter only if your website has Secure Sockets Layer (SSL) activated. For a default web installation, specify **Default Web Site** for the `/WebSiteName` parameter.

    ```
    setup.exe /silent /AcceptEndUserLicenseAgreement:1 /upgrade
    /WebsiteName: "<WebSiteName>" [/WebConsoleUseSSL]
    /WebConsoleAuthorizationMode: [Mixed|Network]
    ```

## Next steps

- To understand the post-upgrade tasks you should perform to complete the upgrade to your management group, see [Post-Upgrade Tasks When Upgrading to System Center Operations Manager](deploy-upgrade-post-tasks.md).

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
