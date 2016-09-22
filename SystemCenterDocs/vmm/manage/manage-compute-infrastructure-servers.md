---
title: Set up infrastructure servers in the VMM compute fabric
description: This article describes how to set up infrastructure servers in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Set up infrastructure servers in the VMM compute fabric

>Applies To: System Center 2016 - Virtual Machine Manager

Read this article to learn about adding and managing infrastructure servers in the System Center 2016 - Virtual Machine Manager (VMM) fabric.


In addition to the infrastructure servers used by the VMM fabric ([library server](manage-library-overview.md), [PXE servers](manage-compute-bare-metal-hyper-v.md), [IPAM servers](manage-network-ipam.md)), you can add other infrastructure servers such as Active Directory, DNS, DHCP, System Center to the VMM fabric. This allows you to manage and update all of these servers in the same location.

The **Infrastructure** node in the VMM console shows infrastructure servers you add, as well as the VMM management server, vCenter servers, VMM library servers, IPAM and PXE servers if you add them.

## Add an infrastructure server

1. Click **Fabric** > **Servers** > **Infrastructure** > **Add Resources** > **Infrastructure Server**.
2. In **Add Infrastructure Server Wizard** specify the FQDN of the server you want to add an account with permissions for the server. Then click **Add**.

## Update infrastructure servers

In order to update infrastructure servers you'll need to set up a WSUS server and configure update baselines. [Learn more](manage-compute-update-servers.md)

After the WSUS server is in place you can update infrastructure servers as follows:

1. In **Fabric** > **Servers** > **Home** > **Show** > **Compliance** select the server you want to update. All the baselines for the server will be shown. The server could be compliant for some baselines and not for others.
2. Click **Remediate**. You'll only see this option if the selected objects aren't compliant.
3. In **Update Remediation** select or clear update baselines or individual updates to determine which updates to install. When you select a computer all updates are initially selected.
4. f you prefer to restart the server manually after remediation completes click **Do not restart the servers after remediation**. By default, the server restarts if any updates require it. If you choose not to restart and updates need it the computer status will be **Pending Machine Reboot** after the remediation. The updates won't be activated until you restart. With this status VMM won't scan the machines for compliance during refreshes.
5. Click **Remediate** to start updating.
