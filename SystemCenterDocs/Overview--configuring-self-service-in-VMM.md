---
title: Overview: configuring self-service in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b1e0fbf-a1df-4de0-9b9b-8cd6a4426896
---
# Overview: configuring self-service in VMM
In [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)], self\-service user roles provide a way for self\-service users to create, deploy, and manage virtual machines as well as services in a private cloud.

[!INCLUDE[vmm12short](./Token/vmm12short_md.md)] offers multiple self\-service features, in the following categories:

-   [Actions that self-service users can take](./Overview--configuring-self-service-in-VMM.md#BKMK_actions): Self\-service users can deploy their virtual machines and services to private clouds. They can create their own templates and profiles. They can also create virtual machines from building blocks such as virtual hard disks \(VHDs\) rather than just templates.

-   [Ways that self-service users can work with the interface](./Overview--configuring-self-service-in-VMM.md#BKMK_interface): Self\-service users can use the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console or the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] command shell. Also, a person who is a member of more than one user role can open a second [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] session to operate under a different user role, and then switch between sessions as needed.

-   [Ways that resources and Run As accounts can be made available to self-service users](./Overview--configuring-self-service-in-VMM.md#BKMK_resources): More types of library resources, including virtual machine templates, service templates, and multiple types of profiles, can be assigned to a self\-service user role. Resources can be shared between self\-service user roles if an administrator assigns the Share and Receive actions to self\-service users. Also, an administrator can assign Run As accounts \(to provide credentials\) to the user role of a self\-service user.

The following sections provide more details about these additions and enhancements.

## <a name="BKMK_actions"></a>Actions that self\-service users can take
In [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], self\-service users can take the following actions:

-   Self\-service users can deploy their virtual machines and services to private clouds. A private cloud consists of one or more host groups that provide computing capacity and disk resources to self\-service user roles. A private cloud can be assigned to multiple self\-service user roles. Role\-level quotas on each self\-service user role that has the private cloud within its scope are used to allocate computing capacity and other storage within the cloud. Member\-level quotas set individual limits for self\-service user role members.

    During virtual machine and service deployment in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], self\-service users view a simplified placement map that shows the private cloud that their virtual machine or service will be deployed to. If the self\-service user role has more than one private cloud within its scope, users select the appropriate cloud before placement runs.

-   Self\-service users can create their own templates and profiles. The **Author** action for a self\-service user role grants self\-service users authoring rights. Users with authoring rights can create hardware profiles, guest operating system profiles, application profiles, SQL Server profiles, virtual machine templates, and service templates.

-   Self\-service users can be granted permissions to create virtual machines from building blocks such as virtual hard disks \(VHDs\) rather than just templates. To grant these permissions, add the **Deploy** action to the self\-service user role. In contrast, to require users to use templates, grant the **Deploy \(From template only\)** action. Both the **Deploy** action and the **Deploy \(From template only\)** action extend to [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] services.

## <a name="BKMK_interface"></a>Ways that self\-service users can work with the interface
In [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], self\-service users can work with the interface in the following ways:

-   Self\-service users can use the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console or the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] command shell to create and manage their own virtual machines and services. In the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console, self\-service users can view status, resource usage, jobs, and PRO tips \(by permission only\) for their own virtual machines and services. They can view available capacity and quota usage within their assigned private clouds, but they cannot see host groups, hosts, library servers and shares, or network and storage configurations.

    You can also use App Controller as a self\-service portal. For more information, see[App Controller](http://technet.microsoft.com/library/hh546834.aspx).

-   While working in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console, a person who is a member of more than one user role can open another [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] session to operate under a different user role by using the **Open New Connection** action, and can then switch between [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] sessions by using the Taskbar or CTRL\+TAB.

    A self\-service user who belongs to more than one self\-service user role must choose one self\-service user role for each [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] session.

## <a name="BKMK_resources"></a>Ways that resources and Run As accounts can be made available to self\-service users
In [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], resources and Run As accounts can be made available to self\-service users in the following ways:

-   To support application deployment and the various profiles and templates associated with service creation, self\-service user roles can be assigned hardware profiles, guest operating system profiles, virtual machine templates, application profiles, SQL Server profiles, and service templates.

-   In [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], resources can be shared between self\-service user roles. The **Share** action allows user role members to share resources that they own with members of self\-service user roles that allow the **Receive** action. Sharable resources include hardware profiles, guest operating system profiles, virtual machine templates, application profiles, SQL Server profiles, service templates, virtual machines, and services.

-   In [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], the credentials for application, virtual machine, and service deployment are provided by Run As accounts. An administrator assigns Run As accounts to the user role of self\-service users to provide the credentials that the users need to deploy their virtual machines and services.

## See Also
[Managing a self-service environment for tenants](./Managing-a-self-service-environment-for-tenants.md)
[Creating user roles in VMM](./Creating-user-roles-in-VMM.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)


