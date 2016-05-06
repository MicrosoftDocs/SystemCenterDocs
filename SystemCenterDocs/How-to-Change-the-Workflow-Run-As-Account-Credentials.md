---
title: How to Change the Workflow Run As Account Credentials
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3b4abd2-a00d-47d8-a578-c54fb32eda21
---
# How to Change the Workflow Run As Account Credentials
During setup, you defined the account to be assigned to the [!INCLUDE[smshort](./Token/smshort_md.md)] Workflow Run As account. If the password for that account changes, you must update the Workflow Run As account with the new password. If you want to change the account for the [!INCLUDE[smshort](./Token/smshort_md.md)] Workflow Run As account, you must change both the Workflow Run As account and the Workflow User Role.

Use the following procedures to define a new user account for the Workflow Run As account and to update a new password for the existing account.

### To change the Workflow Run As account using new credentials

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, expand **Security**, and then click **Run As Accounts**.

3.  In the **Run As Accounts** pane, click **Workflow Account**.

4.  In the **Tasks** pane, click **Properties**.

5.  In the **Workflow Account** page, in the **User name**, **Password**, and **Domain** boxes, type the new credentials for the Workflow Run As account, and then click **OK**.

6.  In the **Administration** pane, click **User Roles**.

7.  In the **User Roles** pane, click **Workflows**.

8.  In the **Tasks** pane, click **Properties**.

9. In the Edit User Role Wizard, click **Users**.

10. Click **Remove** to remove the existing credentials, click **Add** to add the credentials you specified in step 5, and then click **OK**.

    > [!IMPORTANT]
    > Failure to configure the new account for the Workflow Run As account and User Role causes [!INCLUDE[smshort](./Token/smshort_md.md)] to stop functioning.

### To change the password for the Workflow Run As account credentials

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, expand **Security**, and then click **Run As Accounts**.

3.  In the **Run As Accounts** pane, click **Workflow Account**.

4.  In the **Tasks** pane, click **Properties**.

5.  In the **Workflow Account** page, in the **Password** box, type the new password for the Workflow Run As account, and then click **OK**.


