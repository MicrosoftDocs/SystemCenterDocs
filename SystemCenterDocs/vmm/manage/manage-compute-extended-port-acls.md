---
ms.assetid:  2684494b-1779-4df8-9f11-db46a0d96542
title:  Manage port ACLs in VMM 2016
description: Describes how to manage Hyper-V port access control lists (ACLs)
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  03/30/2017
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Manage port ACLs in VMM

>Applies To: System Center 2016 - Virtual Machine Manager

In System Center 2016 - Virtual Machine Manager (VMM), you can centrally configure and manage Hyper-V port access control lists (ACLs). Port ACLs can be configured for both a Network Controller- managed fabric, and for networks that aren't managed by Network Controller.

- A port ACL is a set of rules that filter traffic at the layer 2 port level. A port ACL in VMM filters access to a particular VMM  object. A network object can have no more than one port ACL attached.
- An ACL contains rules, and can be attached to any number of network objects. You can create an ACL without rules, and then add rules at a later time. Each ACL rule corresponds to a only one port ACL
- If an ACL has multiple rules, they are applied based on priority. After a rule matches criteria and is applied, no other rules are processed.
- A global settings port ACL is applied to all VM virtual network adapters in an infrastructure. There's no separate object type for global settings. Instead, the global settings port ACL is attached to the VMM management server.
- Port ACL settings are exposed only through PowerShell cmdlets in VMM, and can't be configured in the VMM console.
- Port ACLs can be applied to:
    - Virtual subnets and adapters in a Network Controller deployment.
    - Virtual subnets, network adapters, VM networks, and the VMM management server in networks that aren't managed by Network Controller.



## Before you start

- To apply an ACL to objects managed by Network Controller, you use the **ManagedByNC** flag, and set it to **True**. If it's not set to **True**, the ACL only applies to network objects that aren't managed by Network Controller.
- ACL types aren't interchangeable. You can’t apply an ACL with **ManagedByNC** set to **false**, to objects managed by Network Controller, and vice versa.
- The key difference between these two kinds of ACLs is that you need to remediate each network adapter, after applying ACL on objects that aren't managed by Network Controller.
- There's also a difference in priority ranges:
    - **Hyper-V port ACLs (not managed by Network Controller)**: 1 - 65535
    - **SDN port ACLs (managed by Network Controller)**: 1 - 64500
- You need full VMM admin permissions to attach a port ACL to global settings. To attach the ACL to VMM objects (VM networks, subnets, virtual network adapters), you need to be a VMM admin or tenant admin, or a self-service user.



## Unsupported scenarios

Here's what you can't currently do:

- Manage individual rules for a single instance, when the ACL is shared with multiple instances. All rules are managed centrally within their parent ACLs, and apply wherever the ACL is attached.
- Attach more than one ACL to an entity.
- Apply port ACLs to virtual network adapters n the Hyper-V parent partition (management operating system).
- Create port ACL rules in VMM that include IP-level protocols (other than TCP or UDP). Other protocols are still supported natively by Hyper-V.
- Apply port ACLs to logical networks, network sites (logical network definitions), subnet VLANs, and other VMM networking objects that aren't mentioned as specifically supported.

## Deployment steps

Use the VMM PowerShell interface to do the following:

1. Define port ACLs and rules.
    - The rules are applied to virtual switch ports on Hyper-V servers as "extended port ACLs" (``VMNetworkAdapterExtendedAcl``). This means that they can apply only to hosts running Windows Server 2012 R2 or later, because VMM doesn't create legacy Hyper-V port ACLs (``VMNetworkAdapterAcl``) for earlier versions.
    - All port ACL rules defined in VMM are stateful for TCP. You can't create stateless TCP ACL rules.
2. Attach a port ACL to global settings. This applies the ACL to all VM virtual network adapters.
3. Attach the port ACLs to VM networks, VM subnets, or VM virtual network adapters.
4. Manage port ACL rules.




## Create port ACLs

1. Open PowerShell in VMM.
2. Create a port ACL with the [New-SCPortACL](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/new-scportacl) cmdlet.

    ```
    New-SCPortACL [-Name] <String> [-Description <String>] [-JobVariable <String>] [-ManagedByNC] [-OnBehalfOfUser <String>] [-OnBehalfOfUserRole <UserRole>] [-Owner <String>] [-PROTipID <Guid>] [-RunAsynchronously] [-UserRole <UserRole>] [-VMMServer <ServerConnection>] [<CommonParameters>]
    ```


### Parameters

