---
ms.assetid: de43c081-201d-47e8-8d49-639ebd5b518b
title: Set up self-service in VMM
description: This article describes how to set up self-service in VMM
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2016
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---


# Set up self-service in VMM


This article describes how to set up self-service in System Center - Virtual Machine Manager (VMM).

VMM offers a number of options for self-service users:

- **Virtual machines/Services**: Users can deploy their virtual machines and services to private clouds. A private clouds can be assigned to multiple self-service user roles. Role-level quotas for each self-service user role with the private cloud in scope are used to allocate cloud compute and storage capacity. Member-level quotas set individual limits for members of the self-service user role.
- **Virtual hard disks**: Users can deploy VMs from VHDs as well as templates.
- **Templates/Profiles**: Users can create their own templates and profiles. The **Author** action for a self-service user role providing these authoring rights to create hardware profiles, guest operating system profiles, app profiles, SQL Server profiles, VM templates, and service templates. Note that these resources can be created by a user with the self-service role, and shared with other members of the self-service user role.

Self-service users use the VMM console (or PowerShell) to create and manage VMs, services etc. In the VMM console self-service users can view status, resource usage, jobs, and PRO tips (if enabled) for their  own VMs and services. They can view available capacity and quota usage in their private clouds. They can't see host groups, hosts, library servers and shares, or network and storage configuration settings.

You set up self-service in VMM as follows:

1. Create a self-service user role. Specify actions that the role can perform, assign resources to the role, and configure Run As accounts that self-service users can use when interacting with VMM.
2. Set up the VMM library. Assign a library share on which resources available to self-service users will reside. In addition, set up a share so that self-service users can share their resources with other users.



## Set up a self-service user role

1.  Click **Settings** > **Create** > **Create User Role**.
2.  In the **Create User Role Wizard**, enter a name and optional description for the role, and then click **Next**.
3.  In **Profile** page, select **Self-Service User**, and then click **Next**.
4.  In **Members**, click **Add** to add user accounts and Active Directory groups to the role. Then click **Next**.
5.  In **Scope**, select at least one private cloud that members of the role will use. Then click **Next**.
6.  In **Quotas**, set quota for each private cloud. Each quota sets an individual limit for each member of the user role. If you want all role members to share overall quotas, create a security group in Active Directory, and assign that group to the  user role. Supported quota types include:

    - **Virtual CPUs**: Limits the total number of VM CPUs that can be consumed from the private cloud.
    - **Memory (MB)**: Limits the amount of VM memory that can be consumed from the private cloud.
    - **Storage (GB)**: Limits the amount of VM storage that can be consumed from the private cloud.
    - **Quota (points)**: Sets a quota on VMs deployed on the private cloud based on total quota points assigned to the VMs via their VM templates.
    - **Virtual machines**: Limits the total number of VMs that can be deployed on a private cloud. includ

7. In **Resources**, click **Add** to add resources that the role can use. You can assign hardware profiles, OS profiles, VM templates, app profiles, SQL Server profiles, and service templates that can be used when creating VMs and services.
8. In **Specify user role data path**, click **Browse** to specify a library path that members of this user role can use to upload and share their own data. Then click **Next**.
9. In **Actions**, select the actions that users are allowed to perform.

    - **Author**: Users can author templates and profiles, including hardware profiles, operating system profiles, application profiles, SQL Server profiles, virtual machine templates and service templates.
    - **Checkpoint**: Users can create, edit, and delete checkpoints for their own VMs, and to restore a VM to a previous checkpoint. VMM doesn't support checkpoint actions on services.
    - **Checkpoint (Restore only)**: Users can restore their own VMs to a checkpoint but can't create, edit, and delete checkpoints.
    - **Deploy**: Users can deploy virtual machines and services from templates and virtual hard disks that are assigned to their role. They can't author templates and profiles.
    - **Deploy (from template only)**: Users can deploy VMs and services from templates only. They don't have authoring rights.
    - **Local Administrator**: Users can be Local Admins on their own VMs. You must enable **Local Administrator** on any User role that has the **Deploy (From template)** enabled, so that those users can set the Local Admin password during VM and service deployment. Users will the Deploy action don't need this to set credentials.
    - **Pause and resume**: Users can pause and resume their own VMs and services.
    - **Receive**: Users can use resources that are shared by members of other self-service user roles.
    - **Remote connection**: Users can connect to their VMs from the VMM console or App Controller.
    - **Remove/Save**: Users can remove or save their VMs.
    - **Share**: Users can share resources that they own with other self-service user roles. Sharable resources include hardware profiles, operating system profiles, application profiles, SQL Server profiles, virtual machine templates, virtual machines, service templates, and services. A self-service user must be the owner of a resource to share it. For a user role to use the resources, it must have the **Receive** action.
    **Start/Stop**: Users can start and stop their own VMs and services.
    **Store and redeploy**: Users can store their own virtual machines in the VMM library, and redeploy those virtual machines. Virtual machines stored in the library do not count against a user's virtual machine quota. VMM doesn't support storing services.

