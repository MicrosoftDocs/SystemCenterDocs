---
ms.assetid: f27d87a8-d387-4648-a0b9-848a74429538
title: Automatic monitoring template in Management Pack for Azure SQL Managed Instance
description: This article explains how to configure automatic monitoring template with Managed Identity in Management Pack for Azure SQL Managed Instance.
author: fkornilov
ms.author: v-fkornilov
manager: evansma
ms.date: 06/28/2024
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
---

# Automatic monitoring template with Managed Identity

Automatic monitoring template allows you to configure monitoring by discovering all managed instances in the specified Azure subscription automatically. This article describes the automatic monitoring template using the Managed Identity options of choice: system-assigned managed identity and user-assigned managed identity.

## System-assigned managed identity

### Prerequisites

1. Enable system-assigned managed identity for management server VM in Azure Portal.

   Go to the Virtual Machine -> Security -> Identity.

   Switch **System-assigned status** to **On** and click **Save**.

   For more details, got to [Configure managed identities on Azure virtual machines](/entra/identity/managed-identities-azure-resources/how-to-configure-managed-identities?pivots=qs-configure-portal-windows-vm#system-assigned-managed-identity)

2. Grant Reader permission to the system-assigned identity for the subscription or specific resource group where your System Center Operations Manager and Azure SQL Managed Instances reside.

    Go to subscription or resource group -> **Access Control (IAM)** and click **Add**.

    Click **Add Role-assignment** and Select **Reader** permission in the Role tab.

    Assign-access to the managed identity in the Member tab and select your identity by name.

    Save the updates by clicking **Review + assign** button.

   For more details, check the [Adding permissions to the identity](/entra/identity/managed-identities-azure-resources/overview-for-developers?tabs=portal%2Cdotnet#adding-permissions-to-the-identity)

### Add Monitoring Wizard and create a destination management pack

To configure monitoring using the automatic monitoring template, perform the following steps:

1. In the System Center Operations Manager console, navigate to **Authoring | Management Pack Templates**, right-click **Azure SQL MI - Automatic**, and select **Add Monitoring Wizard**.

    ![Screenshot showing the Run Add Monitoring Wizard.](./media/managed-instance-management-pack/running-monitoring-wizard.png)

2. At the **Monitoring Type** step, select **Azure SQL MI - Automatic**, and select **Next**.

    ![Screenshot showing the Select monitoring type.](./media/managed-instance-management-pack/selecting-monitoring-type-mi.png)

3. At the **General Properties** step, enter a name and description, and from the **Select destination management pack** dropdown list, select a management pack that you want to use to store the template.

    ![Screenshot showing the Select destination management pack.](./media/managed-instance-management-pack/destination-management-pack-mi.png)

### Azure endpoints

At this step, select the **Enable checkbox if you want to change default Azure Endpoints** checkbox, and modify the default Azure endpoints, if necessary. The default endpoints for creating Azure Service Principal Name are as follows:

- Authority URI: `https://login.microsoftonline.com`
- Management Service URI: `https://management.azure.com`
- Database Resource URI: `https://database.windows.net`  
- Graph API Resource URI: `https://graph.windows.net`

![Screenshot showing the Configure Azure endpoints.](./media/managed-instance-management-pack/configuring-azure-endpoints-mi.png)

### Select Authentication Method

At this step, select a system-assigned managed identity from the list. This means that your management server will use the system-assigned identity from its VM to connect to the Azure SQL Managed Instance.

![Screenshot of selecting system-assigned managed identity](./media/managed-instance-management-pack/mis-selecting-authentication-method.png)

### SQL connection settings

At this step, select an authentication method that you want to use to connect to your managed instances.

There are two options:

- **Microsoft Entra ID**. Azure SQL Managed Instance must have enabled Entra ID Admin for this connection.
  
  Go to Azure SQL Managed Instance in Azure Portal -> Settings -> Microsoft Entra ID.

  Click **Set Admin** and specify an account. Save changes.

  Grant permissions for the Azure SQL Managed Instance to access Entra ID.

  > [!WARNING]
  > You need to be a Company Administrator or Global Administrator to Grant Read permission to the principal that represents Managed Instance identity.

- **SQL Credentials**. Create a new Run As account by selecting **New** and specifying an account name and connection credentials to access the managed instance.

    ![Screenshot showing the Configure Run As account for Automatic template.](./media/managed-instance-management-pack/mis-new-run-as-account-automatic-template.png)

![Screenshot showing the Configure SQL connection settings for SMI.](./media/managed-instance-management-pack/mis-sql-connection-settings.png)

> [!IMPORTANT]
> The public endpoint is the default option for discovery and monitoring Managed Instances. Make sure that you have the appropriate security options configured for the connection. The private endpoint is also supported.

### Instances filtering

[Optionally] At the **Configure Instances Filtering** step, select filtering mode, which can be either **Exclude** or **Include**, and select filtering masks type, which can be either **Wildcard** or **Regular Expression**, enter filtering masks that should match Managed Instance names that you want to exclude from or include to the monitoring list, select **Add**, then select **Next**.

**Wildcard** filtering mask type can contain a server name only lowercase letters, numbers, and the '-' character, but can't start from or end with the '\\' character or contain more than 63 characters. A server exclude list filter mask ignores whitespaces.

![Screenshot of the server exclude list wildcard SPN.](./media/managed-instance-management-pack/mis-configure-instances-filtering.png)

**Regular Expression** filtering mask type supports [.NET regular expressions patterns](/dotnet/standard/base-types/regular-expressions).

If you want to remove an existing mask, select it and select **Delete**.

### Management pool

At this step, specify the Management Server pool which will be used for discovery and monitoring purposes. For more information, see [Azure SQL Managed Instance Monitoring Pool](managed-instance-management-pack-monitoring-pool.md).

![Screenshot showing the Management Pool settings.](./media/managed-instance-management-pack/miu-choose-management-pool.png)

Confirm Run As account distribution to the selected management pool by completing the Summary step.

![Screenshot showing the RunAS account modification confirmation.](./media/managed-instance-management-pack/allowing-runas-modification.png)

### Summary

At this step, review all the configuration and connection settings and select **Create**.

![Screenshot showing the Review connection settings for SMI.](./media/managed-instance-management-pack/mis-review-connection-settings.png)

## User-assigned managed identity

### Prerequisites

1. Create user-assigned managed identity in Azure Portal

   Go to **Managed Identities** -> **Create** -> Specify the information and click **Review + Create**.

   For more details, got to [Creating a user-assigned managed identity](/entra/identity/managed-identities-azure-resources/overview-for-developers?tabs=portal%2Cdotnet#creating-a-user-assigned-managed-identity)

2. Assign identity to virtual machine with Management Server.

   Go to specified VM -> **Security** -> **Identity**.

   Click **Add** and select created user-assigned identity. Save the changes.

3. Grant Reader permission to the user-assigned identity for the subscription or specific resource group where your System Center Operations Manager and Azure SQL Managed Instances reside.

    Go to subscription or resource group -> **Access Control (IAM)** and click **Add**.

    Click **Add Role-assignment** and Select **Reader** permission in the Role tab.

    Assign-access to the managed identity in the Member tab and select your identity by the name.

    Save changes by clicking **Review + assign** button.

   For more details, check the [Adding permissions to the identity](/entra/identity/managed-identities-azure-resources/overview-for-developers?tabs=portal%2Cdotnet#adding-permissions-to-the-identity)

### Add Monitoring Wizard and create a destination management pack

To configure monitoring using the automatic monitoring template, perform the following steps:

1. In the System Center Operations Manager console, navigate to **Authoring | Management Pack Templates**, right-click **Azure SQL MI - Automatic**, and select **Add Monitoring Wizard**.

    ![Screenshot showing the Run Add Monitoring Wizard.](./media/managed-instance-management-pack/running-monitoring-wizard.png)

2. At the **Monitoring Type** step, select **Azure SQL MI - Automatic**, and select **Next**.

    ![Screenshot showing the Select monitoring type.](./media/managed-instance-management-pack/selecting-monitoring-type-mi.png)

3. At the **General Properties** step, enter a name and description, and from the **Select destination management pack** dropdown list, select a management pack that you want to use to store the template.

    ![Screenshot showing the Select destination management pack.](./media/managed-instance-management-pack/destination-management-pack-mi.png)

### Azure endpoints

At this step, select the **Enable checkbox if you want to change default Azure Endpoints** checkbox, and modify the default Azure endpoints, if necessary. The default endpoints for creating Azure Service Principal Name are as follows:

- Authority URI: `https://login.microsoftonline.com`
- Management Service URI: `https://management.azure.com`
- Database Resource URI: `https://database.windows.net`  
- Graph API Resource URI: `https://graph.windows.net`

![Screenshot showing the Configure Azure endpoints.](./media/managed-instance-management-pack/configuring-azure-endpoints-mi.png)

### Select Authentication Method

At this step, select user-assigned managed identity in the list. It means your management server will use user-assigned identity from its VM to connect to Azure SQL Managed Instance.

![Screenshot of selecting user-assigned managed identity](./media/managed-instance-management-pack/miu-selecting-authentication-method.png)

### Set Azure Run As Account

Create a new Run As account by selecting **New** and specifying an account name and user-assigned client ID to access the managed instance with managed identity.

![Screenshot showing the Manual SPN Configuration.](./media/managed-instance-management-pack/miu-new-run-as-account.png)

Once you've created the Run As Account associated with the managed identity, select it from the drop-down list, then select **Next**. This Run As Account will be used for authentication in Azure Cloud.

![Screenshot showing the existing Run As profile.](./media/managed-instance-management-pack/miu-existing-run-as-profile.png)

Next time you can just use created Run As Account with the user-assigned managed identity to fill in the new automatic monitoring template.

### SQL connection settings

At this step, select an authentication method that you want to use to connect to your managed instances.

There are two options:

- **Microsoft Entra ID**. Azure SQL Managed Instance must have enabled Entra ID Admin for this connection.
  
  Go to Azure SQL Managed Instance in Azure Portal -> Settings -> Microsoft Entra ID.

  Click **Set Admin** and specify an account. Save changes.

  Grant permissions for the Azure SQL Managed Instance to access Entra ID.

  > [!WARNING]
  > You need to be a Company Administrator or Global Administrator to Grant Read permission to the principal that represents Managed Instance identity.

- **SQL Credentials**. Create a new Run As account by selecting **New** and specifying an account name and connection credentials to access the managed instance.

![Screenshot showing the Configure SQL connection settings for UMI.](./media/managed-instance-management-pack/miu-sql-connection-settings.png)

> [!IMPORTANT]
> The public endpoint is the default option for discovery and monitoring Managed Instances. Make sure that you have the appropriate security options configured for the connection. The private endpoint is also supported.

### Instances filtering

[Optionally] At the **Configure Instances Filtering** step, select filtering mode, which can be either **Exclude** or **Include**, and select filtering masks type, which can be either **Wildcard** or **Regular Expression**, enter filtering masks that should match Managed Instance names that you want to exclude from or include to the monitoring list, select **Add**, then select **Next**.

**Wildcard** filtering mask type can contain a server name only lowercase letters, numbers, and the '-' character, but can't start from or end with the '\\' character or contain more than 63 characters. A server exclude list filter mask ignores whitespaces.

**Regular Expression** filtering mask type supports [.NET regular expressions patterns](/dotnet/standard/base-types/regular-expressions).

![Screenshot of the server exclude list regular expression SPN.](./media/managed-instance-management-pack/miu-configure-instances-filtering.png)

If you want to remove an existing mask, select it and select **Delete**.

### Management pool

At this step, specify the Management Server pool which will be used for discovery and monitoring purposes. For more information, see [Azure SQL Managed Instance Monitoring Pool](managed-instance-management-pack-monitoring-pool.md).

![Screenshot showing the Management Pool settings.](./media/managed-instance-management-pack/miu-choose-management-pool.png)

Confirm Run As account distribution to the selected management pool by completing the Summary step.

![Screenshot showing the RunAS account modification confirmation.](./media/managed-instance-management-pack/allowing-runas-modification.png)

### Summary

At this step, review all the configuration and connection settings and select **Create**.

![Screenshot showing the Review connection settings for UMI.](./media/managed-instance-management-pack/miu-review-connection-settings.png)