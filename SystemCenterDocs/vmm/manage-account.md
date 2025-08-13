---
ms.assetid: 07eb5def-e680-4b7b-8238-cf2266a675bb
title: Manage roles and permissions in VMM
description: This article describes how to manage roles and permissions in VMM
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---


# Manage roles and permissions in VMM



System Center Virtual Machine Manager (VMM) allows you to manage roles and permissions. VMM provides:

- **Role-based security**: Roles specify what users can do in the VMM environment. Roles consist of a profile that defines a set of available operations for the role, scope which defines the set of objects on which the role can operate, and a membership list that defines the Active Directory user accounts and security groups that are assigned to the role.
- **Run As accounts**: Run As accounts act as containers for stored credentials that you use to run VMM tasks and processes.

## Role based security

The following table summarizes VMM user roles.

:::moniker range=">=sc-vmm-2016 <=sc-vmm-2019"
**VMM user role** | **Permissions** | **Details**
--- | --- | ---
Administrator role | Members of this role can perform all administrative actions on all objects that VMM manages. | Only administrators can add a WSUS server to VMM to enable updates of the VMM fabric through VMM.
Virtual machine administrator | Administrators can create the role (applicable for VMM 2019 and later). | Delegated administrator can create VM administrator role that includes entire scope or a subset of their scope, library servers, and Run-As accounts.
Fabric administrator (delegated administrator) | Members of this role can perform all administrative tasks within their assigned host groups, clouds, and library servers. | Delegated administrators can't modify VMM settings, add or remove members of the administrators user role, or add WSUS servers.
Read-Only administrator | Members of this role can view properties, status, and job status of objects within their assigned host groups, clouds, and library servers, but they can't modify the objects. | The read-only administrator can also view Run As accounts that administrators or delegated administrators have specified for that read-only administrator user role.
Tenant administrator | Members of this role can manage self-service users and VM networks. | Tenant administrators can create, deploy, and manage their own virtual machines and services by using the VMM console or a web portal.<br/><br/> Tenant administrators can also specify which tasks the self-service users can perform on their virtual machines and services.<br/><br/> Tenant administrators can place quotas on computing resources and virtual machines.
Tenant administrator | Members of this role can manage self-service users and VM networks. | Tenant administrators can create, deploy, and manage their own virtual machines and services using the VMM console or a web portal.<br/><br/> Tenant administrators can also specify which tasks the self-service users can perform on their virtual machines and services.<br/><br/> Tenant administrators can place quotas on computing resources and virtual machines.
Application administrator (Self-Service User) | Members of this role can create, deploy, and manage their own virtual machines and services. | They can manage VMM using the VMM console.

:::moniker-end
:::moniker range=">=sc-vmm-2022"
**VMM user role** | **Permissions** | **Details**
--- | --- | ---
Administrator role | Members of this role can perform all administrative actions on all objects that VMM manages. | Only administrators can add a WSUS server to VMM to enable updates of the VMM fabric through VMM.
Virtual machine administrator | Administrators can create the role. | Delegated administrator can create VM administrator role that includes entire scope or a subset of their scope, library servers, and Run-As accounts.
Fabric administrator (delegated administrator) | Members of this role can perform all administrative tasks within their assigned host groups, clouds, and library servers. | Delegated administrators can't modify VMM settings, add or remove members of the administrators user role, or add WSUS servers.
Read-Only administrator | Members of this role can view properties, status, and job status of objects within their assigned host groups, clouds, and library servers, but they can't modify the objects. | The read-only administrator can also view Run As accounts that administrators or delegated administrators have specified for that read-only administrator user role.
Tenant administrator | Members of this role can manage self-service users and VM networks. | Tenant administrators can create, deploy, and manage their own virtual machines and services using the VMM console or a web portal.<br/><br/> Tenant administrators can also specify which tasks the self-service users can perform on their virtual machines and services.<br/><br/> Tenant administrators can place quotas on computing resources and virtual machines.
Application administrator (Self-Service User) | Members of this role can create, deploy, and manage their own virtual machines and services. | They can manage VMM using the VMM console.
:::moniker-end

## Run As accounts

There are different types of Run As accounts:

- **Host computer accounts** are used to interact with virtualization servers.
- **BMC accounts** are used to communicate with the BMC on hosts for out-of-band management or power optimization.
- **External accounts** are used to communicate with external apps such as Operations Manager.
- **Network device accounts** are used to connect with network load balancers.
- **Profile accounts** are used in Run As profiles when you're deploying a VMM service or creating profiles.

>[!NOTE]
> - VMM uses the Windows Data Protection API (DPAPI) to provide operating system level data protection services during storage and retrieval of the Run As account credentials. DPAPI is a password-based data protection service that uses cryptographic routines (the strong Triple-DES algorithm, with strong keys) to offset the risk posed by password-based data protection. [Learn more](/previous-versions/ms995355(v=msdn.10)).
> - When you install VMM, you can configure VMM to use Distributed Key Management to store encryption keys in the Active Directory.
> - You can set up Run As accounts before you start managing VMM, or you can set up Run As accounts if you need them for specific actions.

## Next steps

- [Set up user roles](account-user-role.md).
- [Set up run as accounts](account-runas.md).
