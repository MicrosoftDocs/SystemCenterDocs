---
title: How to scale out a service in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b2c11ea-cf0c-4558-95fb-a3c837f7f02c
---
# How to scale out a service in VMM
Use the following procedure to scale out a tier in a service that is deployed in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)].

### To scale out a service

1.  In the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console, open the VMs and Services workspace.

2.  Select the private cloud or host group to which you deployed the service.

3.  On the **Home** tab, in the **Show** group, click **Services**.

4.  In the Services pane, select the service that you want to scale out.

5.  On the **Service** tab, in the **Update** group, click **Scale Out**.

6.  In the Scale Out Tier wizard, on the **Select Tier** page, in the **Tier** list, select the tier that you want to scale out, and then click **Next**.

    > [!TIP]
    > On the **Select Tier** page, under the **Tier details**, the number of virtual machines currently deployed in the tier and the maximum tier size is displayed.

7.  On the **Specify Virtual Machine Identity** page, enter a name for the new virtual machine, and then click **Next**.

8.  The next steps in the Scale Out Tier wizard depend on whether the service is deployed to a private cloud or to a host group:

    If the tier is part of a service that is deployed to a private cloud, do the following:

    1.  On the **Configure Settings** page, in **Operating System Settings**, enter the computer name to use for the guest operating system of the new virtual machine. Ensure that this computer name is not already being used in your environment.

    2.  After you have entered the computer name, click **Next**.

    If the tier is part of a service that is deployed to a host group, do the following:

    1.  On the **Select Host** page, select a host on which to deploy the new virtual machine, and then click **Next**.

    2.  On the **Configure Settings** page, in **Operating System Settings**, enter the computer name to use for the guest operating system of the new virtual machine. Ensure that this computer name is not already being used in your environment.

        Update any other virtual machine settings as needed, and then click **Next**.

    > [!TIP]
    > The pin icon next to a setting allows you to specify whether the value you enter can be changed when the virtual machine is created and deployed. When the pin is in a horizontal position, the setting will not be changed.

9. On the **Add Properties** page, specify the actions to perform on the virtual machine when the host on which the virtual machine is deployed starts or stops, and then click **Next**.

10. On the **Summary** page, review your settings, and then click **Scale Out**.

    You can track the progress of the scale out operation in the Jobs window. A **Create virtual machine** job is created for a scale out operation.

    > [!TIP]
    > Deploying a virtual machine can take 15 minutes or longer. You can perform other tasks in the VMM console while you monitor the job.

11. After the **Create virtual machine** job completes successfully, open the VMs and Services workspace and verify that the new virtual machine was added to the tier of the service. For information about viewing a service and its tiers, see [How to view and manage a deployed service](./How-to-view-and-manage-a-deployed-service.md).

## See Also
[Scaling out services in VMM](./Scaling-out-services-in-VMM.md)
[Managing services with VMM](./Managing-services-with-VMM.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)


