---
ms.assetid: 8e15d2ef-be27-483d-ad4a-09df62ed6618
title:  How to Install the Operations Manager Web console
description: This article describes how to install the Operations Manager Web console. 
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to install the Operations Manager Web console

>Applies To: System Center 2016 - Operations Manager

You can install the web console when you install Operations Manager, or you can install it separately. You can install a stand-alone web console or install it on an existing management server that meets the prerequisites. For information about the prerequisites, see [System Requirements for System Center 2016 - Operations Manager](../orchestrator/system-requirements.md). After you install the web console, you must configure permissions inheritance to allow users to view performance and diagram views. For instructions, see [To configure permissions inheritance for the web console](#to-configure-permissions-inheritance-for-the-web-console).

> [!IMPORTANT]
> If you install a stand-alone web console on a server, you will not be able to add the management server feature to this server. If you want to install the management server and web console on the same server, you must either install both features simultaneously, or install the management server before you install the web console.

When you install the web console, the following three components are installed:

-   Operations Manager web console

-   Application Diagnostics console

-   Application Advisor console

> [!NOTE]
> If Application Diagnostics console is not installed, when viewing APM alerts, you will not be able to use the link embedded in the alert description to launch the APM event details. To use this feature, install the web console within the management group.

If you plan to use network load balancing with Application Diagnostics console and Application Advisor console, be sure to use sticky sessions. This ensures that the same instance of the console is used for the entire session. For more information about network load balancing, see [Network Load Balancing](http://go.microsoft.com/fwlink/p/?linkID=158320). For more information about sessions, see [Support for Sessions](http://go.microsoft.com/fwlink/p/?linkID=251693).

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

1.  Log on to the computer that will host the web console with an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **Select features to install** page, select **Web console**. To read more about what each feature provides and its requirements, click **Expand all**, or expand the buttons next to each feature, and then click **Next**.

4.  On the **Getting Started**, **Select installation location** page, accept the default location of **C:\Program Files\System Center 2016\Operations Manager**, or type in a new location or browse to one, and then click **Next**.

5.  On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and then click **Verify Prerequisites Again** to recheck the system.

    > [!NOTE]
    > Installation of the web console requires that ISAPI and CGI Restrictions in IIS be enabled for ASP.NET 4. To enable this, select the web server in IIS Manager, and then double-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.0.30319**, and then click **Allow**.

    > [!IMPORTANT]
    > You must install IIS before installing .NET Framework 4. If you installed IIS after installing .NET Framework 4, you must register ASP.NET 4.0 with IIS. Open a Command prompt window by using the **Run As Administrator** option and then run the following command:
    > 
    > **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -r**

6.  If the Prerequisites checker does not return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Configuration**, **Specify a management server** page, enter the name of a management server that only the web console uses, and then click **Next**.

8.  On the **Configuration**, **Specify a web site for use with the Web console** page, select the **Default Web Site**, or the name of an existing website. Select **Enable SSL** only if the website has been configured to use Secure Sockets Layer (SSL), and then click **Next**.

    > [!WARNING]
    > Installing the web console on a computer that has SharePoint installed is not supported.

9. On the **Configuration**, **Select an authentication mode for use with the Web console** page, select your options, and then click **Next**.

    > [!NOTE]
    > If you install the management server on a server using a domain account for System Center Configuration service and System Center Data Access service, and then install the web console on a different server and select Mixed Authentication, you may need to register Service Principle Names and configure constraint delegations, as described in [Running the Web Console Server on a standalone server using Windows Authentication](http://blogs.technet.com/b/momteam/archive/2008/01/31/running-the-web-console-server-on-a-standalone-server-using-windows-authentication.aspx).

10. On the **Diagnostic and Usage Data** page, please review data collection terms and then click **Next** to continue.  

11. If Microsoft Update is not enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and then click **Next**.

12. Review your selections on the **Configuration**, **Installation Summary** page, and then click **Install**. Setup continues.

13. When Setup is finished, the **Setup is complete** page appears. Click **Close**.

### To install the Web console on an existing Management server

1.  Log on to the computer that is hosting a management server with an account that has local administrative credentials.

2.  On the Operations Manager installation media, run **Setup.exe**, and then click **Install**.

3.  On the **Getting Started**, **What do you want to do?** page, click **Add a feature**.

4.  On the **Getting Started, Select features to install** page, select **Web console**, and then click **Next**.

5.  On the **Prerequisites** page, review and address any warnings or errors, and then click **Verify Prerequisites Again** to recheck the system.

    > [!NOTE]
    > Installation of the web console requires that ISAPI and CGI Restrictions in IIS be enabled for ASP.NET 4. To enable this, select the web server in IIS Manager, and then double-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.0.30319**, and then click **Allow**.

    > [!IMPORTANT]
    > You must install IIS before installing .NET Framework 4. If you installed IIS after installing .NET Framework 4, you must register ASP.NET 4.0 with IIS. Open a Command prompt window by using the **Run As Administrator** option and then run the following command:
    > 
    > **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -r**

6.  If the Prerequisite checker returns no warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Click **Next**.

7.  On the **Configuration**, **Specify a web site for use with the Web console** page, select the **Default Web Site**, or the name of an existing website. Select **Enable SSL** only if the website has been configured to use Secure Sockets Layer (SSL), and then click **Next**.

8.  On the **Configuration**, **Select an authentication mode for use with the Web console** page, select your options, and then click **Next**.

9. If Windows Update is not activated on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and then click **Next**.

10. Review your selections on the **Configuration**, **Installation Summary** page, and click **Install**. Setup continues.

11. On the **Setup is complete** page, click **Close**.

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

1.  In Windows Explorer, navigate to the MonitoringView folder in the installation directory for the web console (by default, C:\Program Files\System Center 2016\Operations Manager\WebConsole\MonitoringView), right-click the TempImages folder, and click **Properties**.

2.  On the **Security** tab, click **Advanced**.

3.  On the **Permissions** tab, click **Change Permissions**.

4.  Select the **Include inheritable permissions from this object's parent** checkbox.

5.  In **Permission entries**, click **Administrators**, and then click **Remove**. Repeat for the **SYSTEM** entry, and then click **OK**.

6.  Click **OK** to close **Advanced Security Settings for TempImages**, and then click **OK** to close **TempImages Properties**.

All information and content at http://blogs.technet.com/b/momteam/archive/2008/01/31/running-the-web-console-server-on-a-standalone-server-using-windows-authentication.aspx is provided by the owner or the users of the website. Microsoft makes no warranties, express, implied or statutory, as to the information at this website.

## Next steps

- See [Distributed Deployment of Operations Manager](Distributed-Deployment-of-Operations-Manager.md) to understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group.  
