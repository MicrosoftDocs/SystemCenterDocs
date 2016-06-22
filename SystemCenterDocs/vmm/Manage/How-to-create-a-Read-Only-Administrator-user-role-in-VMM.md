---
title: How to create a Read-Only Administrator user role in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d31878b-2515-4c56-be56-85619127984c
---
# How to create a Read-Only Administrator user role in VMM
Use this procedure to create a Read\-Only Administrator user role in Virtual Machine Manager \(VMM\).

**Account requirements** Administrators and delegated administrators can create a Read\-Only Administrator role. Delegated administrators can create Read\-Only Administrator user roles that include a subset of the Delegated Administrator user role’s scope, library servers, and Run As accounts.

### To create a Read\-Only Administrator user role

1.  In the **Settings** workspace, on the **Home** tab in the **Create** group, click **Create User Role**.

2.  In the **Create User Role Wizard**, enter a name and optional description for this **Read\-Only Administrator**. Click **Next** to continue.

3.  On the **Profile** page, select **Read\-Only Administrator** and then click **Next**.

4.  On the **Members** page, click **Add** to add user accounts and Active Directory groups to the user role with the **Select Users, Computers, or Groups** dialog box. After you have added the members, click **Next**.

5.  On the **Scope** page, select private clouds or host groups for this read\-only administrator, and then click **Next**. A read\-only administrator can only view items within this defined scope.

6.  On the **Library servers** page, click **Add** to select one or more library server with the **Select a Library server** dialog box. Click **OK** to select a server, and then click **Next**.

7.  On the **Run As accounts** page, click **Add** to open the **Select a Run As account** dialog box. Select one or more accounts and click **OK** to add the account to the **Run As accounts** page.

    -   Use the Ctrl key to select multiple accounts.

    -   Click the **Create Run As Account** button to access the **Create Run As Account** dialog box.

    After selecting accounts, click **Next** to continue.

8.  Review the settings you have entered and then click **Finish** to create the Read\-Only Administrator user role.

After you create a read\-only administrator, you can change its **Members**, **Scope**, **Library servers**, and **Run As accounts** in the **Properties** dialog box for the Read\-Only Administrator user role.


