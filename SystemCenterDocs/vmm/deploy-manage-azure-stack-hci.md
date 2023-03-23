---
ms.assetid: 40d9b3b7-3e5a-463c-bbc0-161450e59714
title: Deploy and manage Azure Stack HCI clusters in VMM
description: This article describes how to set up an Azure Stack HCI cluster in VMM.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 11/15/2022
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
monikerRange: '>=sc-vmm-2019'
ms.custom: UpdateFrequency.5, intro-deployment
---

# Deploy and manage Azure Stack HCI clusters in VMM

This article provides information about how to set up an Azure Stack HCI cluster in System Center - Virtual Machine Manager (VMM). You can deploy an Azure Stack HCI cluster by provisioning from bare-metal servers or by adding existing hosts. [Learn more](https://aka.ms/AzureStackHCI) about the new Azure Stack HCI.

::: moniker range="sc-vmm-2022"

[VMM 2019 Update Rollup 3 (UR3)](/system-center/vmm/whats-new-in-vmm?view=sc-vmm-2019#new-features-in-vmm-2019-ur3&preserve-view=true) supports Azure Stack HCI, version 20H2. The current product is Azure Stack HCI, version 21H2. Starting with [System Center 2022](/system-center/vmm/whats-new-in-vmm?view=sc-vmm-2022#support-for-azure-stack-hci-clusters-21h2&preserve-view=true), VMM supports Azure Stack HCI, version 20H2; Azure Stack HCI, version 21H2; and Azure Stack HCI, version 22H2 (supported from VMM 2022 UR1).


::: moniker-end

>[!IMPORTANT]
>Azure Stack HCI clusters that are managed by Virtual Machine Manager shouldn’t join [the preview channel](/azure-stack/hci/manage/preview-channel) yet. System Center (including Virtual Machine Manager, Operations Manager, and other components) does not currently support Azure Stack preview versions. For the latest updates, see the [System Center blog](https://techcommunity.microsoft.com/t5/system-center-blog/bg-p/SystemCenterBlog).

## Before you start

Ensure that you're running VMM 2019 UR3 or later.

**What’s supported?**

- Addition, creation, and management of Azure Stack HCI clusters. [See detailed steps](provision-vms.md) to create and manage HCI clusters.

- Ability to provision & deploy VMs on the Azure Stack HCI clusters and perform VM life cycle operations. VMs can be provisioned using VHD(x) files, templates, or from an existing VM. [Learn more](provision-vms.md).

- [Set up VLAN based network on Azure Stack HCI clusters](manage-networks.md).

- [Deployment and management of SDN network controller on Azure Stack HCI clusters](sdn-controller.md).

- Management of storage pool settings, creation of virtual disks, creation of cluster shared volumes (CSVs), and application of [QoS settings](qos-storage-clusters.md#assign-storage-qos-policy-for-clusters).

- Moving VMs between Windows Server and Azure Stack HCI clusters works via Network Migration and migrating an offline (shut down) VM. In this scenario, VMM does export and import under the hood, even though it's performed as a single operation. 

- The PowerShell cmdlets used to manage Windows Server clusters can be used to manage Azure Stack HCI clusters as well.

::: moniker range="sc-vmm-2022"

**Register and unregister Azure Stack HCI clusters**

With VMM 2022, we're introducing VMM PowerShell cmdlets to register and unregister Azure Stack HCI clusters.

Use the following cmdlets to register an HCI cluster:

```PowerShell
Register-SCAzStackHCI -VMHostCluster <HostCluster> -SubscriptionID <string>
```

Use the following command to unregister a cluster:

```PowerShell
Unregister-SCAzStackHCI -VMHostCluster <HostCluster> -SubscriptionID <string>
```

For detailed information on the supported parameter, see [Register-SCAzStackHCI](/powershell/module/virtualmachinemanager/register-scazstackhci) and [Unregister-SCAzStackHCI](/powershell/module/virtualmachinemanager/unregister-scazstackhci).

::: moniker-end

**What’s not supported?**

- Management of Azure Stack HCI [stretched clusters](/azure-stack/hci/concepts/stretched-clusters) is currently not supported in VMM.

- Azure Stack HCI is intended as a virtualization host where you run all your workloads in virtual machines. The Azure Stack HCI terms allow you to run only what's necessary for hosting virtual machines. Azure Stack HCI clusters shouldn't be used for other purposes like WSUS servers, WDS servers, or library servers. Refer to [Use cases for Azure Stack HCI](/azure-stack/hci/overview#use-cases-for-azure-stack-hci), [When to use Azure Stack HCI](/azure-stack/hci/concepts/compare-windows-server#when-to-use-azure-stack-hci), and [Roles you can run without virtualizing](/azure-stack/hci/overview#roles-you-can-run-without-virtualizing).

- Live migration between any version of Windows Server and Azure Stack HCI clusters isn't supported. 

> [!NOTE]
> Live migration between Azure Stack HCI clusters works, as well as between Windows Server clusters.

- The only storage type available for Azure Stack HCI is Storage Spaces Direct (S2D). Creation or management of non-S2D cluster with Azure Stack HCI nodes isn't supported. If you need to use any other type of storage, for example SANs, use Windows Server as the virtualization host.

> [!NOTE]
> You must enable S2D when creating an Azure Stack HCI cluster.
> To enable S2D, in the cluster creation wizard, go to **General Configuration**. Under **Specify the cluster name and host group**, select **Enable Storage Spaces Direct** as shown below:

![Screenshot of S2D enabled.](./media/s2d/s2d-enable.png)

After you enable a cluster with S2D, VMM does the following:
- The Failover Clustering feature is enabled.
- Storage replica and data deduplication are enabled.
- The cluster is optionally validated and created.
- S2D is enabled, and a storage array object is created in VMM with the same name as you provided in the wizard.

When you use VMM to create a hyper-converged cluster, the pool and the storage tiers are automatically created by running `Enable-ClusterStorageSpacesDirect -Autoconfig $True`.

After these prerequisites are in place, you provision a cluster, and set up storage resources on it. You can then deploy VMs on the cluster.

Follow these steps:


## Step 1: Provision the cluster

You can provision a cluster by Hyper-V hosts and bare-metal machines:

### Provision a cluster from Hyper-V hosts

If you need to add the Azure Stack HCI hosts to the VMM fabric, [follow these steps](hyper-v-existing.md). If they’re already in the VMM fabric, skip to the next step.

> [!NOTE]
> - When you set up the cluster, select the **Enable Storage Spaces Direct** option on the **General Configuration** page of the **Create Hyper-V Cluster** wizard.
> - In **Resource Type**, select **Existing servers running a Windows Server operating system**, and select the Hyper-V hosts to add to the cluster.
> - All the selected hosts should have Azure Stack HCI installed.
> - Since S2D is enabled, the cluster must be validated.

### Provision a cluster from bare metal machines

> [!NOTE]
> Typically, S2D node requires RDMA, QoS, and SET settings. To configure these settings for a node using bare metal computers, you can use the post deployment script capability in PCP. Here's the  [sample PCP post deployment script](hyper-v-bare-metal.md#sample-script).
> You can also use this script to configure RDMA, QoS, and SET while adding a new node to an existing S2D deployment from bare metal computers.

1.	Read the [prerequisites](hyper-v-bare-metal.md#before-you-start) for bare-metal cluster deployment. 

> [!NOTE]
> - The generalized VHD or VHDX in the VMM library should be running Azure Stack HCI with the latest updates. The **Operating system** and **Virtualization platform** values for the hard disk should be set.
> - For bare-metal deployment, you need to add a pre-boot execution environment (PXE) server to the VMM fabric. The PXE server is provided through Windows Deployment Services. VMM uses its own WinPE image, and you need to ensure that it’s the latest. To do this, select **Fabric** > **Infrastructure** > **Update WinPE image**, and ensure that the job finishes.

2.	Follow the instructions for [provisioning a cluster from bare-metal computers](hyper-v-bare-metal.md).

## Step 2: Set up networking for the cluster

After the cluster is provisioned and managed in the VMM fabric, you need to set up networking for cluster nodes.

1.	Start by [creating a logical network](network-logical.md) to mirror your physical management network.
2.	You need to [set up a logical switch](network-switch.md) with Switch Embedded Teaming (SET) enabled so that the switch is aware of virtualization. This switch is connected to the management logical network and has all of the host virtual adapters, which are required to provide access to the management network or configure storage networking. S2D relies on a network to communicate between hosts. RDMA-capable adapters are recommended.
3.	[Create VM networks](network-virtual.md).


## Step 3: Configure DCB settings on the Azure Stack HCI cluster

>[!NOTE]
>Configuration of DCB settings is an optional step to achieve high performance during S2D cluster creation workflow. Skip to step 4 if you do not wish to configure DCB settings.

### Recommendations
- If you've vNICs deployed, for optimal performance, we recommend you to map all your vNICs with the corresponding pNICs. Affinities between vNIC and pNIC are set randomly by the operating system, and there could be scenarios where multiple vNICs are mapped to the same pNIC. To avoid such scenarios, we recommend you to manually set affinity between vNIC and pNIC by following the steps listed [here](hyper-v-network.md#set-affinity-between-vnics-and-pnics).


- When you create a network adapter port profile, we recommend you to allow **IEEE priority**. [Learn more](network-port-profile.md#create-a-virtual-network-adapter-port-profile).

   You can also set the IEEE Priority by using the following PowerShell commands:

   ```PowerShell
   Set-VMNetworkAdapterVlan -VMNetworkAdapterName 'SMB2' -VlanId '101' -Access -ManagementOS
   Set-VMNetworkAdapter -ManagementOS -Name 'SMB2' -IeeePriorityTag on
   ```


**Use the following steps to configure DCB settings**:

1. [Create a new Hyper-V cluster](hyper-v-standalone.md), select **Enable Storage Spaces Direct**.
   *DCB Configuration* option gets added to the Hyper-V cluster creation workflow.

    ![Screenshot of Hyper-V cluster.](./media/s2d/create-hyperv-cluster-wizard.png)

2. In **DCB configuration**, select **Configure Data Center Bridging**.

3. Provide **Priority** and **Bandwidth** values for SMB-Direct and Cluster Heartbeat traffic.

>[!NOTE]
>Default values are assigned to **Priority** and **Bandwidth**. Customize these values based on your organization's environment needs.

   ![Screenshot of Priority bandwidth.](./media/s2d/assign-priority-bandwidth.png)

   Default values:

   | Traffic Class | Priority | Bandwidth (%) |
   | --- | --- | --- |
   | Cluster Heartbeat | 7 | 1 |
   | SMB-Direct | 3 | 50 |

4. Select the network adapters used for storage traffic. RDMA is enabled on these network adapters.

   > [!NOTE]
   > In a converged NIC scenario, select the storage vNICs. The underlying pNICs should be RDMA capable for vNICs to be displayed and available for selection.

    ![Screenshot of Enable RMDS.](./media/s2d/enable-rmds-storage-network.png)

5. Review the summary and select **Finish**.

    An Azure Stack HCI cluster will be created and the DCB parameters are configured on all the S2D nodes.

   > [!NOTE]
   > - DCB settings can be configured on the existing Hyper-V S2D clusters by visiting the **Cluster Properties** page and navigating to the **DCB configuration** page.
   > - Any out-of-band changes to DCB settings on any of the nodes will cause the S2D cluster to be non-compliant in VMM. A Remediate option will be provided in the **DCB configuration** page of cluster properties, which you can use to enforce the DCB settings configured in VMM on the cluster nodes.

## Step 4: Register Azure Stack HCI cluster with Azure

After creating an Azure Stack HCI cluster, it must be registered with Azure within 30 days of installation per Azure Online Service terms. If you're using System Center 2022, use `Register-SCAzStackHCI` cmdlet in VMM to register the Azure Stack HCI cluster with Azure. Alternatively, follow [these steps](/azure-stack/hci/deploy/register-with-azure) to register the Azure Stack HCI cluster with Azure.

The registration status will reflect in VMM after a successful cluster refresh.

## Step 5: View the registration status of Azure Stack HCI clusters

1. In the VMM console, you can view the registration status and last connected date of Azure Stack HCI clusters.
2. Select **Fabric**, select and hold the **Azure Stack HCI** cluster, and select **Properties**.

   ![Screenshot of Registration status.](./media/s2d/registration-status.png)

3. Alternatively, run `Get-SCVMHost` and observe the properties of returned object to check the registration status.

## Step 6: Manage the pool and create CSVs

You can now modify the storage pool settings and create virtual disks and CSVs.

1. Select **Fabric** > **Storage** > **Arrays**.
2. Select and hold the cluster > **Manage Pool**, and select the storage pool that was created by default. You can change the default name and add a classification.
3. To create a CSV, select and hold the cluster > **Properties** > **Shared Volumes**.
4. In the **Create Volume Wizard** > **Storage Type**, specify the volume name and select the storage pool.
5. In **Capacity**, you can specify the volume size, file system, and resiliency (Failures to tolerate) settings.

    ![Screenshot of Volume settings.](./media/s2d/storage-spaces-volume-settings.png)

6. Select **Configure advanced storage and tiering settings** to set up these options.

    ![Screenshot of configure Storage settings.](./media/s2d/storage-spaces-tiering.png)

7. In **Summary**, verify settings and finish the wizard. A virtual disk will be created automatically when you create the volume.

## Step 7: Deploy VMs on the cluster

In a hyper-converged topology, VMs can be directly deployed on the cluster. Their virtual hard disks are placed on the volumes you created using S2D. You [create and deploy these VMs](provision-vms.md) just as you would create any other VM.

> [!Important]
> If the Azure Stack HCI cluster isn't registered with Azure or not connected to Azure for more than 30 days post registration, high availability virtual machine (HAVM) creation will be blocked on the cluster. Refer to step 4 & 5 for cluster registration.


## Next steps

- [Provision VMs](provision-vms.md)
- [Manage the cluster](s2d-manage.md)
