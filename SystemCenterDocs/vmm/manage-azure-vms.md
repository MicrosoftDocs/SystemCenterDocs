---
ms.assetid: ed0e035b-4714-4bc4-a8fa-b4eef618e719
title: Manage Azure VMs
description: This article provides information about the basic actions you can do on Azure instances, without leaving the VMM console.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: vvithal
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Manage Azure VMs
This article provides information about the Manage Azure Virtual Machines (VMs) feature.

This feature allows you to perform basic actions on azure instances attached to an azure profile, created for Azure VM management.

>[!NOTE]
> To perform these actions, you must create [Azure profile](azure-subscription.md) with **Profile Usage** selected as **Azure VM Management**. Once an Azure profile  for Azure VM Management is created, the VMs deployed on Azure will be accessible on the **VMs and Services** page of VMM console, and will be listed under *Azure Subscriptions*.

You can perform the following actions on Azure instances, without leaving the VMM console.

- Add and remove one or more Azure subscriptions by using the VMM console.
- See a list view with details and status of all role instances in all deployments in that subscription.
- Manually refresh the list of instances.
- Perform the following basic actions on the instances:
    - Start
    - Stop
    - Shutdown
    - Restart
    - Connect via RDP

## What is not supported
This feature is not intended to provide feature parity with the Microsoft Azure Management Portal. The functionality of this feature is a minor subset of the features at https://manage.windowsazure.com but you can view your Azure instances and do other basic actions, to simplify everyday tasks and management.

With this feature, You cannot:
- Manage your Azure subscription
- Deploy instances to Azure
- Migrate on-premises virtual machines to Azure
- Manage Azure Storage
- Manage Azure Networks
- See the Dashboard Summary view
- See the Performance Monitoring Summary
