---
title: How to Restore Windows Azure Hyper-V Recovery Manager Provider
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 083ef398-adca-4925-ba95-bb9748ebde4f
---
# How to Restore Windows Azure Hyper-V Recovery Manager Provider
If Windows Azure Hyper\-V Recovery Manager is implemented in the VMM environment, then after the upgrade of [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], you need to restore the Windows Azure Hyper\-V Recovery Manager Provider on the VMM management server, as described below. It is recommended that you restore the provider immediately after completing the upgrade to prevent any data loss due to operations being performed before the provider is installed.

### To restore the Windows Azure Hyper\-V Recovery Manager Provider

1.  Re\-install the latest version of Windows Azure Hyper\-V Recovery Manager Provider \(version 3.3.140.0 or later\), which you can download from the[Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=42285). This restores the Provider registration information that was removed during the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] upgrade.

2.  In the Azure portal, in the jobs view, wait for the **Repair Provider** job to complete.

You can now continue to use the service from the Azure portal by re\-initiating any operation that was running before the upgrade.

## See Also
[Performing Post-Upgrade Tasks in VMM](./Performing-Post-Upgrade-Tasks-in-VMM.md)


