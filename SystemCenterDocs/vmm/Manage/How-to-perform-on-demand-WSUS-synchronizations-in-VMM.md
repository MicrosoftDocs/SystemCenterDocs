---
title: How to perform on-demand WSUS synchronizations in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b305e444-db77-4de3-bad0-a70870ad88cb
---
# How to perform on-demand WSUS synchronizations in VMM
Use this procedure to perform on-demand update synchronization for a Windows Server Update Services (WSUS) server in Virtual Machine Manager (VMM). To get updates, the WSUS server contacts Microsoft Update. WSUS determines if any new updates have been made available since the last synchronization. WSUS then downloads the new metadata. Then VMM imports the changes into the VMM update catalog.

When the update server is added to VMM, an initial synchronization is performed. VMM does not perform automatic synchronizations after that. You should perform on-demand synchronizations on a schedule that meets your organization's needs. Typically an organization synchronizes updates at least every 15-30 days, in accordance with Microsoft security and update release cycles.

> [!IMPORTANT]
> After you add a WSUS server to VMM, you should only manage the WSUS server in VMM. VMM does not synchronize settings that are entered in the WSUS Administration Console with those that are entered in the update server properties. In VMM, update the properties of the update server to configure a proxy server for synchronizations and to change the update categories, products, and supported languages that are synchronized by the WSUS server. For more information, see [How to update WSUS settings in VMM](How-to-update-WSUS-settings-in-VMM.md).

### To synchronize updates in VMM

1.  Open the **Fabric** workspace.

2.  On the **Fabric** pane, expand **Servers**, and then click **Update Server**.

3.  On the **Update Server** tab, in the **Update Server** group, click **Synchronize**.

After the synchronization is completed, you can view all new updates in the **Library** workspace under   **Update Catalog and Baselines**; you can add any update to baselines. To find out how many new updates were downloaded, how many updates expired, and how many updates were revised during synchronization, view job details for the **Synchronize Update Server** job in the **Jobs** workspace or the **Jobs** window.

## See Also
[Performing update remediation in VMM](Performing-update-remediation-in-VMM.md)
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


