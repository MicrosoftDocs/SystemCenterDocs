---
ms.assetid: 81cb4616-6574-471f-a939-d05198d0d65c
title: Control Access by Using the Health Service Lockdown Tool in Operations Manager
description: This article describes how to configure the Operations Manager agent Health Service with restricted privileges.   
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Control access by using the Health Service Lockdown Tool in Operations Manager

>Applies To: System Center 2016 - Operations Manager

On computers requiring high security, for example a domain controller, you may need to deny certain identities access to rules, tasks, and monitors that might jeopardize the security of your server. The Health Service lockdown tool (HSLockdown.exe) enables you to use various command\-line options to control and limit the identities used to run a rule, task, or monitor.  
  
> [!NOTE]  
> You will be unable to start the System Center Management service if you have used the Health Service Lockdown tool to lock out the Action Account. To be able to restart the System Center Management service, follow the second procedure in this topic to unlock the Action Account.  
  
The following command\-line options are available:  
  
-   HSLockdown \[ManagementGroupName\] /L - List Accounts\/groups  
  
-   HSLockdown \[ManagementGroupName\] /A - Add an allowed account|group  
  
-   HSLockdown \[ManagementGroupName\] /D - Add a denied account|group  
  
-   HSLockdown \[ManagementGroupName\] /R - Remove an allowed\/denied account|group  
  
Accounts must be specified in one of the following fully qualified domain name (FQDN) formats:  
  
-   NetBios : DOMAIN\username  
  
-   UPN     : username@fqdn.com  
  
If you used the add or deny options when running the Health Service Lockdown tool, you will need to restart the System Center Management service before the changes take effect.  
  
When evaluating allowed and denied listings, know that denies takes priority over allows. If a user is listed as allowed, and the same user is a member of a group that is listed as denied, the user will be denied.  
  
### To use the health service lockdown tool  
  
1.  Log on to the computer with an account that is a member of the Administrators group.  
  
2.  On the Windows desktop, click **Start**, and then click **Run**.  
  
3.  In the **Run** dialog box, type **cmd** and then click **OK**.  
  
4.  At the command prompt, type ```<drive_letter>:``` (where ```<drive_letter>``` is the drive where the Operations Manager agent is installed) and then press ENTER.  
  
5.  Type **cd\Program Files\Microsoft Monitoring Agent\Agent** and then press ENTER.  
  
6.  Type **HSLockdown \[Management Group Name\] /D \[account or group\]** to deny the group or account, and then press ENTER.  
  
### To unlock the Action account  
  
1.  Log on to the computer with an account that is a member of the Administrators group.  
  
2.  On the Windows desktop, click **Start**, and then click **Run**.  
  
3.  In the **Run** dialog box, type **cmd** and then click **OK**.  
  
4.  At the command prompt, type ```<drive_letter>:``` (where ```<drive_letter>``` is the drive where the Operations Manager agent is installed) and then press **ENTER**.  
  
5.  Type **cd\Program Files\Microsoft Monitoring Agent\Agent** and then press ENTER.  
  
6.  Type **HSLockdown \[Management Group Name\] /A \<Action Account\>** and then press ENTER.  
  
## Next steps

- To understand how to create a Run As account and associate with a Run As profile, see [How to Create a Run As Account and Associate with a Run As Profile](../om/manage/how-to-create-a-run-as-account-and-associate-to-a-profile.md).

- If you need to create new credentials for the management server action account, see [How to Create a New Action Account in Operations Manager](../../z-harvest-om/om/manage/how-to-create-a-new-action-account-in-operations-manager.md).

- Review [Distribution and Targeting for Run As Accounts and Profiles](manage-security-dist-target-runas-profiles.md) to understand how to target Run As account  distribution to agent-managed computers securely.  
