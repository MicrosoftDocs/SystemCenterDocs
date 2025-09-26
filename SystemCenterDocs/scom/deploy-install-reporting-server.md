---
ms.assetid: bc3c9818-6019-4af3-bcaa-990229650c0c
title: Install the Operations Manager Reporting Server
description: This article describes how to install the Operations Manager reporting server role.
author: jyothisuri
ms.author: jsuri
ms.date: 03/19/2025
ms.custom: engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: install-set-up-deploy
---

# Install the Operations Manager reporting server

This article shows you how to install the System Center Operations Manager reporting server on a standalone server that's hosting the SQL Server database and SQL Server Reporting Services (SSRS).

Although SSRS is installed on the standalone server, you don't access Operations Manager reports on this server. Instead, you access them in the **Reporting** workspace on the operations console.

## Prerequisites

- Ensure that your server meets the minimum [system requirements for Operations Manager](./system-requirements.md).

- Before you install SSRS, ensure that the account that you're using to run the installer for the Operations Manager reporting role has [sysadmin (SA)](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) permissions on both the operational database (**OperationsManager**) and reporting (**ReportServer**) SQL Server instances. This step allows the installer to deploy all logins and permissions as required.

  After installation, you can safely remove the SA role from the account that you used for the installer. Otherwise, the setup fails and all changes are rolled back, which might leave SSRS in an inoperable state. If this situation happens, you can try to run a tool to reset SSRS to a working condition. The program is **ResetSRS.exe**, which is an executable file inside the folder for support tools on your Operations Manager installation media.

[!INCLUDE [ntauthority-note-operations-manager.md](../includes/ntauthority-note-operations-manager.md)]

## Important considerations

::: moniker range="sc-om-2019"

- Operations Manager 2019 UR1 and later support a single installer for all supported languages, instead of language-specific installers. The installer automatically selects the language based on the computer's language settings where you're installing it.

::: moniker-end

::: moniker range=">=sc-om-2022"

- Operations Manager supports a single installer for all supported languages, instead of language-specific installers. The installer automatically selects the language based on the computer's language settings where you're installing it.

- You can successfully install the reporting and web consoles regardless of the updates installed on the Operations Manager management server.

::: moniker-end

::: moniker range="sc-om-2016"

- If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 Reporting services role will fail because the setup media doesn't include the updates to support TLS 1.2. The only way that you can install this role is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system. This limitation doesn't apply to Operations Manager version 1801.

::: moniker-end

::: moniker range=">=sc-om-2019"

[!INCLUDE [validation-operations-manager.md](../includes/validation-operations-manager.md)]

::: moniker-end

## Install and configure SSRS

An installation of SSRS that Operations Manager uses *can't be shared with any other application*. The reason is that the base SSRS installation undergoes changes to accommodate user roles and authentication with Operations Manager. If any reports exist on the SSRS instance where the Operations Manager installer for reporting services runs, all existing data and reports are overwritten.

For information about how to install and configure SSRS, see the [SQL Server installation guide](/sql/database-engine/install-windows/install-sql-server).

### Install SSRS on NTLM-hardened enterprises

In Operations Manager 2016 and later, disabling NTLM as an organizational policy affects Operations Manager reporting services. If your organization disabled NTLM, you can select the reporting manager's **Authentication Type** value as **Windows Negotiate** while installing SSRS. NTLM is the default option.

> [!NOTE]
> Options for authentication type are available only when you install the reporting manager on a remote server.

To disable NTLM, you must meet these requirements:

