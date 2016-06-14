---
title: How to add users to the Administrator user role in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb9a9e46-9a99-45f0-9c57-9aa97704b2d1
---
# How to add users to the Administrator user role in VMM
The Administrator user role is created when you install [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)]. The user who performs the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] installation and all domain users in the Local Administrators group are added to the Administrator user role.

Use this procedure to add users to the Administrator user role in [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] or remove users from the user role.

**Account requirements** Administrators can add new users to the Administrator user role or remove users from that user role.

### To add users to the Administrator user role

1.  In the **Settings** workspace, click **Security**, then click **User Roles**. Under **User Roles**, click the **Administrator** user role to select it.

2.  In the **Home** tab, in the **Properties** group, click **Properties**

3.  In the **Administrator Properties** dialog box, click **Members** to access the **Members** page, and then click **Add** to open the **Select Users, Computers, or Groups** dialog box.

4.  Enter a user or Active Directory group of users and click **OK** to continue. The dialog box verifies that your selections are valid users.

    > [!NOTE]
    > You can delete members from the **Members** page by selecting an entry and then clicking **Remove**.

5.  Click **OK** to save your changes.

## See Also
[Creating user roles in VMM](Creating-user-roles-in-VMM.md)
[Securing VMM resources](Securing-VMM-resources.md)


