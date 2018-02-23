---
ms.assetid: 05fe26c2-25a5-44a0-8a34-20a387d317a3
title: VMM 1801 release notes
description: This article details release notes for System Center Virtual Machine Manager 1801.
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  riyazp
ms.date:  02/05/2018
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
monikerRange: 'sc-vmm-1801'
---

# VMM 1801 release notes

This article summarizes the release notes for System Center 1801 - Virtual Machine Manager (VMM).

## Latest accessibility fixes in Console are not available

 **Description**: Latest accessibility fixes in Console might not be available when you use .NET 4.7 while installing the VMM Console.

 **Workaround**: We recommend using .NET 4.7.1 while installing the VMM Console. For detailed information on .NET 4.7.1 migration, see [the article on .NET migration
  ](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/retargeting/4.7-4.7.1).

## Backend adapter connectivity for SLB MUX doesn't work as expected

**Description**: Backend adapter connectivity of SLB MUX might not work as expected after VM migration.

**Workaround**: Users scale in/scale out in the SLB MUX VM as a workaround.

## Connectivity issues for SLB addresses

**Description**: For frontend and backend IP addresses assigned to Software Load Balancer MUX VMs, you might experience connectivity issues if **Register this connection's address in DNS** is selected.

**Workaround**: Clear the setting to avoid issues with these IP addresses.

## Upgrade might fail if the name of a default port classification has been changed

**Description**: When you change the original name of a default port classification and then try to upgrade to VMM 1801 – upgrade might fail with the following error message in the VMM set log.

*Violation of PRIMARY KEY constraint 'PK_tbl_NetMan_PortClassification'. Cannot insert duplicate key in object 'dbo.tbl_NetMan_PortClassification*. 

**Workaround**: Change the port classification name back to original name, and then trigger the upgrade. After the upgrade, you can change the default name to a different one.
