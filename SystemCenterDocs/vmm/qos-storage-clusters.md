---
ms.assetid: 74defbac-c24a-4e32-8445-f29a853942aa
title: Set storage QoS for clusters
description: This article describes how to set storage QoS policies for clusters
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/27/2025
ms.custom: engagement-fy24
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
monikerRange: '>sc-vmm-2016'
---

# Manage storage QoS for clusters




This article describes how to manage storage quality-of-service (QoS) policies for clusters in System Center Virtual Machine Manager (VMM).  

::: moniker range=">=sc-vmm-2019 <=sc-vmm-2022"
## Assign storage QoS policy for clusters
Windows server 2016 and later allows the deployments to use the storage QoS feature with any VHDs residing on a Cluster Shared Volume (CSV). In VMM 2016, the management of SQoS is limited to VHDs residing on the S2D hyper-converged type clusters and Scale-Out File Servers only (SOFS). Also, the scope of QoS policies is based on the storage arrays, which isn't scalable to the scenarios like SAN, where VMM only manages the compute cluster.
::: moniker-end
::: moniker range=">=sc-vmm-2019"

VMM supports QoS on all managed clusters and also SOFS running on Windows Server 2016 and later.

::: moniker-end

::: moniker range="sc-vmm-2019"
> [!NOTE]
> VMM 2019 UR3 and later supports [Azure Stack Hyper Converged Infrastructure (HCI, version 20H2)](deploy-manage-azure-stack-hci.md).
::: moniker-end

::: moniker range="sc-vmm-2025"
## Assign storage QoS policy for clusters
Windows server 2019 and later allows the deployments to use the storage QoS feature with any VHDs residing on a Cluster Shared Volume (CSV). In VMM 2025, the management of SQoS is limited to VHDs residing on the S2D hyper-converged type clusters and Scale-Out File Servers only (SOFS). Also, the scope of QoS policies is based on the storage arrays, which isn't scalable to the scenarios like SAN, where VMM only manages the compute cluster.

VMM 2025 supports QoS on all managed clusters and also SOFS running on Windows Server 2019 and later.

::: moniker-end

**Use these steps**:

1. Select **Fabric** > **Storage** > **QoS Policies** > **Create Storage QoS Policy**.
2. In the wizard > **General**, specify a policy name.
3. In **Policy Settings**, specify how the policy must apply. Select **All virtual disk instances share resources** to specify that the policy must be applied to all virtual disks on the file server (pooled, single instance). Select **Resources allocated to each virtual disk instance** to specify that the policy is applied separately to each specified virtual disk (multi-instance). Specify the minimum and maximum IOPS. A setting of 0 means that no policy is enforced.
4. In **Scope**, select the managed cluster under **Clusters** to which you want to apply the policy.
   ![Screenshot of select cluster.](media/storage-sqos-clusters/sqos-clusters.png)

5. In **Summary**, verify the settings and finish the wizard.

**On Upgrade**

After upgrade, existing deployments that are managing their QoS with VMM can seamlessly migrate to the new QoS scoping based on the cluster name.

### PowerShell cmdlets

The following new parameters are added:

**Affected cmdlet** | **Parameter** | **Details**
--- | --- |---
**New-SCStorageQoSPolicy** |-HostCluster | Specifies an array of HostCluster objects for QoS policy scope. **Optional**.
**New-SCVIrtualDiskDrive** |-StorageQoSPolicy | Allows you to select the storage QoS policy for the Virtual Disk Drive. **Optional**.
**Set-SCStorageQoSPolicy** |-HostCluster | Specifies an array of HostCluster objects to be added in the QoS policy scope. **Optional**.
**Get-SCStorageQoSPolicy**	 |-HostCluster | Specifies a HostCluster object for which we want to query the QoS policies. **Optional**.


## Assign  a storage QoS Policy from templates
   Templates usage is a common way for deploying VMs and Services on a cloud.



::: moniker range=">=sc-vmm-2019"

   You can select storage QoS policies from a template as well. For information on how to assign storage QoS policies from templates, see the related procedure in the [create a VM template](library-vm-templates.md) article.

::: moniker-end

## Next steps
  [Manage QoS](./manage-sofs-qos.md)
