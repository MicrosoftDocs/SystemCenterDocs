---
title: Manage client auto deployment settings
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fed9fefc-6540-4409-889c-345bb3bfb3e9
---
# Manage client auto deployment settings
You can configure a number of settings for the Operations Manager Client Auto Deployment management pack for DPM, including:

[Add or remove a DPM Server for client auto deployment](#BKMK_AddRemove)

[Specify the number of clients a DPM server can handle](#BKMK_Clients)

[Change settings for all DPM servers configured for client auto deployment](#BKMK_All)

[Change settings for selected DPM servers configured for client auto deployment](#BKMK_DPMSelected)

[Manage stale clients that haven’t been backed up recently](#BKMK_Stale)

## <a name="BKMK_AddRemove"></a>Add or remove a DPM server for client auto deployment

1.  On the System Center Operations Manager console, go to the **Monitoring** view, expand **DPM Client Auto Deployment**, and then select **Auto deployment DPM server state**.

2.  On the main pane, select the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server you want to include. On the **Actions** pane, click **Include DPM for auto deployment**.

    You can also select **Exclude DPM for auto deployment** to remove a DPM server.

## <a name="BKMK_Clients"></a>Specify the number of clients a DPM server can handle

1.  To change the number of client computers a [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server can be allotted, use the following [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Management Shell cmdlet:

2.  Set\-DPMGlobalProperty –Dpmservername <DPMServer> \-MaxCapacityForClientAutoDeployment <NewCapacity>

## <a name="BKMK_All"></a>Change settings for all DPM servers configured for client auto deployment

1.  To change the settings, edit the ClientPGSettings.xml file. See [Set up client auto deployment](../Topic/Set-up-client-auto-deployment.md).

2.  To apply the changes on all DPM servers, in the System Center Operations Manager console, go to the **Monitoring** view, expand **[!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Client Auto Deployment**, and then click **Auto deployment server state**.

3.  Select a System Center Operations Manager server from the main pane.

4.  On the **Actions** pane, click **Apply modified PG settings**.

5.  On the **Run task** dialog box, click **Run**.

    The changes will be applied to all protection groups created by [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] client auto deployment on all relevant [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers.

## <a name="BKMK_DPMSelected"></a>Change settings for selected DPM servers configured for client auto deployment

1.  To change the settings, edit the ClientPGSettings.xml file. See [Set up client auto deployment](../Topic/Set-up-client-auto-deployment.md).

2.  To apply the settings on selected DPM servers, on System Center Operations Manager console, go to the **Monitoring** view, expand **[!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Client Auto Deployment**, and then click **Auto deployment server state**.

3.  Select a System Center Operations Manager server from the main pane.

4.  On the **Actions** pane, click **Apply modified PG settings**.

5.  On the **Run task** dialog box, click **Override**.

6.  On the **Override Task Parameters** dialog box, provide a comma\-separated list of FQDNs for the DPM servers in the **New Value** text box.

    The changes will be applied on the DPM servers you specify.

7.  Click **Override**.

8.  Click **Run**.

## <a name="BKMK_Stale"></a>Manage stale clients that haven’t been backed up recently

1.  A stale client is a client computer which resides in a protection group for [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] client auto deployment and hasn’t been backed up for the period specified by the administrator. The default period is 90 days.

2.  To set the stale threshold, open the Registry Editor:

    -   Navigate to **HKLM\\SOFTWARE\\Microsoft\\Microsoft Data Protection Manager\\Configuration\\Client**.

    -   Set the following—Value: **StaleClientThresholdInDays**; Data: Number of days; Type: **DWORD**.

3.  To stop protecting clients that reach the threshold, open the Registry Editor:

    -   Navigate to **HKLM\\SOFTWARE\\Microsoft\\Microsoft Data Protection Manager\\Configuration\\Client**.

    -   Set the following—Value: **StopProtectStaleClients**; Data: **1** to stop protection, **0** to continue protection; Type: **DWORD**.

