---
title: How to Create a Run As Account_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd81e7eb-88b4-41df-a4c4-73c4259043a6
---
# How to Create a Run As Account_1
This procedure tells you how to create a Run As Account by using a set of Windows credentials as an example. Then it shows you how to edit the properties of the Run As Account to modify the security level and distribution of the credentials.  You use this same procedure for all other account types.

The credentials that you provide in a Run As Account are used to run tasks, rules, monitors and discoveries as defined by the management pack that they are in. The management pack guide has the settings that you need for configuring the Run As Account and the Run As Profile.

When you create a Run As Account you are warned that you must associate the Run As Account with a Run As profile, and you are not presented with the option to configure Run As Account credential distribution. Both of these activities can be accomplished in the Run As Profile wizard. Alternately, you can configure Run As Account credential distribution by editing the properties of the Run As Account as shown next.

### To create a Run As account

1.  Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**.

3.  In the **Administration** workspace, right\-click **Accounts**, and then click **Create Run As Account**.

4.  In the **Create Run As Account Wizard**, on the **Introduction** page click **Next.**

5.  On the **General Properties** page, do the following:

    1.  Select **Windows** in the **Run As Account type:** list.

    2.  Type a display name in the **Display Name** text box.

    3.  Optionally, type a description in the **Description** box.

    4.  Click **Next**.

6.  On the **Credentials** page, type a user name, and its password, and then select the domain for the account that you want to make a member of this Run As account.

7.  Click **Next**.

8.  On the **Distribution Security** page, select the **Less secure** or **More secure** option as appropriate. For more information, see [Distribution and Targeting for Run As Accounts and Profiles](./Distribution-and-Targeting-for-Run-As-Accounts-and-Profiles.md).

9. Click **Create**.

10. On the **Run As Account Creation Progress** page, click **Close**.

### To modify Run As account properties

1.  In the Operations console, click **Administration**.

2.  In the **Administration** workspace, click **Accounts**.

3.  In the results pane, double\-click the Run As account that you want to edit to open its properties.

4.  On the **Run As Account Properties** page, you can edit values on the **General Properties**, **Credentials**, or the **Distribution** tabs. In this case, select the **Distribution** tab.

5.  On the **Distribution** tab, in the **Selected computers:** area, click **Add** to open the **Computer Search** tool.

6.  On the **Computer Search** page, click the **Option:** list and select one of the following options:

    1.  **Search by computer name \(Default\)**, then type in the computer name in the **Filter by: \(Optional\)** box.

    2.  **Show suggested computers**, if you have already associated the Run As Account object with a Run As profile, a list of discovered computers that host the monitored service are presented here.

    3.  **Show management servers**, in some cases, for example cross platform monitoring, all monitoring is performed by a management server and therefore the credentials have be distributed to the management servers that is performing the monitoring.

7.  Optionally, type in a value in the **Filter by: \(Optional\)** box to narrow the search result set and click **Search**. A list of computers that match the search criteria is displayed in the **Available items** box.

8.  Select the computers that you want to distribute the credentials to, and click **Add**. The computers appear in the **Selected Items** box.

9. Click **OK**. This returns you to the **Distribution** tab and the computers are displayed. Click **OK**.

## See Also
[Managing Run As Accounts and Profiles](./Managing-Run-As-Accounts-and-Profiles.md)
[Distribution and Targeting for Run As Accounts and Profiles](./Distribution-and-Targeting-for-Run-As-Accounts-and-Profiles.md)
[How to Associate a Run As Account to a Run As Profile](./How-to-Associate-a-Run-As-Account-to-a-Run-As-Profile.md)
[How to Create a New Run As Account for Accessing the Operations Manager Database](./How-to-Create-a-New-Run-As-Account-for-Accessing-the-Operations-Manager-Database.md)
[How to Configure Run As Accounts and Profiles for UNIX and Linux Access](./How-to-Configure-Run-As-Accounts-and-Profiles-for-UNIX-and-Linux-Access.md)


