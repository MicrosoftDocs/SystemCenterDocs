---
description: Troubleshoot client protection End user recovery.
ms.topic: article
ms.service: system-center
keywords:
ms.date: 08/06/2024
title: Client protection End user Recovery (EUR) doesn’t work
ms.subservice: data-protection-manager
ms.assetid:
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.custom:
---

# Client protection End user Recovery (EUR) doesn’t work

DPM offers client desktop protection to backup designated folders and files.  One of the benefits of Client protection is that Administrators and client machine end users can recover their own data from the DPM server without asking the DPM Administrator to restore the files from the backup server.

For more information on Recovering data for client desktop machines, see [Back up client computers with DPM](/system-center/dpm/back-up-workstations?&tabs=AllowClients2016%2CAllowClients#recover-client-data).

The **Allow clients to recover their data** section details how End User Recovery works. However, this feature isn’t working as designed.  

**Issue**:

Administrators and optionally configured end users can’t recover their own data. When you search for recovery points, you see the following message:

*DPM found no recovery points which you are authorized to restore on the specified DPM server. You can restore only those recovery points for which you were an administrator at the time the backup was taken.  To restore other recovery points, contact your DPM administrator, or attempt to restore from another DPM.*

:::image type="content" source="media/client-protection-end-user-recovery/data-protection-manager-client.png" alt-text="Screenshot of Data Protection Manager client.":::

**Workaround**:

Allow administrators and designated users to recover their own files.  

To allow administrators and designated users to recover their own files, follow these steps:

1. On the DPM/MAB Server, select **Start** > **Run** and enter **MMC.EXE** to open the Microsoft Management Console.

2. From the File menu, select **Add/Remove snap-in…** to display the list of snap-in. 

3. Select **Authorization Manager** and select **Add**.  

4. Select **OK**.

5. Right-click the **Authorization Manager** and select **Open Authorization Store…**. XML File is selected by default.

6. Select **Browse…** and navigate to DPM installation > Azman Store folder and select the **AzMan.xml** file and select **OK**.

7. Select **DPMClientSvc** object, under **Role Assignments**, you can find the entries for each client machine’s FQDN.

8. For each client machine, add permissions for each Administrator and other user accounts (optionally) who must be able to recover their own file.

      1. Select one of the machines accounts > **Role Assignments** and then select **guid$client** object.
      2. Under **Name**, right-click **guid$client** entry and select **Properties**
      3. Select **Members** tab and then select **Select…** to add the users.
      4. Add the Domain Administrator and any other Domain users, then select **Check Names**.
      5. Select **OK**.

      :::image type="content" source="media/client-protection-end-user-recovery/console.png" alt-text="Screenshot of Data Protection Manager console.":::

After you complete these steps for each client machine, the Administrator and other added users can recover data from any NEW recovery points that were created after you added them.

:::image type="content" source="media/client-protection-end-user-recovery/client.png" alt-text="Screenshot of client.":::
