---
title: How to disable and enable Run As accounts in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a631141-cf10-4200-94ed-f539098d73cd
---
# How to disable and enable Run As accounts in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

To temporarily make a Run As account unavailable for use in Virtual Machine Manager (VMM), you can disable the account. To make the Run As account available for use again, enable the account.

**Account requirements** Administrators and delegated administrators can disable and enable Run As accounts. Delegated administrators can only disable and enable Run As accounts in the scope of their user role.

### To disable a Run As account in VMM

1.  Open the **Settings** workspace.

2.  On the **Settings** pane, expand **Security**, and then click **Run As Accounts**.

3.  On the **Run As Accounts** pane, select the Run As account.

4.  On the **Home** tab, in the **Run As account** group, click **Disable**.

The **Enabled** status of the Run As account changes to a red X. The account is not available until it is enabled.

### To enable a disabled Run As account

1.  Open the **Settings** workspace.

2.  On the **Settings** pane, expand **Security**, and then click **Run As Accounts**.

3.  On the **Run As Accounts** pane, select the disabled Run As account.

4.  On the **Home** tab, in the **Run As account** group, click **Enable**.

## See Also
[Configuring Run As accounts in VMM](Configuring-Run-As-accounts-in-VMM.md)
[Securing VMM resources](Securing-VMM-resources.md)



