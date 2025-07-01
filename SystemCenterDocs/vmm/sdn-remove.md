---
ms.assetid: 2e2323c5-6ec6-4fd2-bec5-70537d328fbe
title: Remove a Software Defined Network (SDN) Infrastructure from VMM
description: This article describes how to remove SDN from the VMM fabric.
author: jyothisuri
ms.author: jsuri
ms.date: 04/09/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---

# Remove a Software Defined Network (SDN) from VMM fabric



To remove an SDN from the System Center Virtual Machine Manager (VMM) fabric, you must remove the following objects in the specified order:

1. VM networks (associated with the NC managed logical networks).
2. Logical networks (managed by NC).
3. Software load balancer (if deployed or deployed and configured).
4. Gateway (if deployed or deployed and configured).
5. Network controller (if deployed or deployed and configured).

## Remove the VM networks

> [!NOTE]
> Ensure that no VMs or NICs are connected to the VM networks that you want to remove.

To remove the VM networks, follow these steps:

1. Select **VMs and Services** > **VM Networks**, and select the VM network to remove.
2. Right-click the VM network and select **Delete**.
3. Repeat steps 1 and 2 for each VM network that you need to remove.

## Remove the logical networks

> [!NOTE]
> Ensure that no port profiles are associated with the logical networks that you want to remove. You can only remove HNV logical network. Do not remove transient network.
>
To remove the logical networks, follow these steps:

1. Select **Fabric** > **Logical networks** and select the logical network to remove.
2. Right-click the logical network and select **Remove**.
3. Repeat steps 1 and 2 for each logical network that you need to remove.

> [!NOTE]
> Logical networks associated with the SLB cannot be removed from the console. Use force delete to remove these (by using **-Force** flag).
>

## Remove the software load balancer

To remove the software load balancer, follow these steps:

1. Select **Fabric** > **Network Services** and select the software load balancer role.
2. Under **Services** > **Associated Services**, select **Browse**, and then select **Clear Selection**.

    This action removes the software load balancer service. Ensure the job is complete. If the job fails, restart the job after making the required changes that the error message details you.
3. Uncheck the pools that are associated with the SLB, except for the private VIP pool that is associated with the SLB Manager VIP.
4. To complete the removal of the SLB, force delete the private VIP pool, the corresponding logical network definition, and the logical networks (by using **-Force** flag).

## Remove the gateway

To remove the gateway, follow these steps:

1. Select **Fabric** > **Network Services** and select the Gateway manager role.
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
To remove the network controller, follow these steps:

1. Select **Fabric** > **Network Services** and select the network controller.
2. Right-click the NC and select **Remove**.

    This action removes the NC service. Ensure that the job is complete. If the job fails, restart the job after making the required changes that the error message details you.
