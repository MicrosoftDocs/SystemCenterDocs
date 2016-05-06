---
title: Configuring the VMM library to support self-service users
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27c1dc26-4f36-41a6-b306-b717ce4f7edc
---
# Configuring the VMM library to support self-service users
This topic provides guidance on new methods that are available for sharing resources with self\-service users in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] and describes the self\-service user's view of the **Library** workspace. If you already understand the background information and want detailed steps for configuring the library, see [How to configure the VMM library to support self-service users](../Topic/How-to-configure-the-VMM-library-to-support-self-service-users.md).

To enable self\-service users to create their own virtual machines and services and deploy them to private clouds, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] provides multiple ways for administrators to make resources available to self\-service users. Self\-service users can use the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, and can see their logical and physical resources in the **Library** workspace. Self\-service users who are assigned the **Author** action can create their own templates and profiles, and can share their service templates and virtual machine templates with other self\-service users. A user data path is provided to the self\-service user role to enable those users to upload and share their own resources. Read\-only library paths are provided on private clouds to enable the administrator to share resources among all cloud users.

## Providing resources for self\-service users
Use the following methods to provide resources to self\-service users who deploy services and virtual machines in private clouds:

-   **Read\-only library shares for private clouds** Use the read\-only library shares for private clouds to share resources that should be widely available to self\-service users who deploy services to a cloud. For example, an administrator might store the Application Frameworks resources that are provided with [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] on a read\-only library share for a private cloud so that cloud users can use the resources to sequence and deploy their own applications. For more information about the Application Frameworks resources, see [Deploying applications with services in VMM](../Topic/Deploying-applications-with-services-in-VMM.md).

-   **Self\-service user data paths** Configure user data paths on self\-service user roles to provide a place where members of a self\-service user role can upload and share their own resources. The user data path also is the best place for administrators to store resources that only members of a self\-service user role need to use. For example, a user data path might store the application packages for services that a self\-service user role deploys. Permissions on the user data path are controlled through the file system. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] discovers all files that the current self\-service user has access to. Access control permissions determine whether the users have Read\/Write or Read\/only access.

    To enable administrators to audit and manage resources on users' data paths, the data paths must be on a library share.

    > [!NOTE]
    > Only self\-service users whose user role has the **Author** action or the **Deploy** action can actually use these physical resources in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. The **Author** action enables members to create templates and profiles for their own virtual machines and services. The **Deploy** action enables members to deploy virtual machines by using VHDs as well as virtual machine templates that are assigned to or shared with their user role. For more information, see [How to create a Self-Service User role in VMM](../Topic/How-to-create-a-Self-Service-User-role-in-VMM.md).

-   **Assigned resources** To make virtual machine templates and service templates available to the self\-service users who will deploy virtual machines and services in a private cloud, assign the templates to the self\-service user roles. In addition, self\-service users with the **Author** action can benefit from using standard guest operating system profiles, hardware profiles, application profiles, SQL Server profiles, and virtual machine templates that an administrator provides. Self\-service users do not need access to the physical resources that are referenced by templates and by profiles assigned to their self\-service user role.

    > [!IMPORTANT]
    > When you create templates for self\-service users, be aware of the following changes in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]:
    > 
    > -   In [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], the concept of a "self\-service owner" for a template no longer exists. A template that is to be shared by members of a self\-service user role should have no owner assigned. When a template with no owner is assigned to a self\-service user role that has the **Author**, **Deploy**, or **Deploy \(Template Only\)** action assigned to it, all members can use the template. However, when an owner is assigned to the template, only the owner can use the template.
    > -   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] provides new types of quotas for self\-service users' deployed virtual machines. The quota points that are assigned to virtual machine templates in earlier releases of [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] still are supported as "custom quotas." Administrators also can place individual\- or role\-level quotas on virtual CPU, memory, storage, and the total number of virtual machines deployed in each private cloud that is in the scope of a self\-service user role. For more information, see [How to create a Self-Service User role in VMM](../Topic/How-to-create-a-Self-Service-User-role-in-VMM.md).

-   **Shared resources** Allow self\-service users to share their resources with other self\-service users. You can configure self\-service user roles to allow the owners of virtual machine templates and service templates to share their resources with other members of their own self\-service user role, with another self\-service user role, or with an individual member of another self\-service user role. For example, members of a **Service Developers** self\-service user role might share their fully tested service templates with a **Service Manager** self\-service user role for deployment into a production environment. The **Share** action enables a self\-service user role to share resources; the **Receive** action enables a self\-service user role to receive resources that are shared by another self\-service user role. For more information, see [How to enable self-service users to share resources in VMM](../Topic/How-to-enable-self-service-users-to-share-resources-in-VMM.md).

## A self\-service user's view of the VMM Library
Self\-service users can use the following in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] library:

-   Instead of the **Library Servers** node that administrators see, self\-service users see a **Cloud Libraries** node, which displays physical resources that are available to self\-service users through private clouds. The **Cloud Libraries** node displays a node for each of the private cloud that is in the scope of the self\-service user role. Each private cloud node displays physical resources on read\-only library shares that have been configured for the private cloud.

    > [!NOTE]
    > Administrators see both the **Library Servers** node and the **Cloud Libraries** node. Delegated administrators see only the library servers and cloud libraries that are in the scope of their user roles.

-   In the **Self\-Service User Data** node, self\-service users see physical resources that they have access to on the user data path for their self\-service user role. Access control permissions in the file system determine what the users see.

-   In the **Templates** and **Profiles** nodes, self\-service users see only templates and profiles that they own, that are assigned to their self\-service user roles, or that are shared with them by other self\-service users.

## See Also
[Managing a self-service environment for tenants](../Topic/Managing-a-self-service-environment-for-tenants.md)
[How to configure the VMM library to support self-service users](../Topic/How-to-configure-the-VMM-library-to-support-self-service-users.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)
[Managing tenant resources in the VMM library](../Topic/Managing-tenant-resources-in-the-VMM-library.md)
[Managing the VMM library and its resources](../Topic/Managing-the-VMM-library-and-its-resources.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

