---
ms.assetid: c1d20c47-3a30-4c5a-a9ec-e1c7f3a95bf3
title: Provision a scale-out file server (SOFS) from standalone file servers in the VMM fabric
description: This article describes how to provision an SOFS in the VMM fabric
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 05/12/2022
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Provision a scale-out file server (SOFS) from standalone file servers in the VMM fabric

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

Use the instructions in this article if you want to use System Center - Virtual Machine Manager (VMM) to create a scale-out-file server (SOFS) from standalone file servers that are managed in the VMM fabric.


1.  In the VMM console, select **Fabric** > **Create** > **File Server Cluster**.
2.  In the **Create Clustered File Server** wizard > **General**, specify a cluster name, a file server name, and IP addresses if required.
::: moniker range="sc-vmm-2016"
3. In **Resource Type**, select the option to provision computers on which Windows Server 2012 R2 or later is installed and fill in the details.
::: moniker-end
::: moniker range=">sc-vmm-2016"
3. In **Resource Type**, select the option to provision computers on which Windows Server 2016 or later is installed and fill in the details.
::: moniker-end
4.  In **Cluster Nodes**, define a list of computers to add to the cluster.
5.  On the **Summary** page, confirm the settings and then select **Finish**.

You can monitor the cluster status on the **Jobs** page. After the job finishes, check the cluster in **Fabric** > **Storage** > **File servers**.
