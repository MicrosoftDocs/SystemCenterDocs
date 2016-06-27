---
title: How to delete a Run As account in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0097ed16-d9c3-4af4-9d14-7abd73afcbc1
---
# How to delete a Run As account in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Use the following procedure to delete a Run As account that is not being currently consumed by any process in Virtual Machine Manager (VMM). VMM blocks deletion of any Run As account being consumed by a process.

**Account requirements** Administrators can delete Run As accounts. Delegated administrators who have Run As accounts in the scope of their user role can delete those Run As accounts.

### To delete a Run As account

1.  Open the **Settings** workspace.

2.  In the **Settings** pane, expand **Security**, and then click **Run As accounts**.

3.  In the results pane, select the Run As account.

4.  On the **Home** tab, in the **Delete** group, click **Delete**, and then click **Yes** to confirm.

The credentials are removed from the VMM database.

## See Also
[Configuring Run As accounts in VMM](Configuring-Run-As-accounts-in-VMM.md)
[Securing VMM resources](Securing-VMM-resources.md)



