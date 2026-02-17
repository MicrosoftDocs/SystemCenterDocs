---
ms.assetid: 8fea0c85-7091-48f7-8f50-0ad2dd56da64
title: Set up user roles in VMM
description: This article describes how to set up VMM roles and permissions
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 06/04/2025
ms.update-cycle: 365-days
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency3, engagement-fy24
---


# Set up user roles in VMM

This article describes how to set up System Center Virtual Machine Manager (VMM) user roles.

## Before you start

- [Learn more](manage-account.md#role-based-security) about user roles.
- Ensure you've the right permissions to create the role or to add users to it.

  - **Administrator role**: Administrators can add and remove users.

  - **Delegate Administrator role**: Administrators can create the role. Delegated administrators can create delegated administrator roles that include a subset of their scope, library servers, and Run As accounts.

  - **Read-only Administrator role**: Administrators can create the role. Delegated administrators can create Read-only Administrator roles that include a subset of their scope, library servers, and Run As accounts.
:::moniker range=">=sc-vmm-2016 <=sc-vmm-2019"
  - **Virtual Machine Administrator role** (applicable for VMM 2019 and later): Administrators can create the role. Delegated administrator can create VM administrator role that includes entire scope or a subset of their scope, library servers, and Run As accounts.
:::moniker-end
:::moniker range=">=sc-vmm-2022"
  - **Virtual Machine Administrator role**: Administrators can create the role. Delegated administrator can create VM administrator role that includes entire scope or a subset of their scope, library servers, and Run As accounts.
:::moniker-end
  - **Tenant Administrator role**: Administrators and Delegated administrators can create this role.

- The Administrator role is created by default when you install VMM. The user who performs the installation and all domain users in the local Administrators group on the server are added to the Administrator role. You can add or remove members in the role properties.

## Create a role

1.  Select **Settings** > **Create** > **Create User Role**.
2.  In the **Create User Role Wizard**, enter a name and optional description for the role, and select **Next**.
3.  In **Profile** page, select the role, and select **Next**.
4.  In **Members**, select **Add** to add user accounts and Active Directory groups to the user role. Add the members in **Select Users, Computers, or Groups**, and select **Next**.
5.  In **Scope**, select the VMM clouds or host groups that the members of the role can use. Select **Next**.
6.  If one or more **Quotas** pages appear (based on whether you selected VMM clouds on the previous wizard page), review and specify quotas as needed for each VMM cloud. Otherwise, skip to the next step. Read-only Administrators can only view items in this defined scope.

    To set quotas for the combined use of all members of this user role, use the upper list. To set quotas for each individual member of this user role, use the lower list. By default, quotas are unlimited. To create a limit, clear the appropriate checkbox under **Use Maximum** and then, under **Assigned Quota**, select a limit. When you've completed all settings, select **Next**.

7. If the **Library servers** page appears, add one or more library servers.
8. In **Networking**, select **Add** to add the VM networks that the members of this role can use. Select **Next**.
9. In **Resources**, select **Add** to add resources. In **Specify user role data path**, select **Browse** to specify a library path that members of this user role can use to upload data. Select **Next**.
10. In **Permissions** page, select global actions, and any cloud-specific actions that you want to allow members of this role to perform. Select **Next**.
11. If the **Run As accounts** page appears, add Run As accounts that you want the members of this role to be able to use. Otherwise, skip to the next step.
12. If the **Quotas for VM networks** page appears, review and specify quotas to limit the number of VM networks that members of this user role can create. Otherwise, skip to the next step.

    To limit the combined number of VM networks that can be created by all members of this user role, use the upper setting. To limit the number of VM networks that can be created by each individual member of this user role, use the lower setting.

13. In **Summary** page, review the settings, and select **Finish** to create the role. Verify the role appears in **Settings** > **Security** > **User Roles**.