- If SSRS and SQL Server are both installed on remote servers, ensure that [SDK](/troubleshoot/system-center/scom/http-500-error-connecting-to-web-console#register-the-sdk-spns), [SSRS](/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server), and [SQL Server](/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections) service principal names (SPNs) are set.
- If SSRS is installed on a remote server, and SQL Server and the management server are installed on the same machine, [SDK](/troubleshoot/system-center/scom/http-500-error-connecting-to-web-console#register-the-sdk-spns) and [SSRS](/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server) SPNs are required.
- If SQL Server is installed on remote server, and SSRS and the management server are installed on the same machine, ensure that [SQL Server](/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections), [SSRS](/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server), and [SDK](/troubleshoot/system-center/scom/http-500-error-connecting-to-web-console#register-the-sdk-spns) SPNs are set.

### Verify that SSRS is configured correctly

1. Verify that the **ReportServer** and **ReportServerTempDB** databases in SQL Server Management Studio are located on the standalone server:

   1. Open SQL Server Management Studio and connect to the default database instance.
   1. Open the **Databases** node and verify that the two SSRS databases exist under this node.

2. Verify the correct configuration of SSRS:

   1. Select **Start**, point to **Programs**, point to the appropriate SQL Server offering, point to **Configuration Tools**, and then select **Reporting Services Configuration Manager**.
   1. Connect to the instance on which you installed SSRS.

3. On the left pane, select **\<servername>\SQLinstance**. This step displays the reporting server's status on the results pane. Ensure that the **Report Server Status** value is **Started**.

4. On the left pane, select **Scale-out Deployment**. Ensure that the **Status** column has the value of **Joined**.

5. If **Report Server** isn't started and **Scale out Deployment** isn't joined, check the configuration of **Service Account**, **Web Service URL**, and **Database**.

    > [!NOTE]
    > Although SSRS supports a scale-out deployment model that allows you to run multiple report server instances that share a single report server database, it isn't supported with Operations Manager. Operations Manager reporting installs a custom security extension as part of the setup of the front-end components. This extension can't be replicated across the web farm.

6. Confirm that the SSRS service is running. On the taskbar, select **Start**, point to **Administrative Tools**, and then select **Services**.

7. In the **Name** column, find **SQL Server Reporting Services**. Verify that its status reads **Started** and that the **Startup Type** value is **Automatic**.

8. In the **Name** column, find **SQL Server Agent**. Verify that its status is **Started** and that its **Startup Type** value is **Automatic**.

9. Verify that the reporting server website is functioning and available by browsing to `http://<servername>/reportserver/_<$instance>`. A page should appear with `<servername>/ReportServer/_<$instance>` and the text **Microsoft SQL Server Reporting Services Version ##.#.####.##**, where the number signs represent the version number of your SQL Server installation.

10. Verify that the reporting manager website is configured correctly by opening a browser and going to `http://<servername>/reports/_<$instance>`.

11. On the reporting manager website, select **New Folder** to create a folder. Enter a name and description, and then select **OK**. Ensure that the newly created folder is visible on the reporting manager website.

## Install Operations Manager reporting

> [!IMPORTANT]
> The Operations Manager reporting role must be installed directly on the SSRS server. Remote SSRS instances are not supported and don't appear in the installation wizard.

1. Sign in to the SSRS server as a local administrator.

2. On the Operations Manager installation media, run **Setup.exe**, and then select **Install**.

3. On the **Getting Started** > **Select features to install** page, select the **Reporting server** feature. To read more about each feature and its requirements, select **Expand all** (or expand the button next to each feature). Then select **Next**.

4. On the **Getting Started** > **Select installation location** page, accept the default value. Or you can enter a new location or browse to one. Then select **Next**.

5. On the **Prerequisites** page, review and resolve any warnings or errors. Then select **Verify Prerequisites Again** to recheck the system.

6. If the prerequisites checker doesn't return any warnings or errors, the **Prerequisites** > **Proceed with Setup** page appears. Select **Next**.

7. On the **Configuration** > **Specify a Management server** page, enter the name of a management server that that only the reporting features use. Then select **Next**.

8. On the **Configuration** > **SQL Server instance for reporting services** page, select the instance of SQL Server that hosts SSRS. Then select **Next**.

9. On the **Configuration** > **Configure Operations Manager accounts** page, enter the credentials for **Data Reader account**. Then select **Next**.

10. On the **Configuration** > **Help improve System Center - Operations Manager** page, select your options, and then select **Next**.

11. If Windows Update isn't activated on the computer, the **Configuration** > **Microsoft Update** page appears. Select your options, and then select **Next**.

12. Review the options on the **Configuration** > **Installation Summary** page, and then select **Install**.

13. When Setup finishes, the **Setup is complete** page appears. Select **Close**.

## Install Operations Manager reporting from the command prompt

1. Sign in to the server by using an account that has local administrative credentials.

2. Open the Command Prompt window by using the **Run as Administrator** option.

3. Change the path to where the Operations Manager **setup.exe** file is located, and run the following command. Keep this parameter information in mind:

    - The `/ManagementServer` parameter is required only when you're installing reporting on a server that isn't a management server.
    - The `/SRSInstance` parameter is the name of the local SSRS instance; for example, `SSRS`.

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

## Confirm the health of Operations Manager reports

1. Open the operations console, and select the **Reporting** workspace.

    > [!NOTE]
    > After the initial deployment, reports can require up to 30 minutes to appear.

2. Select **Microsoft ODR Report Library**, and double-click any of the reports listed. The selected report is then generated and displayed in a new window.

    By default, the following reports should appear:

    - **Alerts Per Day**
    - **Instance Space**
    - **Management Group**
    - **Management Packs**
    - **Most Common Alerts**

3. Close the report window.

## Related content

- To understand the sequence and steps for installing the Operations Manager server roles across multiple servers in your management group, see [Distributed deployment of Operations Manager](deploy-distributed-deployment.md).
