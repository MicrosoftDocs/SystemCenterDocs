---
ms.assetid: c1d20c47-3a30-4c5a-a9ec-e1c7f3a95bf3
title: Provision a scale-out file server (SOFS) from standalone file servers in the VMM fabric
description: This article describes how to provision an SOFS in the VMM fabric
ms.date: 04/23/2025
author: Jeronika-MS
ms.author: v-gajeronika
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---

# Provision a scale-out file server (SOFS) from standalone file servers in the VMM fabric

This article describes how to provision an SOFS in the VMM fabric.

Use the instructions in this article if you want to use System Center Virtual Machine Manager (VMM) to create a scale-out-file server (SOFS) from standalone file servers that are managed in the VMM fabric.

To provision a SOFS from standalone file servers in the VMM fabric, follow these steps:

1.  In the VMM console, select **Fabric** > **Create** > **File Server Cluster**.

2.  In the **Create Clustered File Server** wizard > **General**, specify a cluster name, a file server name, and IP addresses if required.
::: moniker range="sc-vmm-2016"
3. In **Resource Type**, select the option to provision computers on which Windows Server 2012 R2 or later is installed and fill in the details.
::: moniker-end
::: moniker range=">=sc-vmm-2019 <=sc-vmm-2022"
3. In **Resource Type**, select the option to provision computers on which Windows Server 2016 or later is installed and fill in the details.
::: moniker-end
::: moniker range="sc-vmm-2025"
3. In **Resource Type**, select the option to provision computers on which Windows Server 2019 or later is installed and fill in the details.
::: moniker-end
4.  In **Cluster Nodes**, define a list of computers to add to the cluster.

5.  On the **Summary** page, confirm the settings and select **Finish**.

You can monitor the cluster status on the **Jobs** page. After the job finishes, check the cluster in **Fabric** > **Storage** > **File servers**.
