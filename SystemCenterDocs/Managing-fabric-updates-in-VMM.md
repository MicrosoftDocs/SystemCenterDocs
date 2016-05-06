---
title: Managing fabric updates in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b327b3ad-b820-4852-8144-c4d326a66dc4
---
# Managing fabric updates in VMM
The procedures in this scenario explain how to set up update management in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] and how to perform updates on servers that are managed by [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].

For information about Windows Server Update Service \(WSUS\) requirements, see [Preparing your environment for System Center 2016 - Virtual Machine Manager](../Topic/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

## Why should you manage fabric updates through [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]?
Fabric servers include the following physical computers managed by [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]: Hyper\-V hosts and Hyper\-V clusters, library servers, Pre\-Boot Execution Environment \(PXE\) servers, the Windows Server Update Management \(WSUS\) server, and the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management server.

[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] supports on demand compliance scanning and remediation of the fabric. Administrators can monitor the update status of the servers. They can scan for compliance and remediate updates for selected servers. Administrators also can exempt resources from installation of an update.

[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] supports orchestrated updates of Hyper\-V host clusters. When a [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] administrator performs update remediation on a host cluster, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] places one cluster node at a time in maintenance mode and then installs updates. If the cluster supports live migration, intelligent placement is used to migrate virtual machines off the cluster node. If the cluster does not support live migration, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] saves state for the virtual machines.

## Managing the update server
After you add a WSUS server to [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you should not manage the WSUS using the WSUS console. In [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], an administrator updates the properties of the update server to configure a proxy server for synchronizations and to change the update categories, products, and supported languages that are synchronized by the WSUS server.

If you add the update server to [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] in Single Sockets Layer \(SSL\) mode, you can update proxy server credentials for synchronization in the update server properties. If the update server is not added to [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] in SSL mode, proxy server credentials are managed in the WSUS Administration Console.

For more information, see [How to update WSUS settings in VMM](../Topic/How-to-update-WSUS-settings-in-VMM.md).

## User roles and update management
In [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], administrators and delegated administrators manage fabric updates. Only administrators can manage the update server and synchronize updates. Delegated administrators can scan and remediate updates on computers that are within the scope of their user roles. Delegated administrators can use baselines created by administrators and other delegated administrators. But delegated administrators cannot modify or delete baselines created by others. For more information about user roles, see [Creating user roles in VMM](../Topic/Creating-user-roles-in-VMM.md).

## In This Section
Follow these procedures to install a WSUS update server, add the update server to [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], configure update baselines, scan computers for compliance, and perform update remediations. The final procedure demonstrates how to orchestrate updates within a Hyper\-V host cluster.

|Procedure|Description|
|-------------|---------------|
|[How to install a WSUS server for VMM](../Topic/How-to-install-a-WSUS-server-for-VMM.md)|Describes requirements for installing a dedicated WSUS server to use with [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].|
|[How to add an update server to VMM](../Topic/How-to-add-an-update-server-to-VMM.md)|Describes how to enable update management in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] by adding a WSUS server to [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].|
|[How to configure update baselines in VMM](../Topic/How-to-configure-update-baselines-in-VMM.md)|Describes how to edit a built\-in update baseline and how to create new updates baselines for your [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] environment.|
|[How to scan for update compliance in VMM](../Topic/How-to-scan-for-update-compliance-in-VMM.md)|Describes how to scan managed computers for update compliance in **Compliance** view of the VMM console.|
|[Performing update remediation in VMM](../Topic/Performing-update-remediation-in-VMM.md)|Describes how to perform update remediations on stand\-alone Hyper\-V hosts that are managed by [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] and how to orchestrate updates on a Hyper\-V host cluster in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].|
|[How to create and remove update exemptions for resources in VMM](../Topic/How-to-create-and-remove-update-exemptions-for-resources-in-VMM.md)|Describes how to create an update exemption to prevent installation of an update on a resource and how to remove an update exemption and then return the resource to update compliance.|
|[How to perform on-demand WSUS synchronizations in VMM](../Topic/How-to-perform-on-demand-WSUS-synchronizations-in-VMM.md)|Describes how to use the **Synchronize** action in the **Fabric** workspace to synchronize updates in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].|
|[How to update WSUS settings in VMM](../Topic/How-to-update-WSUS-settings-in-VMM.md)|Describes how to configure a proxy server for synchronization and how to change the update classifications, products, and supported languages that WSUS synchronizes by updating the properties of the update server in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].|
|[How to integrate fabric updates with Configuration Manager](../Topic/How-to-integrate-fabric-updates-with-Configuration-Manager.md)|Describes how to configure [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to use a WSUS server that is part of a Microsoft System Center Configuration Manager environment.|
|[Using infrastructure servers in VMM](../Topic/Using-infrastructure-servers-in-VMM.md)|Describes how you can add infrastructure servers such as DHCP servers to [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. After you add infrastructure servers, you can manage updates to them through [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].|

## See Also
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

