---
title: How to create a Delegated Administrator user role in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 251e813d-6d69-4b6b-b25b-0a3fa0e70c60
---
# How to create a Delegated Administrator user role in VMM
Use this procedure to create a Delegated Administrator user role in Virtual Machine Manager \(VMM\).

**Account requirements** Administrators and delegated administrators can create a Delegated Administrator user role. Delegated administrators can create Delegated Administrator user roles that include a subset of their scope, library servers, and Run As accounts.

### To create a Delegated Administrator user role

1.  In the **Settings** workspace, on the **Home** tab in the **Create** group, click **Create User Role**.

2.  In the **Create User Role Wizard**, enter a name and optional description for this Delegated Administrator user role. Click **Next** to continue.

3.  On the **Profile** page, select **Delegated Administrator**, and then click **Next**.

4.  On the **Members** page, click **Add** to add user accounts and Active Directory groups to the user role with the **Select Users, Computers, or Groups** dialog box. After you have added the members, click **Next**.

5.  On the **Scope** page, select private clouds or host groups for this Delegated Administrator, and then click **Next**. A delegated administrator differs from an administrator by having a defined scope in which the delegated administrator can make changes.

6.  On the **Library servers** page, click **Add** to select one or more library servers with the **Select a Library server** dialog box. Click **OK** to select a server, and then click **Next**.

7.  On the **Run As accounts** page, click **Add** to open the **Select a Run As account** dialog box. Select one or more accounts and click **OK** to add the account to the **Run As accounts** page.

    -   Use the Ctrl key to select multiple accounts.

    -   Click the **Create Run As Account** button to access the **Create Run As Account** dialog box.

    After selecting accounts, click **Next** to continue.

8.  Review the settings you have entered and then click **Finish** to create the Delegated Administrator user role.

After you create a delegated administrator, you can change **Members**, **Scope**, **Library servers**, and **Run As accounts** in the **Properties** dialog box for the Delegated Administrator user role.



