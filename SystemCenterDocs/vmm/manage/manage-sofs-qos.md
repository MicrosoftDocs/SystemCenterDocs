---
ms.assetid: 45c58fcc-8a94-42f2-8e73-11e490213d31
title: Set QoS for storage resources
description: This article describes how to set QoS policies for SOFS storage
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  01/30/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Set QoS for storage resources

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to set up quality-of-service (QoS) policies, to control IOPS for a scale-out file server (SOFS) in the System Center 2016 Virtual Machine Manager (VMM) fabric.

## Before you start

You can verify the status of currently defined QoS policies for an SOFS cluster by running the  Get-StorageQoSPolicy PowerShell cmdlet on a cluster node.

## Create a QoS policy

1. Click **Fabric** > **Storage** > **QoS Policies** > **Create Storage QoS Policy**.
2.  In the wizard > **General**, specify a policy name.
3. In **Policy Settings**, specify how the policy should apply. Select **All virtual disk instances share resources** to specify that the policy should be applied to all virtual disks on the file server (pooled, single instance). Select **Resources allocated to each virtual disk instance** to specify that the policy is applied separately to each specified virtual disk (multi instance). Specify the minimum and maximum IOPS. A setting of 0 means that no policy is enforced.
4. In **Scope**, select the file servers to which the policy is applied. If you select multiple servers, each server will receive the same policy GUID. This ensures there won't be any issues if you migrate VM storage.
5. In **Summary**, verify settings and finish the wizard.


## Next steps

When you deploy a virtual machine and place it on a host, you can select the storage QoS when you review VM settings, in **Virtual Machine Settings** > **Machine Resources** > **Virtual Hard Disk**. [Learn more](../manage/manage-vm-overview.md) about deploying VMs.
