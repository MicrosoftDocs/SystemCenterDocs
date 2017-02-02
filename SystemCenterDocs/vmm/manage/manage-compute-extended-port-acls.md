---
ms.assetid:  2684494b-1779-4df8-9f11-db46a0d96542
title:  Manage port ACLs in VMM 2016
description: Describes how to manage Hyper-V port access control lists (ACLs)
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  02/02/2017
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Manage port ACLs in VMM 2016

>Applies To: System Center 2016 - Virtual Machine Manager


System Center 2016 Virtual Machine Manager (VMM) supports  Hyper-V port access control lists (port ACLS) and SDN port ACLs. You can centrally configure and manage these port ACLs.


- A port access control list (port ACL) is an object that is attached to various networking primitives to describe the network security.
- Port ACLs serve as a collection of access control entries or rules. An ACL can contain zero or more ACL rules.
- A port ACL entry or rule is an object that describes filtering policy. Multiple ACL rules can exist in the same port ACL and can be applied based on their priority. Each ACL rule corresponds to exactly one port ACL.
- An ACL can be attached to zero or more networking primitives, such as a VM network, VM subnet, virtual network adapter, or the VMM management server itself.
- Each compatible VMM networking primitive  can have either one port ACL attached or none.
- Global settings describe a port ACL that is applied to all VM virtual network adapters in the infrastructure. There is no separate object type for Global Settings. Instead, the Global Settings port ACL attaches to the VMM management server itself. The VMM management server object can have either one port ACL or none.

**Note**:  Port ACL settings are exposed only through PowerShell cmdlets in VMM and are not available in the VMM console.

 Virtual Machine Manager 2016 supports the following (Two) Port ACLs:
 - ACLS that can be applied on Network Controller (NC) managed objects.

     - Applicable only to NIC and subnets. This type of ACL can’t be applied on VMM Servers and VM Networks.

- ACLS that can be applied on non-NC managed objects.

    - Applicable to VM network, VM subnet, virtual network adapter, or the VMM management server itself.

**Note**: To apply an ACL to NC managed objects, you must use **ManagedByNC** flag and set it to **true**. Else, the created ACL will only be applicable to non-NC managed objects.

The ACL types are not interchangeable. which means, you can’t apply an ACL with **ManagedByNC** set as **false** to NC managed objects and vice versa.

One key difference between the two kinds of ACL is that while you need to remediate each NIC after applying ACL on non-NC objects, no such step is required in case you are applying Port ACLs on NC managed objects.

Also, note the difference in the priority ranges between NC managed and Non-NC managed ACL rules.

**Here are the priority ranges**:
- Hyper-V port ACLs:    1 - 65535
- SDN port ACLs:        1 - 64500



## Supported scenarios

Use the VMM PowerShell interface to do the following:

- Define port ACLs and ACL rules
    - The rules are applied to virtual switch ports on Hyper-V servers as "extended port ACLs" (``VMNetworkAdapterExtendedAcl``) in Hyper-V terminology. This means that they can apply only to hosts running Windows Server 2012 R2 or later.
    - VMM will not create the "legacy" Hyper-V port ACLs (``VMNetworkAdapterAcl``). Therefore, you cannot apply port ACLs to hosts running Windows Server 2012 or earlier.
    - All port ACL rules defined in VMM are stateful for TCP. You cannot use VMM to create stateless TCP ACL rules.
- Attach a port ACL to Global Settings. This applies it to all virtual machine virtual network adapters. It is available only to full administrators.
- Attach the port ACLs to VM networks, VM subnets, or VM virtual network adapters. This is available to full administrators, tenant administrators, and self-service users (SSUs).
- View and update port ACL rules configured on the individual virtual machine vNICs.
- Delete port ACLs and their ACL rules.

## Unsupported scenarios

Currently, VMM does not support the following:
* Manage/update individual rules for a single instance when the ACL is shared with multiple instances. All rules are managed centrally within their parent ACLs and apply wherever the ACL is attached.
* Attach more than one ACL to an entity.
* Apply port ACLs to virtual network adapters (vNICs) in the Hyper-V parent partition (management operating system).
* Create port ACL rules that include IP-level protocols (other than TCP or UDP).
* Apply port ACLs to logical networks, network sites (logical network definitions), subnet vLANs, and other VMM networking primitives that are not listed earlier.


## Define port ACL rules for the port ACL

Each port ACL consists of a collection of port ACL rules. Each rule contains different parameters:
*	Name
*	Description
*	Type Inbound/Outbound (the direction in which the ACL will be applied)
*	Action Allow/Deny (the action of the ACL, either to allow the traffic or to block the traffic)
*	LocalAddressPrefix
*	LocalPortRange
*	RemoteAddressPrefix
*	RemotePortRange
*	Protocol: TCP/UDP/Any IP-level protocols are not supported in port ACLs that are defined by VMM. They are still supported natively by Hyper-V.
*	Priority: 1 " 65535 (lowest number has highest priority). This priority is relative to the layer in which it is applied. More information about how ACL rules are applied based on priority and the object to which the ACL is attached follows.
If you are configuring Port ACLs for a network controller managed fabric, you must specify a priority equal to or greater than 100. The network controller currently doesn't support a priority below 100.


