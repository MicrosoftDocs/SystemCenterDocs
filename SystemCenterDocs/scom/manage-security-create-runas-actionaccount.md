---
ms.assetid: 24cefdb6-cc98-4153-af9a-f172d4f72bbf
title: How to Create a New Action Account in Operations Manager
description: This article describes how to create a management server action account in Operations Manager.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 02/09/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# How to create a new action account in Operations Manager

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

Use the following procedure to create a new management server action account. The new action account won't, by default, have access to Operations Manager database unless access is inherited in the credentials you assign to the action account. If not, a new account for accessing the Operations Manager database needs to be created.  

## To create a new action account  

1.  Sign in to the computer with an account that is a member of the Operations Manager Administrators role.  

2.  In the Operations console, select **Administration**.  

3.  In the Administration workspace, right-click **Run As Accounts**, and then select **Create Run As Account**.  

4.  In the **Create Run As Account Wizard**, on the **Introduction** page, select **Next**.  

5.  On the **General** page, do the following:  

    1.  In the **RunAsAccounttype** list, select **Action Account**.  

    2.  Enter a display name in the **Display Name** text box.  

        > [!NOTE]  
        > The display name you enter here becomes the Run As account you will add to a new Run As profile in the following steps.  

    3.  You can also enter a description in the **Description** text box.  

    4.  Select **Next**.  

6.  On the **Account** page, enter a user name, password, and then select the domain for the account that you want to make a member of this Run As account, and select **Next**.  

7.  On the **Distribution Security** page, the **More secure** option is selected and can't be changed. Select **Create**.  

8.  In the **Administration** workspace, select **Run As Profiles**.  

9. In **Run As Profiles**, right-click **Default Action Account**, and then select **Properties**.  

10. On the **Introduction** and **General Properties** pages, select **Next**.  

11. On the **Run As Accounts** page, select **Add**, select the Run As account you created, and select **OK** twice.  

12. Select **Save**.  

## Next steps

- To understand how to create a Run As account and associate with a Run As profile, see [How to Create a Run As Account and Associate with a Run As Profile](manage-security-create-runas-link-profile.md).

- The Report Server unattended execution account is used to query data from the Reporting Data Warehouse. To understand how to reconfigure the user name or password for this account, see [How to Manage the Report Server Unattended Execution Account in Operations Manager](how-to-manage-the-report-server-unattended-execution-account.md).  

- To learn about how you can use the Health Service lockdown tool to limit the identities used to run a rule, task, or monitor on agent-managed systems, see [Control Access by Using the Health Service Lockdown Tool in Operations Manager](~/scom/manage-security-overview-hslockdown.md).  
