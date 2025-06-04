---
ms.assetid: bc3c9818-6019-4af3-bcaa-990229650c0c
title: Install the Operations Manager Reporting Server
description: This article describes how to install the Operations Manager Reporting server role.
author: jyothisuri
ms.author: jsuri
ms.date: 03/19/2025
ms.custom: engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Install the Operations Manager Reporting server

In this procedure, the Reporting server is installed on a standalone server that's hosting the SQL Server database and SQL Server Reporting Services.

> [!WARNING]
> Although SQL Server Reporting Services is installed on the standalone server, Operations Manager reports aren't accessed on this server; instead, they are accessed in the **Reporting** workspace in the Operations console.

You must ensure that your server meets the minimum system requirement for Operations Manager. For more information, see [System Requirements for System Center - Operations Manager](./system-requirements.md).

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

::: moniker range="sc-om-2019"

> [!NOTE]
> Operations Manager 2019 UR1 and later supports a single installer for all supported languages, instead of language-specific installers. The installer automatically selects the language based on the computer's language settings where you're installing it.

::: moniker-end

::: moniker range=">=sc-om-2022"

> [!NOTE]
>
> - Operations Manager supports a single installer for all supported languages, instead of language-specific installers. The installer automatically selects the language based on the computer's language settings where you're installing it.
> - Installation of Reporting and Web Console will be successful irrespective of the updates installed on Operations Manager Management Server.

::: moniker-end

::: moniker range="sc-om-2016"

> [!NOTE]
> If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 Reporting services role will fail because the setup media doesn't include the updates to support TLS 1.2. The only way you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system. This limitation doesn't apply to Operations Manager version 1801.

::: moniker-end

::: moniker range=">=sc-om-2019"

[!INCLUDE [validation-operations-manager.md](../includes/validation-operations-manager.md)]

::: moniker-end

## Install Operations Manager reporting

An installation of SQL Server Reporting Services used by Operations Manager **can't be shared with any other application** as changes are made to the base SSRS installation to accommodate user roles and authentication with System Center Operations Manager. If any reports exist on the SSRS instance where the Operations Manager Reporting Services installer executes, all existing data and reports are overwritten.

Ensure that SQL Server Reporting Services is correctly installed and configured. For more information about how to install and configure SQL Server Reporting Services, see [SQL Server Installation](/sql/database-engine/install-windows/install-sql-server).

> [!NOTE]
> Before you continue with this procedure, ensure that the account that you are using to run the installer for the Operations Manager Reporting Role has [SA (sysadmin)](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) on both the Operational Database (_OperationsManager_) and Reporting (_ReportServer_) SQL Instances. This will allow the installer to deploy all logins and permissions as required. The SA role can be safely removed from the account used for the installer after installation. Otherwise, the Setup fails, and all changes are rolled back, which may leave SQL Server Reporting Services in an inoperable state. If this happens you can attempt run a tool to reset SSRS to a working condition. The program is: **ResetSRS.exe** which is an executable inside of the support tools folder on your Operations Manager installation media.

## Install Reporting Services on NTLM hardened enterprises

In Operations Manager 2016 and later, if NTLM is disabled as an organization policy, Operations Manager’s reporting services were impacted. For organizations with NTLM disabled, you can select the Reporting Manager **Authentication Type**, as **Windows Negotiate** while installing. NTLM is the default option.

> [!NOTE]
> Authentication Type options are available only when you install the reporting manager on a remote server.

### Prerequisites to disable NTLM

