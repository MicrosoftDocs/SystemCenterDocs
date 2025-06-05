---
ms.assetid: 05fe26c2-25a5-44a0-8a34-20a387d317a3
title: include file
description: include file to detail the release notes for System Center Virtual Machine Manager 1801
author: jyothisuri
ms.author: jsuri
ms.date:  04/30/2018
ms.topic:  include
ms.service:  system-center
ms.subservice:  virtual-machine-manager
---

## VMM 1801 release notes

The following sections summarize the release notes for VMM 1801 and include the known issues and workarounds.

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

## Upgrade might fail if the name of a default port classification has been changed

**Description**: When you change the original name of a default port classification and then try to upgrade to VMM 1801 – upgrade might fail with the following error message in the VMM setup log.

*Violation of PRIMARY KEY constraint 'PK_tbl_NetMan_PortClassification'. Cannot insert duplicate key in object 'dbo.tbl_NetMan_PortClassification'*.

**Workaround**: Change the port classification name back to the original name, and then trigger the upgrade. After the upgrade, you can change the default name to a different one.

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