---
ms.assetid: 1e66b2cf-70f3-4992-b2d8-a71e02fb712d
title: Set up infrastructure servers in the VMM compute fabric
description: This article describes how to manage infrastructure servers in the VMM fabric
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 11/07/2017
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Set up infrastructure servers in the VMM compute fabric

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

Read this article to learn about adding and managing infrastructure servers in the System Center - Virtual Machine Manager (VMM) fabric.

In addition to the infrastructure servers used by the VMM fabric ([library server](manage-library-server.md), [PXE servers](hyper-v-bare-metal.md), and [IPAM servers](network-ipam.md)), you can add other infrastructure servers such as Active Directory, DNS, DHCP, and System Center to the VMM fabric. This allows you to manage and update all of these servers in the same location.

The **Infrastructure** node in the VMM console shows the infrastructure servers you add. It also shows the VMM management servers, vCenter servers, VMM library servers, IPAM servers, and PXE servers if you add them.

## Add an infrastructure server

1. Select **Fabric** > **Servers** > **Infrastructure** > **Add Resources** > **Infrastructure Server**.
2. In **Add Infrastructure Server Wizard** specify the FQDN of the server you want to add an account with permissions for the server. Then select **Add**.

## Update infrastructure servers

In order to update infrastructure servers, you'll need to [set up a WSUS server and configure update baselines](update-server.md).

After the WSUS server is in place, you can update infrastructure servers as follows:

1. In **Fabric** > **Servers** > **Home** > **Show** > **Compliance**, select the server you want to update. All the baselines for the server will be shown. The server could be compliant for some baselines and not for others.
2. Select **Remediate**. You'll only see this option if the selected objects aren't compliant.
3. In **Update Remediation**, select or clear update baselines or individual updates to determine which updates to install. When you select a computer, all updates are initially selected.
4. If you prefer to restart the server manually after remediation completes, select **Do not restart the servers after remediation**. By default, the server restarts if any updates require it. If you choose not to restart and updates need it, the computer status will be **Pending Machine Reboot** after the remediation. The updates won't be activated until you restart. With this status, VMM won't scan the machines for compliance during refreshes.
5. Select **Remediate** to start updating.
