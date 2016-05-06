---
title: How to Create a New Run As Account for Accessing the Operations Manager Database
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 001dae2a-a333-4725-965b-ab536a8d184d
---
# How to Create a New Run As Account for Accessing the Operations Manager Database
Use the following procedure to create a new Run As account that can access the operational database.

### To create a new Run As account for accessing the Operations Manager database

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In the **Administration** workspace, right\-click **Run As Accounts**, and then click **Create Run As Account** .

4.  In the **Create Run As Account Wizard**, on the **Introduction** page, click **Next**.

5.  On the **General** page, do the following:

    1.  Select **Windows** in the **Run As Account type** list.

    2.  Type a display name in the **Display Name** text box.

        > [!NOTE]
        > The display name you enter here becomes the Run As account you will add to a new Run As profile in the following procedure.

    3.  You can also type a description in the **Description** text box.

    4.  Click **Next**.

6.  On the **Account** page, type a user name, password, and then select the domain for the account that you want to make a member of this Run As account, and then click **Create**.

### To assign the new Run As account to the Operational Database Account Run As profile

1.  In the **Administration** workspace, under **Run As Configuration**, click  **Profiles**.

2.  In the **Profiles** list, right\-click **Operational Database Account**, and then click **Properties**.

3.  On the **Introduction** and **General Properties** pages, click **Next**.

4.  Under **Run As accounts**, click **Add**.

5.  In the **Add a Run As Account** dialog box, click the **Run As Account** dropdown menu, click the Run As account you created in the previous procedure, and then click **OK**.

6.  Click **Save**.

### To grant SQL Server Login rights for the new account

1.  On the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.

2.  In the **Connect to Server** dialog box, in the **Server Type** list, select **Database Engine**, in the **Server Name** list select the server and instance for your Operations Manager database \(for example, computer\\INSTANCE1\), in **Authentication** list, select **WindowsAuthentication**, and then click **Connect**.

3.  In the **Object Explorer** pane, expand **Security**, right\-click **Logins**, and then select **New Login**.

4.  In the **Login \- New** dialog box, click **Windows authentication**, and then click **Search**.

5.  In the **Select User or Group** dialog box, enter the user or group name that you used when you created the new Run As account, click **Check Names**, and then click **OK**.

6.  In the **Login \- New** dialog box, click **OK**.

### To grant access to the Operations Manager database

1.  On the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008** , and then click **SQL Server Management Studio**.

2.  In the **Connect to Server** dialog box, in the **Server Type** list, select **Database Engine**, in the **Server Name** list select the server and instance for your Operations Manager database \(for example, computer\\INSTANCE1\), in **Authentication** list, select **WindowsAuthentication**, and then click **Connect**.

3.  In the **Object Explorer** pane, expand **Databases**, expand **Operations Manager**, expand **Security**, right\-click **Users**, and then click **New User**.

4.  In the **Database User \- New** dialog box, type a name for this new user in the **User name** text box, and then click the ellipses \(**…**\) next to the **Login name** option.

5.  In the **Select Login** dialog box, click **Browse**.

6.  In the **Browse for Objects** dialog box, click the check box next to the new login, and then click **OK**.

7.  In the **Database User \- New** dialog box, in the **Database role membership** list, select **dbmodule\_users**, and then click **OK**.

## See Also
[Managing Run As Accounts and Profiles](../Topic/Managing-Run-As-Accounts-and-Profiles.md)
[How to Create a Run As Account](../Topic/How-to-Create-a-Run-As-Account.md)
[Distribution and Targeting for Run As Accounts and Profiles](../Topic/Distribution-and-Targeting-for-Run-As-Accounts-and-Profiles.md)
[How to Associate a Run As Account to a Run As Profile](../Topic/How-to-Associate-a-Run-As-Account-to-a-Run-As-Profile.md)
[How to Configure Run As Accounts and Profiles for UNIX and Linux Access](../Topic/How-to-Configure-Run-As-Accounts-and-Profiles-for-UNIX-and-Linux-Access.md)

