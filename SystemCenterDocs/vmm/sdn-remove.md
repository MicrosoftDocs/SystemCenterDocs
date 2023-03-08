---
ms.assetid: 2e2323c5-6ec6-4fd2-bec5-70537d328fbe
title: Remove a Software Defined Network (SDN) infrastructure from VMM 2016
description: This article describes how to remove SDN from the VMM fabric.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 11/07/2017
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
ms.custom: UpdateFrequency3
---

# Remove a Software Defined Network (SDN) from VMM fabric

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

To remove an SDN from the System Center Virtual Machine Manager (VMM) fabric, you must remove the following objects in the specified order:

- VM networks (associated with the NC managed logical networks).
- Logical networks (managed by NC).
- Software load balancer (if deployed or deployed and configured).
- Gateway (if deployed or deployed and configured).
- Network controller (if deployed or deployed and configured).

## Remove the VM networks

> [!NOTE]
> Ensure that no VMs or NICs are connected to the VM networks that you want to remove.
>

1. Select **VMs and Services** > **VM Networks**, and select the VM network to remove.
2. Select and hold the VM network and select **Delete**.
3. Repeat steps 1&2 for each VM network that you need to remove.

## Remove the logical networks

> [!NOTE]
> Ensure that no port profiles are associated with the logical networks that you want to remove. You can only remove HNV logical network. Do not remove transient network.
>

1. Select **Fabric** > **Logical networks**, and select the logical network to remove.
2. Select and hold the logical network and select **Remove**.
3. Repeat steps 1 and 2 for each logical network that you need to remove.

> [!NOTE]
> Logical networks associated with the SLB cannot be removed from the console. Use force delete to remove these (by using **-Force** flag).
>

## Remove the software load balancer

1. Select **Fabric** > **Network Services**, and select the software load balancer role.
2. Under **Services** > **Associated Services**, select **Browse**, and then select **Clear Selection**.

    This action removes the software load balancer service. Ensure the job is complete. If the job fails, restart the job after making the required changes that the error message details you.
3. Uncheck the pools that are associated with the SLB, except for the private VIP pool that is  associated with the SLB Manager VIP.
4. To complete the removal of the SLB, force delete the private VIP pool, the corresponding logical network definition, and the logical networks ((by using **-Force** flag).

## Remove the gateway

1. Select **Fabric** > **Network Services**, and select the Gateway manager role.
2. Under **Services** > **Associated Services**, select **Browse**, and then select **Clear Selection**.

    This action removes the gateway service. Ensure the job is complete. If the job fails, restart the job after making the required changes that the error message details you.
3. To complete the removal of the gateway, remove the gateway pool by using the following PowerShell scripts:

    ```powershell
    $nc=get-scnetworkservice | Where {$_.Model -eq "Microsoft Network Controller"}
    $gwrole=get-scfabricrole -NetworkService $nc | Where {$_.RoleType -eq "Gateway"}
    Set-SCFabricRole -FabricRole  $gwrole  -GatewayConfiguration $null
    ```

## Remove the network controller

> [!NOTE]
> Ensure that SLB/GW and associated logical networks are successfully removed.
>

1. Select **Fabric** > **Network Services**, and select the network controller.
2. Select and hold the NC and select **Remove**.

    This action removes the NC service. Ensure that the job is complete. If the job fails, restart the job after making the required changes that the error message details you.