- If SSRS and SQL both installed on remote servers, ensure [SDK](/troubleshoot/system-center/scom/http-500-error-connecting-to-web-console#register-the-sdk-spns), [SSRS](/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server), and [SQL](/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections) SPNs are set.
- If SSRS is installed on remote server and SQL and Management Server are installed on the same server, [SDK](/troubleshoot/system-center/scom/http-500-error-connecting-to-web-console#register-the-sdk-spns) and [SSRS](/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server) SPNs are required.
- If SQL installed on remote server and SSRS and Management Server are installed on the same server, ensure that [SQL](/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections), [SSRS](/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server), and [SDK](/troubleshoot/system-center/scom/http-500-error-connecting-to-web-console#register-the-sdk-spns) SPNs are set.

#### Verify that Reporting Services is configured correctly

Follow these steps to verify that Reporting Services is configured correctly:

1. Verify that the **ReportServer** and **ReportServerTempDB** databases in SQL Server Management Studio are located on the standalone server. Open **SQL Server Management Studio**, and then connect to the default database instance. Open the **Databases** node, and verify that the two Reporting Services databases exist under this node.

2. Verify the correct configuration of SQL Server Reporting Services. Select **Start**, point to **Programs**, point to the appropriate offering of Microsoft SQL Server, point to **Configuration Tools**, and select **Reporting Services Configuration Manager**. Connect to the instance on which you installed Reporting Services.

3. In the navigation pane, select the `<servername>\SQLinstance`. This displays the Report Server status in the results pane. Ensure that the **Report Server Status** is **Started**.

4. In the navigation pane, select **Scale-out Deployment**, and ensure that the **Status** column has the value of **Joined**.

5. If **Report Server** isn't started and the **Scale out Deployment** isn't joined, check the configuration of **Service Account**, **Web Service URL**, and **Database**.

    > [!NOTE]
    > While SQL Server Reporting Services supports a scale-out deployment model that allows you to run multiple report server instances that share a single report server database, it isn't supported with Operations Manager. Operations Manager Reporting installs a custom security extension as part of the setup of the front-end components, which can't be replicated across the web farm.

6. Confirm that the SQL Server Reporting Services service is running. On the taskbar, select **Start**, point to **Administrative Tools**, and select **Services**.

7. In the **Name** column, find the **SQL Server Reporting Services** instance service and verify that its status reads **Started** and that the **Startup Type** is **Automatic**.

8. In the **Name** column, find the **SQL Server Agent** service and verify that its status reads **Started** and that its **Startup Type** is **Automatic**.

9. Verify that the Report Server website is functioning and available by browsing to `http://<servername>/reportserver/_<$instance>`. You should see a page with the `<servername>/ReportServer/_<$instance>` and the text, **Microsoft SQL Server Reporting Services Version** ##.#.####.## where the # is the version number of your SQL Server installation.

10. Verify that the Report Manager website is configured correctly by opening **Internet Explorer** and browsing to `http://<servername>/reports/_<$instance>`.

11. In the Report Manager website, select **New Folder** to create a new folder. Enter a name and description, and select **OK**. Ensure that the new, created folder is visible on the Report Manager website.

#### Install Operations Manager reporting

> [!IMPORTANT]
> The Operations Manager Reporting role must be installed directly on the SQL Server Reporting Server. Remote SSRS instances are not supported and will not appear in the installation wizard.

Follow these steps to install Operations Manager reporting:

1. Sign in to the SSRS server as a local administrator.

2. On the Operations Manager installation media, run **Setup.exe**, and select **Install**.

3. On the **Getting Started**, **Select features to install** page, select the **Reporting server** feature. To read more about each feature and its requirements, select **Expand all**, or expand the buttons next to each feature, and select **Next**.

4. On the **Getting Started**, **Select installation location** page, accept the default value, or enter a new location or browse to one, and select **Next**.

5. On the **Prerequisites** page, review and resolve any warnings or errors, and select **Verify Prerequisites Again** to recheck the system.

6. If the Prerequisites checker doesn't return any warnings or errors, continue to the **Prerequisites**, **Proceed with Setup** page. Select **Next**.

7. On the **Configuration**, **Specify a Management server** page, enter the name of a management server that is used by the Reporting features only. Then select **Next**.

8. On the **Configuration**, **SQL Server instance for reporting services** page, select the instance of SQL Server that hosts SQL Server Reporting Services, and select **Next**.

9. On the **Configuration**, **Configure Operations Manager accounts** page, enter the credentials for the **Data Reader account**, and select **Next**.

10. On the **Configuration**, **Help improve System Center - Operations Manager** page, select your options, and select **Next**.

11. If Windows Update isn't activated on the computer, the **Configuration**, **Microsoft Update** page appears. Select your options, and select **Next**.

12. Review the options on the **Configuration**, **Installation Summary** page, and select **Install**. Setup continues.

13. When the Setup is finished, the **Setup is complete** page appears. Select **Close**.

#### Install Operations Manager reporting from the command prompt

Follow these steps to install Operations Manager reporting from the command prompt:

1. Sign in to the server by using an account that has local administrative credentials.

2. Open the Command Prompt window by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager setup.exe file is located, and run the following command.

    > [!NOTE]
    >
    > - The `/ManagementServer` parameter is only required when you're installing reporting on a server that isn't a management server.
    > - The `/SRSInstance` parameter is the name of the local SSRS instance, for example 'SSRS'.

    ```cmd
    setup.exe /silent /install /components:OMReporting
    /ManagementServer:<ManagementServerName>
    /SRSInstance:[SSRS|<server\instance>]
    /DataReaderUser:<domain\username>
    /DataReaderPassword:<password>
    /SendODRReports:[0|1]
    /UseMicrosoftUpdate:[0|1]
    /AcceptEndUserLicenseAgreement:1
    ```

#### Confirm the health of Operations Manager reports

Follow these steps to confirm the health of Operations Manager reports:

1. Open the Operations console, and select the **Reporting** workspace.

    > [!NOTE]
    > After the initial deployment, reports can require up to 30 minutes to appear.

2. Select **Microsoft ODR Report Library**, and double-click any of the reports listed. The selected report is then generated and displayed in a new window.

    By default, you should see the following reports:

    - Alerts Per Day
    - Instance Space
    - Management Group
    - Management Packs
    - Most Common Alerts

3. Close the report window.

## Next steps

To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed Deployment of Operations Manager](deploy-distributed-deployment.md).
