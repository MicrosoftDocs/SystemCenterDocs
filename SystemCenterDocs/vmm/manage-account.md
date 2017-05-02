---
ms.assetid: 07eb5def-e680-4b7b-8238-cf2266a675bb
title: Manage roles and permissions in VMM
description: This article describes how to manage roles and permissions in VMM
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  10/16/2016
ms.topic:  reference
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---


# Manage roles and permissions in VMM

> Applies To: System Center 2016 - Virtual Machine Manager

System Center 2016 - Virtual Machine Manager (VMM) allows you to manage roles and permissions. VMM provides:

- **Role-based security**: Roles specify what users can do in the VMM environment. Roles consist of a profile that defines a set of available operations for the role, scope which define the set of objects on which the role can operate, and a membership list that defines the Active Directory user accounts and security groups that are assigned to the role.
- **Run As accounts**: Run As accounts act as containers for stored credentials that you use to run VMM tasks and processes.

## Role based security

The following table summarizes VMM user roles.

**VMM user role** | **Permissions** | **Details**
--- | --- | ---
Administrator role | Members of this role can perform all administrative actions on all objects that VMM manages. | Only administrators can add a WSUS server to VMM to enable updates of the VMM fabric through VMM.
Fabric Administrator (Delegated Administrator) | Members of this role can perform all administrative tasks within their assigned host groups, clouds, and library servers. | Delegated Administrators cannot modify VMM settings, add or remove members of the Administrators user role, or add WSUS servers.
Read-Only Administrator | Members of this role can view properties, status, and job status of objects within their assigned host groups, clouds, and library servers, but they cannot modify the objects. | The read-only administrator can also view Run As accounts that administrators or delegated administrators have specified for that read-only administrator user role.
Tenant Administrator | Members of this role can manage self-service users and VM networks. | Tenant administrators can create, deploy, and manage their own virtual machines and services by using the VMM console or a web portal.<br/><br/> Tenant administrators can also specify which tasks the self-service users can perform on their virtual machines and services.<br/><br/> Tenant administrators can place quotas on computing resources and virtual machines.
Application Administrator (Self-Service User) | Members of this role can create, deploy, and manage their own virtual machines and services. | They can manage VMM using the VMM console.


## Run As accounts

There are different types of Run As accounts:

- **Host computer accounts** are used to interact with virtualization servers.
- **BMC accounts** are used to communicate with the BMC on hosts for out-of-band management or power optimization.
- **External account** are used to communication with external apps such as Operations Manager.
- **Network device accounts** are used to connect with network load balancers.
- **Profile accounts** are used in Run As profiles when you're deploying a VMM service, or creating profiles.

Note that:

- VMM uses the Windows Data Protection API (DPAPI) to provide operating system level data protection services during storage and retrieval of the Run As account credentials. DPAPI is a password-based data protection service that uses cryptographic routines (the strong Triple-DES algorithm, with strong keys) to offset the risk posed by password-based data protection. [Learn more](https://msdn.microsoft.com/library/ms995355).
- When you install VMM, you can configure VMM to use Distributed Key Management to store encryption keys in Active Directory.
- You can set up Run As accounts before you start managing VMM, or you can set up Run As accounts if you need them for specific actions.

## Next steps

- [Set up user roles](account-user-role.md)
- [Set up run as accounts](account-runas.md)
