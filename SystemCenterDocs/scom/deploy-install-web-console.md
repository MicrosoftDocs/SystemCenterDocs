---
ms.assetid: 8e15d2ef-be27-483d-ad4a-09df62ed6618
title: How to Install the Operations Manager Web console
description: This article describes how to install the Web console for System Center Operations Manager.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 04/08/2020
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# How to install the Operations Manager Web console

You can install the web console when you install System Center - Operations Manager, or you can install it separately. You can install a stand-alone web console or install it on an existing management server that meets the prerequisites.

::: moniker range="sc-om-2019"

>[!NOTE]
> Operations Manager 2019 UR1 supports a single installer for all supported languages, instead of language specific installers. The installer automatically selects the language, based on the computer's language settings, where you are installing it.

::: moniker-end

 For information about the prerequisites, see [System Requirements for System Center Operations Manager](plan-system-requirements.md).

> [!IMPORTANT]
> If you install a stand-alone web console on a server, you will not be able to add the management server feature to this server. If you want to install the management server and web console on the same server, you must either install both features simultaneously, or install the management server before you install the web console.

When you install the web console, the following three components are installed:

-   Operations Manager web console

-   Application Diagnostics console

-   Application Advisor console

> [!NOTE]
> If Application Diagnostics console is not installed, when viewing APM alerts, you will not be able to use the link embedded in the alert description to launch the APM event details. To use this feature, install the web console within the management group.