**Parameter** | **Details**
--- | ---
Name; Description | Port ACL name and description
JobVariable | Stores job progress
ManagedByNC | Specifies whether objects are managed by Network Controller
OnBehalfOfUser/OnBehalfOfRole | Run job with user name or role
Owner | Specifies the owner of a VMM object in the form of a valid domain user account. Example: Contoso\PattiFuller or PattiFuller@Contoso
ProTipID | ID of ProTip that triggered action
RunAsychronously | Indicates whether job runs asynchronously
UserRole | Specifies user role
VMMServer | Specifies VMM server
CommonParameters | [Learn more](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_CommonParameters)



### Examples

Create a port ACL for objects managed by Network Controller "DemoACLManagedByNC":

    `` PS: C:\> New-SCPortACL -Name "DemoACLManagedByNC" -Description "PortACL Example Managed by NC" -ManagedByN ``

Create a port ACL for objects not managed Network Controller "DemPortACL":

    `` PS: C:\> New-SCPortACL -Name "DemoPortACL" -Description "Port ACL Example Non Managed by NC" ``


## Define port ACL rules for a port ACL

1. Open PowerShell in VMM.
2. Create one or more rules with the [New-SCPortACLRule](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/new-scportaclrule) cmdlet.

    ```
    New-SCPortACLrule -PortACL <PortACL> -Name <string> [-Description <string>] -Type <Inbound | Outbound> -Action <Allow | Deny> -Priority <uint16> -Protocol <Tcp | Udp | Any> [-LocalAddressPrefix <string: IPAddress | IPSubnet>] [-LocalPortRange <string:X|X-Y|Any>] [-RemoteAddressPrefix <string: IPAddress | IPSubnet>] [-RemotePortRange <string:X|X-Y|Any>]

    ```

### Parameters

**Parameter** | **Details**
--- | ---
Name, Description | Rule name and description
Type | Specifies the traffic direction for which the ACL is applied (Inbound or Outbound)
Action | Specifies whether the ACL allows or blocks traffic (Allow or Deny)
LocalAddressPrefix | Specifies the source IP address or subnet that's used to identify traffic that should be filtered.
LocalPortRange | Specifies the source port range that's used to identify traffic.
RemoteAddressPrefix | Specifies the destnation IP address or subnet that's used to identify traffic for filtering.
RemotePortRange | Specifies the destination port range that's used to  identify traffic.
Protocol | Specifies the protocol for which the rule is applied.
Priority | Specify the priority of the rule in in port ACL. Rules are applied according to order. Set a priority between 1 and 65535, where the lowest number has highest priority. Port ACLs  rules for objects managed by Network Controller should be set equal to or greater than 100. Network Controller doesn't support priority below 100.

### Examples

Create a port ACL and store the object in $portACL:

    `` PS: C:\> $portACL = New-SCPortACL -Name "RDP ACL" -Description "Acl on RDP access" ``


Create a port ACL rule to allow RDP access from a remote subnet:

`` PS: C:\> New-SCPortACLRule -Name "AllowRDPAccess" -PortACL $portACL -Description "Allow RDP Rule from a subnet" -Action Allow -Type Inbound -Priority 110 -Protocol Tcp -LocalPortRange 3389 -RemoteAddressPrefix 10.184.20.0/24 ``


Modify the priority of an ACL rule: 
    
    `` PS: C:\> $portACLRule = Get-SCPortACLRule -Name "AllowRDPAccess" `` <br/><br/> `` PS: C:\> Set-SCPortACLRule -PortACLRule $portACLRule -Priority 220 ``
    
The first command gets the port ACL rule "AllowRDPAccess". The second command changes the priority of the rule to 220.


Modify the port ACL rule for the destination address range and protocol for a rule: 

    `` PS: C:\> $portACLRule = Get-SCPortACLRule -Name "AllowRDPAccess" `` <br/><br/> `` PS: C:\> Set-SCPortACLRule -PortACLRule $portACLRule -RemoteAddressPrefix 172.185.21.0/24 -Protocol Udp ``

The first command retrieves rule "AllowRDPAccess". The second changes the protocol to UDP, and sets the destination to subnet 172.185.21.0/24.


## Attach and detach port ACLs

A port ACL can be attached to global settings, VM networks, VM subnets, and virtual network adapters. A port ACL attached to global settings applies by default to all VM virtual network adapters.

1. Open PowerShell in VMM.
2. Attach a portal ACL using the [Set-SCVMMServer](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/set-scvmmserver) cmdlet.

    ```
    Set-SCVMMServer –VMMServer <VMMServer> [-PortACL <NetworkAccessControlList> | -RemovePortACL ]

    ```
### Parameters

**Parameter** | **Details**
--- | ---
VMM server | Name of the VMM server on which the port ACL is applied.
PortACL | Optionally attaches the specified port ACL to global settings.

### Examples

#### Example 1

