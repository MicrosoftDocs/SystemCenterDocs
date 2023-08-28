---
ms.assetid: 
title: Store domain credentials in Key vault
description: This article describes how to store domain credentials inkey vault.
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

# Store domain credentials in key vault

This article describes how to store domain credentials inkey vault.

## To store domain credentials in key vault

1. Go to the Key vault resource created in [step4](create-key-vault.md).

2. On the left pane, under **Objects**, select **Secrets**.
  
     >[!Note]
     >You must create two secrets to store the domain account credentials:
     >- Username 
     >- Password 

3. Select **+ Generate/Import**.
4.	On the **Create a secret** page, do the following:
     1. **Upload options**: Select **Manual**.
     2. **Name**: Enter the name of the secret. For example, you can use *Username* for the username secret and **Password** for the password secret.
     3. **Secret value**: For the username value (in the format *domain\username*), enter the domain account username. For the password value, enter the domain account password. For example, if the domain is contoso.com, the username should be in the format *contoso\username*.
     4. Leave the **Content type (optional)**, **Set activation date**, **Set expiration date**, **Enabled**, and **Tags** areas as default, and select **Create** to create the secret.


## Next steps

- [Create a static IP](create-static-ip.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
