---
ms.assetid: 00698994-021a-413e-94fb-54b07ebe3e4a
title: Deploy VMM for high availability
description: This article describes how to deploy the VMM server in high availability mode.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 01/08/2025
ms.topic: install-set-up-deploy
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-deployment, engagement-fy24
---

# Deploy VMM for high availability

For resilience and scalability, you can deploy System Center Virtual Machine Manager (VMM) in a high availability mode.

## Before you start
::: moniker range=">=sc-vmm-2016 <=sc-vmm-2022"
Prepare for a high availability deployment by considering the following:

- Only one instance of VMM can be deployed to a failover cluster of up to 16 nodes.

::: moniker-end

::: moniker range="sc-vmm-2022"
- Requirements for computers running as VMM management nodes:
  - All cluster nodes that will act as VMM servers must be running either Windows Server 2019 or Windows Server 2022.
  - Each cluster node must be joined to a domain and must have a computer name that doesn't exceed 15 characters.
  - The VMM service network name must not exceed 15 characters.
  - Windows ADK needs to be installed on each computer. Install from setup or the [download center](/windows-hardware/get-started/adk-install). Select **Deployment Tools** and **Windows Preinstallation Environment** when you install.
  - If you plan to deploy VMM services that use SQL Server data-tier applications, install the related command-line utilities on your VMM management server. The command line utility is available in the [SQL Server 2012 feature pack](https://www.microsoft.com/download/details.aspx?id=56041) or [SQL Server 2014 feature pack](https://www.microsoft.com/download/details.aspx?id=53164) or [SQL Server 2016 feature pack](https://www.microsoft.com/download/details.aspx?id=56833) or [SQL Server 2017 feature pack](https://www.microsoft.com/download/details.aspx?id=55992) or [SQL Server 2019 feature pack](https://www.microsoft.com/en-us/download/details.aspx?id=100450).
- Don't install on a Hyper-V host parent partition. You can install VMM on a VM.
- Before you start, set up the VMM service account and distributed key management. [Learn more](/previous-versions/system-center/system-center-2012-R2/gg697604(v=sc.12))
::: moniker-end

::: moniker range="<=sc-vmm-2019"
- Requirements for computers running as VMM management nodes:
  - All cluster nodes that are VMM servers must be running Windows Server 2016.
  - Each cluster node must be joined to a domain and must have a computer name that doesn't exceed 15 characters.
  - The VMM service network name must not exceed 15 characters.
  - Windows ADK needs to be installed on each computer. Install from setup or the [download center](/windows-hardware/get-started/adk-install). Select **Deployment Tools** and **Windows Preinstallation Environment** when you install.
  - If you plan to deploy VMM services that use SQL Server data-tier applications, install the related command-line utilities on your VMM management server. The command line utility is available in the [SQL Server 2012 feature pack](https://www.microsoft.com/download/details.aspx?id=56041) or [SQL Server 2014 feature pack](https://www.microsoft.com/download/details.aspx?id=53164) or [SQL Server 2016 feature pack](https://www.microsoft.com/download/details.aspx?id=56833).
- Don't install on a Hyper-V host parent partition. You can install VMM on a VM.
- Before you start, set up the VMM service account and distributed key management. [Learn more](/previous-versions/system-center/system-center-2012-R2/gg697604(v=sc.12))
:::moniker-end

:::moniker range="sc-vmm-2025"
Prepare for a high availability deployment by considering the following:

- Only one instance of VMM can be deployed to a failover cluster of up to 16 nodes.
- Requirements for computers running as VMM management nodes:
  - All cluster nodes that are VMM servers must be running Windows Server 2025.
  - Each cluster node must be joined to a domain and must have a computer name that doesn't exceed 15 characters.
  - The VMM service network name must not exceed 15 characters.
  - Windows ADK needs to be installed on each computer. Install from setup or the [download center](/windows-hardware/get-started/adk-install). Select **Deployment Tools** and **Windows Preinstallation Environment** when you install.
  - If you plan to deploy VMM services that use SQL Server data-tier applications, install the related command-line utilities on your VMM management server. The command line utility is available in the [SQL Server 2016 feature pack](https://www.microsoft.com/download/details.aspx?id=56833) or later.
- Don't install on a Hyper-V host parent partition. You can install VMM on a VM.
- Before you start, set up the VMM service account and distributed key management. [Learn more](/previous-versions/system-center/system-center-2012-R2/gg697604(v=sc.12))

::: moniker-end

## Deploy high availability components

- [Deploy the VMM management server in a failover cluster](ha-server.md).
- [Make library server file shares highly available](ha-library.md).
- [Deploy the SQL Server VMM database as highly available](ha-sql.md).

## Next steps

[Deploy a highly available VMM management server](./ha-server.md).

