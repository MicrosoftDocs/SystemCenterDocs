---
title: Creating user roles in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b0b7644-2af3-4c67-8c48-0965b0266d43
---
# Creating user roles in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can create user roles in Virtual Machine Manager (VMM) to define the objects that users can manage and the management operations that users can perform. The following table summarizes the capabilities of each user role in VMM.

### User role descriptions for VMM

|VMM user role|Capabilities|
|---------------------------------------------------------------|----------------|
<<<<<<< HEAD
|Administrator|Members of the Administrators user role can perform all administrative actions on all objects that VMM manages. Only administrators can add a Windows Server Update Services (WSUS) server to VMM to enable updates of the VMM fabric through VMM.
|Fabric Administrator (Delegated Administrator)|Members of the Delegated Administrator user role can perform all administrative tasks within their assigned host groups, clouds, and library servers, except for adding WSUS servers. Delegated Administrators cannot modify VMM settings, and cannot add or remove members of the Administrators user role.
|Read-Only Administrator|Read-only administrators can view properties, status, and job status of objects within their assigned host groups, clouds, and library servers, but they cannot modify the objects. Also, the read-only administrator can view Run As accounts that administrators or delegated administrators have specified for that read-only administrator user role.
|Tenant Administrator|Members of the Tenant Administrator user role can manage self-service users and VM networks. Tenant administrators can create, deploy, and manage their own virtual machines and services by using the VMM console or a web portal. Tenant administrators can also specify which tasks the self-service users can perform on their virtual machines and services. Tenant administrators can place quotas on computing resources and virtual machines.
|Application Administrator (Self-Service User)|Members of the Self-Service User role can create, deploy, and manage their own virtual machines and services by using the VMM console or a Web portal.
=======
|Administrator|Members of the Administrators user role can perform all administrative actions on all objects that VMM manages. Only administrators can add a Windows Server Update Services (WSUS) server to VMM to enable updates of the VMM fabric through VMM.<br /><br />To change the members of the Administrator user role, see [How to add users to the Administrator user role in VMM](How-to-add-users-to-the-Administrator-user-role-in-VMM.md).|
|Fabric Administrator (Delegated Administrator)|Members of the Delegated Administrator user role can perform all administrative tasks within their assigned host groups, clouds, and library servers, except for adding WSUS servers. Delegated Administrators cannot modify VMM settings, and cannot add or remove members of the Administrators user role.<br /><br />To create a delegated administrator, see [How to create a Delegated Administrator user role in VMM](How-to-create-a-Delegated-Administrator-user-role-in-VMM.md).|
|Read-Only Administrator|Read-only administrators can view properties, status, and job status of objects within their assigned host groups, clouds, and library servers, but they cannot modify the objects. Also, the read-only administrator can view Run As accounts that administrators or delegated administrators have specified for that read-only administrator user role.<br /><br />To create a read-only administrator, see [How to create a Read-Only Administrator user role in VMM](How-to-create-a-Read-Only-Administrator-user-role-in-VMM.md).|
|Tenant Administrator|Members of the Tenant Administrator user role can manage self-service users and VM networks. Tenant administrators can create, deploy, and manage their own virtual machines and services by using the VMM console or a web portal. Tenant administrators can also specify which tasks the self-service users can perform on their virtual machines and services. Tenant administrators can place quotas on computing resources and virtual machines.<br /><br />To create a tenant administrator, see [How to create a Tenant Administrator user role in VMM](How-to-create-a-Tenant-Administrator-user-role-in-VMM.md).|
|Application Administrator (Self-Service User)|Members of the Self-Service User role can create, deploy, and manage their own virtual machines and services by using the VMM console or a Web portal.

> [!CAUTION]
> If you grant rights for a particular template to a user that does not have rights to the Run As account that the template is configured with, then the user can potentially extract the credentials for the Run As account from the template.

You can also use the **Create User Role Wizard** to configure user roles with a set of permitted actions on a per-cloud basis in addition to the global settings. These settings apply only to the tenant administrator and the self-service user roles. With these settings, the user’s effective permitted actions for a given cloud are the combination of their global permitted actions and cloud permitted actions.

## See Also
[Securing VMM resources](Securing-VMM-resources.md)



