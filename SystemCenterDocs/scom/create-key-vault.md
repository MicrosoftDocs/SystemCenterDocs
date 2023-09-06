---
ms.assetid: 
title: Create a Key vault
description: This article describes how to create a Key vault.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 09/06/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create a Key vault

This article describes how to create a key vault to store the domain credentials.

>[!Note]
> To know about the SCOM Managed Instance (preview) Architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

## Create a key vault to store the secrets

For security, you can store the domain account credentials in a key vault secrets; Later, you can use these secrets in SCOM Managed Instance creation.

Azure Key Vault is a cloud service that provides a secure store for keys, secrets, and certificates. For more information, see [About Azure Key Vault](/azure/key-vault/general/overview).

1. In the Azure portal, search for and select **Key vaults**.

     :::image type="Key vaults in portal" source="media/create-key-vault/azure-portal-key-vaults-inline.png" alt-text="Screenshot of the icon for key vaults in the Azure portal." lightbox="media/create-key-vault/azure-portal-key-vaults-expanded.png":::

   The **Key vaults** page opens.

1. Select **+ Create**.

     :::image type="Key vault" source="media/create-key-vault/key-vaults-inline.png" alt-text="Screenshot of the button for creating a key vault." lightbox="media/create-key-vault/key-vaults-expanded.png":::

1. For **Basics**, do the following:
    - **Project details**:
        - **Subscription**: Select the subscription.
        - **Resource group**: Select the desired resource group.
    - **Instance details**:
        - **Key vault name**: Enter the name of your key vault. There are no added restrictions, except for those that apply to names in other Azure services.
        - **Region**: Choose the region that you're going to select for your other resources.
        - **Pricing tier**: Select **Standard** or **Premium** as required.
    - **Recovery options**:
        - **Days to retain deleted vaults**: Enter a value from 7 to 90.
        - **Purge protection**: We recommend enabling this feature to have a mandatory retention period.

   :::image type="Create a key vault" source="media/create-key-vault/create-a-key-vault.png" alt-text="Screenshot of basic information for creating a key vault.":::
1. Select **Next**. For now, no change is required in access configuration, access configuration will be done in the [step5](create-user-assigned-identity.md).

1. For **Networking**, do the following:
    - Select **Enable public access**.
    - Under **Public Access**, for **Allow access from**, select **All networks**.

   :::image type="Networking tab" source="media/create-key-vault/networking-inline.png" alt-text="Screenshot of selections for enabling public access on the Networking tab." lightbox="media/create-key-vault/networking-expanded.png":::
1. Select **Next**.
1. For **Tags**, select the tags if required, and then select **Next**.
1. For **Review + create**, review the selections, and then select **Create** to create the key vault.
  
    :::image type="Tab for reviewing selections before creating a key vault" source="media/create-key-vault/review.png" alt-text="Screenshot of the tab for reviewing selections before creating a key vault.":::

## Next steps

- [Create a user assigned identity](create-user-assigned-identity.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