#### New PowerShell cmdlets

* New-SCPortACLrule -PortACL <PortACL> -Name <string> [-Description <string>] -Type <Inbound | Outbound> -Action <Allow | Deny> -Priority <uint16> -Protocol <Tcp | Udp | Any> [-LocalAddressPrefix <string: IPAddress | IPSubnet>] [-LocalPortRange <string:X|X-Y|Any>] [-RemoteAddressPrefix <string: IPAddress | IPSubnet>] [-RemotePortRange <string:X|X-Y|Any>]


*	Get-SCPortACLrule
* Title: Retrieves all the port ACL rules.
*	Name: Optionally filter by name
*	ID: Optionally filter by ID
*	PortACL: Optionally filter by port ACL
*	Get-SCPortACL

*	Title: Get a PortACL
*	Description:  The command gets the specified PortACL

*	Example 1:
*	PS: C:\> Get-SCPortACL -Name "DemoPortACL"


*	Set-SCPortACL
*	Title: Modifies description of the PortACL
*	Description:  The first command gets the PortACL by name "DemoPortACL". The second command changes the port ACL description.

* Code:  
*	PS: C:\> $portACL = Get-SCPortACL -Name "DemoPortACL"
*	PS: C:\> Set-SCPortACL -PortACL $portACL -Description "Port ACL Example Non Managed by Network Controller"

*	New-SCPortACL
*	Title: Creates a Port ACL Not managed by NC
*	Description: The command creates a port ACL with name "DemPortACL" which is not managed by NC

*	Example 1:
*	PS: C:\> New-SCPortACL -Name "DemoPortACL" -Description "Port ACL Example Non Managed by NC"

*	Title: Creates a PortACL managed by NC
*	Description:  The command creates a port ACL with name "DemoACLManagedByNC" which is managed by NC

*	Example2:
*	PS: C:\> New-SCPortACL -Name "DemoACLManagedByNC" -Description "PortACL Example Managed by NC" -ManagedByNC


*	Remove-SCPortACL
*	Title: Removes a PortACL
*	Description: The first command gets a port ACL by name "DemoPortACL". The second command removes the port ACL.

*	Example1:
*	PS: C:\> $portACL = Get-SCPortACL -Name "DemoPortACL"
*	PS: C:\> Remove-SCPortACL -PortACL $portACL


*	New-SCPortACLRule
*	Title: Create a new port acl rule
*	Description: The first command creates a port ACL and stores the object in $portACL. The second command creates a port ACL rule to allow RDP access from a remote subnet.

*	Example 1:
*	PS: C:\> $portACL = New-SCPortACL -Name "RDP ACL" -Description "Acl on RDP access"
*	PS: C:\> New-SCPortACLRule -Name "AllowRDPAccess" -PortACL $portACL -Description "Allow RDP Rule from a subnet" -Action Allow -Type Inbound -Priority 110 -Protocol Tcp -LocalPortRange 3389 -RemoteAddressPrefix 10.184.20.0/24


*	Get-SCPortACLRule
*	Title: Get a port acl rule
*	Description: The command gets the port acl rule by name "AllowRDPAccess"

*	Example 1:
*	PS: C:\> Get-SCPortACLRule -Name "AllowRDPAccess"	 
*	Title: Get port acl rules from an acl
*	Description:  The first command gets the port ACL of name "RDP ACL". The second command gets all the rules under the port ACL

*	Example 2:
*	PS: C:\> $portACL = Get-SCPortACL -Name "RDP ACL"
*	PS: C:\> Get-SCPortACLRule -PortACL $portACL


*	Remove-SCPortACLRule
*	Title: Remove a port ACL rule
*	Description: The first command gets the port ACL rule of name "AllowRDPAccess". The second command gets removes the port ACL rule.

*	Example 1:
*	PS: C:\> $portACLRule = Get-SCPortACLRule -Name "AllowRDPAccess"
*	PS: C:\> Remove-SCPortACLRule -PortACLRule $portACLRule


*	Set-SCPortACLRule
*	Title: Modify the port ACL rule priority
*	Description: The first command gets the port acl rule of name "AllowRDPAccess". The second command changes the priority of the rule to 220.

*	Example 1:
*	PS: C:\> $portACLRule = Get-SCPortACLRule -Name "AllowRDPAccess"
*	PS: C:\> Set-SCPortACLRule -PortACLRule $portACLRule -Priority 220


*	Title: Modify the port acl rule remote address range & protocol
*	Description: The first command gets the port acl rule of name "AllowRDPAccess". The second command changes the protocol of the acl rule to udp and sets the remote address range to a new subnet 172.185.21.0/24
*	Example2:
*	PS: C:\> $portACLRule = Get-SCPortACLRule -Name "AllowRDPAccess"
*	PS: C:\> Set-SCPortACLRule -PortACLRule $portACLRule -RemoteAddressPrefix 172.185.21.0/24 -Protocol Udp
