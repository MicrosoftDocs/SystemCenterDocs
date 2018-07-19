---
ms.assetid: 1bbf9096-f1aa-438a-b40e-8df3c021f3b2
title: include file
description: include file to detail the release notes for System Center 1807 Virtual Machine Manager
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  07/24/2018
ms.topic:  include
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

## VMM 1807 release notes

The following sections summarize the release notes for VMM 1807 and includes the known issues and workarounds.

## Latest accessibility fixes in Console are not available

 **Description**: Latest accessibility fixes in Console might not be available when you use .NET 4.7 while installing the VMM Console.

 **Workaround**: We recommend using .NET 4.7.1 while installing the VMM Console. For detailed information on .NET 4.7.1 migration, see [the article on .NET migration
  ](https://docs.microsoft.com/dotnet/framework/migration-guide/retargeting/4.7-4.7.1).

## Backend adapter connectivity for SLB MUX doesn't work as expected

**Description**: Backend adapter connectivity of SLB MUX might not work as expected after VM migration.

**Workaround**: Users scale in/scale out in the SLB MUX VM as a workaround.

## Connectivity issues for SLB addresses

**Description**: For frontend and backend IP addresses assigned to Software Load Balancer MUX VMs, you might experience connectivity issues if **Register this connection's address in DNS** is selected.

**Workaround**: Clear the setting to avoid issues with these IP addresses.

## VMM integrated with ASR will not support DRA versions earlier than 5.1.3100

**Description**: In case you are using a VMM integrated with Azure Site Recovery (ASR), VMM supports DRA version [5.1.3100](http://aka.ms/downloaddra) or higher. Earlier versions are not supported.

**Workaround**: Use the following steps and upgrade the DRA version:

1. Uninstall existing version of DRA
2. Install VMM 1807 patch
3. [Install 5.1.3100](http://aka.ms/downloaddra) version or higher.   

**Workaround**:
