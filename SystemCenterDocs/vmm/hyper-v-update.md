---
ms.assetid: 929257eb-5089-415b-9ad9-f5d7623c0983
title: Update Hyper-V hosts and clusters
description: This article describes how to update Hyper-V hosts and clusters in the VMM fabric
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 09/19/2023
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---

# Update Hyper-V hosts and clusters

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

Read this article to learn about keeping Hyper-V hosts and clusters updated in the System Center Virtual Machine Manager (VMM) fabric.

## Before you start

You'll need to set up an update (WSUS server) in the VMM fabric and configure update baselines.

## Update a host or cluster

1. In **Fabric** > **Servers** > **Show** > **Compliance**, select the computers you want to update. All the baselines for the computer will be shown. The computer could be compliant for some baselines and not for others.
2. Select **Remediate**. You'll only see this option if the selected objects aren't compliant.
3. In **Update Remediation**, select or clear update baselines or individual updates to determine which updates to install. When you select a computer, all updates are initially selected. If you're running a Hyper-V cluster, ensure that:
      - To update all cluster nodes, select the host cluster by its cluster name.
      - To update single nodes, select the individual hosts in the cluster. With this setting, VMM doesn't display cluster remediation options but treats each node as a standalone Hyper-V host.
4. If you prefer to restart the computers manually after remediation completes, select **Do not restart the servers after remediation**. By default, the computer restarts if any updates require it. If you choose not to restart and updates need it, the computer status will be **Pending Machine Reboot** after the remediation. The updates won't be activated until you restart. With this status, VMM won't scan the machines for compliance during refreshes.
5. If you're running a cluster:
      - If cluster node is already in maintenance mode, select **Allow remediation of clusters with nodes already in maintenance mode**. In maintenance mode, VMs can't be created or moved to the host. The host has a zero rating and is excluded from dynamic optimization.
      - Select **Live migration** to remove virtual machines from a host before performing update remediation so that they remain online. If you don't need to keep them online and want to perform a quicker update, select **Save state** to shut down virtual machines and proceed with remediation.
6. Select **Remediate** to start updating. After remediation, if no reboot is pending, the server or cluster will show as **Compliant**.

::: moniker range="sc-vmm-1807"

  >[!NOTE]
  >Remediation of a single node in a S2D cluster might not succeed if remediation is done by selecting the host. We recommend you to remediate at cluster level and then select the hosts for remediation.

In S2D cluster, once the update is installed on the node, the node is rebooted and repair (resync) operation is initiated. If the resync isn't completed within 600 minutes (default value), the update job fails. To avoid the job failure, you can change the wait time in the registry key.

- Minimum value for the resync wait time is 600 minutes and the maximum value can be 2880 minutes.

- **S2DResyncWaitTimeInMins** is the registry key setting that you can use to change the default  Resync wait time.

- *Here's the path for the registry key*:

  \HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings > RegistryKey  

::: moniker-end

## Next steps

[Learn about](update-rollups.md) VMM updates.
