---
ms.assetid: cc915e2b-67b5-4e54-ae26-8eab534f3759
title: Create Run As accounts in VMM
description: This article describes how to manage Run As accounts in VMM
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Create Run As accounts in VMM

>Applies To: System Center 2016 - Virtual Machine Manager


This article describes how to create and manage Run As accounts in System Center 2016 - Virtual Machine Manager (VMM) server.

A Run As account is a container for a set of stored credentials. In VMM a Run As account can be provided for any process that requires credentials. Administrators and Delegated Administrators can create Run As accounts. [Learn more](manage-permissions-overview.md#run-as-accounts) about different types of Run As accounts.


1.  Click **Settings**, and in **Create** click **Create Run As Account**.
2. In **Create Run As Account**  specify name and optional description to identify the credentials in VMM.
3. In **User name** and **Password** specify the credentials. The credentials can be a valid Active Directory user or group account, or local credentials.
4.  Clear **Validate domain credentials** if you don't need it, and click **OK** to create the Run As account.
