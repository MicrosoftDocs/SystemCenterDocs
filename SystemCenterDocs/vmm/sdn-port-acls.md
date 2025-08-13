---
ms.assetid: fcb4ef4c-b511-402c-9ba6-724169598fe9
title: Allow and block VM traffic with port ACLs in the SDN infrastructure using VMM
description: This article describes how to allow and block network traffic to a particular VM using VMM.
ms.date: 04/21/2025
author: jyothisuri
ms.author: jsuri
ms.update-cycle: 1095-days
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency3, engagement-fy23, engagement-fy24
---

# Allow and block VM traffic using SDN port ACLs



In System Center Virtual Machine Manager (VMM), you can centrally configure and manage software defined network (SDN) port access control lists (ACLs).

- A port ACL is a set of port ACL rules that filter the traffic at layer 2 port level.
- A port ACL in VMM filters access to a specific VMM network object.
- Each VMM network object can have only one port ACL attached.
- An ACL contains rules and can be attached to any number of VMM network objects. You can create an ACL without rules and add the rules later.
- If an ACL has multiple rules, they're applied based on the priority. After a rule matches the criteria and is applied, no other rules are processed.  
- SDN Port ACLs can be applied to virtual subnets and virtual network adapters.

> [!NOTE]
> Port ACL settings are exposed only through PowerShell cmdlets in VMM and can't be configured in the VMM console.  

Using VMM PowerShell, you can also configure Hyper-V port ACLs. For more information, see [Hyper-V port ACLs](hyper-v-acls.md).

This article provides information on how to create and manage SDN port ACLs by using the VMM PowerShell cmdlets.

## Before you start
Before you configure and manage SDN port ACLs, ensure that [SDN network controller](sdn-controller.md) is deployed.


## Create a port ACL

To create a port ACL, follow these steps:

1.	Open PowerShell in VMM.
2.	Create a port ACL.

    ```powershell
    PS C:\> New-SCPortACL -Name "RDPAccess" -Description "PortACL to control RDP access" -ManagedByNC
    ```

    >[!NOTE]
    >
    > The parameter **-ManagedByNC** ensures that the port ACL is managed by Network Controller (NC) and can only be attached to NC managed objects.
    > The cmdlets provided here use example values.

## Create a port ACL rule

To create a port ACL rule, follow these steps:

1.	Get an existing port ACL.

    ```powershell
    PS C:\> $portACL = Get-SCPortACL -Name "RDPAccess"
    ```
2.	Create a port ACL rule.

    ```powershell
    PS C:\> New-SCPortACLRule -Name "AllowRDPAccess" -PortACL $portACL -Description "Allow RDP Rule from a subnet" -Action Allow -Type Inbound -Priority 110 -Protocol Tcp -LocalPortRange 3389 -RemoteAddressPrefix 10.184.20.0/24
    ```
    >[!NOTE]
    > -	Priority range for SDN port ACL rules: 1 – 64500.
    > - Only TCP/UDP/Any protocol parameters are supported for creating ACL rules.

## Attach an ACL to a virtual network adapter

To attach an ACL to a virtual network adapter, follow these steps:

1.	Get the virtual network adapter.

    ```powershell
    PS C:\> $vm = Get-SCVirtualMachine -Name “TenantVM”
    PS C:\> $adapter = Get-SCvirtualNetworkAdapter -VM $vm"
    ```
3. Attach an existing port ACL to the virtual network adapter.

    ```powershell
    PS C:\> $portACL = Get-SCPortACL -Name "RDPAccess"
    PS C:\> Set-SCVirtualNetworkAdapter -VirtualNetworkAdapter $adapter -PortACL $portACL
    ```

    >[!NOTE]
    >
    >You can also attach a port ACL while creating the virtual network adapter through **New-SCVirtualNetworkAdapter** cmdlet. [Learn more](/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/new-scvirtualnetworkadapter).


## Detach a port ACL from a virtual network adapter

To detach a port ACL from a virtual network adapter, follow these steps:

1.	Get the virtual network adapter that you want to detach the port ACL from.

    ```powershell
    PS C:\> $vm = Get-SCVirtualMachine -Name “TenantVM”
    PS C:\> $adapter = Get-SCvirtualNetworkAdapter -VM $vm
    ```

2.	Detach the port ACL from the virtual network adapter.

    ```powershell
    PS C:\> Set-SCVirtualNetworkAdapter -VirtualNetworkAdapter $adapter -RemovePortACL
    ```


## Attach an ACL to a VM subnet

To attach an ACL to a VM subnet, follow these steps:

1. Get the VM subnet to attach the ACL.

   ```powershell
   PS C:\> $vmSubnet = Get-SCVMSubnet -Name “Tenant Subnet”
   ```
2. Attach an existing port ACL to the VM subnet.

    ```powershell
    PS C:\> Set-SCVMSubnet -VMSubnet $vmSubnet -PortACL $portACL
    ```
   >[!NOTE]
   >
   > You can also attach a port ACL while creating VM subnet through **New-SCVMSubnet cmdlet**. [Learn more](/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/new-scvmsubnet).

## Detach a port ACL from a VM subnet

To detach a port ACL from a VM subnet, follow these steps:

1.	Get the VM subnet that you want to detach the port ACL from.

    ```powershell
    PS C:\> $vmSubnet = Get-SCVMSubnet -Name “Tenant Subnet”
    ```
2. Detach the port ACL from the VM subnet.

    ```powershell
    PS C:\> Set-SCVMSubnet –VMSubnet $vmSubnet -RemovePortACL
    ```

## Remove a port ACL rule

To remove a port ACL rule, follow these steps:

1.	Get the port ACL rule that you want to remove.

    ```powershell
    PS C:\> $portACLRule = Get-SCPortACLRule –Name “AllowRDPAccess”
    ```

2. Remove the port ACL rule.

    ```powershell
    PS C:\> Remove-SCPortACLRule -PortACLRule $portACLRule
    ```

## Remove a port ACL

To remove a port ACL, follow these steps:

1.	Get the port ACL that you want to remove.

    ```powershell
    PS C:\> $portACL = Get-SCPortACL -Name “RDPAccess”
    ```

2. Remove the port ACL.

    ```powershell
    PS C:\> Remove-SCPortACL -PortACL $portACL
    ```