Attach an ACL to global settings:

    ``Set-SCVMMServer -VMMServer "VMM.Contoso.Local" -PortACL $acl`` <br/><br/> ExampleL: `` Set-SCVMMServer -VMMServer "VMM.Contoso.Local" -PortACL $acl ``

#### Example 2

Detach an ACL from global settings:

    ``Set-SCVMMServer -VMMServer "VMM.Contoso.Local" -RemovePortACL ``
    
#### Example 3

Attach an ACL to a VM network during creation:

    ``New-SCVMNetwork [–PortACL <NetworkAccessControlList>] [rest of the parameters] ``
 
#### Example 4
    
Attach an ACL to an existing VM network:

    ``Set-SCVMNetwork -PortACL $acl ``
    
#### Example 5

Attach an ACL to a VM subnet during creation:

    ``New-SCVMSubnet [–PortACL <NetworkAccessControlList>] [rest of the parameters] ``
    
#### Example 6

Attach an ACL to an existing VM subnet:

    `` Set-SCVMSubnet [–PortACL <NetworkAccessControlList> | -RemovePortACL] [rest of the parameters] ``

## Retrieve and view port ACLs and rules

1. Open PowerShell in VMM.
2. Run the [Get-SCPortACL](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/get-scportacl) cmdlet, to retrieve and view a port ACL:

    ```
    Get-SCPortACL [[-Name] <String> ] [-ID <Guid> ] [-OnBehalfOfUser <String> ] [-OnBehalfOfUserRole <UserRole> ] [-VMMServer <ServerConnection> ] [ <CommonParameters>]

    ```
3. Run the [Get-SCPortACLRule](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/get-scportaclrule) to retrieve and view a rule:

    ```
    Get-SCPortACLRule [-Name <String> ] [-ID <Guid> ] [-OnBehalfOfUser <String> ] [-OnBehalfOfUserRole <UserRole> ] [-PortACL <PortACL> ] [-VMMServer <ServerConnection> ] [ <CommonParameters>] 
    
    ```

### Parameters

**Parameter** | **Details**
--- | ---
No parameters | Retrieves all ACLs
Name/ID | Retrieve by name or GUID
OnBehalfOfUser/OnBehalfOfUserRole | Run with user name or role
VMMServer | Retrieve ACLs on specific VMM server
CommonParameters | [Learn more](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_CommonParameters)

### Examples

Retrieve a specific ACL:
    
    `` PS: C:> $portACL = Get-SCPortACL -Name "DemoPortACL" ``

Get rules for a specific ACL:

    `` PS: C:> Get-SCPortACLRule -Name "AllowRDPAccess" `` 
    
Get all rules for ACL:

    `` PS: C:> Get-SCPortACLRule -PortACL $portACL ``

## Modify port ACLs and rules

1. Open PowerShell in VMM.
2. Run the [Set-SCPortACL](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/VirtualMachineManager/vlatest/Set-SCPortACL) cmdlet, to modify a port ACL:

    `` Set-SCPortACL [-PortACL] <PortACL> [[-Description] <String>] [-JobVariable <String>] [-Name <String>] [-OnBehalfOfUser <String>] [-OnBehalfOfUserRole <UserRole>] [-PROTipID <Guid>] [-RunAsynchronously] [-VMMServer <ServerConnection>] [<CommonParameters>] ``

3. Run the [Remove-SCPortACL](https://docs.microsoft.com/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/remove-scportacl) to remove an ACL:

    `` Remove-SCPortACL [-PortACL] <PortACL> [-Confirm] [-JobVariable <String>] [-OnBehalfOfUser <String>] [-OnBehalfOfUserRole <UserRole>] [-PROTipID <Guid>] [-RunAsynchronously] [-VMMServer <ServerConnection>] [-WhatIf] [<CommonParameters>] ``

 ### Parameters
 
**Parameter** | **Details**
--- | ---
Name/Description | Name and description of port ACL
JobVariable | Stores job progress
OnBehalfOfUser/OnBehalfOfUserRole | Run with user name or role.
ProTipID | ID of ProTip that triggered action
RunAsynchronously | Indicates whether job runs asynchronously.
Confirm | Prompts before running job
WhatIf | Shows what happens without running command


### Examples

Set an ACL description:

    `` PS: C:> $portACL = Get-SCPortACL -Name "DemoPortACL" ``
    `` PS: C:> Set-SCPortACL -PortACL $portACL -Description "Port ACL Example Non Managed by Network Controller" ``

The first cmdlet retrieves the ACL, the second sets the description on the ACL.


Remove an ACL:

`` PS: C:> $portACL = Get-SCPortACL -Name "DemoPortACL" `` 
`` PS: C:> Remove-SCPortACL -PortACL $portACL ``

The first cmdlet retrieves the ACL, the second removes it.
