---
ms.assetid: cc915e2b-67b5-4e54-ae26-8eab534f3759
title: Create Run As accounts in VMM
description: This article describes how to manage Run As accounts in VMM
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 11/07/2017
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---


# Create Run As accounts in VMM

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

This article describes how to create and manage Run As accounts in System Center - Virtual Machine Manager (VMM).

A Run As account is a container for a set of stored credentials. In VMM, a Run As account can be provided for any process that requires credentials. Administrators and delegated administrators can create Run As accounts. [Learn more](manage-account.md#run-as-accounts) about different types of Run As accounts.


1. Select **Settings**, and in **Create**, select **Create Run As Account**.
2. In **Create Run As Account**, specify name and optional description to identify the credentials in VMM.
3. In **User name** and **Password**, specify the credentials. The credentials can be a valid Active Directory user or group account or local credentials.
4.  Clear **Validate domain credentials** if you don't need them, and select **OK** to create the Run As account.
