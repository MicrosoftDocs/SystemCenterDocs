---
title: Deploy the Service Manager Self-Service portal
description: This article describes prerequisites, installation steps, and configuration options for the Service Manager Self-Service portal.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.subservice: service-manager
ms.topic: install-set-up-deploy
ms.custom: intro-deployment
---

# Deploy the Self-Service portal for Service Manager

The Self-Service portal provides web-based access to the features of System Center - Service Manager for end users. This article describes how you can deploy the Self-Service portal and customize it.

## Supported operating systems

::: moniker range="<sc-sm-2019"
 - Windows Server 2016
 - Windows Server 2012 R2
::: moniker-end

::: moniker range="sc-sm-2019"
 - Windows Server 2019
 - Windows Server 2016
 - Windows Server 2012 R2
 ::: moniker-end

::: moniker range="sc-sm-2022"
 - Windows Server 2022
 - Windows Server 2019
 - Windows Server 2016
 - Windows Server 2012 R2
 ::: moniker-end

::: moniker range="sc-sm-2025"
 - Windows Server 2025
 - Windows Server 2022
 - Windows Server 2019
 - Windows Server 2016
 ::: moniker-end

For more information, see [system requirements](system-requirements.md)

## Supported web browsers

The Self-Service portal needs a screen resolution above 1024 X 768. It's supported on the following browsers.

::: moniker range="sc-sm-2025"
- Microsoft Edge 121.0.2277.4 or later
::: moniker-end

::: moniker range="<=sc-sm-2022"
- Microsoft Edge
::: moniker-end

- Microsoft Internet Explorer 10 and 11

- Mozilla Firefox 42 and later

- Google Chrome 46 and later

## Set up the Self-Service portal

You'll use the following sections to set up the Self-Service portal.

### Set up the web server

Join the Windows server machine to the same domain where the Service Manager SDK Service is running. Ideally, on the secondary server. Enable the IIS role and ASP.NET 4.5 on the server using following steps.

1. Start the Add Roles and Features Wizard and then enable IIS.

    ![Screenshot showing the select server roles.](./media/deploy-self-service-portal/sm-ssp01.png)

2. Enable the .NET features.

    1. Enable .NET 3.5

        ![Screenshot showing the select features.](./media/deploy-self-service-portal/sm-sspdeploy2a.png)

    2. Enable HTTP Activation

        ![Screenshot showing the select HTTP activation.](./media/deploy-self-service-portal/sm-sspdeploy2b.png)

    3. Enable ASP.NET 4.5

        ![Screenshot showing the select ASP.NET 4.5.](./media/deploy-self-service-portal/sm-sspdeploy2c.png)

3. Enable the following role services on the Web Server Role (IIS) page.

    1. **Basic Authentication** and **Windows Authentication**

        ![Screenshot showing the basic authentication and Windows authentication.](./media/deploy-self-service-portal/sm-sspdeploy3a.png)

    2. Add **Application Development** and under it, add **.NET Extensibility 4.5**, **ASP**, and **ASP.NET 4.5**.

        ![Screenshot showing the application development.](./media/deploy-self-service-portal/sm-ssp03b.png)

### Install the Self-Service Portal Webapp using Setup

Use the following steps to install the Self-Service Portal WebApp using Setup.

1. Select **Service Manager Self-Service Portal** in Service Manager setup wizard.

2. Go through the EULA and accept it.

    ![Screenshot showing the EULA.](./media/deploy-self-service-portal/sm-ssp06.png)

3. Choose your installation location.

    ![Screenshot showing the installation location.](./media/deploy-self-service-portal/sm-ssp07.png)

4. Review the System check results.