10. If the **Run As accounts** page appears, add Run As accounts that you want the members of this role to be able to use in the actions to create VMs and services. Then click **Next**.
11. In **Summary** page, review the settings, and click **Finish** to create the role. Verify the role appears in **Settings** > **Security** > **User Roles**.

After you create the role, you can modify its settings on the properties page.


## Prepare the VMM library for self-service

Self-service users with the required permissions can access the VMM library. Users with the Author action can create templates and profiles in the library. They can also share those templates and profiles with other self-service users. In order for self-service users to interact with the library you need to prepare the following:

- **Read-only library shares**: To share physical resources such as VHDs and ISO images with self-service users, you set up read-only library shares for private clouds, and add the resources to the path. The resources are then available for self-service users that have the private cloud in their scope. You could also store resources such as Application Frameworks on these shares to enable self-service users to configure templates and profiles with scripts.
- **Self-service user data paths**: Set up user data paths on self-service roles to provides a place where members of the role can upload and share their own resources. For example a path might store app packages for services deployed by a self-service user role. Read and write permissions for the path are controlled through the file system. VMM discovers all paths that the current self-service user can access. These data paths must be on a library share.

## Before you start

All of these procedures must be performed by a VMM administrator. Delegated administrators can add library shares on library servers that are in the scope of their user role, can configure read-only library shares on private clouds that they created, and can configure user data paths on self-service user roles that they created. Only members of the local Administrators group can grant access permissions on their user data paths.


## Create read-only library shares

1. Create a shared folder to store resources. The folder will include read-only library shares for private clouds, and user data paths for self-service user roles. We recommend that you crate the folder near your default library share so that it's easy to access when you're managing the library. For example C:\ApplicationData\Virtual Machine Manager Cloud Resources.
2. In the shared folder, create a folder to store the \ApplicationFrameworks resources in case you want to use them. For example C:\ApplicationData\Virtual Machine Manager Cloud Resources\ApplicationFrameworks. Share the folder so that you can add it as a library share. Note that the shared folder can't be in the default library share path. You can't add a library shares that's in the path of an existing library share.
3. Copy the \ApplicationFrameworks folder from the default library share to the share you created for private cloud resources.
4. Add the share to the VMM library. In **Library** > **Library Server** > **Add Library Share**, select each shared folder you want to add to the library. Verify that the share is added in **Library Servers**.
5. To add the read-only share to a private clouds open VMs and Services > clouds, and select the private cloud you want to update.
6. In the cloud, click **Folder** > **Properties** > **Library** > **Read-only library shares** > **Add**.


## Enable self-service users to share resources

To enable self-service users with the Author action to share resources they create you need to create a folder to store shared resources, and then enable resource sharing for the self-service user role.


### Create a folder to share user resources

Configure a user data path for the self-service user role, and grant read/write permission on the folder.

1. Create a folder to store all resources that will be shared by self-service users. For example, C:\ProgramData\Virtual Machine Manager Cloud Resources\Self-Service User Data.
2. Within that folder, create a subfolder to store resources for the self-service user role. For example: C:\ProgramData\Virtual Machine Manager Cloud Resources\Self-Service User Data\Finance Service Managers.
3. Then within that subfolder, create a third-level subfolder to store all the application packages for all releases of the virtual application that you will use in this scenario. For example: C:\ProgramData\Virtual Machine Manager Cloud Resources\Self-Service User Data\Finance Service Managers\<MyApplication>.
4. In that subfolder, create a fourth-level subfolder to store the application package for the first release of the service. For example: C:\ProgramData\Virtual Machine Manager Cloud Resources\Self-Service User Data\Finance Service Managers\<MyApplication>\MyApplication v1>.

    Each time you update and re-sequence an application by using Server App-V, you will need to store the new application package in a separate folder.

5. To enable members of the self-service user role to access the resources and upload their own resources to the folder, grant all members read/write permission on the folder.
6. If needed, share the folder that contains user data for all self-service user roles, and then add the share to the VMM library. To be assigned to a self-service user role, a user data path must be on a library share.
7. Configure the path for a self-service user role as follows:

    1. In **Settings** > **Security** > **User Roles**, click the self-service user role.
    2. In the **User Role** group, click **Properties** > **Resource**.
    3. Browse and select the folder that will hold the shared resources. After you save the changes, the data path is added to the library. Verify the path in **Library** > **Self-Service User Content**.

### Enable sharing for self-service users

To share a resource with a member of another self-service user role, you need the following:

- The self-service user who shares the resource must be the owner of the resource.
- The resource owner must belong to a self-service user role that has been assigned the Share action.
- The resource receiver must belong to a self-service user role that has been assigned the Receive action.

Enable resource sharing as follows:

1. Click **Settings** > **Security** > User Roles, and click the self-service user role for which you want to enable resource sharing.
2. In the **User Role** group, click **Properties**.
3. In **Actions**, select **Share**, and then click **OK**. Members of this self-service user role can now share their own resources with members of any self-service user role that has the **Receive** action assigned to it.
3. To configure a user role with the **Receive** action, select the role > **Properties** >  **Action**, and select **Receive**.
