---
ms.assetid: 40d9b3b7-3e5a-463c-bbc0-161450e59714
title: Manage Azure Stack HCI clusters in VMM
description: This article describes how to manage an Azure Stack HCI cluster in VMM.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/01/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
monikerRange: sc-vmm-2025
ms.custom: UpdateFrequency.5, intro-deployment, engagement-fy23
---

# Manage Azure Stack HCI clusters in VMM

This article provides information about the management of an Azure Stack HCI cluster in System Center Virtual Machine Manager (VMM).

Starting with [System Center 2025](/system-center/vmm/whats-new-in-vmm?view=sc-vmm-2025#support-for-azure-stack-hci-clusters-23h2&preserve-view=true), VMM supports Azure Stack HCI, 23H2 that are updated to 2408.2 or 2411. [Learn more](https://aka.ms/AzureStackHCI) about the new Azure Stack HCI.


>[!IMPORTANT]
> Azure Stack HCI clusters that are managed by Virtual Machine Manager must not join [the preview channel](/azure-stack/hci/manage/preview-channel) yet. System Center (including Virtual Machine Manager, Operations Manager, and other components) does not currently support Azure Stack preview versions. For the latest updates, see the [System Center blog](https://techcommunity.microsoft.com/t5/system-center-blog/bg-p/SystemCenterBlog).


**Supported Azure Stack HCI management scenarios with VMM**

- Addition and management of Azure Stack HCI clusters. [See detailed steps](./hyper-v-existing.md#add-servers) to add Azure Stack HCI clusters to VMM.

- Ability to provision and deploy VMs on the Azure Stack HCI clusters and perform VM life cycle operations. VMs can be provisioned using VHD(x) files, templates, or from an existing VM. [Learn more](provision-vms.md).

- Management of storage pool settings, creation of virtual disks, creation of cluster shared volumes (CSVs), and application of [QoS settings](qos-storage-clusters.md#assign-storage-qos-policy-for-clusters).

- Moving VMs between Windows Server and Azure Stack HCI clusters works via Network Migration and migrating an offline (shut down) VM. In this scenario, VMM does export and import under the hood, even though it's performed as a single operation. 

- The PowerShell cmdlets used to manage Windows Server clusters can be used to manage Azure Stack HCI clusters as well.

**Unsupported Azure Stack HCI management scenarios with VMM**

- Creation of Azure Stack HCI cluster using SCVMM. See the [deployment methods for Azure Stack HCI 23H2 clusters](/azure-stack/hci/deploy/deployment-introduction#about-deployment-methods).

- Management of Azure Stack HCI [stretched clusters](/azure-stack/hci/concepts/stretched-clusters).

- Registration and deregistration of Azure Stack HCI clusters is supported only through Azure.

- Azure Stack HCI clusters shouldn't be used for other purposes like WSUS servers, WDS servers, or library servers. Refer to [Use cases for Azure Stack HCI](/azure-stack/hci/overview#use-cases-for-azure-stack-hci), [When to use Azure Stack HCI](/azure-stack/hci/concepts/compare-windows-server#when-to-use-azure-stack-hci), and [Roles you can run without virtualizing](/azure-stack/hci/overview#roles-you-can-run-without-virtualizing). Azure Stack HCI is intended as a virtualization host where you run all your workloads in virtual machines. The Azure Stack HCI terms permit you to run only what is required for hosting virtual machines.

- Live migration between any version of Windows Server and Azure Stack HCI clusters isn't supported. 

> [!NOTE]
> Live migration between Azure Stack HCI clusters works, as well as between Windows Server clusters.

- The only storage type available for Azure Stack HCI is Storage Spaces Direct (S2D). If you need to use any other type of storage, for example SANs, use Windows Server as the virtualization host.

## Manage the storage pool and create CSVs

After adding the Azure Stack HCI cluster to SCVMM, you can modify the storage pool settings and create virtual disks and CSVs.

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

## Migrate VMs from Windows Server to Azure Stack HCI cluster

Use Network migration functionality in VMM to migrate workloads from Hyper-V (Windows Server 2019 and later) to Azure Stack HCI.

>[!Note]
>Live migration between Windows Server and Azure Stack HCI isn’t supported. Network migration from Azure Stack HCI to Windows Server isn’t supported. 

1. Temporarily disable the live migration at the destination Azure Stack HCI host.
2.	Select **VMs and Services** > **All Hosts**, and then select the source Hyper-V host from which you want to migrate. 
3.	Select the VM that you want to migrate. The VM must be in a turned off state. 
5.	Select **Migrate Virtual Machine**.
6.	In **Select Host**, review and select the destination Azure Stack HCI host. 
6.	Select **Next** to initiate network migration. VMM will perform imports and exports at the back end. 
7.	To verify that the virtual machine is successfully migrated, check the VMs list on the destination host. Turn on the VM and re-enable live migration on the Azure Stack HCI host.

## Next steps

- [Provision VMs on top of Azure Stack HCI clusters using VMM](provision-vms.md).