5. Configure the Self-Service Portal server and enter configuration details for your server.

    - **WebSite Name** : The name of the website to display in the IIS Management console.

    - **SM Server name**: You can provide a fully qualified domain name or the NetBIOS name of the server running the Service Manager SDK service. We recommend that you use a dedicated secondary Service Manager management server to communicate with the portal. For more information, see [Deployment topologies](/system-center/scsm/learn-self-service-portal?#deployment-topologies).

    - **Portal Port**: The port number that the website will use.

    - **SSL Certificate:** (Optional) The SSL certificate to configure the website in secure mode (https://). This is the recommended setting if you're using Basic Authentication. The default is Windows  Authentication.

    ![Screenshot showing the configure the Self-Service Portal server.](./media/deploy-self-service-portal/sm-ssp09.png)

6. Configure the account for the Self-Service Portal. This is the account that the IIS instance will run under. This account should have the Service Manager Admin role.

    ![Screenshot showing the Self-Service portal account.](./media/deploy-self-service-portal/sm-ssp10.png)

7. The Diagnostic and usage data notification information is displayed, informing you that data is sent to Microsoft by default. You can change this setting in the Service Manager console. Select **Next**.

    ![Screenshot showing the diagnostic and usage data.](./media/deploy-self-service-portal/sm-ssp11.png)

8. Choose whether to automatically install Microsoft updates.

    ![Screenshot showing the Microsoft updates.](./media/deploy-self-service-portal/sm-ssp12.png)

9. Wait for installation to complete.

    ![Screenshot showing the Finished page.](./media/deploy-self-service-portal/sm-ssp13.png)

### Install the Self-Service portal webapp using the command line

You can modify the following example to install the Self-Service portal.

```
SetupWizard.exe /Install:SelfServicePortal /silent /accepteula /CustomerExperienceImprovementProgram:No /EnableErrorReporting:No /PortalWebSiteName:<Portal Name> /SMServerName:<SDK Server Name> /PortalWebSitePort:<PortNumber> /PortalAccount:<domain>\<user>\<pwd>
```

### Complete the installation

Use the following step to complete your installation.

- Restart IIS. You can access the Web App (http://yourwebsite:port) in your browser. It will resemble the following image.

  ![Screenshot showing the Self-Service Portal.](./media/deploy-self-service-portal/sm-sspdeploy-complete.png)

## Customize the Self-Service portal

The following section describes how you can customize the Self-Service portal to suit your organization.

Before you install any Update Rollup for Service Manager, note that all customizations are made in the portal sidebar (CustomSidebar.cshtml). Then use the following steps to get started.

1. Create a new cshtml file named CustomSidebar.cshtml in the &lt;Self-Service Portal install path&gt;\inetpub\wwwroot\SelfServicePortal\Views\Shared folder path.
2. Move your customizations from sidebar.cshtml to the new file, which is CustomSidebar.cshtml.

In the future, you need to make all customizations to the Service Manager Self-Service portal’s sidebar in the CustomSidebar.cshtml file.

### Basic customization

The `<appSettings>` tab in the Web.config file offers some standard settings to easily customize and personalize the areas that are most often modified. Here's a list of them.

| Key | Purpose |
| ------- | ----------- |
|CompanyName|The value of this key appears as the company's name inside the portal.|
|CompanyLogoLocation|The value of this key is used as the image file, which is displayed as the company's logo inside the portal.|
|ITPhone|This key takes the value to configure the IT help desk's phone number. This information appears at the bottom of the navigation menu.|
|ITEmail|The value of this key is used to configure the IT help desk's email ID. This information appears at the bottom of the navigation menu.|
|DefaultLanguage|By default, the Portal web pages are loaded as defined by the browser's language. Then current user can manually select the language in the top-right corner of each page.<br />The value of this key defines the default failover language, which is chosen by the portal when the browser's language isn't available.|
|GenericOffering|The value of this key accepts the name of the request offering, which is mapped to the generic request button. This generic request button is used by the user, when they can't find an appropriate request offering in the catalog.|
|SDKServerName|The value of this key defines the name of the server where the Service Manager SDK runs, and it's used to interact with other Service Manager servers. By default, it has the same value that you provided in Setup.<br />You can use the fully qualified domain name or the NetBIOS name of the server running the Service Manager SDK service. We recommend that you dedicate a secondary Service Manager management server to communicate with the portal.|
|MaxQueryResults|The value of this key defines the maximum number of results that are returned by any query form element inside your request offering forms.|
|UserCacheTimeout|The Portal uses a caching infrastructure to provide a swift user experience. The value of this key defines the timeout, in seconds, to cache user-specific details of the signed-in user.|
|DataCacheTimeout|The Portal uses a caching infrastructure to provide a swift user experience. The value of this key defines the timeout, in seconds, to cache generic data which can be shared among different users.|
|EnableTelemetry|The value of this key defines your selection about participating in Microsoft's Customer Experience Improvement Program. Your portal sends usage telemetry data to Microsoft when this key is marked as **True**. By default, it has the same value that you chose during Setup.|
|CustomActiveRequestStatusEnumList|By default, the Self Service portal puts custom enumerations for My Request (incident and service requests) states in the *Closed* filter category. This key allows customization to map required custom states to the *Active* filter category. The value of this key should be a comma separated list containing *EnumTypeName* values of enumerations which are required to be mapped with the Active category in the Self Service Portal. You can look for desired custom states labeled *EnumTypeName* in the *EnumType* table, using the following example. </br></br> `SELECT [EnumTypeName]` </br></br> `FROM [<Service Manager DB name, which by default is “ServiceManager”>].[dbo].[EnumType]`|

> [!NOTE]
> You must restart the IIS service after you make any changes to the Web.config file.

### Style customization

Web page style, such as font, color, and background, is customized by adding the Custom.css file in the \Content\css website folder.

Styles defined in the CSS file override the default styles of the Self-Service Portal.

### Customizing the left menu bar

You can modify the content shown in the left navigation bar (menu) by editing the Sidebar.cshtml file, which is in the \Views\Shared inside the website folder.

For example:

![Screenshot showing the sidebar.cshtml.](./media/deploy-self-service-portal/sm-sspsidebar.png)

You can add or remove shortcuts from the menu, and you can customize them with details for the CSS class, keyboard hotkeys, and others.

## Next steps

- To configure Windows Server Network Load Balancing with Service Manager, review [Guidance for load balancing](load-balancing.md).
