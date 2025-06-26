---
ms.assetid: 54833c06-7479-47cd-8926-1eb703634a3f
title: Manage a VMM private cloud
description: This article provides instructions for managing a private cloud in the VMM fabric
author: jyothisuri
ms.author: jsuri
ms.date: 02/28/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency3, engagement-fy24
---

# Manage a VMM private cloud



This article describes how to manage System Center - Virtual Machine Manager (VMM) cloud settings.

## Manage cloud capacity

You place virtual machines in a VMM cloud if they fit within your capacity settings for the cloud.

- By default, VMM assumes that all the resources allocated to a replica VM are in use and uses this assumption when figuring out whether placing a VM in a cloud or host group will fit within the cloud or host group limits.
- If you want to override this default behavior, you can configure a registry key that allows you to overcommit cloud and host groups in the VMM fabric. In other words, you can place a VM in a cloud or host group even if that placement will bring a cloud or group above its capacity limits. This is useful if you know that you don't need all your replica VMs to be running simultaneously.

### Example with the default settings

You have a cloud with a maximum setting of 32 GB of memory. That cloud has two VMs with 4 GB of memory each. If you don't want to place a third VM with 26 GB of memory, the action will fail with **Not enough memory available**.

### Example with the registry setting

You have a cloud with a maximum setting of 32 GB of memory. That cloud has two VMs with 4 GB of memory each.

To place a third VM with 26 GB of memory, follow these steps:

1. Update the capacity in the cloud properties to accommodate the increased memory size to, say 64 GB.
2. Navigate to the registry key **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings\Placement\IgnoreMemoryForStoppedReplicaVM**.
3. Set the DWORD value to 1. If the value **IgnoreMemoryForStoppedReplicaVM** doesn't exist, create it.
