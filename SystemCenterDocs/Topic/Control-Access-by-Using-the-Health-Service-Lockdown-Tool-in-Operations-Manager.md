---
title: Control Access by Using the Health Service Lockdown Tool in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f9a2852-5b2c-4738-a796-5a83fe10d6d3
---
# Control Access by Using the Health Service Lockdown Tool in Operations Manager
On computers requiring high security, for example a domain controller, you may need to deny certain identities access to rules, tasks, and monitors that might jeopardize the security of your server. The Health Service lockdown tool \(HSLockdown.exe\) enables you to use various command\-line options to control and limit the identities used to run a rule, task, or monitor.

> [!NOTE]
> You will be unable to start the System Center Management service if you have used the Health Service Lockdown tool to lock out the Action Account. To be able to restart the System Center Management service, follow the second procedure in this topic to unlock the Action Account.

The following command\-line options are available:

-   HSLockdown \[ManagementGroupName\] \/L \- List Accounts\/groups

-   HSLockdown \[ManagementGroupName\] \/A \- Add an allowed account|group

-   HSLockdown \[ManagementGroupName\] \/D \- Add a denied account|group

-   HSLockdown \[ManagementGroupName\] \/R \- Remove an allowed\/denied account|group

Accounts must be specified in one of the following fully qualified domain name \(FQDN\) formats:

-   NetBios : DOMAIN\\username

-   UPN     : username@fqdn.com

If you used the add or deny options when running the Health Service Lockdown tool, you will need to restart the System Center Management service before the changes take effect.

When evaluating allowed and denied listings, know that denies takes priority over allows. If a user is listed as allowed, and the same user is a member of a group that is listed as denied, the user will be denied.

### To use the health service lockdown tool

1.  Log on to the computer with an account that is a member of the Administrators group.

2.  On the Windows desktop, click **Start**, and then click **Run**.

3.  In the **Run** dialog box, type **cmd** and then click **OK**.

4.  At the command prompt, type <drive\_letter>: \(where <drive\_letter> is the drive where the Operations Manager installation media is located\) and then press ENTER.

5.  Type **cd\\Program Files\\System Center Operations Manager 2012\\Server** and then press ENTER.

6.  Type **HSLockdown \[Management Group Name\] \/D \[account or group\]** to deny the group or account, and then press ENTER.

### To unlock the Action Account

1.  Log on to the computer with an account that is a member of the Administrators group.

2.  On the Windows desktop, click **Start**, and then click **Run**.

3.  In the **Run** dialog box, type **cmd** and then click **OK**.

4.  At the command prompt, type <drive\_letter>: \(where <drive\_letter> is the drive where the Operations Manager installation media is located\) and then press **ENTER**.

5.  Type **cd\\Program Files\\System Center Operations Manager 2012** and then press ENTER.

6.  Type **HSLockdown \[Management Group Name\] \/A <Action Account>** and then press ENTER.

## See Also
[Managing Access in Operations Manager](../Topic/Managing-Access-in-Operations-Manager.md)
[Operations Manager Accounts](../Topic/Operations-Manager-Accounts.md)
[Implementing User Roles](../Topic/Implementing-User-Roles.md)
[How to Create a New Action Account in Operations Manager](../Topic/How-to-Create-a-New-Action-Account-in-Operations-Manager.md)
[How to Manage the Report Server Unattended Execution Account in Operations Manager](../Topic/How-to-Manage-the-Report-Server-Unattended-Execution-Account-in-Operations-Manager.md)
[Accessing UNIX and Linux Computers in Operations Manager](../Topic/Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)
[Managing Run As Accounts and Profiles](../Topic/Managing-Run-As-Accounts-and-Profiles.md)

