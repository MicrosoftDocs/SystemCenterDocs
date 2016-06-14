---
title: How to integrate fabric updates with Configuration Manager
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e867fdc-a1a1-4766-b34f-3e2910725088
---
# How to integrate fabric updates with Configuration Manager
[!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)] supports using a WSUS server that is part of a Configuration Manager environment. This will also enable you to use the reporting capabilities of Configuration Manager to provide compliance information.

If you use an existing WSUS server from a Configuration Manager environment, changes to configuration settings for the WSUS server \(for example, update classifications, languages, and proxy settings\) should only be made from Configuration Manager. The [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] administrator can view the configuration settings from the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console, but cannot make changes.

> [!NOTE]
> For [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)], the synchronization schedule is always on\-demand, regardless of the setting specified in Configuration Manager.

Before you perform any configuration steps for update management in [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)], you should first configure the Configuration Manager environment.

The following procedure contains an overview of the steps you need to perform in Configuration Manager. For more information, see the following Configuration Manager documentation:

-   [Software Updates in Configuration Manager](http://technet.microsoft.com/library/gg682068.aspx)

-   [Reporting in Configuration Manager](http://technet.microsoft.com/library/gg699377.aspx)

### To configure Configuration Manager to share a WSUS server with VMM

1.  In Configuration Manager, create a collection. This collection will contain all the computers that [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] will manage.

2.  To the collection, add the computers that [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] will manage. This includes all computers for which [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] will perform update management. This includes computers such as the following:

    -   Virtual machine hosts

    -   Library servers

    -   [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] management server

    -   PXE servers

    -   The WSUS server

3.  Exclude this collection from any software update deployments delivered by Configuration Manager to ensure that [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] controls update management of those computers.

    > [!NOTE]
    > You will still be able to view compliance information for this collection in Configuration Manager reports.

4.  If you want to include [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] compliance information in Configuration Manager reports, create an update group in Configuration Manager that contains all the updates against which you want to measure compliance for the computers managed by [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)].

    > [!IMPORTANT]
    > You are creating this update group only to provide reporting capabilities. Do not deploy this update group to the computers managed by [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)].

### To configure [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to use a WSUS server shared with Configuration Manager

1.  Add the WSUS server to [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] by following the steps in [How to add an update server to VMM](How-to-add-an-update-server-to-VMM.md).

2.  After you have added the WSUS server to [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)], open the Fabric workspace, expand **Servers**, and click **Update Server**, and then select the update server.

3.  On the **Update Server** tab, in the **Properties** group, click **Properties**.

4.  On the **General** page, ensure that the **Allow Update Server configuration changes** check box is not selected, and then click **OK**.

For more information about configuring update management, see [Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md).

## See Also
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


