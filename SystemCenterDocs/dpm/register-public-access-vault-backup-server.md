---
title: Reregister the DPM server with Recovery Services vault using public access
description: Learn how to reregister your DPM server with an Azure Backup Recovery Services vault using public access after deleting private endpoints.
#customer intent: As a DPM user, I want to register my server with a Recovery Services vault using private endpoints so that I can back up on-premises data securely.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/25/2025
ms.topic: how-to
monikerRange: >=sc-dpm-2022
ms.service: system-center
ms.subservice: data-protection-manager
---

# Reregister the DPM server with Recovery Services vault using public access

If you don't want to continue using private endpoints for backup, delete them from the vault and re-register DPM. You don’t need to stop protection.

This article describes how to delete private endpoints and reregister your System Center Data Protection Manager (DPM) server to use public access of the Recovery Services vault after deleting private endpoints.

## Delete private endpoints

To delete the private endpoint from Recovery Service vault, follow these steps:

1. Go to the vault you created, and then select **Settings** > **Networking** > **Private access**.

1. To stop using the private endpoint, select the **private endpoint** from the list, and then select **Reject** > **Yes**.

   After you confirm rejection, the vault starts rejecting private endpoint connections. Wait for the operation to complete. Once the operation completes the private endpoint **Connection Status** changes to **Rejected**.

   :::image type="content" source="media/private-endpoint-vault-backup-server/private-endpoint-connection-rejected.png" alt-text="Screenshot shows the rejected status of private endpoint connection." lightbox="media/private-endpoint-vault-backup-server/private-endpoint-connection-rejected.png":::

1. To confirm the deletion for the private endpoint, select the **private endpoint** > **Delete** > **Yes** .

   :::image type="content" source="media/private-endpoint-vault-backup-server/private-endpoint-deletion-confirmation.png" alt-text="Screenshot shows the private endpoint deletion confirmation dialog box." lightbox="media/private-endpoint-vault-backup-server/private-endpoint-deletion-confirmation.png":::

1. After the private endpoint deletion is complete, go to the **Vault** > **Settings** > **Networking** > **Public access**, and then select **Allow from all network and select apply**.

   :::image type="content" source="media/private-endpoint-vault-backup-server/vault-public-access-settings.png" alt-text="Screenshot shows the vault public access settings with allow from all networks option." lightbox="media/private-endpoint-vault-backup-server/vault-public-access-settings.png":::

## Reregister the DPM Server with vault

After you delete the private endpoints from the vault, download a new Credential File from the Azure portal for that vault.

To reregister the DPM Server with the vault, follow these steps:

1. Sign in to the **DPM** Server, and then select **Management** > **Online** > **Register**.

1. On the **Register Server Wizard**, follow the onscreen instruction and provide the **same passphrase** that was used initially to register DPM Server on the **Encryption Setting** pane.

1. Select **Register** and wait for the registration process to complete.

   :::image type="content" source="media/private-endpoint-vault-backup-server/backup-server-re-registration.png" alt-text="Screenshot shows the backup server re-registration process and encryption settings.":::
