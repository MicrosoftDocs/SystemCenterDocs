---
ms.assetid: 
title: Create a user assigned identity
description: This article describes how to create a user assigned identity, provide admin access to SQL MI, and grant get and list access on key-vault.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 08/16/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create a user assigned identity

This article describes how to create a user assigned identity, provide admin access to SQL MI, and grant *get and list access* on key-vault.

## Create a managed service identity

The managed service identity (MSI) provides an identity for applications to use when they're connecting to resources that support Azure Active Directory (Azure AD) authentication. For SCOM Managed Instance (preview), a managed identity replaces the traditional four System Center Operations Manager service accounts. It is used to access the Azure SQL Managed Instance database. You can also use the MSI to access the key vault.

>[!Note]
>- Ensure that you're a contributor in the subscription where you create the MSI.
>- The MSI must have admin permission on Azure SQL Managed Instance and read permission on the key vault that you use for domain account credentials.

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

>[!Important]
>To minimize the need for extensive communication with both your Active Directory admin and Network Admin, review  [**Self-verification**](/system-center/scom/scom-mi-self-verification-of-steps?view=sc-om-2022). The outlines the procedures through which the AD admin and network admin validate their configuration changes and ensure their successful implementation; thus, reducing unnecessary back-and-forth interactions with Operations Manager admin time.

## Next steps

- [Create gMSA account](create-gmsa-account.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
