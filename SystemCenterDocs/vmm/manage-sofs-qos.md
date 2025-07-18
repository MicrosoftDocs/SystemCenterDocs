---
ms.assetid: 45c58fcc-8a94-42f2-8e73-11e490213d31
title: Set QoS for storage resources
description: This article describes how to set QoS policies for SOFS storage
author: jyothisuri
ms.author: jsuri
ms.date: 08/22/2024
ms.update-cycle: 1095-days
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency3, engagement-fy24
---

# Set QoS for storage resources

This article describes how to set up quality-of-service (QoS) policies to control IOPS for a scale-out file server (SOFS) in the System Center Virtual Machine Manager (VMM) fabric.

## Before you start

You can verify the status of currently defined QoS policies for a SOFS cluster by running the Get-StorageQoSPolicy PowerShell cmdlet on a cluster node.

## Create a QoS policy

1. Select **Fabric** > **Storage** > **QoS Policies** > **Create Storage QoS Policy**.
2. In the wizard > **General**, specify a policy name.
3. In **Policy Settings**, specify how the policy must apply. Select **All virtual disk instances share resources** to specify that the policy must be applied to all the virtual disks on the file server (pooled, single instance). Select **Resources allocated to each virtual disk instance** to specify that the policy is applied separately to each specified virtual disk (multi-instance). Specify the minimum and maximum IOPS. A setting of 0 means that no policy is enforced.
4. In **Scope**, select the file servers to which the policy is applied. If you select multiple servers, each server will receive the same policy GUID. This ensures there won't be any issues if you migrate VM storage.
5. In **Summary**, verify settings and finish the wizard.


## Next steps

When you deploy a virtual machine and place it on a host, you can select the storage QoS when you review VM settings in **Virtual Machine Settings** > **Machine Resources** > **Virtual Hard Disk**. [Learn more](provision-vms.md) about deploying VMs.
