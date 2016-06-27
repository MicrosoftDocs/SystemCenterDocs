---
title: Configure Hyper-V extended port ACLs with System Center VMM 2016 Technical Preview
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.service: virtual-network
ms.suite: na
ms.technology: 
  - techgroup-networking
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2684494b-1779-4df8-9f11-db46a0d96542
---
# Configure Hyper-V extended port ACLs with System Center VMM 2016 Technical Preview

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

## Summary
Using System Center Virtual Machine Manager 2016 Technical Preview, you can centrally confgiure and manage Hyper-V port access control lists (ACLs) in your Software Defined Networking (SDN) fabric. These ACLs can be configured for both a Network Controller managed fabric and a non-Network Controller managed fabric.
## Introduction
A port access control list (port ACL) is an object that is attached to various networking primitives to describe network security. The port ACL serves as a collection of access control entries or rules. An ACL can be attached to zero or more networking primitives, such as a VM network, VM subnet, virtual network adapter, or the VMM management server itself. An ACL can contain zero or more ACL rules. Each compatible VMM networking primitive (VM network, VM subnet, virtual network adapter, or VMM management server) can have either one port ACL attached or none.

A port ACL entry or rule is an object that describes filtering policy. Multiple ACL rules can exist in the same port ACL and apply based on their priority. Each ACL rule corresponds to exactly one port ACL.

Global Settings describe a port ACL that is applied to all virtual machine virtual network adapters in the infrastructure. There is no separate object type for Global Settings. Instead, the Global Settings port ACL attaches to the VMM management server itself. The VMM management server object can have either one port ACL or none.

## Supported scenarios

You can use the VMM PowerShell interface to do the following:
* Define port ACLs and ACL rules
The rules are applied to virtual switch ports on Hyper-V servers as "extended port ACLs” (``VMNetworkAdapterExtendedAcl``) in Hyper-V terminology. This means that they can apply only to hosts running Windows Server 2012 R2 or later.

  VMM will not create the "legacy" Hyper-V port ACLs (``VMNetworkAdapterAcl``). Therefore, you cannot apply port ACLs to hosts running Windows Server 2012 or earlier.
  
  All port ACL rules defined in VMM are stateful for TCP. You cannot use VMM to create stateless TCP ACL rules.
* Attach a port ACL to Global Settings. This applies it to all virtual machine virtual network adapters. It is available only to full administrators.
* Attach the port ACLs to VM networks, VM subnets, or VM virtual network adapters. This is available to full administrators, tenant administrators, and self-service users (SSUs).
* View and update port ACL rules configured on the individual virtual machine vNICs.
* Delete port ACLs and their ACL rules.

Each of these actions is covered in more detail later in this topic.

Port ACL settings are exposed only through PowerShell cmdlets in VMM and are not available in the VMM console user interface.

### Define port ACL rules for the port ACL
Each port ACL consists of a collection of port ACL rules. Each rule contains different parameters:
* Name
* Description
* Type
  Inbound/Outbound (the direction in which the ACL will be applied)
* Action
  Allow/Deny (the action of the ACL, either to allow the traffic or to block the traffic)
* SourceAddressPrefix
* SourcePortRange
* DestinationAddressPrefix
* DestinationPortRange
* Protocol: TCP/UDP/Any
   IP-level protocols are not supported in port ACLs that are defined by VMM. They are still supported natively by Hyper-V.
* Priority: 1 – 65535 (lowest number has highest priority). 
  This priority is relative to the layer in which it is applied. More information about how ACL rules are applied based on priority and the object to which     the ACL is attached follows.

If you are configuring Port ACLs for a network controller managed fabric, you must specify a priority equal to or greater than 100. The network controller currently doesn’t support a priority below 100.
#### New PowerShell cmdlets
* ``New-SCPortACLrule -PortACL <PortACL> -Name <string> [-Description <string>] -Type <Inbound | Outbound> -Action <Allow | Deny> -Priority <uint16> -Protocol <Tcp | Udp | Any> [-SourceAddressPrefix <string: IPAddress | IPSubnet>] [-SourcePortRange <string:X|X-Y|Any>] [-DestinationAddressPrefix <string: IPAddress | IPSubnet>] [-DestinationPortRange <string:X|X-Y|Any>]``
* ``Get-SCPortACLrule``
Retrieves all the port ACL rules.
* Name: Optionally filter by name
* ID: Optionally filter by ID
* PortACL: Optionally filter by port ACL

Sample commands:
 

## Unsupported scenarios
VMM does not support the following:
* Manage/update individual rules for a single instance when the ACL is shared with multiple instances. All rules are managed centrally within their parent ACLs and apply wherever the ACL is attached.
* Attach more than one ACL to an entity.
* Apply port ACLs to virtual network adapters (vNICs) in the Hyper-V parent partition (management operating system).
* Create port ACL rules that include IP-level protocols (other than TCP or UDP).
* Apply port ACLs to logical networks, network sites (logical network definitions), subnet vLANs, and other VMM networking primitives that are not listed earlier.
 


