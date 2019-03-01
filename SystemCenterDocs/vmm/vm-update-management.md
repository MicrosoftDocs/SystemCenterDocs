---
ms.assetid: cbf4471e-e219-4aa2-a1fe-590d3f84d664
title: Azure update management in VMM
description: This article provides information about how to manage Azure updates for VMs and workloads in VMM.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.date: 03/01/2019
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
MonikerRange: '>=sc-vmm-2019'
---

# Azure update management
This article provides information about Azure update management feature in Virtual Machine Manager (VMM).

Using Azure update Management feature, you can manage updates for Virtual Machines (VMs) and Workloads running in a VMM.

Currently, VMM supports update management feature for all new VMs with Windows Server operating system, and are deployed using a VM template with *Azure Update Management Extension* enabled.

## Create a VM template linked to Azure profile

Follow these steps:

1.	Create a profile for Azure Update management using steps detailed in [Azure subscriptions article](azure-subscription.md)    
2.	In the **Create VM Template** wizard, select **Source Page** > select  **Use an existing VM template or a virtual hard disk stored in the library**.
3.	On the **Extension** page, select **Enable Azure Update Management** and select the Azure Profile from the drop-down menu.  Click **OK**.

    ![extension page](./media/azure-profile/extensions-page.png)

4.	Deploy the VMs from the VM template.
5.	VMM does the onboarding for the VMs deployed through VM template to the *Azure Update Management* service and provides the link to the Azure console for managing the updates.
    ![virtual machines information](./media/azure-profile/virtual-machines-information.png)
6.	Click the **Update Status** link under **Azure Update Management info** to assess and deploy the updates for the VM.

>[!NOTE]
> Azure update management capability also supports service deployments using service templates, the flow is same as the above.  

::: moniker-end
