---
description: Troubleshoot client protection End User Recovery in Data Protection Manager.
ms.topic: concept-article
ms.service: system-center
keywords:
ms.date: 01/28/2026
title: Client protection End User Recovery (EUR) doesn’t work in DPM.
ms.subservice: data-protection-manager
ms.assetid:
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: v-gajeronika
ms.custom:
---

# Client protection End User Recovery (EUR) doesn't work

DPM offers client desktop protection to backup designated folders and files.  One of the benefits of client protection is that administrators and client machine end users can recover their own data from the DPM server without asking the DPM Administrator to restore the files from the backup server.

For more information on recovering data for client desktop machines, see [Back up client computers with DPM](/system-center/dpm/back-up-workstations?&tabs=AllowClients2016%2CAllowClients#recover-client-data).

The **Allow clients to recover their data** section details how End User Recovery works. However, this feature isn't working as designed.  

## Issue

Administrators and optionally configured end users can't recover their own data. When you search for recovery points, you see the following message:

*DPM found no recovery points which you are authorized to restore on the specified DPM server. You can restore only those recovery points for which you were an administrator at the time the backup was taken.  To restore other recovery points, contact your DPM administrator, or attempt to restore from another DPM.*

:::image type="content" source="media/client-protection-end-user-recovery/data-protection-manager-client.png" alt-text="Screenshot of Data Protection Manager client.":::

## Workaround

Allow administrators and designated users to recover their own files.  

To allow administrators and designated users to recover their own files, follow these steps:

1. On the DPM or MAB server, select **Start** > **Run**, and enter **MMC.EXE** to open the Microsoft Management Console.

2. From the File menu, select **Add/Remove snap-in…** to display the list of snap-ins. 

3. Select **Authorization Manager** and select **Add**.  

4. Select **OK**.

5. Right-click the **Authorization Manager** and select **Open Authorization Store…**. XML File is selected by default.

6. Select **Browse…** and navigate to DPM installation > Azman Store folder and select the **AzMan.xml** file and select **OK**.

7. Select **DPMClientSvc** object. Under **Role Assignments**, you can find the entries for each client machine’s FQDN.

8. For each client machine, add permissions for each administrator and other user accounts (optionally) who must be able to recover their own file.

      1. Select one of the machine accounts > **Role Assignments** and then select **guid$client** object.
         2. Under **Name**, right-click **guid$client** entry and select **Properties**.
      3. Select **Members** tab and then select **Select…** to add the users.
         4. Add the domain administrator and any other domain users, and then select **Check Names**.
      5. Select **OK**.
     
      :::image type="content" source="media/client-protection-end-user-recovery/console-inline.png" alt-text="Screenshot of Data Protection Manager console." lightbox="media/client-protection-end-user-recovery/console-expanded.png":::

After you complete these steps for each client machine, the administrator and other added users can recover data from any new recovery points that are created after you add them.

:::image type="content" source="media/client-protection-end-user-recovery/client-recovery-tab.png" alt-text="Screenshot of client.":::
