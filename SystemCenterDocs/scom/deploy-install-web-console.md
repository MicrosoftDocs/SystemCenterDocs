---
ms.assetid: 8e15d2ef-be27-483d-ad4a-09df62ed6618
title: Install the Operations Manager Web console
description: This article describes how to install the Web console for System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 03/19/2025
ms.custom: engagement-fy23, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
---

# Install the Operations Manager Web console

You can install the web console when you install System Center - Operations Manager, or you can install it separately. You can install a stand-alone web console or install it on an existing management server that meets the prerequisites.

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

::: moniker range=">=sc-om-2022"

Installation of Reporting and Web Console will be successful, regardless of the updates installed on Operations Manager Management Server.

::: moniker-end

::: moniker range="=sc-om-2019"

>[!NOTE]
> Operations Manager 2019 UR1 and later supports a single installer for all supported languages, instead of language-specific installers. The installer automatically selects the language based on the computer's language settings where you are installing it.

::: moniker-end

::: moniker range=">=sc-om-2022"

>[!NOTE]
> Operations Manager supports a single installer for all supported languages, instead of language-specific installers. The installer automatically selects the language based on the computer's language settings where you are installing it.

::: moniker-end

 For information about the prerequisites, see [System Requirements for System Center Operations Manager](./system-requirements.md).

> [!IMPORTANT]
> If you install a standalone web console on a server, you won't be able to add the management server feature to this server. If you want to install the management server and web console on the same server, you must either install both features simultaneously or install the management server before you install the web console.

When you install the web console, the following three components are installed:

- Operations Manager web console

- Application Diagnostics console

- Application Advisor console

> [!NOTE]
> If Application Diagnostics console isn't installed, when viewing APM alerts, you won't be able to use the link embedded in the alert description to launch the APM event details. To use this feature, install the web console within the management group.

If you plan to use network load balancing with Application Diagnostics console and Application Advisor console, be sure to use sticky sessions. This ensures that the same instance of the console is used for the entire session. For more information about network load balancing, see [Network Load Balancing](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770558(v=ws.11)). For more information about sessions, see [Support for Sessions](/previous-versions/windows/it-pro/windows-server-2003/cc738968(v=ws.10)).

> [!NOTE]
> A Network Load Balancer isn't supported for the Operations Manager web console server.

> [!IMPORTANT]
> The web console operates with sensitive data, such as clear text user credentials, server names, IP addresses, and so on. If these are exposed on the network, they can represent a significant security risk. If Internet Information Services (IIS) doesn't have Secure Sockets Layer (SSL) configured, you're advised to configure it manually. For more information about security, see [Data Encryption for Web console and Reporting server Connections](plan-data-encryption-server-roles.md).

If the web console doesn't have sufficient access to the operational database or the data warehouse database, you'll receive a warning during the web console configuration step. You can proceed with Setup, but the web console won't be configured correctly for .NET Application monitoring. To resolve this issue, you can have your database administrator run the following SQL Server statement on both the operational database and data warehouse database:

```
EXEC [apm].GrantRWPermissionsToComputer N'[LOGIN]'
```

The local and remote parameters are as follows:

- For local installation, the LOGIN is: IIS APPPOOL\OperationsManagerAppMonitoring

- For remote installation, the LOGIN is: Domain\MachineName$

> [!NOTE]
> If you run **Repair** on the web console after installation, the settings that were selected during installation will be restored. Any changes that you manually make to the web console configuration after the installation will be reset.

::: moniker range=">=sc-om-2019"

[!INCLUDE [validation-operations-manager.md](../includes/validation-operations-manager.md)]

::: moniker-end

### Install a stand-alone Web console

::: moniker range="sc-om-2016"

>[!NOTE]
>If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 Web console role will fail because the setup media doesn't include the updates to support TLS 1.2. The only way you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system.

::: moniker-end

1. Sign in to the computer that will host the web console with an account that has local administrative credentials.

2. On the Operations Manager installation media, run **Setup.exe**, and select **Install**.

3. On the **Getting Started**, **Select features to install** page, select **Web console**. To read more about what each feature provides and its requirements, select **Expand all**, or expand the buttons next to each feature, and select **Next**.

4. On the **Getting Started**, **Select installation location** page, accept the default location, or type in a new location or browse to one, and select **Next**.

  ::: moniker range="sc-om-2016"
   > [!NOTE]
   > The default path is `C:\Program Files\Microsoft System Center 2016\Operations Manager`. 
