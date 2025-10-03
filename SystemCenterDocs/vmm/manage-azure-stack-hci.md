---
ms.assetid: 40d9b3b7-3e5a-463c-bbc0-161450e59714
title: Manage Azure Local instances in VMM
description: This article describes how to manage an Azure Local instance in VMM.
author: jyothisuri
ms.author: jsuri
ms.date: 09/09/2025
ms.update-cycle: 180-days
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
monikerRange: sc-vmm-2025
ms.custom: UpdateFrequency.5, intro-deployment, engagement-fy23, engagement-fy24
---

# Manage Azure Local instances in VMM

This article provides information about the management of an Azure Local instance in System Center Virtual Machine Manager (VMM).

Starting with [System Center 2025](/system-center/vmm/whats-new-in-vmm?view=sc-vmm-2025#support-for-azure-local-instances-23h2&preserve-view=true), VMM supports Azure Local machines that are updated to 2408.2, 2411 or later. [Learn more](https://aka.ms/AzureStackHCI) about the new Azure Local offering.


>[!IMPORTANT]
> Azure Local instances that are managed by Virtual Machine Manager must not join [the preview channel](/azure/azure-local/deploy/download-23h2-software) yet. System Center (including Virtual Machine Manager, Operations Manager, and other components) does not currently support Azure Local preview versions. For the latest updates, see the [System Center blog](https://techcommunity.microsoft.com/t5/system-center-blog/bg-p/SystemCenterBlog).


**Supported Azure Local management scenarios with VMM**

- Addition and management of Azure Local instances. [See detailed steps](./hyper-v-existing.md#add-servers) to add Azure Local instances to VMM.

- Ability to provision and deploy VMs on the Azure Local instances and perform VM life cycle operations. VMs can be provisioned using VHD(x) files, templates, or from an existing VM. [Learn more](provision-vms.md).

- Management of storage pool settings, creation of virtual disks, creation of cluster shared volumes (CSVs), and application of [QoS settings](qos-storage-clusters.md#assign-storage-qos-policy-for-clusters).

- Moving VMs between Windows Server and Azure Local instances works via Network Migration and migrating an offline (shut down) VM. In this scenario, VMM does export and import under the hood, even though it's performed as a single operation. 

- The PowerShell cmdlets used to manage Windows Server clusters can be used to manage Azure Local instances as well.

**Unsupported Azure Local management scenarios with VMM**

- Creation of Azure Local instance using SCVMM. See the [deployment methods for Azure Local instances](/azure/azure-local/deploy/deployment-introduction#about-deployment-methods).

- Networking configuration of Azure Local hosts and clusters. VMM doesn't support Network ATC and can't recognize Arc-enabled Software Defined Networking configuration.

- Management of Azure Local hosts and clusters which are deployed with AD-less methods like [local identity](/azure/azure-local/deploy/deployment-local-identity-with-key-vault).

- Management of Azure Local [stretched clusters](/azure/azure-local/concepts/stretched-clusters).

- Registration and deregistration of Azure Local instances is supported only through Azure.

- Azure Local instances shouldn't be used for other purposes like WSUS servers, WDS servers, or library servers. Refer to [Use cases for Azure Local](/azure/azure-local/overview#common-use-cases-for-azure-local), [When to use Azure Local](/azure/azure-local/concepts/compare-windows-server#when-to-use-azure-local), and [Roles you can run without virtualizing](/azure/azure-local/overview#roles-you-can-run-without-virtualizing). Azure Local machines are intended as virtualization hosts where you run all your workloads in virtual machines. Azure Local Product Terms enable you to run only what is required for hosting virtual machines.

- Live migration between any version of Windows Server and Azure Local instances isn't supported.

> [!NOTE]
> Live migration between Azure Local instances works, as well as between Windows Server clusters.

- The only storage type available for Azure Local is Storage Spaces Direct (S2D). If you need to use any other type of storage, for example SANs, use Windows Server as the virtualization host.

## Manage the storage pool and create CSVs

After adding the Azure Local instance to SCVMM, you can modify the storage pool settings and create virtual disks and CSVs.

1. Select **Fabric** > **Storage** > **Arrays**.
2. Right-click the cluster > **Manage Pool**, and select the storage pool that was created by default. You can change the default name and add a classification.
3. To create a CSV, right-click the cluster > **Properties** > **Shared Volumes**.
4. In the **Create Volume Wizard** > **Storage Type**, specify the volume name and select the storage pool.
5. In **Capacity**, you can specify the volume size, file system, and resiliency (Failures to tolerate) settings. Select **Configure advanced storage and tiering settings** to set up these options.

    ![Screenshot of Volume settings.](./media/s2d/storage-spaces-volume-settings.png)

6. In **Storage settings**, you can specify the storage tier split, capacity, and resiliency.

    ![Screenshot of configure Storage settings.](./media/s2d/storage-spaces-tiering.png)

8. In **Summary**, verify settings and finish the wizard. A virtual disk will be created automatically when you create the volume.

## Deploy VMs on the cluster

In a hyper-converged topology, VMs can be directly deployed on the cluster. Their virtual hard disks are placed on the volumes you created using S2D. You [create and deploy these VMs](provision-vms.md) just as you would create any other VM.

## Migrate VMs from Windows Server to Azure Local instance

Use Network migration functionality in VMM to migrate workloads from Hyper-V (Windows Server 2019 and later) to Azure Local.

>[!Note]
>Live migration between Windows Server and Azure Local isn’t supported. Network migration from Azure Local to Windows Server isn’t supported. 

1. Temporarily disable the live migration at the destination Azure Local host.
2.	Select **VMs and Services** > **All Hosts**, and then select the source Hyper-V host from which you want to migrate. 
3.	Select the VM that you want to migrate. The VM must be in a turned off state. 
5.	Select **Migrate Virtual Machine**.
6.	In **Select Host**, review and select the destination Azure Local host. 
6.	Select **Next** to initiate network migration. VMM will perform imports and exports at the back end. 
7.	To verify that the virtual machine is successfully migrated, check the VMs list on the destination host. Turn on the VM and re-enable live migration on the Azure Local host.

## Next steps

- [Provision VMs on top of Azure Local instances using VMM](provision-vms.md).
