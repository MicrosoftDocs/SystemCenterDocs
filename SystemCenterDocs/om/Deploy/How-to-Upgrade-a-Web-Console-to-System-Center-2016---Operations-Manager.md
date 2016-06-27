---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  mgoedtel
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-27
title:  How to Upgrade a Web Console to System Center 2016   Operations Manager
ms.technology:  operations-manager
ms.assetid:  0415dfa5-bf13-4f0e-9105-8cc6cd36c6e2
---



# How to Upgrade a Web Console to System Center 2016 - Operations Manager
If you have a stand-alone System Center 2012 Service Pack 1 (SP1), Operations Manager web console server, you can upgrade it to System Center 2012 R2 Operations Manager.

Before you begin the upgrade process, make sure that your server meets the minimum supported configurations. For more information, see [System Requirements: System Center 2012 R2 Operations Manager](http://go.microsoft.com/fwlink/?LinkId=309038)

> [!NOTE]
> When you upgrade the web console, any customizations that were made to the web.config file after the web console was installed will be reset.

If you made changes after you set up your web console to either enable or disable Secure Sockets Layer (SSL), the SSL settings will be reset during upgrade. To resolve the issue, you must make changes to the registry key before you upgrade the web console, as follows:

### To set the registry to enable or disable SSL on the web console

1.  Logon on to the web console with an account that has local administrator rights, and on the desktop, click **Start**, and then click **Run**.

2.  Type **regedit**, and then click **OK**. The Registry Editor starts.

    > [!CAUTION]
    > Incorrectly editing the registry can severely damage your system. Before you make changes to the registry, you should back up any valued data that is on the computer.

3.  Navigate to the **HKey_Local_Machine\Software\Microsoft\System Center Operations Manager\12\Setup\WebConsole\\** key.

4.  To enable SSL, set the following:

    HTTP_GET_ENABLED=0

    BINDING_CONFIGURATION=DefaultHttpsBinding

5.  To disable SSL, set the following:

    HTTP_GET_ENABLED=1

    BINDING_CONFIGURATION=DefaultHttpBinding

### To upgrade the web console server

1.  Log on to the computer that hosts the web console server with an Operations Manager Administrators role account for your Operations Manager management group.

2.  On the Operations Manager source media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **System Center 2012 R2 Operations Manager Upgrade** page, review the features that will be upgraded, and then click **Next**.

4.  On the **Select installation location** page, accept the default value of **C:\Program Files\Microsoft System Center 2012 R2\Operations Manager**, or type in a new location or browse to one. Then click **Next**.

5.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify Prerequisites Again** to recheck the system.

6.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  When the **Ready to Upgrade** page appears, review the upgrade summary, and then click **Upgrade**.

### To upgrade the web console server by using the Command Prompt window

1.  Log on to the computer that hosts the web console server with an Operations Manager Administrators role account for your Operations Manager management group.

2.  Open a Command Prompt window by using the **Run as Administrator** option.

3.  Change the path to where the Operations Manager Setup.exe file is located, and run the following command.

    > [!IMPORTANT]
    > Use the `/WebConsoleUseSSL` parameter only if your website has Secure Sockets Layer (SSL) activated. For a default web installation, specify **Default Web Site** for the `/WebSiteName` parameter.

    ```
    setup.exe /silent /AcceptEndUserLicenseAgreement:1 /upgrade 
    /WebsiteName: "<WebSiteName>" [/WebConsoleUseSSL]
    /WebConsoleAuthorizationMode: [Mixed|Network]
    ```


