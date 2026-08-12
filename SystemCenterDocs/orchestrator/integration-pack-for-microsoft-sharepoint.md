---
title: System Center integration pack for SharePoint
description: This article describes the SharePoint integration pack for System Center - Orchestrator.
ms.date: 11/19/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
author: Jeronika-MS
ms.author: v-gajeronika
ms.update-cycle: 1095-days
ms.custom:
  - engagement-fy23
  - sfi-image-nochange
---

# Integration pack for SharePoint

Integration packs are add-ons for System Center - Orchestrator. They help you to optimize the IT operations across heterogeneous environments. Using integration packs, you can design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and non-Microsoft products.

[Learn more](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx) about Orchestrator privacy.

This article provides information about System Center integration pack for Microsoft SharePoint.

The System Center Integration Pack for Microsoft SharePoint enables the automation of common tasks in SharePoint. For example, to create list items, to upload and download documents, and to monitor a list for changes.

>[!Note]
>Azure Active Directory or Azure AD or AAD mentioned in Integration packs refers to Microsoft Entra ID. [Learn more](https://azure.microsoft.com/updates/azure-ad-is-becoming-microsoft-entra-id/).

## System requirements

The integration pack for SharePoint requires the following software to be installed and configured before you implement the integration.

::: moniker range="sc-orch-2016"

- System Center - Orchestrator
- Microsoft .NET Framework 4
- Microsoft SharePoint

::: moniker-end

::: moniker range="=sc-orch-2019"

- System Center - Orchestrator 2019
- Microsoft .NET Framework 4.6.1 or above (latest .NET Framework recommended)

> [!IMPORTANT]
>
> 1. SharePoint Integration Pack (v10.19.38.0 or above) targets .NET Framework 4.6.1. Ensure
>    that .NET Framework Runtime v4.6.1 or later is installed on Runbook Designer and Runbook Server
>    machines. We recommend installing the latest available .NET framework version.
> 2. Create the following files with (identical) contents as shown below to update
>    `supportedRuntimeVersion` to v4:
>    - `%systemdrive%/Program Files (x86)/Microsoft System Center/Orchestrator/Runbook Designer/RunbookDesigner.exe.config`
>    - `%systemdrive%/Program Files (x86)/Microsoft System Center/Orchestrator/Runbook Designer/RunbookTester.exe.config`
>    - `%systemdrive%/Program Files (x86)/Microsoft System Center/Orchestrator/Runbook Server/PolicyModule.exe.config`
>
>    Contents:
>
>    ```xml
>    <?xml version="1.0" encoding="utf-8"?>
>    <configuration>
>      <startup useLegacyV2RuntimeActivationPolicy="true">
>        <supportedRuntime version="v4.0.30319"/>
>      </startup>
>      <system.xml.serialization>
>        <xmlSerializer tempFilesLocation="C:\ProgramData\Microsoft System Center 2012\Orchestrator\Activities\XmlSerializers\"/>
>      </system.xml.serialization>
>    </configuration>
>    ```

::: moniker-end

::: moniker range=">=sc-orch-2022"

- System Center - Orchestrator 2022
- Microsoft .NET Framework 4.7 or above (latest .NET Framework recommended)

::: moniker-end

## Download the pack

::: moniker range="sc-orch-2025"

SharePoint Integration Pack for Orchestrator 2022 continues to work with Orchestrator 2025.

Download the SharePoint Integration Pack [here](https://www.microsoft.com/download/details.aspx?id=104332).

::: moniker-end

::: moniker range="sc-orch-2022"

- [Download the pack for 2022](https://www.microsoft.com/download/details.aspx?id=104332)

::: moniker-end

::: moniker range="<=sc-orch-2019"
- [Download the pack for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all)
- [Download the pack for 2016](https://www.microsoft.com/download/details.aspx?id=54098)
::: moniker-end

## Register and deploy the integration pack

After you download the integration pack file, you must register it with the Orchestrator management server, and then deploy it to runbook servers and Runbook Designers. Learn about [installing the pack](how-to-add-an-integration-pack.md).

The SharePoint Integration Pack performs actions on behalf of a user who can access your SharePoint domain. The IP authenticates with SharePoint as this user in two modes:

- Basic Auth (default, supports both SharePoint Online and SharePoint on-premises).
- Modern Auth (also known as OAuth) using Azure AD (applicable only for SharePoint Online).

## Configure the pack connections for Basic Auth

A connection establishes a reusable link between Orchestrator and a SharePoint site. You can create as many connections as you require to specify links to multiple sites. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

1. In the **Orchestrator Runbook Designer**, select **Options**, and select **Microsoft SharePoint.**
2. The **Microsoft SharePoint** dialog appears.
3. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears.
4. In the **Name** box, enter a name for the connection. This name can be the name of the SharePoint site or a descriptive name to distinguish the type of connection.
5. In the **Type** box, select **SharePoint Configuration.**
6. In the **SharePoint Site** box, enter the URL of the SharePoint site that you want to integrate with.
7. In the **User Name** and **Password** boxes, enter the credentials that Orchestrator will use to connect to the SharePoint site.
8. In the **Domain** box, enter the name of the domain to authorize access.
9. In the **SharePoint Online** box, enter **False** if the SharePoint instance is on-premises.
10. Set the **Utilize OAuth** box to **False**.
11. In the **Default Monitor Interval (seconds)** box, enter a timeout value in seconds or keep the default value.
12. In the **Default Maximum Items** box, enter a maximum value, or keep the default value.
13. Select **OK**.
14. Add additional connections, if applicable, and select **Finish**.

## Configure the pack connections for Modern Auth (SharePoint Online)

Register an AD Client Application on your Azure Active Directory (AD Instance), and configure the IP to use this client. The IP authenticates on your behalf; hence, your credentials are required in the IP configuration pane.

> [!NOTE]
> This authentication mode is supported only for SharePoint Online.

### Register a Client application on Azure AD

To register a client application on Azure AD, follow these steps:

1. Go to the [Azure portal](https://aad.portal.azure.com/).

2. Navigate to **Azure Active Directory** > **App registrations**, and select **New registration** to register.

3. Set an applicable name for the application and choose the indicated Redirect URI (Public Client/native app) from the dropdown menu.

   ![Screenshot of Registration page.](./media/integration-pack-for-sharepoint/sp-reg.png)

4. Choose the account type depending on your AD setup and whether you use both on-premises and online products.

5. Select **Register**.

#### App overview

The **ApplicationID** and **TenantID** are displayed under **Overview**; note them down.

![Screenshot of Overview.](./media/integration-pack-for-sharepoint/sp-overview.png)

#### Redirect URI

Set the OAuth redirection URI. Choose the Public client (Mobile/Desktop app) platform:

1. Under **Platform configurations**, select **Add a platform.**

   ![Screenshot of Add platform.](./media/integration-pack-for-sharepoint/sp-add-platform.png)

2. Select `https://login.microsoftonline.com/common/oauth2/nativeclient` as the Redirect URI and select **Configure**.

   :::image type="content" source="./media/integration-pack-for-sharepoint/sp-redirect-uri.png" alt-text="Screenshot of Redirect URI." lightbox="./media/integration-pack-for-sharepoint/sp-redirect-uri.png":::

3. Under **Advanced Setting**, set **Allow Public Client flows** to **Yes** and select **Save**.

   ![Screenshot of Client flows.](./media/integration-pack-for-sharepoint/sp-client-flows.png)

#### API permissions

SharePoint offers different API scopes/permissions.

Follow these steps to set API permissions:

1. Under **Configured permissions**, select **Add a permission**, and select **SharePoint**.

   ![Screenshot of SharePoint API.](./media/integration-pack-for-sharepoint/sp-api.png)

2. Grant the **AllSites.Write** permission to the app, or higher and then select **Add permissions**. **AllSites.Write** is required for all the SharePoint IP activities to work, and you can choose a narrower scope depending on the activities that your runbooks use.  

   ![Screenshot of SharePoint API Scopes.](./media/integration-pack-for-sharepoint/sp-api-scope.png)

### Configure Certificate
#### Generate a certificate
Follow the steps below to generate a certificate. The sample script is for illustrative only. Replace the certificate name, file paths, and password with values that are appropriate for your environment.
1. Open PowerShell as as Administrator.
2. Create a self-signed certificate by running the following script. The certificate is created in the current user's personal certificate store.
```powershell
$cert = New-SelfSignedCertificate -Subject "CN=OrchestratorSharePoint" -CertStoreLocation "Cert:\CurrentUser\My" -KeyExportPolicy Exportable -KeyAlgorithm RSA    -KeyLength 2048 -HashAlgorithm SHA256
```
3. Create a secure password that protects the exported PFX file.
```powershell
$pwd = ConvertTo-SecureString -String "yourpwd" -AsPlainText -Force
```
4. Export the certificate as a PFX file. This file contains the certificate and private key and is imported to the Orchestrator server..
```powershell
Export-PfxCertificate -Cert $cert -FilePath "C:\Temp\OrchestratorSharePoint.pfx" -Password $pwd
```
5. Export the public certificate as a CER file. This file is uploaded to the Microsoft Entra ID application registration..
```powershell
Export-Certificate -Cert $cert -FilePath "C:\Temp\OrchestratorSharePoint.cer"
```
6. Retrieve the certificate thumbprint by running.
```powershell
$cert.Thumbprint
```
7. Record the certificate thumbprint for later use to configure the SharePoint Integration Pack connection.

#### To install the certificate on the Orchestrator server, follow these steps:
1. Copy `OrchestratorSharePoint.pfx` to the Orchestrator server.
2. Double-click the PFX file to open **Certificate Import** Wizard.
3. Select Local Machine and then select **Next**.
4. Confirm the file path and select **Next**.
5. Enter the password used when exporting.
6. Check **Mark this key as exportable** and select **Next**.
7. Select **Place all certificates in the following store**.
8. Select **Browse** > **Personal** and then select **OK**.
9. Select **Next**, then **Finish**.

#### To upload certificate to app registration, follow these steps:
1. In Microsoft Entra ID, go to your app registration.
2. Select **Certificates & secrets**.
3. Select the **Certificates** tab and then select **Upload certificate**.
4. Browse to `OrchestratorSharePoint.cer` generated in previous steps.
6. Select **Add**.

#### To grant private key access, follow these steps:
1. On Orchestrator server machine, press Win+R.
2. Type **certlm.msc** and press Enter.
3. Go to **Personal** > **Certificates**.
4. Find the certificate named **OrchestratorSharePoint**.
5. Right-click the certificate.
6. Select **All Tasks** > **Manage Private Keys**.
7. Select **Add** and enter NETWORK SERVICE (or your Orchestrator service account)
8. Select **Check Names** and then select **OK**.
9. Ensure Read permission is checked and select **OK**.

### Configure the SharePoint IP for Modern Auth
Use the following steps to configure the SharePoint IP for OAuth authentication:
1. In the **Orchestrator Runbook Designer**, select **Options**, and select **Microsoft SharePoint**.
2. The **Microsoft SharePoint** dialog appears. 
4. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears. 
5. In the **Name** box, enter a name for the connection. This name can be the name of the SharePoint site or a descriptive name to distinguish the type of connection. 
6. In the **Type** box, select **SharePoint Configuration**.
7. In the **SharePoint Site** box, enter the URL of the SharePoint site that you want to integrate with.
8. Set the **SharePoint Online** box to **True**.
9. Set the **Authenticate via AAD using OAuth** box to **True**.
10. Set the **Use App-Only Authentication** box to **True**.
11. Set the **Application ID** to the application ID seen on the portal.
12. Set the **Directory ID** to the directory (tenant) ID seen on the portal. This is also referred to as Microsoft 365 Tenant ID.
13. Set the **Certificate Thumbprint** to the value you get from step  **Generate a certificate**.
14. Keep **User Name**, **Password**, and **Domain** boxes blank.
15. Set the **Azure Active Directory URI** to your AD URL (or leave it to default value).
16. Select **OK**.
17. Add additional connections, if applicable, and select **Finish**.

### Get data from SharePoint

After performing the above steps, create a new runbook and use the **Get List Items** SharePoint activity. When you set the desired configuration in the activity's settings, the **Runbook Designer** will exercise your connection options to fetch some data from SharePoint.

A pop-up appears in case there's some problem with the credentials or other settings.
