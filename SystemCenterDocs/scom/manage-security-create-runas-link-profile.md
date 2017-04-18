---
ms.assetid: afe18fe0-2d80-4176-b020-972b09ba6f27
title: How to Create a Run As Account and Associate with a Run As Profile
description: This article describes how to create a Run As account and associate with a profile in Operations Manager 2016. 
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to create a Run As account and associate with a Run As profile

>Applies To: System Center 2016 - Operations Manager

This procedure describes how you create a Run As Account by using a set of Windows credentials as an example. Then it shows you how to edit the properties of the Run As Account to modify the security level and distribution of the credentials. You use this same procedure for all other account types. Once you are completed creating the Run As account, you will associate it with a Run As Profile.  

The credentials that you provide in a Run As Account are used to run tasks, rules, monitors and discoveries as defined by the management pack that they are in. The management pack guide has the settings that you need for configuring the Run As Account and the Run As Profile.
When you create a Run As Account you are warned that you must associate the Run As Account with a Run As profile, and you are not presented with the option to configure Run As Account credential distribution. Both of these activities can be accomplished in the Run As Profile wizard. Alternately, you can configure Run As Account credential distribution by editing the properties of the Run As Account as shown below.  

Both distribution and targeting of Run As accounts must be correctly configured for the Run As profile to work properly.


## Create a Run As account

1. Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2. In the Operations console, click **Administration**.

3. In the **Administration** workspace, right-click **Accounts**, and then click **Create Run As Account**.

4. In the **Create Run As Account Wizard**, on the **Introduction** page click **Next**.

5. On the **General Properties** page, do the following:

    a. Select **Windows** in the **Run As Account** type: list.

    b. Type a display name in the **Display Name** text box. 

    c. Optionally, type a description in the **Description** box.

    d. Click **Next**.

6. On the **Credentials** page, type a user name, and its password, and then select the domain for the account that you want to make a member of this Run As account.

7. Click **Next**.

8. On the **Distribution Security** page, select the **Less secure** or **More secure** option as appropriate. For more information, see [Distribution and Targeting for Run As Accounts and Profiles](manage-security-dist-target-runas-profiles.md).

9. Click **Create**.

10. On the **Run As Account Creation Progress** page, click **Close**.


## Modify Run As account properties

1. In the Operations console, click **Administration**.

2. In the **Administration** workspace, click **Accounts**.

3. In the results pane, double-click the Run As account that you want to edit to open its properties.

4. On the **Run As Account Properties** page, you can edit values on the **General Properties**, **Credentials**, or the **Distribution** tabs. In this case, select the **Distribution** tab.

5. On the **Distribution** tab, in the Selected computers: area, click **Add** to open the **Computer Search** tool. 

6. On the **Computer Search** page, click the Option: list and select one of the following options:

    a. **Search by computer name (Default)**, then type in the computer name in the **Filter by: (Optional)** box. 

    b. **Show suggested computers**, if you have already associated the Run As Account object with a Run As profile, a list of discovered computers that host the monitored service are presented here.

    c. **Show management servers**, in some cases, for example cross platform monitoring, all monitoring is performed by a management server and therefore the credentials have be distributed to the management servers that is performing the monitoring.

7. Optionally, type in a value in the **Filter by: (Optional)** box to narrow the search result set and click **Search**. A list of computers that match the search criteria is displayed in the **Available items** box.

8. Select the computers that you want to distribute the credentials to, and click **Add**. The computers appear in the **Selected Items** box.

9. Click **OK**. This returns you to the **Distribution** tab and the computers are displayed.

10. Click **OK**.


## Associate a Run As account to a Run As profile

This procedure can be used for creating and configuring a new Run As profile, or you can use the configuring section to modify or configure Run As profiles that are pre-existing in your management group. This procedure assumes that you have not previously created a Run As account.

1. Log on to the Operations console with an account that is a member of the Operations Manager Administrators role.

2. In the Operations console, click **Administration**.

3. In the **Administration** workspace, click **Profiles**. 

4. In the results pane, double-click the Run As profile that you want to configure. The **Run As Profile Wizard** opens.

5. In the left pane, click **Run As Accounts**.

6. On the **Run As Accounts** page, click **Add**.

7. In the **Add a Run As Account** window, in the **Run As account** field, select an existing Run As account from the dropdown menu. You can also create an account by clicking **New** and following [Create a Run As Account](#create-a-run-as-account) steps above.

8. Select **All targeted objects** or **A selected class, group, or object**. If you select **A selected class, group, or object**, click **Select**, and then locate and select the class, group, or object that you want the Run As account to be used for. For more information, see [Distribution and Targeting for Run As Accounts and Profiles](manage-security-dist-target-runas-profiles.md).

9. Click **OK** to close the **Add a Run As Account** window. 

10. On the **Run As Accounts** page, click **Save**.

11. On the **Run As Profile Wizard Completion** page, if every account you associated is configured for **Less Secure distribution**, click **Close**. If you associated a Run As account that is configured for **More Secure distribution**, you will see the Run As account listed as a link. Click the link to configure credential distribution, using the following procedure. 


### Configure distribution of a Run As account

1. Open the properties for the Run As account using one of the following methods:

    -  On the **Run As Profile Wizard Completion** page, click the account link.
    -  In the Operations console, in the **Administration** workspace, under **Run As Configuration**, click **Accounts**, and then in the results pane, double-click the account you want to configure.

2. On the **Distribution** tab, click **Add for the Selected computers** box and do the following:

    a. Select **Search by computer name (Default)** or **Show suggested computers**, or **Show management servers**.

	b. Optionally type in a value in the **Filter by: (Optional)** box.

    c. Click **Search**. The result set is returned in the **Available items** box.

    d. Select the computers you want from the result set, and click **Add**. This adds the selected computers to the **Selected objects** box. 

    e. Click **OK**.

3. Click **OK**. 


## Next steps

- Review [Distribution and Targeting for Run As Accounts and Profiles](manage-security-dist-target-runas-profiles.md) to understand how to target Run As account  distribution to agent-managed computers securely.  

- If you need to create new credentials for the management server action account, see [How to Create a New Action Account in Operations Manager](../../z-harvest-om/om/manage/how-to-create-a-new-action-account-in-operations-manager.md).

- To learn about how you can use the The Health Service lockdown tool to limit the identities used to run a rule, task, or monitor on agent-managed systems, see [Control Access by Using the Health Service Lockdown Tool in Operations Manager](How-to-control-access-using-the-health-service-lockdown-tool.md).  
