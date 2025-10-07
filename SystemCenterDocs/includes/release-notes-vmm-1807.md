---
ms.assetid: 1bbf9096-f1aa-438a-b40e-8df3c021f3b2
title: include file
description: include file to detail the release notes for System Center 1807 Virtual Machine Manager
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  07/24/2018
ms.topic:  include
ms.service:  system-center
ms.subservice:  virtual-machine-manager
---

## VMM 1807 release notes

The following sections summarize the release notes for VMM 1807 and include the known issues and workarounds.

## Latest accessibility fixes in Console are not available

 **Description**: Latest accessibility fixes in Console might not be available when you use .NET 4.7 while installing the VMM Console.

 **Workaround**: We recommend using .NET 4.7.1 while installing the VMM Console. For detailed information on .NET 4.7.1 migration, see [the article on .NET migration
  ](/dotnet/framework/migration-guide/retargeting/4.7-4.7.1).

## Backend adapter connectivity for SLB MUX doesn't work as expected

**Description**: Backend adapter connectivity of SLB MUX might not work as expected after VM migration.

**Workaround**: Users scale in/scale out in the SLB MUX VM as a workaround.

## Connectivity issues for SLB addresses

**Description**: For frontend and backend IP addresses assigned to Software Load Balancer MUX VMs, you might experience connectivity issues if **Register this connection's address in DNS** is selected.

**Workaround**: Clear the setting to avoid issues with these IP addresses.

## VMM integrated with Azure Site Recovery will not support DRA versions earlier than 5.1.3100

**Description**: In case you're using a VMM integrated with Azure Site Recovery, VMM supports Data Recovery Agent (DRA) version [5.1.3100](https://aka.ms/downloaddra) or higher. Earlier versions aren't supported.

**Workaround**: Use the following steps and upgrade the DRA version:

1. Uninstall existing version of DRA
2. Install VMM 1807 patch)
3. [Install 5.1.3100](https://aka.ms/downloaddra) version or higher.

## Host/Cluster refresh might take longer if there are large number of logical network definitions

**Description**: When there are a large number of logical network definitions in the environment, cluster/host refresh might take longer than expected.

## Set-SCVMSubnet -RemovePortACL job completes in VMM without removing portACL association from NC VMSubnet object

**Description**: Set-SCVMSubnet -RemovePortACL job completes in VMM without removing portACL association from NC VMSubnet object, due to which Remove-PortACL job fails with NC Exception that is still in use.

**Workaround**: Remove the VMSubnet from VMM and then remove Port-ACL.

 Import-Module NetworkController

 #Replace the URI of the Network Controller with REST IP or FQDN

 ```
 $uri = "<NC FQDN or IP>"

 ```

 #Provide NC Admin credentials

 ```
 $cred = Get-Credential

 ```

 #Identify the virtual network that contains the subnet

 ```
 $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Fabrikam_VNet1" -Credential $cred

 ```

 #Identify the subnet for which the ACL needs to be removed

 ```
 $vnet.Properties.Subnets[0].Properties = $vnet.Properties.Subnets[0].Properties | Select-Object -Property * -ExcludeProperty AccessControlList

 ```

 #Update

 ```
 New-NetworkControllerVirtualNetwork -ResourceId "Fabrikam_VNet1" -ConnectionUri $uri –Properties $vnet.Properties -Credential $cred

 ```