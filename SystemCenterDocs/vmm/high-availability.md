---
ms.assetid: 00698994-021a-413e-94fb-54b07ebe3e4a
title: Deploy VMM for high availability
description: This article describes how to deploy the VMM server in high availability mode.
author: JYOTHIRMAISURI
ms.author: raynew
manager: carmonm
ms.date: 11/07/2017
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
ms.custom: intro-deployment
---

# Deploy VMM for high availability

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

For resilience and scalability you can deploy System Center - Virtual Machine Manager (VMM) in high availability mode.

## Before you start

Prepare for a high availability deployment by considering the following:

- Only one instance of VMM can be deployed to a failover cluster of up to 16 nodes.
- Requirements for computers running as VMM management nodes:
  - All cluster nodes that are VMM servers must be running Windows Server 2016.
  - Each cluster node must be joined to a domain and must have a computer name that does not exceed 15 characters.
  - The VMM service network name must not exceed 15 characters.
  - Windows ADK needs to be installed on each computer. Install from setup or the [download center](/windows-hardware/get-started/adk-install). Select **Deployment Tools** and **Windows Preinstallation Environment** when you install.
  - If you plan to deploy VMM services that use SQL Server data-tier applications, install the related command-line utilities on your VMM management server. The command line utility is available in the [SQL Server 2012 feature pack](https://www.microsoft.com/download/details.aspx?id=56041) or [SQL Server 2014 feature pack](https://www.microsoft.com/download/details.aspx?id=53164) or [SQL Server 2016 feature pack](https://www.microsoft.com/download/details.aspx?id=56833).
- Don't install on a Hyper-V host parent partition. You can install VMM on a VM.
- Before you start, set up the VMM service account and distributed key management. [Learn more](/previous-versions/system-center/system-center-2012-R2/gg697604(v=sc.12))

## Deploy high availability components

- [Deploy the VMM management server in a failover cluster](ha-server.md)
- [Make library server file shares highly available](ha-library.md)
- [Deploy the SQL Server VMM database as highly available](ha-sql.md)
