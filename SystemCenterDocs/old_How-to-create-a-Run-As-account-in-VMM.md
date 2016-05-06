---
title: old_How to create a Run As account in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef8633a6-06f4-4277-b6eb-09575fb2c587
---
# old_How to create a Run As account in VMM
In[!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)], the credentials that a user enters for any process can be provided by a Run As account. A Run As account is a container for a set of stored credentials. For more information about Run As accounts, see [Configuring Run As accounts in VMM](../Topic/Configuring-Run-As-accounts-in-VMM.md).

**Account requirements** Administrators and delegated administrators can create Run As accounts.

### To create a Run As account in VMM

1.  Open the **Settings** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create Run As Account**.

    The **Create Run As Account** dialog box opens.

3.  Enter a name and optional description to identify the credentials in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)].

4.  Enter credentials for the Run As account in the **User name** and **Password** text boxes. The credentials can be a valid Active Directory user or group account or they can be local credentials.

5.  Unselect **Validate domain credentials**, if desired.

6.  Click **OK** to create the Run As account.

