---
title: Set up user roles in VMM
description: This article describes how to set up VMM roles and permissions
author:  rayne-wiselman
manager:  cfreemanwa
ms.date:  2016-09-14
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Set up user roles in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager


This article describes how to set up System Center 2016 - Virtual Machine Manager (VMM) user roles.

## Before you start

- [Learn more](manage-permissions-overview.md#role-based-security) about user roles.
- Ensure you have the right permissions to create the role or add users to it.

    - **Administrator role**: Administrators can add and remove users
    - **Delegate Administrator role**: Administrators can create the role. Delegated Administrators can create Delegated Administrator roles that include a subset of their scope, library servers, and Run As accounts.
    - **Read-only Administrator role**: Administrators can create the role. Delegated Administrators can create Read-only Administrator roles that include a subset of their scope, library servers, and Run As accounts.
    - **Tenant Administrator role**: Administrators and Delegated Administrators can create this role.
- The Administrator role is created by default when you install VMM. The user who performs the installation, and all domain users in the Local Admistrators group on the server, are added to the Administrator role. You can add or remove members in the role properties.

## Create a role

1.  Click **Settings** > **Create** > **Create User Role**.
2.  In the **Create User Role Wizard**, enter a name and optional description for the role, and then click **Next**.
3.  In **Profile** page, select the role, and then click **Next**.
4.  In **Members**, click **Add** to add user accounts and Active Directory groups to the user role. Add the members in **Select Users, Computers, or Groups**, and then click **Next**.
5.  In **Scope**, select the private clouds or host groups that the members of the role can use. Then click **Next**.
6.  If one or more **Quotas** pages appear (based on whether you selected private clouds on the previous wizard page), review and specify quotas as needed for each private cloud. Otherwise, skip to the next step. Read-only Administrators can only view items in this defined scope.

    To set quotas for the combined use of all members of this user role, use the upper list. To set quotas for each individual member of this user role, use the lower list. By default, quotas are unlimited. To create a limit, clear the appropriate check box under **Use Maximum** and then, under **Assigned Quota**, select a limit. When you have completed all settings, click **Next**.

7. If the **Library servers** page appears, add one or more library servers.
8. In **Networking** click **Add** to add the VM networks that the members of this role can use. Then click **Next**.
9. In **Resources**, click **Add** to add resources. In **Specify user role data path**, click **Browse** to specify a library path that members of this user role can use to upload data. Then click **Next**.
10. In **Permissions** page, select global actions, and any cloud-specific actions that you want to allow members of this role to perform. Click **Next**.
11. If the **Run As accounts** page appears, add Run As accounts that you want the members of this role to be able to use. Otherwise, skip to the next step.
12. If the **Quotas for VM networks** page appears, review and specify quotas to limit the number of VM networks that members of this user role can create. Otherwise, skip to the next step.

    To limit the combined number of VM networks that can be created by all members of this user role, use the upper setting. To limit the number of VM networks that can be created by each individual member of this user role, use the lower setting.

13. In **Summary** page, review the settings, and click **Finish** to create the role. Verify the role appears in **Settings** > **Security** > **User Roles**.


After you create a user role, you can change its settings in the role properties.
