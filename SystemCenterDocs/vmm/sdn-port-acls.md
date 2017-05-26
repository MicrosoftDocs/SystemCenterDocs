---
ms.assetid: fcb4ef4c-b511-402c-9ba6-724169598fe9
title: Allow and block VM traffic with port ACLs in the SDN infrastructure using VMM 2016
description: This article describes how to allow and block network traffic to a particular VM using VMM.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: riyazp
ms.date: 05/26/2017
ms.topic: article
ms.prod: system-center-2016
ms.technology: virtual-machine-manager
---

# Allow and block VM traffic with port ACLs in the SDN infrastructure

>Applies To: System Center 2016 - Virtual Machine Manager

In System Center 2016 Virtual Machine Manager (VMM), you can centrally configure and manage software defined network (SDN) port access control lists (ACLs).

- A port ACL is a set of port ACL rules that filter the traffic at layer 2 port level.
- A port ACL in VMM filters access to a specific VMM network object.
- Each VMM network object can have only one port ACL attached.
- An ACL contains rules, and can be attached to any number of VMM network objects. You can create an ACL without rules, and add the rules later.
- If an ACL has multiple rules, they are applied based on the priority. After a rule matches the criteria and is applied, no other rules are processed.  
- SDN Port ACLs can be applied to virtual subnets and virtual network adapters.

> [!NOTE]
>
Port ACL settings are exposed only through PowerShell cmdlets in VMM, and can't be configured in the VMM console.  

Using VMM PowerShell, you can also configure Hyper-V port ACLs. For more information, see [Hyper-v port ACLs](hyper-v-acls.md).

This article provides information about how to create and manage SDN port ACLs by using the VMM PowerShell cmdlets.

## Before you start
Ensure that [SDN network controller](sdn-controller.md) is deployed.


## Create a port ACL

>!NOTE]

> The parameter **-ManagedByNC** ensures that the port ACL is managed by Network Controller (NC) and can only be attached to NC managed objects.

1.	Open PowerShell in VMM.
2.	Create a port ACL.

    ```powershell

        New-SCPortACL -Name "RDPAccess" -Description "PortACL to control RDP access" -ManagedByNC

        ```


## Create a port ACL rule

>!NOTE]
> -	Priority range for SDN port ACL rules: 1 – 64500
> - Only TCP/UDP/Any protocol parameters are supported for creating ACL rules.

1.	Get an existing port ACL.

    ```powershell

    $porACL = Get-SCPortACL -Name "DemoACLManagedByNC"

    ```
2.	Create a port ACL rule.

    ```powershell

    New-SCPortACLRule -Name "AllowRDPAccess" -PortACL $portACL -Description "Allow RDP Rule from a subnet" -Action Allow -Type Inbound -Priority 110 -Protocol Tcp -LocalPortRange 3389 -RemoteAddressPrefix 10.184.20.0/24
    ```


## Attach an ACL to a virtual network adapter

1.	Get the virtual network adapter.

    ```powershell

    $vm = Get-SCVirtualMachine -Name “TenantVM”
    $adapter = Get-SCvirtualNetworkAdapter -VM $vm"

    ```
3. Attach an existing port ACL to the virtual network adapter.

    ```powershell

    $portACL = Get-SCPortACL -Name "DemoACLManagedByNC"
    Set-SCVirtualNetworkAdapter -VirtualNetworkAdapter $adapter -PortACL $portACL

    ```
    >!NOTE]

    > You can also attach a port ACL while creating the virtual network adapter through New-SCVirtualNetworkAdapter cmdlet. [Learn more](https://docs.microsoft.com/en-us/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/new-scvirtualnetworkadapter).


## Detach the port ACL from virtual network adapter
1.	Get the virtual network adapter that you want to detach the port ACL from.

    ```powershell

    $vm = Get-SCVirtualMachine -Name “TenantVM”
    $adapter = Get-SCvirtualNetworkAdapter -VM $vm

    ```

2.	Detach the port ACL from the virtual network adapter.

    ```powershell

    Set-SCVirtualNetworkAdapter -VirtualNetworkAdapter $adapter -RemovePortACL

    ```


## Attach an ACL to a VM subnet

1.	Get the VM subnet to attach the ACL.

    ```powershell

    $vmSubnet = Get-SCVMSubnet -Name “Tenant Subnet”

    ```
2. Attach an existing port ACL to the VM subnet.
    ```powershell

        Set-SCVMSubnet -VMSubnet $vmSubnet -PortACL $portACL

        ```
    >[!NOTE]

    > You can also attach a port ACL while creating VM subnet through New-SCVMSubnet cmdlet. [Learn more](https://docs.microsoft.com/en-us/powershell/systemcenter/systemcenter2016/virtualmachinemanager/vlatest/new-scvmsubnet).

## Detach the port ACL from the VM subnet

1.	Get the VM subnet that you want to detach the port ACL from.

    ```powershell

        $vmSubnet = Get-SCVMSubnet -Name “Tenant Subnet”

    ```
2. Detach the port ACL from the VM subnet.

    ```powershell

        Set-SCVMSubnet – VMSubnet $vmSubnet -RemovePortACL

    ```

## Remove port ACL rule

1.	Get the port ACL rule to remove.

    ```powershell

        $portACLRule = Get-SCPortACLRule –Name “AllowRDPAccess”

    ```

2. Remove the port ACL rule.

    ```powershell

        Remove-SCPortACLRule -PortACLRule $portACLRule

    ```

## Remove port ACL

1.	Get the Port ACL that you want to remove.

    ```powershell

        $portACL = Get-SCPortACL -Name “DemoACLManagedByNC”

    ```

2. Remove the port ACL.

    ```powershell

    Remove-SCPortACL -PortACL $portACL

    ```
