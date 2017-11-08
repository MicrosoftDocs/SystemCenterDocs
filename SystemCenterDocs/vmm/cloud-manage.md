---
ms.assetid: 54833c06-7479-47cd-8926-1eb703634a3f
title: Manage VMM cloud settings
description: This article provides instructions for managing a private cloud in the VMM fabric
author: rayne-wiselman
ms.author: raynew
manager: carmonm
ms.date: 11/07/2017
ms.topic: article
ms.prod: system-center-2016
ms.technology: virtual-machine-manager
---

# Manage VMM cloud settings

This article describes how to manage System Center - Virtual Machine Manager (VMM) cloud settings.

## Manage cloud capacity

You place virtual machines in a VMM cloud if they fit within your capacity settings for the cloud.

- By default VMM assumed that all resources allocated to a replica VM are in use, and uses this assumption when figuring out whether placing a VM in a cloud or host group will fit within the cloud or host group limits.
- If you want to override this default behavior, you can configure a registry key that allows you to overcommit cloud and host groups in the VMM fabric. In other words, you can placing a VM in a cloud or host group even if that placement will bring a cloud or group above its capacity limits. This is useful if you know that you don't need all your replica VMs to be running simultaneously.

### Example with the default settings

You have a cloud with a maximum setting of 32 GB of memory. That cloud have two VMs with 4 GB of memory each. If you not want to place a third VM with 26 GB of memory the action will fail with "Not enough memory available"

### Example with the registry setting

You have a cloud with a maximum setting of 32 GB of memory. That cloud have two VMs with 4 GB of memory each. To place a third VM with 26 GB of memory you do the following:

1. Update the capacity in the cloud properties to accommodate the increased memory size. Say to 64 GB.
2. Navigate to registry key **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings\Placement\IgnoreMemoryForStoppedReplicaVM**.
3. Set the DWORD value to 1. If the value **IgnoreMemoryForStoppedReplicaVM**.doesn't exist, create it.