If you plan to use network load balancing with Application Diagnostics console and Application Advisor console, be sure to use sticky sessions. This ensures that the same instance of the console is used for the entire session. For more information about network load balancing, see [Network Load Balancing](https://go.microsoft.com/fwlink/p/?linkID=158320). For more information about sessions, see [Support for Sessions](https://go.microsoft.com/fwlink/p/?linkID=251693).

> [!NOTE]
> A Network Load Balancer is not supported for the Operations Manager web console server.

> [!IMPORTANT]
> The web console operates with sensitive data, such as clear text user credentials, server names, IP addresses, and so on. If these are exposed on the network, they can represent a significant security risk. If Internet Information Services (IIS) does not have Secure Sockets Layer (SSL) configured, you are advised to configure it manually. For more information about security see [Data Encryption for Web console and Reporting server Connections](plan-data-encryption-server-roles.md)

If the web console does not have sufficient access to the operational database or the data warehouse database, you will receive a warning during the web console configuration step. You can proceed with Setup, but the web console will not be configured correctly for .NET Application monitoring. To resolve this issue, you can have your database administrator run the following SQL Server statement on both the operational database and data warehouse database:

```
EXEC [apm].GrantRWPermissionsToComputer N'[LOGIN]'
```

The local and remote parameters are as follows:

-   For local installation, the LOGIN is: IIS APPPOOL\OperationsManagerAppMonitoring

-   For remote installation, the LOGIN is: Domain\MachineName$

> [!NOTE]
> If you run **Repair** on the web console after installation, the settings that were selected during installation will be restored. Any changes that you manually make to the web console configuration after the installation will be reset.

### To install a stand-alone Web console

::: moniker range="sc-om-2016"

>[!NOTE]
>If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 Web console role will fail because the setup media does not include the updates to support TLS 1.2.  The only way you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system.  This limitation does not apply to Operations Manager version 1801.

::: moniker-end

1.  Log on to the computer that will host the web console with an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **Select features to install** page, select **Web console**. To read more about what each feature provides and its requirements, click **Expand all**, or expand the buttons next to each feature, and then click **Next**.

4.  On the **Getting Started**, **Select installation location** page, accept the default location, or type in a new location or browse to one, and then click **Next**.

    > [!NOTE]
    > For System Center 2016 - Operations Manager, the default path is C:\Program Files\Microsoft System Center 2016\Operations Manager.  For all later releases (1801, 1807 and 2019), the default path is C:\Program Files\Microsoft System Center\Operations Manager.
    >

5.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify Prerequisites Again** to recheck the system.

    > [!NOTE]
    > Installation of the web console requires that ISAPI and CGI Restrictions in IIS be enabled for ASP.NET 4. To enable this, select the web server in IIS Manager, and then double-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.0.30319**, and then click **Allow**.

6.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood and agree with the license terms**, and then click **Next**.

8.  On the **Configuration**, **Specify a management server** page, enter the name of a management server that only the web console uses, and then click **Next**.

9.  On the **Configuration**, **Specify a web site for use with the Web console** page, select the **Default Web Site**, or the name of an existing website. Select **Enable SSL** only if the website has been configured to use Secure Sockets Layer (SSL), and then click **Next**.

    > [!WARNING]
    > Installing the web console on a computer that has SharePoint installed is not supported.

10. On the **Configuration**, **Select an authentication mode for use with the Web console** page, select your option, and then click **Next**.

    > [!NOTE]
    > If you install the management server on a server using a domain account for System Center Configuration service and System Center Data Access service, and then install the web console on a different server and select Mixed Authentication, you may need to register Service Principle Names and configure constraint delegations, as described in [Running the Web Console Server on a standalone server using Windows Authentication](https://techcommunity.microsoft.com/t5/system-center-blog/running-the-web-console-server-on-a-standalone-server-using/ba-p/340345).

10. On the **Diagnostic and Usage Data** page, please review data collection terms and then click **Next** to continue.  

11. If Microsoft Update is not enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your option, and then click **Next**.

12. Review your selections on the **Configuration**, **Installation Summary** page, and then click **Install**. Setup continues.

13. When Setup is finished, the **Setup is complete** page appears. Click **Close**.

### To install the Web console on an existing Management server

1.  Log on to the computer that is hosting a management server with an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **What do you want to do?** page, click **Add a feature**.

4.  On the **Getting Started, Select features to install** page, select **Web console**, and then click **Next**.

5.  On the **Prerequisites** page, review and address any warnings or errors, and then click **Verify Prerequisites Again** to recheck the system.

    > [!NOTE]
    > Installation of the System Center - Operations Manager web console requires that ISAPI and CGI Restrictions in IIS be enabled for ASP.NET 4. To enable this, select the web server in IIS Manager, and then double-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.0.30319**, and then click **Allow**.

6.  If the Prerequisite checker returns no warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood and agree with the license terms**, and then click **Next**.

8.  On the **Configuration**, **Specify a web site for use with the Web console** page, select the **Default Web Site**, or the name of an existing website. Select **Enable SSL** only if the website has been configured to use Secure Sockets Layer (SSL), and then click **Next**.

9.  On the **Configuration**, **Select an authentication mode for use with the Web console** page, select your option, and then click **Next**.

10. If Windows Update is not activated on the computer, the **Configuration**, **Microsoft Update** page appears. Select your option, and then click **Next**.

11. Review your selections on the **Configuration**, **Installation Summary** page, and click **Install**. Setup continues.

12. On the **Setup is complete** page, click **Close**.

> [!IMPORTANT]
> The Default website must have an http or https binding configured.

### To install a Web console by using the Command Prompt window

1.  Log on to the computer with an account that has local administrative credentials.

2.  Open a Command Prompt window by using the **Run as Administrator** option.

3.  Change the path to where the Operations Manager setup.exe file is located, and run the following command.

    > [!IMPORTANT]
    > Use the `/WebConsoleSSL` parameter only if your website has Secure Sockets Layer (SSL) activated.
    >
    > For a default web installation, specify **Default Web Site** for the `/WebSiteName` parameter.

    > [!NOTE]
    > The /ManagementServer parameter is only required when you are installing the web console on a server that is not a management server.

    ```
    setup.exe /silent /install /components:OMWebConsole
    /ManagementServer: <ManagementServerName>
    /WebSiteName: "<WebSiteName>" [/WebConsoleUseSSL]
    /WebConsoleAuthorizationMode: [Mixed|Network]
    /UseMicrosoftUpdate: [0|1]
    ```

## To configure permissions inheritance for the Web console

The following steps are for configuring permission inheritance for the System Center - Operations Manager Web console.  

1.  In Windows Explorer, navigate to the MonitoringView folder in the installation directory for the web console (by default, C:\Program Files\System Center \<version\>\Operations Manager\WebConsole\MonitoringView), right-click the TempImages folder, and click **Properties**.

2.  On the **Security** tab, click **Advanced**.

3.  On the **Permissions** tab, click **Change Permissions**.

::: moniker range="<sc-om-2019"

4.  Select the **Include inheritable permissions from this object's parent** checkbox. Skip this step for Windows 2016 and later.

5.  In **Permission entries**, click **Administrators**, and then click **Remove**. Repeat for the **SYSTEM** entry, and then click **OK**.

6.  Click **OK** to close **Advanced Security Settings for TempImages**, and then click **OK** to close **TempImages Properties**.

::: moniker-end

::: moniker range="sc-om-2019"

4.  In **Permission entries**, click **Administrators**, and then click **Remove**. Repeat for the **SYSTEM** entry, and then click **OK**.

5.  Click **OK** to close **Advanced Security Settings for TempImages**, and then click **OK** to close **TempImages Properties**.

::: moniker-end

All information and content at https://techcommunity.microsoft.com/t5/system-center-blog/running-the-web-console-server-on-a-standalone-server-using/ba-p/340345 is provided by the owner or the users of the website. Microsoft makes no warranties, express, implied or statutory, as to the information at this website.

## Next steps

- See [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  
