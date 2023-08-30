---
ms.assetid: 
title: Create a user assigned identity
description: This article describes how to create a user assigned identity, provide admin access to SQL MI, and grant get and list access on key-vault.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 08/28/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create a user assigned identity

This article describes how to create a user assigned identity, provide admin access to SQL MI, and grant *get and list access* on key-vault.

>[!Note]
> To know about the SCOM Managed Instance (preview) Architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

## Create a managed service identity

The managed service identity (MSI) provides an identity for applications to use when they're connecting to resources that support Azure Active Directory (Azure AD) authentication. For SCOM Managed Instance (preview), a managed identity replaces the traditional four System Center Operations Manager service accounts. It's used to access the Azure SQL Managed Instance database. It's also used to access the key vault.

>[!Note]
>- Ensure that you're a contributor in the subscription where you create the MSI.
>- The MSI must have admin permission on Azure SQL Managed Instance and read permission on the key vault that you use to store the domain account credentials.

1. Sign in to the [Azure portal](https://portal.azure.com). Search for and select **Managed Identities**.

   :::image type="Managed Identity in Azure portal" source="media/create-user-assigned-identity/azure-portal-managed-identity.png" alt-text="Screenshot of the icon for managed identities in the Azure portal.":::
1. On the **Managed Identities** page, select **+ Create**.

   :::image type="Managed Identity" source="media/create-user-assigned-identity/managed-identities.png" alt-text="Screenshot of Managed Identity.":::

   The **Create User Assigned Managed Identity** pane opens.
1. Under **Basics**, do the following:
    - **Project details**:
        - **Subscription**: Select the Azure subscription in which you want to create the SCOM managed instance.
        - **Resource group**: Select the resource group in which you want to create the SCOM managed instance.
    - **Instance details**:
        - **Region**: Select the region in which you want to create the SCOM managed instance.
        - **Name**: Enter a name for the instance.

    :::image type="Create user assigned managed identity" source="media/create-user-assigned-identity/create-user-assigned-managed-identity.png" alt-text="Screenshot of project and instance details for a user-assigned managed identity.":::
1. Select **Next : Tags >**.
1. Under **Tags**, enter the **Name** value, and then select the resource.

   Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see [Use tags to organize your Azure resources and management hierarchy](/azure/azure-resource-manager/management/tag-resources?wt.mc_id=azuremachinelearning_inproduct_portal_utilities-tags-tab&tabs=json).
1. Select **Next : Review + Create >**.
1. Under **Review + create**, review all the information that you provided, and then select **Create**.

   :::image type="Managed identity review" source="media/create-user-assigned-identity/managed-identity-review.png" alt-text="Screenshot of the tab for reviewing a managed identity before creation.":::

Your deployment is now created on Azure. You can access the resource and view its details.

### Set the Active Directory admin value in the SQL managed instance

To set the Active Directory admin value in the SQL managed instance created in [Step3](create-sql-mi.md), follow these steps:

>[!Note]
>You must have Global Administrator or Privileged Role Administrator permissions for the subscription to perform the following operations.

1. Open the SQL managed instance. Under **Settings**, select **Active Directory admin**.

   :::image type="Active directory admin" source="media/create-user-assigned-identity/active-directory-admin.png" alt-text="Screenshot of the pane for Active Directory admin information.":::

2. Select **Set admin**, and search for your MSI. This is the same MSI that you provided during the SCOM Managed Instance (preview) creation flow. You find the admin added to the SQL managed instance.

   :::image type="Azure Active directory admin" source="media/create-user-assigned-identity/azure-active-directory.png" alt-text="Screenshot of MSI information for Azure Active Directory.":::

3. If you get an error after you add a managed identity account, it indicates that read permissions aren't yet provided to your identity. Be sure to provide the necessary permissions before you create your SCOM Managed Instance, else your SCOM Managed Instance creation fails.

   :::image type="SQL Active directory admin" source="media/create-user-assigned-identity/sql-active-directory-admin.png" alt-text="Screenshot that shows successful Active Directory authentication.":::

For more information about permissions, see [Directory Readers role in Azure Active Directory for Azure SQL](/azure/azure-sql/database/authentication-aad-directory-readers-role?view=azuresql&preserve-view=true).

## Grant permission on the key vault

To grant permission on the key vault created in [Step4](create-key-vault.md), follow these steps:

1. Go to the Key vault resource created in [step4](create-key-vault.md) and select **Access policies**.

2. On the **Access policies** page, select **Create**.

    :::image type="Access Policies" source="media/create-user-assigned-identity/access-policies.png" alt-text="Screenshot that shows Access Policies page.":::

3. Under **Permissions** tab, select **Get** and **List** options.

    :::image type="Create Access policy" source="media/create-user-assigned-identity/create-access-policy.png" alt-text="Screenshot that shows create access policy page.":::

4. Select **Next**.

5. Under **Principal** tab, enter the name of the MSI created above.

6. Select **Next**. Select the same MSI that you used in Azure SQL Managed Instance admin configuration.

    :::image type="Principal tab" source="media/create-user-assigned-identity/principal.png" alt-text="Screenshot that shows Principal tab.":::

7. Select **Next** and then select **Create**.

## Next steps

- [Create gMSA account](create-gmsa-account.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