::: moniker-end
    
::: moniker range=">sc-om-2016"
   > [!NOTE]
   > The default path is `C:\Program Files\Microsoft System Center\Operations Manager`.
::: moniker-end

5. On the **Prerequisites** page, review and address any warnings or errors that the Prerequisites checker returns, and select **Verify Prerequisites Again** to recheck the system.

    > [!NOTE]
    >- Installation of the web console requires that ISAPI and CGI Restrictions in IIS be enabled for ASP.NET 4. To enable this, select the web server in IIS Manager, and then double-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.0.30319**, and select **Allow**.
    >- Select **ASP.NET v4.8**, and select **Allow** (applicable for Operations Manager 2022).

6. If the Prerequisites checker doesn't return any warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Select **Next**.

7. On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood and agree with the license terms**, and select **Next**.

8. On the **Configuration**, **Specify a management server** page, enter the name of a management server that only the web console uses, and select **Next**.

9. On the **Configuration**, **Specify a web site for use with the Web console** page, select the **Default Web Site**, or the name of an existing website. Select **Enable SSL** only if the website has been configured to use Secure Sockets Layer (SSL), and select **Next**.

    > [!WARNING]
    > Installing the web console on a computer that has SharePoint installed isn't supported.

10. On the **Configuration**, **Select an authentication mode for use with the Web console** page, select your option, and select **Next**.

    > [!NOTE]
    > If you install the management server on a server using a domain account for System Center Configuration service and System Center Data Access service, and then install the web console on a different server and select Mixed Authentication, you may need to register Service Principle Names and configure constraint delegations, as described in [Running the Web Console Server on a standalone server using Windows Authentication](/troubleshoot/system-center/scom/http-500-error-connecting-to-web-console).

11. On the **Diagnostic and Usage Data** page, review data collection terms and then select **Next** to continue.  

12. If Microsoft Update isn't enabled on the computer, the **Configuration**, **Microsoft Update** page appears. Select your option, and select **Next**.

13. Review your selections on the **Configuration**, **Installation Summary** page, and select **Install**. Setup continues.

14. When Setup is finished, the **Setup is complete** page appears. Select **Close**.

### Install the Web console on an existing Management server

1. Sign in to the computer that is hosting a management server with an account that has local administrative credentials.

2. On the Operations Manager installation media, run **Setup.exe**, and select **Install**.

3. On the **Getting Started**, **What do you want to do?** page, select **Add a feature**.

4. On the **Getting Started, Select features to install** page, select **Web console**, and select **Next**.

5. On the **Prerequisites** page, review and address any warnings or errors, and select **Verify Prerequisites Again** to recheck the system.

    > [!NOTE]
    >- Installation of the System Center - Operations Manager web console requires that ISAPI and CGI Restrictions in IIS be enabled for ASP.NET 4. To enable this, select the web server in IIS Manager, and then double-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.0.30319** (for SCOM 2016 and SCOM 2019), and select **Allow**.
    >- For SCOM 2022 and newer: Select **ASP.NET v4.8**, and select **Allow**.

6. If the Prerequisite checker returns no warnings or errors, the **Prerequisites**, **Proceed with Setup** page appears. Select **Next**.

7. On the **Configuration**, **Please read the license terms** page, review the Microsoft Software License Terms, select **I have read, understood and agree with the license terms**, and select **Next**.

8. On the **Configuration**, **Specify a web site for use with the Web console** page, select the **Default Web Site**, or the name of an existing website. Select **Enable SSL** only if the website has been configured to use Secure Sockets Layer (SSL), and select **Next**.

9. On the **Configuration**, **Select an authentication mode for use with the Web console** page, select your option, and select **Next**.

10. If Windows Update isn't activated on the computer, the **Configuration**, **Microsoft Update** page appears. Select your option, and select **Next**.

11. Review your selections on the **Configuration**, **Installation Summary** page, and select **Install**. Setup continues.

12. On the **Setup is complete** page, select **Close**.

> [!IMPORTANT]
> The Default website must have an http or https binding configured. If you configure a specific IP address or host header in the bindings of the web console website, create additional bindings on the website for the same ports by using the loopback address or the localhost hostname, depending on the scenario. For more information, see [Host header or IP address binding causes web console login errors in Operations Manager](/troubleshoot/system-center/scom/web-console-login-errors).

### Install a Web console by using the Command Prompt window

1. Sign in to the computer with an account that has local administrative credentials.

