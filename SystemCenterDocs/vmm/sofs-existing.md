---
ms.assetid: fb56f8b6-660d-430c-90e4-9bd5e5926228
title: Add an existing SOFS to the VMM fabric
description: This article provides about managing your Hyper-V environment in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Add an existing SOFS to the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

You can add an existing scale-out file server (SOFS) to the System Center 2016 - Virtual Machine Manager (VMM) storage fabric. When you add a file server, VMM automatically discovers all file shares on it.

1. Click **Fabric** > **Storage** > **Home** > **Add Resource** > **Storage Devices** to open the **Add Storage Devices Wizard**.
1. If the file server is in a domain that's not trusted by the Hyper-V hosts for which it will provide storage, select **This computer is in an untrusted Active Directory domain**. Click **Browse** and select a Run As account with admin permissions on the SOFS. Or create a Run As account if you don't have one.
1. In **Select Provider type**, select **Windows-based file server**.
1. In **Specify Discovery Scope**, type in the FQDN or IP address of the SOFS (not of the underlying cluster)
1. In **Gather Information**, VMM discovers and import information about the SOFS.
1. In **Select Storage Device**, select the file shares that you want VMM to manage. You can configure more settings on the file server after you finish the wizard.
1. On the **Summary** page, confirm the settings and then click **Finish**. You can monitor the cluster status on the **Jobs** page. After the job finishes check the SOFS in **Fabric** > **Storage** > **File servers**.
