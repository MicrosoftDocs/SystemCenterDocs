---
title: How to Create a New Action Account in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3696c39-5624-47cf-bf07-d15213a132f9
---
# How to Create a New Action Account in Operations Manager
Use the following procedure to create a new action account. The new action account will not, by default, have access to the Operations Manager database unless access is inherited in the credentials you assign to the action account. If not, a new account for accessing the Operations Manager database will need to be created.

### To create a new action account

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In the Administration workspace, right\-click **Run As Accounts**, and then click **Create Run As Account**.

4.  In the **Create Run As Account Wizard**, on the **Introduction** page, click **Next**.

5.  On the **General** page, do the following:

    1.  In the **RunAsAccounttype** list, select **Action Account**.

    2.  Type a display name in the **Display Name** text box.

        > [!NOTE]
        > The display name you enter here becomes the Run As account you will add to a new Run As profile in the following procedure.

    3.  You can also type a description in the **Description** text box.

    4.  Click **Next**.

6.  On the **Account** page, type a user name, password, and then select the domain for the account that you want to make a member of this Run As account, and then click **Next**.

7.  On the **Distribution Security** page, the **More secure** option is selected and cannot be changed. Click **Create**.

8.  In the **Administration** workspace, click **Run As Profiles**.

9. In **Run As Profiles**, right\-click **Default Action Account**, and then click **Properties**.

10. On the **Introduction** and **General Properties** pages, click **Next**.

11. On the **Run As Accounts** page, click **Add**, select the Run As account you created, and then click **OK** twice.

12. Click **Save**.

## See Also
[Managing Access in Operations Manager](./Managing-Access-in-Operations-Manager.md)
[Operations Manager Accounts](./Operations-Manager-Accounts.md)
[Implementing User Roles](./Implementing-User-Roles.md)
[How to Manage the Report Server Unattended Execution Account in Operations Manager](./How-to-Manage-the-Report-Server-Unattended-Execution-Account-in-Operations-Manager.md)
[Control Access by Using the Health Service Lockdown Tool in Operations Manager](./Control-Access-by-Using-the-Health-Service-Lockdown-Tool-in-Operations-Manager.md)
[Accessing UNIX and Linux Computers in Operations Manager](./Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)
[Managing Run As Accounts and Profiles](./Managing-Run-As-Accounts-and-Profiles.md)


