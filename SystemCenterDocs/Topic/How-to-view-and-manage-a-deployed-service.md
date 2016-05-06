---
title: How to view and manage a deployed service
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f045491-5340-4107-821b-2fac1812af9f
---
# How to view and manage a deployed service
Use the following procedures to view and manage a deployed service in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]. For information about how to deploy a service, see [How to deploy a service in VMM](../Topic/How-to-deploy-a-service-in-VMM.md).

### To view a deployed service

1.  In the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, open the VMs and Services workspace.

2.  Select the private cloud or host group to which you deployed the service.

3.  On the **Home** tab, in the **Show** group, click **Services**.

4.  In the Services pane, select the service that you deployed. You can expand the service to show each tier that is deployed and you can expand each tier to show the virtual machines that are deployed as part of that tier. You can also expand each virtual machine to show the applications \(and each application’s settings\) deployed to the virtual machine by [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].

    The Service pane provides information about the status and configuration of the service; for example:

    -   The **VM Status** column provides information about the state of the service, tiers, and virtual machines.  For example, the **VM Status** column could show the following:

        -   For a virtual machine, **Stopped** if the virtual machine is powered off.

        -   For a tier, **Saved Stated** if all virtual machines in the tier are in a saved state.

        -   For a service, **Mixed** if the tiers of the service are in different states.

    -   The **Template Name** column displays the name of the service template that was used to deploy the service.

    -   The **Template Release** column displays the version of the service template that the service is currently using.

    -   The **Update Status** column displays **New Release Available** if there is a new version of the service template available with which to update the service.

    For information about updating a deployed service, see [Updating services in VMM](../Topic/Updating-services-in-VMM.md).

### To manage a deployed service

1.  In the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, open the VMs and Services workspace.

2.  Select the private cloud or host group to which you deployed the service.

3.  On the **Home** tab, in the **Show** group, click **Services**.

4.  In the Services pane, select the service that you want to manage, and then click the **Services** tab on the ribbon.

    The actions that you can perform on the entire service appear on the ribbon. For example, if you want to put all the virtual machines in the service into a saved state, in the  **Service** group, click **Save State**. To view the properties of the service, such as which self\-service users have access to the service, in the **Properties** group, click **Properties**.

    If you want to manage a tier in the service, in the Services pane, select the tier. A **Tier** tab appears on the ribbon. For example, if you want to deploy additional virtual machines to the tier, in the **Machine Tier** group, click **Scale Out**. For information about scaling out a tier, see [Scaling out services in VMM](../Topic/Scaling-out-services-in-VMM.md).

    If you want to manage a virtual machine in the service, in the Services pane, expand the appropriate tier, and then select the virtual machine. A **Virtual Machine** tab appears on the ribbon with a list of actions that can be performed on the virtual machine. For example, if you want to connect to the virtual machine, in the **Window** group, click **Connect or View**, and then click **Connect via Console**.

## See Also
[Deploying services in VMM](../Topic/Deploying-services-in-VMM.md)
[Scaling out services in VMM](../Topic/Scaling-out-services-in-VMM.md)
[Updating services in VMM](../Topic/Updating-services-in-VMM.md)
[Managing services with VMM](../Topic/Managing-services-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

