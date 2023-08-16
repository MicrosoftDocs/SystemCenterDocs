---
ms.assetid: 
title: Create a Key vault
description: This article describes how to create a key vault.
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

# Create a Key vault

This article describes how to create a key vault to store the domain credentials.

## Create a key vault and add credentials as a secret in the key vault  

For security, you can store the domain account (which you created previously in Active Directory) in a key vault.

Azure Key Vault is a cloud service that provides a secure store for keys, secrets, and certificates. For more information, see [About Azure Key Vault](/azure/key-vault/general/overview).

>[!Note]
> You must have Global Administrator or Privileged Role Administrator permissions for the tenant to do the following steps.

1. In the Azure portal, search for and select **Key vaults**.

     :::image type="Key vaults in portal" source="media/create-operations-manager-managed-instance/azure-portal-key-vaults.png" alt-text="Screenshot of the icon for key vaults in the Azure portal.":::

   The **Key vaults** page opens.

1. Select **+ Create**.

     :::image type="Key vault" source="media/create-operations-manager-managed-instance/key-vaults.png" alt-text="Screenshot of the button for creating a key vault.":::

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

   :::image type="create a key vault" source="media/create-operations-manager-managed-instance/create-a-key-vault.png" alt-text="Screenshot of basic information for creating a key vault.":::
1. Select **Next**.
1. For **Access Policy**, do the following:
    - **Access configuration**: Select **Vault access policy**.
    - **Resource access**: Don't select any of the options.
    - **Access policies**: Select **+ Create** to create a new access policy.

      :::image type="Access policies" source="media/create-operations-manager-managed-instance/access-policies.png" alt-text="Screenshot of the button for creating an access policy.":::

      The **Create an access policy** page opens on the right pane.

      1. For **Permissions**, under **Secret permissions**, select **Get** and **List**.

         :::image type="Create an Access policy" source="media/create-operations-manager-managed-instance/create-an-access-policy.png" alt-text="Screenshot of checkboxes for get and list permissions.":::
      1. Select **Next**.
      1. For **Principal**, select the same MSI that you used in Azure SQL Managed Instance admin configuration.

      1. For **Review + create**, review the selections, and then select **Create**.
1. Select the access policy that you created, and then select **Next**.

     :::image type="Access policy" source="media/create-operations-manager-managed-instance/access-policy.png" alt-text="Screenshot of a selected access policy.":::
1. For **Networking**, do the following:
    - Select **Enable public access**.
    - Under **Public Access**, for **Allow access from**, select **All networks**.

   :::image type="Networking tab" source="media/create-operations-manager-managed-instance/networking-inline.png" alt-text="Screenshot of selections for enabling public access on the Networking tab." lightbox="media/create-operations-manager-managed-instance/networking-expanded.png":::
1. Select **Next**.
1. For **Tags**, select the tags if required, and then select **Next**.
1. For **Review + create**, review the selections, and then select **Create** to create the key vault.
  
    :::image type="content" source="media/create-operations-manager-managed-instance/review-inline.png" alt-text="Screenshot of the tab for reviewing selections before creating a key vault." lightbox="media/create-operations-manager-managed-instance/review-expanded.png":::

1. On the left pane, under **Objects**, select **Secrets**.

    :::image type="content" source="./media/create-operations-manager-managed-instance/secrets-inline.png" alt-text="Screenshot of the pane for secrets." lightbox="./media/create-operations-manager-managed-instance/secrets-expanded.png":::

     >[!Note]
     > You must create two secrets to store the domain account credentials: 
     > - Username
     > - Password

1. Select **+ Generate/Import**.

1. On the **Create a secret** page, do the following:
    - **Upload options**: Select **Manual**.
    - **Name**: Enter the name of the secret. For example, you can use *Username* for the username secret and *Password* for the password secret.
    - **Secret value**: For the username value (in the format *domain\username*), enter the domain account username. For the password value, enter the domain account password. For example, if the domain is *contoso.com*, the username should be in the format *contoso\username*.

       :::image type="Secrets" source="media/create-operations-manager-managed-instance/create-a-secret-username.png" alt-text="Screenshot of entering a secret value for a username.":::

       :::image type="Secrets" source="media/create-operations-manager-managed-instance/create-a-secret-password.png" alt-text="Screenshot of entering a secret value for a password.":::

    - Leave the **Content type (optional)**, **Set activation date**, **Set expiration date**, **Enabled**, and **Tags** areas as default, and select **Create** to create the secret.

>[!Important]
>To minimize the need for extensive communication with both your Active Directory admin and Network Admin, review  [**Prerequisites Verification**](/system-center/scom/scom-mi-prerequisites-verification?view=sc-om-2022). The section outlines the procedures through which the AD admin and network admin validate their configuration changes and ensure their successful implementation; thus, reducing unnecessary back-and-forth interactions with Operations Manager admin time.

## Next steps

- [Create a user assigned identity](create-user-assigned-identity.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
