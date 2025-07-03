---
title: Exchange Users Integration Pack for Orchestrator in System Center
description: Integration packs are add-ons for System Center - Orchestrator. Integration packs optimize IT operations across various environments.
ms.custom: engagement-fy24
ms.date: 11/19/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 2a7359ab-604e-4e05-89f3-09eb13a14c58
author: jyothisuri
ms.author: jsuri
---

# Exchange Users integration pack

Integration packs are add-ons for Orchestrator, a component of System Center. Integration packs optimize IT operations across various environments. They enable you to design runbooks in Orchestrator that use activities performed by other System Center components, other Microsoft products, and third-party products.

The Integration Pack for Exchange Users facilitates the automation of user-centric tasks, such as actions to read and send email messages, create appointments, or update tasks and contacts. The operation is carried over HTTP and the connection can be authenticated by the methods enabled on the Exchange Server. Consult with your tenant administrator about the available methods on your on-premises Exchange Server.

This integration pack can be used to connect to both on-premises or Online Exchange servers using their respective [Exchange Web Services](/exchange/client-developer/exchange-web-services/explore-the-ews-managed-api-ews-and-web-services-in-exchange) (EWS) endpoint.

>[!Note]
>Azure Active Directory or Azure AD or AAD mentioned in Integration packs refers to Microsoft Entra ID. [Learn more](https://azure.microsoft.com/updates/azure-ad-is-becoming-microsoft-entra-id/).

::: moniker range=">= sc-orch-2019"

This integration pack operates in the methods shown below:

| Server kind                   | Supported auth mode | Default    |
| ----------------------------- | ------------------- | ---------- |
| Exchange Server (on-premises) | Basic Auth          | Basic Auth |
| Exchange Online               | OAuth               | OAuth      |
| Office 365 Exchange           | OAuth               | OAuth      |

::: moniker-end

Microsoft is committed to protect your privacy while delivering software that brings you the performance, power, and convenience you want. For more information about Orchestrator-related privacy, see the [System Center Orchestrator Privacy Statement](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

## System requirements

Prior to implementing the Exchange Users Integration Pack, you must install and configure the following listed software. For more information on how to install and configure Orchestrator and the Exchange Users Integration Pack, see the respective product documentation.

::: moniker range="<sc-orch-2019"

- System Center 2016 integration packs require System Center 2016 - Orchestrator
- Microsoft .NET Framework 3.5
- Microsoft Exchange 2010 Service Pack 1 or Microsoft Exchange 2013 or Microsoft Exchange
    Online/Microsoft 365

::: moniker-end

::: moniker range=">= sc-orch-2019"
- System Center 2019 integration packs require System Center 2019 - Orchestrator
- System Center 2022 integration packs require System Center 2022 - Orchestrator
- Microsoft .NET Framework 4.7
- Exchange accounts on,
  - (On-premises Exchange Server) Microsoft Exchange 2010 Service Pack 1 or Microsoft Exchange 2013 or
  - (Exchange Online) Microsoft Exchange Online/Microsoft Office 365 Exchange.

::: moniker-end

::: moniker range="=sc-orch-2019"

> [!IMPORTANT]
>
> 1. Exchange User Integration Pack (v10.19.25.0 or above) targets .NET Framework 4.7. Ensure
>    that .NET Framework Runtime v4.7 or later is installed on Runbook Designer and Runbook Server
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

## Download the integration pack

::: moniker range="<=sc-orch-2019"

- To download the Exchange Users Integration Pack for Orchestrator 2016, go to the [Download Center space for 2016](https://www.microsoft.com/download/details.aspx?id=54098).

- To download the Exchange Users Integration Pack for Orchestrator 2019, go to the [Download Center space for 2019](https://www.microsoft.com/download/details.aspx?id=58111&WT.mc_id=rss_alldownloads_all).

::: moniker-end

::: moniker range="sc-orch-2022"

- To download the Exchange Users Integration Pack for Orchestrator 2022, go to the [Download Center space for 2022](https://www.microsoft.com/download/details.aspx?id=104336).

::: moniker-end

::: moniker range="sc-orch-2025"

Exchange Users Integration Pack for Orchestrator 2022 continues to work with Orchestrator 2025.

Download the Exchange Users Integration Pack [here](https://www.microsoft.com/download/details.aspx?id=104336).

::: moniker-end

## Register and deploy the integration pack

Download the integration pack file and register it with the Orchestrator management server using the Deployment Manager. You may then deploy it to runbook servers and Runbook Designers. For procedures on installing integration packs, see [How to Install an Integration Pack](how-to-add-an-integration-pack.md).

::: moniker range=">= sc-orch-2019"

## Configure OAuth

Microsoft Azure Active Directory (Azure AD) implements the OAuth protocol for secure authentication of its users and applications.

### What is an Azure AD client application?

The integration pack requires a [Public Client Application](/azure/active-directory/develop/msal-client-applications) on Azure AD that will operate in *delegated authentication* mode (that is, impersonating the user).

Here's how the connection will be established when the activity runs:

1. User credentials will be obtained from the IP configuration.
2. The credentials will be used to authenticate with Azure AD using OAuth.
3. After authentication, an OAuth token will be received from Azure AD.
4. Activity will perform operations on the EWS endpoint using the OAuth token.

>[!NOTE]
> The alternative of *delegated permissions* is *app-only authentication* where app secrets (credential or secret certificate) are used instead of a user's credentials. The IP doesn't support these kinds of Azure AD applications.

::: moniker-end

::: moniker range=">= sc-orch-2019"

### Register an Azure AD client application in your tenant

1. Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com/).

2. On the **Azure Active Directory admin center** dashboard, select **Azure Active Directory** blade, and the Overview page opens.

3. Under **Manage**, select **App registrations**. The App registrations page opens.

    :::image type="App registrations page" source="media/exchange-users-integration-pack/app-registrations.png" alt-text="Screenshot of App registrations page.":::

4. Select **+ New registration**, and the Register an application page opens.

    :::image type="New registration" source="media/exchange-users-integration-pack/new-registration.png" alt-text="Screenshot of new registration.":::

5. Set the values as below and select **Register**.

    - **Name**: Enter a friendly name for your app.
    - **Supported account types**: Select the Supported account types based on your scenario.
    - **Redirect URI (optional)**: From the **Select a platform** dropdown, select *Public client/native (mobile & desktop)*,  and set the URI to `https://login.microsoftonline.com/common/oauth2/nativeclient`.

      :::image type="registration-form" source="media/exchange-users-integration-pack/registration-form.png" alt-text="Screenshot of registration form.":::

6. In Application overview page, under **Overview** > **Essentials**, copy the **Application (client) ID** and **Directory (tenant) ID**.

    :::image type="Azure AD App overview pane" source="media/exchange-users-integration-pack/app-overview.png" alt-text="Screenshot of Azure AD App overview pane." lightbox="media/exchange-users-integration-pack/app-overview.png":::

7. Select **Authentication**, do the following, and select **Save**.

    1. Ensure that the **Platform configurations** is set to **Mobile and desktop applications** with at least `https://login.microsoftonline.com/common/oauth2/nativeclient` as one of the Redirect URI.

       :::image type="Platform configurations" source="media/exchange-users-integration-pack/auth-platform.png" alt-text="Screenshot of platform configurations.":::

    2. Under **Advanced settings**, ensure **Allow public client flows** is set to **Yes**.
       
       :::image type="Advanced settings" source="media/exchange-users-integration-pack/auth-advanced-settings.png" alt-text="Screenshot of Advanced settings.":::

::: moniker-end

::: moniker range=">= sc-orch-2019"

### Grant EWS permissions

Generally, Public Client Apps that operate in *delegated authentication* mode require explicit consent from the user who wants to use the application. The explicit consent is granted interactively through an embedded browser window.

However, the IP doesn't support the consent grant flow; instead the tenant admin must grant consent on behalf of all users in the tenant.

1. Add the permissions to the app by editing the app **Manifest**.
    1. On the Microsoft Entra admin center, select the Azure AD application.
    2. Follow the [steps to grant EWS permissions](/exchange/client-developer/exchange-web-services/how-to-authenticate-an-ews-application-by-using-oauth#register-your-application) by editing the app **Manifest**.

        :::image type="content" alt-text="Screenshot of Azure AD App manifest."  source="./media/exchange-users-integration-pack/manifest.png" lightbox="./media/exchange-users-integration-pack/manifest.png":::

2. Request your tenant admin to grant "Admin consent" (on the API permissions tab) to this application for `EWS.AccessAsUser.All` permission.

    :::image type="content" alt-text="Screenshot of Azure AD App API permissions."  source="./media/exchange-users-integration-pack/api-permissions.png" lightbox="./media/exchange-users-integration-pack/api-permissions.png":::

In practice, **Admin consent** implies that any user in the tenant can configure the IP with their credentials and execute Exchange activities under their account.

::: moniker-end

## Configure the Exchange Users integration pack connections

A connection describes the recipe to make HTTP requests from Orchestrator to an Exchange server. You can specify as many connections as necessary to create links to multiple servers using different accounts or options. You can also create multiple connections to the same server to allow for differences in security permissions for different user accounts.

The integration pack supports two types of Exchange configurations:

- Basic **Exchange Configuration** connection
- **Exchange Configuration (Item)** configuration

The basic **Exchange Configuration** contains connection information that is used by activities where the item type is either implicit or not required:

- Create and Send E-Mail
- Reply to E-Mail
- Send E-Mail
- Delete Item
- Find Appointments

The **Exchange Configuration (Item)** configuration is used for the remaining activities that operate on a single Exchange Item (an Appointment, Task, Email, or Contact).

### Set up a basic Exchange Configuration connection

1. In the **Orchestrator Runbook Designer**, select **Options**, and then select **Exchange User**. The **Exchange User** dialog appears.

1. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears.

1. In the **Name** box, enter a friendly display name for the connection.

1. In the **Type** box, select **Exchange Configuration**.

1. In the **Exchange Server Address** box, enter the name or IP address of the Exchange server. If you're using the computer name, you can enter the *NetBIOS* name or the fully qualified domain name *(FQDN)*. You may leave the **Exchange Server Address** box empty if you enable the **Use [Autodiscover]**(/exchange/client-developer/exchange-web-services/autodiscover-for-exchange) option.

   >[!NOTE]
   > Usually this is of the form `https://<your-domain-name.com>/EWS/Exchange.asmx`.

1. In the **Username** and **Password** boxes, enter the credentials that Orchestrator will use to connect to the Exchange server.

1. In the **Domain** box, enter the name of the (tenant) domain that will authorize access.

   >[!NOTE]
   > If your email account is of the form `johndoe@contoso.onmicrosoft.com`, then your domain is *contoso.onmicrosoft.com*

::: moniker range=">= sc-orch-2019"

8. Set **Server is Exchange Online or Office365** to `True` if you're connecting to a managed Exchange Online or Office 365 Exchange instance. If so, follow these further steps (ignore otherwise):

    1. In **Azure AD application (client) ID**, specify the Azure AD client app ID created for this purpose.

    2. In **Azure AD Tenant (directory) ID**, specify your Azure AD Tenant ID seen on the AD portal.

    3. In **Azure AD Cloud Instance URL**, enter the URL of your Active directory instance or use the default value. Refer [Azure AD Authority](/azure/active-directory/develop/authentication-national-cloud#azure-ad-authentication-endpoints) to confirm the authentication endpoint.

    4. Set **Log OAuth request/response** to `True` if you wish to inspect authentication failures in detail. The logs will be generated on the path `%windir%\Temp\sc-orchestrator\exchange_user\{date-time-stamp}.msal.txt`. One file will be generated for each execution of an Exchange User activity.

9. Set **Trace EWS request/response** to `True` if you wish to inspect EWS failures in detail. The logs will be generated on the path `%windir%\Temp\sc-orchestrator\exchange_user\{date-time-stamp}.ews-trace.xml.log`. One file will be generated for each execution of an Exchange User activity. We recommend that you use [SOAPe](https://github.com/David-Barrett-MS/SOAPe) to visually inspect the traces.
10. In the **Timeout** box, enter a timeout value or leave the default.
11. Select **OK**.
12. Add any more connections if needed, and then select **Finish**.
::: moniker-end

::: moniker range="<sc-orch-2019"

8. In the **Timeout** box, enter a timeout value or leave the default.
9. Select **OK**.
10. Add any more connections if needed, and then select **Finish**.

::: moniker-end

::: moniker range="<sc-orch-2019"

### Set up an Exchange Configuration (Item) connection

1. In the **Orchestrator Runbook Designer**, select **Options**, and then select **Exchange User**. The **Exchange User** dialog appears.

2. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears.

3. In the **Name** box, enter a friendly display name for the connection.

4. In the Type box, select **Exchange Configuration (Item Activity)**.

5. In the **Exchange Server Address** box, enter the name or IP address of the Exchange server. If you're using the computer name, you can enter the *NetBIOS* name or the fully qualified domain name *(FQDN)*. You may leave the **Exchange Server Address** box empty if you enable the **Use Autodiscover** option.

6. In the **Username** and **Password** boxes, enter the credentials that Orchestrator will use to connect to the Exchange server.

7. In the **Domain** box, enter the name of the domain that will authorize access.

8. In the **Timeout** box, enter a timeout value or leave the default.

9. In the **Item Type** box, enter a valid Exchange Item Type.

10. Add any more connections if applicable, and then select **Finish**.

::: moniker-end

::: moniker range=">= sc-orch-2019"

### Set up an Exchange Configuration (Item) connection

1. In the **Orchestrator Runbook Designer**, select **Options**, and then select **Exchange User**. The **Exchange User** dialog appears.

2. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears.

3. In the **Name** box, enter a friendly display name for the connection.

4. In the Type box, select **Exchange Configuration (Item Activity)**.

5. In the **Item Type**, enter a valid Exchange Item Type.

6. For the remaining parameters, follow the same guidance mentioned above for [basic Exchange Configuration](#set-up-a-basic-exchange-configuration-connection).

::: moniker-end
