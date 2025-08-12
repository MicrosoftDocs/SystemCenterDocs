---
ms.assetid: 81cb4616-6574-471f-a939-d05198d0d65c
title: Control Access by using the Health Service Lockdown Tool in Operations Manager
description: This article describes how to configure the Operations Manager agent Health Service with restricted privileges.
author: jyothisuri
ms.author: jsuri
ms.date: 04/22/2025
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Control access by using the Health Service Lockdown Tool in Operations Manager

This article describes how to configure the Operations Manager agent Health Service with restricted privileges.

On computers requiring high security, for example a domain controller, you might need to deny certain identities access to rules, tasks, and monitors that might jeopardize the security of your server. The Health Service lockdown tool (HSLockdown.exe) enables you to use various command-line options to control and limit the identities used to run a rule, task, or monitor.  

> [!NOTE]  
> You'll be unable to start the Microsoft Monitoring Agent service if you've used the Health Service Lockdown tool to lock out the Action Account. To be able to restart the Microsoft Monitoring Agent service, follow the second procedure in this article to unlock the Action Account.  

The following command\-line options are available:  

-   HSLockdown \[ManagementGroupName\] /L - List Accounts\/groups  

-   HSLockdown \[ManagementGroupName\] /A - Add an allowed account|group  

-   HSLockdown \[ManagementGroupName\] /D - Add a denied account|group  

-   HSLockdown \[ManagementGroupName\] /R - Remove an allowed\/denied account|group  

Accounts must be specified in one of the following fully qualified domain name (FQDN) formats:  

- NetBios : DOMAIN\username  

- UPN     : username@fqdn.com  

If you used the add or deny options when running the Health Service Lockdown tool, you'll need to restart the System Center Management service before the changes take effect.  

When evaluating allowed and denied listings, know that denials take priority over allows. If a user is listed as allowed, and the same user is a member of a group that is listed as denied, the user will be denied.  

## Deny an account with the health service lockdown tool

To deny an account with the health service lockdown tool, follow these steps:

1.  Sign in to the computer with an account that is a member of the Administrators group.  

2.  On the Windows desktop, select **Start**, and then select **Run**.  

3.  In the **Run** dialog, enter **cmd** and then select **OK**.  

4.  At the command prompt, enter ```<drive_letter>:``` (where ```<drive_letter>``` is the drive where the Operations Manager agent is installed) and then press **ENTER**.  

5.  Enter `cd \Program Files\Microsoft Monitoring Agent\Agent` and then press **ENTER**.  

6.  Enter `HSLockdown.exe [Management Group Name] /D [account or group]` to deny the group or account, and then press **ENTER**.  

7.  Restart the Microsoft Monitoring Agent (HealthService) service to apply changes.

## Unlock the Action account

To unlock the Action account, follow these steps:

1.  Sign in to the computer with an account that is a member of the Administrators group.  

2.  On the Windows desktop, select **Start**, and then select **Run**.  

3.  In the **Run** dialog, enter **cmd** and then select **OK**.  

4.  At the command prompt, enter ```<drive_letter>:``` (where ```<drive_letter>``` is the drive where the Operations Manager agent is installed) and then press **ENTER**.  

5.  Enter `cd \Program Files\Microsoft Monitoring Agent\Agent` and then press **ENTER**.  

6.  Enter `HSLockdown.exe [Management Group Name] /A <Action Account>` and then press **ENTER**.  

7.  Restart the Microsoft Monitoring Agent (HealthService) service to apply changes.

## Add the Local System account

To add a Local System account, follow these steps:

1.  Sign in to the computer with an account that is a member of the Administrators group.  

2.  On the Windows desktop, select **Start**, and then select **Run**.  

3.  In the **Run** dialog, enter **cmd** and then select **OK**.  

4.  At the command prompt, enter ```<drive_letter>:``` (where ```<drive_letter>``` is the drive where the Operations Manager agent is installed) and then press **ENTER**.  

5.  Enter `cd \Program Files\Microsoft Monitoring Agent\Agent` and then press **ENTER**.  

6.  Enter `HSLockdown.exe [Management Group Name] /A “NT AUTHORITY\SYSTEM”` and then press **ENTER**.

7.  Restart the Microsoft Monitoring Agent (HealthService) service to apply changes.

## Next steps

- To understand how to create a Run As account and associate with a Run As profile, see [Create a Run As Account and Associate with a Run As Profile](manage-security-create-runas-link-profile.md).

- If you need to create new credentials for the management server action account, see [Create a new Action Account in Operations Manager](manage-security-create-runas-actionaccount.md).

- To understand how to target Run As account distribution to agent-managed computers securely, review [Distribution and Targeting for Run As Accounts and Profiles](manage-security-dist-target-runas-profiles.md).  
