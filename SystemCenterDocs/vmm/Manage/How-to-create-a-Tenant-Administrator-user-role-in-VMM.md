---
title: How to create a Tenant Administrator user role in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a3b82ff-03bd-49f4-b083-d75e4902f345
---
# How to create a Tenant Administrator user role in VMM
In [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)], tenant administrators can create and manage self\-service users and VM networks. Tenant administrators can create, deploy, and manage their own virtual machines and services by using the[!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] console or a web portal. A tenant administrator can specify which tasks the self\-service users can perform on their virtual machines and services, and can place quotas on computing resources and virtual machines.

**Account requirements** Administrators and delegated administrators can create a Tenant Administrator user role.

### To create a Tenant Administrator user role

1.  In the **Settings** workspace, on the **Home** tab in the **Create** group, click **Create User Role**.

2.  In the **Create User Role Wizard**, enter a name and optional description for this Tenant Administrator user role, and then click **Next**.

3.  On the **Profile** page, select **Tenant Administrator**, and then click **Next**.

4.  On the **Members** page, click **Add** to add user accounts and Active Directory groups to the user role. Add the members by using the **Select Users, Computers, or Groups** dialog box, and then click **Next**.

5.  On the **Scope** page, select the private clouds that the members of this Tenant Administrator role can use. If you want to allow members of this role to receive and implement Performance and Resource Optimization \(PRO\) tips, select **Show PRO tips**. Then click **Next**.

6.  If one or more **Quotas** pages appear \(based on whether you selected private clouds on the previous wizard page\), review and specify quotas as needed for each private cloud. Otherwise, skip to the next step.

    To set quotas for the combined use of all members of this user role, use the upper list. To set quotas for each individual member of this user role, use the lower list. By default, quotas are unlimited. To create a limit, clear the appropriate check box under **Use Maximum** and then, under **Assigned Quota**, select a limit. When you have completed all settings, click **Next**.

7.  On the **Networking** page, to add the VM networks that the members of this Tenant Administrator role can use, click the **Add** button, select one or more VM networks, and then click **OK**. Then click **Next**.

8.  On the **Resources** page, do the following:

    1.  Under **Resources**, click **Add** to select resources by using the **Add Resources** dialog box, and then click **OK**.

    2.  Under **Specify user role data path**, click **Browse** to specify a library path that members of this user role can use to upload data.

    3.  Click **Next**.

9. On the **Permissions** page, select global actions, and any cloud\-specific actions that you want to allow members of this role to perform. Click **Next**.

    Click **Next**.

10. If the **Run As accounts** page appears \(based on whether you selected the **Author** action on the **Actions** page\), add Run As accounts that you want the members of this user role to be able to use. Otherwise, skip to the next step.

11. If the **Quotas for VM networks** page appears \(based on whether you selected the **Author VMNetwork** action on the **Actions** page\), review and specify quotas to limit the number of VM networks that members of this user role can create. Otherwise, skip to the next step.

    To limit the combined number of VM networks that can be created by all members of this user role, use the upper setting. To limit the number of VM networks that can be created by each individual member of this user role, use the lower setting.

12. On the **Summary** page, review the settings you have entered. Click **Finish** to create the Tenant Administrator user role, or click **Previous** to change any settings.

13. In the **Settings** pane, expand **Security** and then click **User Roles**. Verify that the Tenant Administrator user role that you created appears in the User Roles pane.

After you create a Tenant Administrator user role, you can change **Members**, **Scope**, **Networking**, **Resources**, and **Actions** in the **Properties** dialog box for the Tenant Administrator user role.

## See Also
[Creating user roles in VMM](Creating-user-roles-in-VMM.md)
[How to create a Self-Service User role in VMM](How-to-create-a-Self-Service-User-role-in-VMM.md)
[Securing VMM resources](Securing-VMM-resources.md)


