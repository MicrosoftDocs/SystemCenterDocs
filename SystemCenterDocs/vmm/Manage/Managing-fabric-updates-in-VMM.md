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
The procedures in this scenario explain how to set up update management in Virtual Machine Manager \(VMM\) and how to perform updates on servers that are managed by VMM.

For information about Windows Server Update Service \(WSUS\) requirements, see [Preparing your environment for System Center 2016 - Virtual Machine Manager](../Deploy/Preparing-your-environment-for-System-Center-2016---Virtual-Machine-Manager.md).

## Why should you manage fabric updates through VMM?
Fabric servers include the following physical computers managed by VMM: Hyper\-V hosts and Hyper\-V clusters, library servers, Pre\-Boot Execution Environment \(PXE\) servers, the Windows Server Update Management \(WSUS\) server, and the VMM management server.

VMM supports on demand compliance scanning and remediation of the fabric. Administrators can monitor the update status of the servers. They can scan for compliance and remediate updates for selected servers. Administrators also can exempt resources from installation of an update.

VMM supports orchestrated updates of Hyper\-V host clusters. When a VMM administrator performs update remediation on a host cluster, VMM places one cluster node at a time in maintenance mode and then installs updates. If the cluster supports live migration, intelligent placement is used to migrate virtual machines off the cluster node. If the cluster does not support live migration, VMM saves state for the virtual machines.

## Managing the update server
After you add a WSUS server to VMM, you should not manage the WSUS using the WSUS console. In VMM, an administrator updates the properties of the update server to configure a proxy server for synchronizations and to change the update categories, products, and supported languages that are synchronized by the WSUS server.

If you add the update server to VMM in Single Sockets Layer \(SSL\) mode, you can update proxy server credentials for synchronization in the update server properties. If the update server is not added to VMM in SSL mode, proxy server credentials are managed in the WSUS Administration Console.

For more information, see [How to update WSUS settings in VMM](How-to-update-WSUS-settings-in-VMM.md).

## User roles and update management
In VMM, administrators and delegated administrators manage fabric updates. Only administrators can manage the update server and synchronize updates. Delegated administrators can scan and remediate updates on computers that are within the scope of their user roles. Delegated administrators can use baselines created by administrators and other delegated administrators. But delegated administrators cannot modify or delete baselines created by others. For more information about user roles, see [Creating user roles in VMM](Creating-user-roles-in-VMM.md).

## In This Section
Follow these procedures to install a WSUS update server, add the update server to VMM, configure update baselines, scan computers for compliance, and perform update remediations. The final procedure demonstrates how to orchestrate updates within a Hyper\-V host cluster.

|Procedure|Description|
|-------------|---------------|
|[How to install a WSUS server for VMM](How-to-install-a-WSUS-server-for-VMM.md)|Describes requirements for installing a dedicated WSUS server to use with VMM.|
|[How to add an update server to VMM](How-to-add-an-update-server-to-VMM.md)|Describes how to enable update management in VMM by adding a WSUS server to VMM.|
|[How to configure update baselines in VMM](How-to-configure-update-baselines-in-VMM.md)|Describes how to edit a built\-in update baseline and how to create new updates baselines for your VMM environment.|
|[How to scan for update compliance in VMM](How-to-scan-for-update-compliance-in-VMM.md)|Describes how to scan managed computers for update compliance in **Compliance** view of the VMM console.|
|[Performing update remediation in VMM](Performing-update-remediation-in-VMM.md)|Describes how to perform update remediations on stand\-alone Hyper\-V hosts that are managed by VMM and how to orchestrate updates on a Hyper\-V host cluster in VMM.|
|[How to create and remove update exemptions for resources in VMM](How-to-create-and-remove-update-exemptions-for-resources-in-VMM.md)|Describes how to create an update exemption to prevent installation of an update on a resource and how to remove an update exemption and then return the resource to update compliance.|
|[How to perform on-demand WSUS synchronizations in VMM](How-to-perform-on-demand-WSUS-synchronizations-in-VMM.md)|Describes how to use the **Synchronize** action in the **Fabric** workspace to synchronize updates in VMM.|
|[How to update WSUS settings in VMM](How-to-update-WSUS-settings-in-VMM.md)|Describes how to configure a proxy server for synchronization and how to change the update classifications, products, and supported languages that WSUS synchronizes by updating the properties of the update server in VMM.|
|[How to integrate fabric updates with Configuration Manager](How-to-integrate-fabric-updates-with-Configuration-Manager.md)|Describes how to configure VMM to use a WSUS server that is part of a Microsoft System Center Configuration Manager environment.|
|[Using infrastructure servers in VMM](Using-infrastructure-servers-in-VMM.md)|Describes how you can add infrastructure servers such as DHCP servers to VMM. After you add infrastructure servers, you can manage updates to them through VMM.|

## See Also
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


