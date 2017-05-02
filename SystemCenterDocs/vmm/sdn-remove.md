---
ms.assetid: 2e2323c5-6ec6-4fd2-bec5-70537d328fbe
title: Remove a Software Defined Network (SDN) from VMM 2016
description: This article describes how to remove SDN from the VMM fabric.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: riyazp
ms.date: 03/01/2017
ms.topic: article
ms.prod: system-center-2016
ms.technology: virtual-machine-manager
---

# Remove a Software Defined Network (SDN) from VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

To remove SDN from System Center 2016 Virtual Machine Manager (VMM), you must remove the following objects - in the specified order:

- VM networks (associated with the NC managed logical networks).
- Logical networks (managed by NC).
- Software load balancer (if deployed or deployed and configured).
- Gateway (if deployed or deployed and configured).
- Network controller (if deployed or deployed and configured).

## Remove the VM networks

> [!NOTE]
> Ensure that no VMs or NICs are connected to the VM networks that you want to remove.
>

1. Click **VMs and Services** > **VM Networks**, select the VM network to remove.
2. Right-click the VM network and click **Delete**.
3. Repeat steps 1&2 for each VM network that you need to remove.

## Remove the logical networks

> [!NOTE]
> Ensure that no port profiles are associated with the logical networks that you want to remove.
>

1. Click **Fabric** > **Logical networks**, select the logical network to remove.
2. Right-click the logical network and click **Remove**.
3. Repeat steps 1&2 for each logical network that you need to remove.

> [!NOTE]
> Logical networks associated with the SLB cannot be removed from the console. Use force delete to remove these (by using **-Force** flag).
>

## Remove the software load balancer

1. Click **Fabric** > **Network Services**, select the software load balancer role.
2. Under **Services** > **Associated Services**, click **Browse** and then click **Clear Selection**.

    This action removes the software load balancer service.  Ensure the job is complete. If the job fails, restart the job after making the required changes that the error message details you.
3. Uncheck the pools that are associated with the SLB, except for the private VIP pool that is  associated with the SLB Manager VIP.
4. To complete the removal of the SLB, force delete the  private VIP pool, corresponding logical network definition and logical networks ((by using **-Force** flag).

## Remove the gateway

1. Click **Fabric** > **Network Services**, select the Gateway manager role.
2. Under **Services** > **Associated Services**, click **Browse** and then click **Clear Selection**.

    This action removes the gateway service.  Ensure the job is complete. If the job fails, restart the job after making the required changes that the error message details you.
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

1. Click **Fabric** > **Network Services**, select the network controller.
2. Right-click the NC and click **Remove**.

    This action removes the NC service.  Ensure the job is complete. If the job fails, restart the job after making the required changes that the error message details you.
