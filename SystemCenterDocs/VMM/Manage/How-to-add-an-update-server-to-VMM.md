---
title: How to add an update server to VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 414f9079-4c8f-4433-b78d-5cec4ecf56ee
---
# How to add an update server to VMM
In order to use [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] to manage updates, you can either install a dedicated Windows Server Update Services \(WSUS\) server or use an existing WSUS server running [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)] or [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)]. For instructions on how to install a WSUS server, see [How to install a WSUS server for VMM](How-to-install-a-WSUS-server-for-VMM.md).

To use an existing WSUS server that is deployed in a System Center Configuration Manager environment, see [How to integrate fabric updates with Configuration Manager](How-to-integrate-fabric-updates-with-Configuration-Manager.md).

This procedure describes how to add a WSUS server to your [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] environment.

**Account requirements** To enable update management, you must be a member of the Administrator user role in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]. You will need an account that has local administrator rights on the WSUS server.

### To add a Windows Server Update Server to [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]

1.  In the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console, open the **Fabric** workspace.

2.  On the **Home** tab, in the **Add** group, click **Add Resources**, and then click **Update Server**.

    The **Add Windows Server Update Services Server** dialog box opens.

3.  Type in the **Computer name** of the WSUS server.

4.  Specify the TCP\/IP port that the WSUS website listens on for connections. For WSUS on a computer running [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)] or [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)], use port 8530 \(non\-SSL\) or 8531 \(SSL\).

5.  Enter credentials for connecting to the WSUS server. The account must have administrator rights on the WSUS server. You can use an existing Run As Account, or create a new one.

6.  If necessary, select the **Use Secure Socket Layer \(SSL\) to communicate with the WSUS server and clients** check box.

7.  Click **Add**.

The WSUS server will be added to [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], followed by initial synchronization of the updates catalog. Depending on how many update classifications and products you chose when you configured the WSUS server, this operation can take a long time, depending on such factors as network traffic and the load on the WSUS server. To find out the status of the operation, monitor the status of the **Add Update Server** and **Synchronize Update Server** jobs in the **Jobs** window or in the **Jobs** workspace.

> [!NOTE]
> After you enable update management in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], you can manage the WSUS server through [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]. If you use the WSUS Administrator Console to update WSUS configuration, then these updates will be visible in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] only after WSUS synchronization.

To verify that the WSUS server was added to [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] successfully:

1.  In the **Fabric** workspace, on the **Fabric** pane, expand **Servers**, expand **Infrastructure Servers**, and then click **Update Server**. The results pane displays the update server.

2.  In the **Library** workspace, on the **Library** pane, expand **Update Catalog and Baselines**, and then click **Update Catalog**. The results pane displays all the available WSUS updates.

After you add the update server to [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], you can configure a proxy server for synchronization and change the update categories, products, and supported languages that WSUS synchronizes by updating the properties of the update server in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]. For more information, see [How to update WSUS settings in VMM](How-to-update-WSUS-settings-in-VMM.md).

## See Also
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


