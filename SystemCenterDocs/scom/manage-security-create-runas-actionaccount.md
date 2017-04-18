---
ms.assetid: 24cefdb6-cc98-4153-af9a-f172d4f72bbf
title: How to Create a New Action Account in Operations Manager
description: This article describes how to create a management server action account in Operations Manager 2016. 
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to create a new action account in Operations Manager

>Applies To: System Center 2016 - Operations Manager

Use the following procedure to create a new management server action account. The new action account will not, by default, have access to Operations Manager database unless access is inherited in the credentials you assign to the action account. If not, a new account for accessing the Operations Manager database will need to be created.  
  
## To create a new action account  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  In the Administration workspace, right-click **Run As Accounts**, and then click **Create Run As Account**.  
  
4.  In the **Create Run As Account Wizard**, on the **Introduction** page, click **Next**.  
  
5.  On the **General** page, do the following:  
  
    1.  In the **RunAsAccounttype** list, select **Action Account**.  
  
    2.  Type a display name in the **Display Name** text box.  
  
        > [!NOTE]  
        > The display name you enter here becomes the Run As account you will add to a new Run As profile in the following steps.  
  
    3.  You can also type a description in the **Description** text box.  
  
    4.  Click **Next**.  
  
6.  On the **Account** page, type a user name, password, and then select the domain for the account that you want to make a member of this Run As account, and then click **Next**.  
  
7.  On the **Distribution Security** page, the **More secure** option is selected and cannot be changed. Click **Create**.  
  
8.  In the **Administration** workspace, click **Run As Profiles**.  
  
9. In **Run As Profiles**, right-click **Default Action Account**, and then click **Properties**.  
  
10. On the **Introduction** and **General Properties** pages, click **Next**.  
  
11. On the **Run As Accounts** page, click **Add**, select the Run As account you created, and then click **OK** twice.  
  
12. Click **Save**.  
  
## Next steps

- To understand how to create a Run As account and associate with a Run As profile, see [How to Create a Run As Account and Associate with a Run As Profile](manage-security-create-runas-link-profile.md).

- The Report Server unattended execution account is used to query data from the Reporting Data Warehouse.  See [How to Manage the Report Server Unattended Execution Account in Operations Manager](how-to-manage-the-report-server-unattended-execution-account.md) to understand how to reconfigure the user name or password for this account.  

- To learn about how you can use the The Health Service lockdown tool to limit the identities used to run a rule, task, or monitor on agent-managed systems, see [Control Access by Using the Health Service Lockdown Tool in Operations Manager](~/scom/manage-security-overview-hslockdown.md).  


