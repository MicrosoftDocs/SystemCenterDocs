---
title: How to update WSUS settings in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a9a055f-1f56-4b26-994e-e32fcc272312
---
# How to update WSUS settings in VMM
Use the following procedure to update the properties of the Windows Server Update Services \(WSUS\) server that is used for fabric updates in [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)]. In [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], you update the properties of the update server to configure a proxy server for use during synchronizations and to change the update categories, products, and supported languages that are synchronized by the WSUS server.

> [!IMPORTANT]
> After you add a WSUS server to [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], you should only manage the WSUS server in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)].

### To update the properties of the Windows Server Update Server in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers**, and then click **Update Server** to display the **Update Server** tab on the ribbon.

3.  On the **Update Server** tab, in the **Properties** group, click **Properties**.

4.  On the **Proxy Server** tab, configure WSUS to use a proxy server when synchronizing updates, or update the port for a proxy server that is already in use.

5.  On the **Update Classifications** tab, select each update classification that you want to synchronize.

6.  On the **Products** tab, select each product to include in update synchronizations.

7.  On the **Languages** tab, select each supported language to include in update synchronizations.

8.  Click **OK** to apply any changes you make.

> [!TIP]
> To manually synchronize updates in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], in the **Fabric** workspace, on the **Fabric** pane, expand **Servers**, and then click **Update Server**. Then, on the **Update Server** tab, in the **Update Server** Group, click **Synchronize**.

## See Also
[How to add an update server to VMM](How-to-add-an-update-server-to-VMM.md)
[How to perform on-demand WSUS synchronizations in VMM](How-to-perform-on-demand-WSUS-synchronizations-in-VMM.md)
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


