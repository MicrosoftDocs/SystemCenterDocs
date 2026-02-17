---
ms.assetid: f27d87a8-d387-4648-a0b9-848a74429538
title: Automatic monitoring template in Management Pack for Azure SQL Managed Instance using service principal name
description: This article explains how to configure automatic monitoring template with Service Principal Name in Management Pack for Azure SQL Managed Instance.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Automatic monitoring template with Service Principal Name

Automatic monitoring template allows to configure monitoring by discovering all Azure SQL Managed Instances in the specified Azure subscription automatically. This article describes the automatic monitoring template creation using Service Principal Name (SPN). 

The Azure SQL Managed Instance management pack creates an SPN with the required permissions for the selected subscription when the automated template is populated.

The permission for a manually created SPN must be assigned using Azure Portal. For more information, see [Assign a role to the application](managed-instance-management-pack-service-principal.md#assign-a-role-to-the-application).

## Add Monitoring Wizard and create a destination management pack

To configure monitoring using the automatic monitoring template, perform the following steps:

1. In the System Center Operations Manager console, navigate to **Authoring | Management Pack Templates**, right-click **Azure SQL MI - Automatic**, and select **Add Monitoring Wizard**.

    ![Screenshot showing the Run Add Monitoring Wizard.](./media/managed-instance-management-pack/running-monitoring-wizard.png)

2. At the **Monitoring Type** step, select **Azure SQL MI - Automatic**, and select **Next**.

    ![Screenshot showing the Select monitoring type.](./media/managed-instance-management-pack/selecting-monitoring-type.png)

3. At the **General Properties** step, enter a name and description, and from the **Select destination management pack** dropdown list, select a management pack that you want to use to store the template.

    ![Screenshot showing the Select destination management pack.](./media/managed-instance-management-pack/destination-management-pack.png)

## Azure endpoints

At this step, select the **Enable checkbox if you want to change default Azure Endpoints** checkbox, and modify the default Azure endpoints, if necessary. The default endpoints for creating Azure Service Principal Name are as follows:

- Authority URI: `https://login.microsoftonline.com`
- Management Service URI: `https://management.azure.com`
- Database Resource URI: `https://database.windows.net`  
- Graph API Resource URI: `https://graph.windows.net`

![Screenshot showing the Configure Azure endpoints.](./media/managed-instance-management-pack/configuring-azure-endpoints.png)

## SPN configuration

At this step, select the configuration option that corresponds to authentication in Azure Cloud.

### Auto-create SPN

Select this option if you want your Azure Service Principal Name to be created automatically by the Azure SQL MI MP library using the Azure REST API.

Ensure that the account that you use must have either the **Owner** role (or higher), **Active Directory Administrator**, **Service Administrator**, or **Сo-Administrator**.

Select an expiration date for the new application client secret based on your corporate policy, then select **Next**.

![Screenshot showing the Automatic Configuring SPN.](./media/managed-instance-management-pack/spn-configuration.png)

If you select the **Auto-Create SPN** option, the **Microsoft Azure sign-in** window will be displayed. In this window, enter your work, school, or personal Microsoft account credentials, select **Next**, and complete the form.

![Screenshot showing the Auto-create SPN.](./media/managed-instance-management-pack/auto-create-spn.png)

Specify the desired Microsoft Entra ID tenant with a specific SQL Managed Instance.

![Screenshot showing step with selecting Azure tenant.](./media/managed-instance-management-pack/selecting-tenant-id.png)

Upon the successful creation of the Azure AD application, at the **Auto-Create SPN Status** step, authentication data will be displayed.

> [!TIP]
> This information is available only once. Ensure to save this information to a secure location for reuse.

![Screenshot showing the SPN status.](./media/managed-instance-management-pack/auto-create-spn-status.png)

### Use existing Run As profile

If you want to use your own Azure Service Principal Name, at the **SPN Configuration** step, select the **Use Existing Run As Profile** option, then select **Next**.

![Screenshot showing the Manual SPN Configuration.](./media/managed-instance-management-pack/use-existing-runas.png)

For more information on how to create a Microsoft Entra application and service principal that can access resources, see [Create a Service Principal](managed-instance-management-pack-service-principal.md).

Once you've created the Run As Account associated with the Azure service principal name, select it from the drop-down list, then select **Next**. This Run As Account will be used for authentication in Azure Cloud.

![Screenshot showing the existing Run As profile.](./media/managed-instance-management-pack/set-runas-account-manual.png)

## Subscription permissions

At this step, select the Azure subscriptions that you want to monitor, multiple subscriptions select is also supported.

![Screenshot showing the Configure subscription permissions.](./media/managed-instance-management-pack/subscription-permissions.png)

## SQL connection settings

At this step, select an authentication method that you want to use to connect to your SQL Managed Instances.

> [!IMPORTANT]
> The public endpoint is the default option for discovery and monitoring Managed Instances. Make sure that you have the appropriate security options configured for the connection. The private endpoint is also supported.

You can also create a new Run As account by selecting **New** and specifying an account name and connection credentials to access the SQL Managed Instance.

![Screenshot showing the Configure Run As account for Automatic template.](./media/managed-instance-management-pack/new-run-as-account-automatic-template.png)

Regardless of the selected option, ensure to grant required SQL permissions to the selected monitoring account for all the SQL Managed Instances. For more information, see [Security Configuration](managed-instance-management-pack-security-configuration.md).

![Screenshot showing the Configure SQL connection settings.](./media/managed-instance-management-pack/sql-connection-settings.png)

## Instances filtering

[Optionally] At the **Configure Instances Filtering** step, select filtering mode, which can be either **Exclude** or **Include**, and select filtering masks type, which can be either **Wildcard** or **Regular Expression**, enter filtering masks that should match SQL Managed Instance names that you want to exclude from or include to the monitoring list, select **Add**, then select **Next**.

**Wildcard** filtering mask type can contain a server name only lowercase letters, numbers, and the '-' character, but can't start from or end with the '\\' character or contain more than 63 characters. A server exclude list filter mask ignores whitespaces.

![Screenshot of the server exclude list wildcard SPN.](./media/managed-instance-management-pack/configure-instances-filtering-wildcard.png)

**Regular Expression** filtering mask type supports [.NET regular expressions patterns](/dotnet/standard/base-types/regular-expressions).

![Screenshot of the server exclude list regular expression SPN.](./media/managed-instance-management-pack/configure-instances-filtering-regex.png)

If you want to remove an existing mask, select it and select **Delete**.

## Management pool

At this step, specify the Management Server pool which will be used for discovery and monitoring purposes. For more information, see [Azure SQL Managed Instance Monitoring Pool](managed-instance-management-pack-monitoring-pool.md).

![Screenshot showing the Management Pool settings.](./media/managed-instance-management-pack/choose-management-pool.png)

Confirm Run As account distribution to the selected management pool by completing the Summary step.

![Screenshot showing the RunAS account modification confirmation.](./media/managed-instance-management-pack/allowing-runas-modification.png)

## Summary

At this step, review all the configuration and connection settings and select **Create**.

![Screenshot showing the Review connection settings.](./media/managed-instance-management-pack/review-connection-settings.png)