2. Open a Command Prompt window by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager setup.exe file is located, and run the following command.

    > [!IMPORTANT]
    > Use the `/WebConsoleUseSSL` parameter only if your website has Secure Sockets Layer (SSL) activated.
    >
    > For a default web installation, specify **Default Web Site** for the `/WebSiteName` parameter.

    > [!NOTE]
    > The /ManagementServer parameter is only required when you're installing the web console on a server that isn't a management server.

    ```
    setup.exe /silent /install /components:OMWebConsole
    /ManagementServer: <ManagementServerName>
    /WebSiteName: "<WebSiteName>" [/WebConsoleUseSSL]
    /WebConsoleAuthorizationMode: [Mixed|Network]
    /UseMicrosoftUpdate: [0|1]
    /AcceptEndUserLicenseAgreement: [0|1]
    ```

## Configure permissions inheritance for the Web console

The following steps are for configuring permission inheritance for the System Center - Operations Manager Web console.  

1. In Windows Explorer, navigate to the MonitoringView folder in the installation directory for the web console (by default, `C:\Program Files\System Center <version>\Operations Manager\WebConsole\MonitoringView`), right-click the TempImages folder, and select **Properties**.

2. On the **Security** tab, select **Advanced**.

3. On the **Permissions** tab, select **Change Permissions**.

::: moniker range="<sc-om-2019"

4. Select the **Include inheritable permissions from this object's parent** checkbox. Skip this step for Windows 2016 and later.

5. In **Permission entries**, select **Administrators**, and select **Remove**. Repeat for the **SYSTEM** entry, and select **OK**.

6. Select **OK** to close **Advanced Security Settings for TempImages**, and select **OK** to close **TempImages Properties**.

::: moniker-end

::: moniker range=">=sc-om-2019"

4. In **Permission entries**, select **Administrators**, and select **Remove**. Repeat for the **SYSTEM** entry, and select **OK**.

5. Select **OK** to close **Advanced Security Settings for TempImages**, and select **OK** to close **TempImages Properties**.

::: moniker-end

All information and content at https://techcommunity.microsoft.com/t5/system-center-blog/running-the-web-console-server-on-a-standalone-server-using/ba-p/340345 is provided by the owner or the users of the website. Microsoft makes no warranties, express, implied or statutory, as to the information at this website.

## Configure the IIS Application Pool Identity

By default, the IIS application pool identity of the Web Console is the built-in account named **ApplicationPoolIdentity**. When connecting to SQL, this account uses the Windows computer login to access the Operations Manager databases. To improve security, it is recommended that you change the Web Console identity to a dedicated Active Directory user account.

To change the Web Console identity, follow these steps:

1. Create a user account in Active Directory to use as the Web Console identity.

1. Add the user to the local Administrators group on the Web Console server.

1. Open **Local Security Policy** on the Web Console server, expand **Security Settings** > **Local Policies** > **User Rights Assignment** and grant the following rights to the user:

   1. **Log on as a service**
   
   1. **Generate security audits**
   
   1. **Replace a process level token**
   
1. Open **SQL Server Management Studio** and connect to the SQL instance that hosts the OperationsManager database.

1. Expand **Security**, right-click **Logins** and select **New Login**.

1. For **Login name**, enter the username of the account you created in Step 1 using *domain*\\*user* format. Alternatively, select **Search** and search Active Directory for the account.

1. Select **User Mapping**.

1. Select the **OperationsManager** database, make sure that the **public** role membership is selected in the lower pane and select **OK**.

1. Repeat steps 4-8 for the OperationsManagerDW database.

1. On the Web Console server, open **IIS Manager** and select **Application Pools**.

1. Right-click **DefaultAppPool** and select **Advanced Settings**.

1. In Advanced Settings, find the **Identity** setting and select the three dots next to **ApplicationPoolIdentity**.

1. Select **Custom account** and select **Set**.

1. Enter the username in *domain*\\*user* format and the password of the account you created in Step 1 and select **OK** three times to return to the main IIS Manager window.

1. Repeat Steps 11-14 for the following application pools:

   1. MonitoringView
   
   1. OperationsManager
   
   1. OperationsManagerAppMonitoring
   
1. Return to **SQL Server Management Studio** and connect to the SQL instance that hosts the OperationsManager database.

1. Expand **Security** > **Logins,** find the computer account of the Web Console server and delete or disable the login.

1. Repeat Steps 16-17 for the OperationsManagerDW database.

## Next steps

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
