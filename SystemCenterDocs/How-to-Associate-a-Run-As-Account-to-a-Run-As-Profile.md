---
title: How to Associate a Run As Account to a Run As Profile
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 946a0d66-6bdc-4a2b-8788-5c8f25b6cd22
---
# How to Associate a Run As Account to a Run As Profile
In [!INCLUDE[om12long](./Token/om12long_md.md)], Run As accounts are associated with Run As profiles to provide the necessary credentials for workflows that use that Run As profile to run successfully. Both distribution and targeting of Run As accounts must be correctly configured for the Run As profile to work properly.

1.  Identify the class, group, or objects the Run As account will be applied to. For more information, see [Distribution and Targeting for Run As Accounts and Profiles](./Distribution-and-Targeting-for-Run-As-Accounts-and-Profiles.md).

2.  Create the Run As account. For more information, see [How to Create a Run As Account](./How-to-Create-a-Run-As-Account.md).

3.  Associate the Run As account with the Run As profile.

4.  Configure the distribution of Run As account object credentials to specific computers.

This procedure can be used for creating and configuring a new Run As profile, or you can use the configuring section to modify or configure Run As profiles that are pre\-existing in your management group. This procedure assumes that you have not previously created a Run As account.

### To associate a Run As account to a Run As profile

1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In the **Administration** workspace, click **Profiles**.

4.  In the results pane, double\-click the Run As profile that you want to configure. The Run As Profile Wizard opens.

5.  In the left pane, click **Run As Accounts**.

6.  On the **Run As Accounts** page, click **Add**.

7.  In the **Add a Run As Account** window, in the **Run As account** field, select an existing Run As account from the dropdown menu. You can also create an account by clicking **New** and following the steps in the [How to Create a Run As Account](./How-to-Create-a-Run-As-Account.md) topic.

8.  Select **All targeted objects** or **A selected class, group, or object**. If you select **A selected class, group, or object**, click **Select**, and then locate and select the class, group, or object that you want the Run As account to be used for. For more information, see [Distribution and Targeting for Run As Accounts and Profiles](./Distribution-and-Targeting-for-Run-As-Accounts-and-Profiles.md).

9. Click **OK** to close the **Add a Run As Account window**.

10. On the **Run As Accounts** page, click **Save**.

11. On the **Run As Profile Wizard Completion** page, if every account you associated is configured for **Less Secure distribution**, click **Close**. If you associated a Run As account that is configured for **More Secure distribution**, you will see the Run As account listed as a link. Click the link to configure credential distribution, using the following procedure.

### To configure distribution of a Run As account

1.  Open the properties for the Run As account using one of the following methods:

    -   On the **Run As Profile Wizard Completion** page, click the account link.

    -   In the Operations console, in the **Administration** workspace, under **Run As Configuration**, click **Accounts**, and then in the results pane, double\-click the account you want to configure.

2.  On the **Distribution** tab, click **Add** for the **Selected computers** box and do the following:

    1.  Select **Search by computer name \(Default\)** or **Show suggested computers**, or **Show management servers**.

    2.  Optionally type in a value in the **Filter by: \(Optional\)**  box.

    3.  Click **Search**. The result set is returned in the **Available items** box.

    4.  Select the computers you want from the result set, and click **Add**. This adds the selected computers to the **Selected objects** box.

    5.  Click **OK**.

3.  Click **OK**.

## See Also
[Managing Run As Accounts and Profiles](./Managing-Run-As-Accounts-and-Profiles.md)
[How to Create a Run As Account](./How-to-Create-a-Run-As-Account.md)
[Distribution and Targeting for Run As Accounts and Profiles](./Distribution-and-Targeting-for-Run-As-Accounts-and-Profiles.md)
[How to Create a New Run As Account for Accessing the Operations Manager Database](./How-to-Create-a-New-Run-As-Account-for-Accessing-the-Operations-Manager-Database.md)
[How to Configure Run As Accounts and Profiles for UNIX and Linux Access](./How-to-Configure-Run-As-Accounts-and-Profiles-for-UNIX-and-Linux-Access.md)


