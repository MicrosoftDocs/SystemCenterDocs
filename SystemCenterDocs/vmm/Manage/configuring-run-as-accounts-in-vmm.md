---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Configuring Run As accounts in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  aa482e44-bd66-4346-92cc-a16ec0ded0b1
---

# Configuring Run As accounts in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

In Virtual Machine Manager (VMM), the credentials that a user enters for any process can be provided by a Run As account. A Run As account is a container for a set of stored credentials.

Only administrators and delegated administrators can create and manage Run As accounts. Read-only administrators can see the account names associated with Run As accounts that are in the scope of their user role.

The same restrictions on creating, managing, and viewing Run As accounts are in effect in both the VMM console and the VMM command shell. Delegated administrators and self-service users can only get objects that are in the scope of their user role and can only perform the actions that their user role allows.

## Security for Run As accounts in VMM
VMM uses the Windows Data Protection API (DPAPI) to provide operating system level data protection services during storage and retrieval of the Run As account credentials. DPAPI is a password-based data protection service that uses cryptographic routines (the strong Triple-DES algorithm, with strong keys) to offset the risk posed by password-based data protection. For more information about DPAPI architecture and security, see [Windows Data Protection](http://msdn.microsoft.com/library/ms995355).

During the installation of a VMM management server, you can configure VMM to use Distributed Key Management to store encryption keys in Active Directory Domain Services (AD DS). For more information, see [Configuring Distributed Key Management in VMM](../Deploy/Configuring-Distributed-Key-Management-in-VMM.md).

## In this section
Use the procedures in this section to perform the following tasks.

|Procedure|Task|
|-------------|--------|
|[How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md)|Describes how to create Run As accounts|
|[How to disable and enable Run As accounts in VMM](How-to-disable-and-enable-Run-As-accounts-in-VMM.md)|Describes how to disable and enable a Run As account to temporarily prevent its use.|
|[How to delete a Run as Account in VMM](How-to-delete-a-Run-As-account-in-VMM.md)|Describes how to delete a Run As account.|

## See Also
[Securing VMM resources](Securing-VMM-resources.md)



