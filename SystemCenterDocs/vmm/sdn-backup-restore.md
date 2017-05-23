---
ms.assetid: 1a71c7fa-faa3-4d0a-a8ef-d022c803f298
title: Back up and restore a software defined network infrastructure using VMM 2016
description: This article describes the procedure to back up and restore the software defined infrastructure.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: riyazp
ms.date: 05/23/2017
ms.topic: article
ms.prod: system-center-2016
ms.technology: virtual-machine-manager
---

# Back up and restore the SDN infrastructure

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes the backup and recovery process of SDN Infrastructure in Virtual Machine Manager (VMM) environment, and provides applicable recommendations.

## Back up the SDN infrastructure

Backup the network controller database using the network controller Rest API. [Learn more](https://docs.microsoft.com/en-us/windows-server/networking/sdn/manage/update-backup-restore#a-namebkmkbackupabackup-the-sdn-infrastructure).

## Bring up the new network controller

Use the following procedures to bring up a new network controller:

1. in the VMM console, **Fabric** > **Network Service**, right-click and select the network controller service, click **Remove**.

    > [!NOTE]

    > Remove the network controller service instance only. Do not remove the network controller.

    ![back up and restore sdn](media/sdn-backup-restore/back-up-restore-sdn.png)

2. Deploy new network controller service instance form the VMM using the same service deployment settings that were  used for the original service instance deployment. [Learn more](https://docs.microsoft.com/en-us/system-center/vmm/sdn-controller).

3. Verify that the deployment job is successful.  



## Restore the SDN infrastructure from a backup

Restore the network controller from a network controller backup by using the network controller Rest API. [Learn more](https://docs.microsoft.com/en-us/windows-server/networking/sdn/manage/update-backup-restore#a-namebkmkrestorearestore-the-sdn-infrastructure-from-a-backup).

## Refresh network controller and synchronize VMM and NC
Depending on the SDN state captured in the network controller backup and current VMM state, some of the resources in VMM and network controller might be out of sync.

Use the following refresh procedures to find any differences between VMM and NC, and accordingly resolve them in case any.


> [!NOTE]
> - Refresh cmdlets for refreshing network controller objects are available from VMM 2016 UR3.
> - If the network controller contains any objects which are not present in VMM DB, then the  VMM will not refresh (even if those objects are created using VMM earlier). Delete those objects from NC and recreate the objects from VMM to manage these objects from VMM again.

### Refresh port ACLs
1. Get all the NC managed port ACLs from the VMM server by using the following cmdlet:

    ```powershell

    Get-SCPortACL | Where-Object {$_.ManagedByNC -eq $True}

    ```
2. Run the Read-SCPortACL cmdlet on all the NC managed port ACLs to refresh:

    ```powershell

    Get-SCPortACL | Where-Object {$_.ManagedByNC -eq $True} | Read-SCPortACL
    ```

3. Verify the VMM job logs for the result status and follow the recommendations from the job's log in case of any failures.

### Refresh logical networks
1.	Get all the NC managed logical networks from the VMM
server by using the following cmdlet:

    ```powershell
    Get-SCLogicalNetwork | Where-Object {$_.IsManagedByNetworkController -eq $True}
    ```

2.	Run the Read- SCLogicalNetwork cmdlet on the NC managed logical networks to refresh.

    ```powershell
    Get-SCLogicalNetwork | Where-Object {$_.IsManagedByNetworkController -eq $True} | Read-SCLogicalNetwork

    ```

3. Verify the VMM job logs for the result status and follow the recommendations from the job's log in case of any failures.

### Refresh gateways and load balancers
1.	Get all the gateways and load balancers by using the following cmdlet:

    ```powershell
    $networkService =  Get-SCNetworkService  | Where-Object {$_.Model -eq 'Microsoft Network Controller'}
    $fabricRoles = Get-SCFabricRole -NetworkService $networkService
    $fabricRoleResources = @()
    foreach($fabricRole in $fabricRoles)
    {
	$fabricRoleResources += $fabricRole.ServiceVMs
    }
    $fabricRoleResources
```

2.	Run Read- SCFabricRoleResource cmdlet to refresh.

    ```powershell
    foreach($fabricRoleResource in $fabricRoleResources)
    {
	Read-SCFabricRoleResource -FabricResource $fabricRoleResource
    }
    ```

3.	Verify the VMM job logs for the result status and follow the recommendations from the job's log in case of any failures.

### Refresh NAT connections and NAT rules
1.	Get all the NAT connections by using the following cmdlet:

    ```powershell

    $vmNetworks = Get-SCVMNetwork | Where-Object {$_.NetworkManager.Model -eq 'Microsoft Network Controller' -and $_.IsolationType -eq 'WindowsNetworkVirtualization'}

    $natConnections = @()
    foreach($vmNetwork in $vmNetworks)
    {
	$natConnections += $vmNetwork.NATConnections
    }
    $natConnections

    ```
2.	Run Read- SCNATConnection  to refresh NAT connections and NAT rules.

    ```powershell
    foreach($natConnection in $natConnections)
    {
	Read-SCNATConnection -NATConnection $natConnection
    }
    ```
3.	Verify the VMM job logs for the result status and follow the recommendations from the job's log in case of any failures.

### Refresh all load balancer VIPs
1.	Get all the load balancer VIPs configured on NC by using the following cmdlet:

    ```powershell
    Get-SCLoadBalancerVIP |  Where-Object {$_.LoadBalancer.Model -eq 'Microsoft Network Controller'}
    ```
2.	Run Read- SCLoadBalancerVIP to refresh all the load balancer VIPs.

    ```powershell
    Get-SCLoadBalancerVIP |  Where-Object {$_.LoadBalancer.Model -eq 'Microsoft Network Controller'}  | Read- SCLoadBalancerVIP  
    ```
3.	Verify the VMM job logs for the result status and follow the recommendations from the job's log in case of any failures.

### Refresh VM Networks
> [!NOTE]

> Refresh cmdlets for VM networks, VM network gateways, and VM network gateway pools  will be available in the upcoming VMM updates. To manually refresh the VM networks, use the following procedure:

1.	Get all the NC managed HNV VM networks from the VMM server by using the following cmdlet:

    ```powershell
    Get-SCVMNetwork | Where-Object {$_.NetworkManager.Model -eq 'Microsoft Network Controller' -and $_.IsolationType -eq 'WindowsNetworkVirtualization'}
    ```
2.	For each VM network, fetch the corresponding virtual network in the NC using the ResourceId as ExternalId of the VM Network. [Learn more](https://technet.microsoft.com/en-us/itpro/powershell/windows/networkcontroller/get-networkcontrollervirtualnetwork).

    ```powershell
    Get-NetworkControllerVirtualNetwork -ResourceId $vmNetwork.ExternalId
    ```

3. Validate if there are any differences between the VMM server  and NC, and update the VM network in the VMM server as required.
4.	Verify the VMM job logs for the result status and follow the recommendations from the job's log in case of any failures.


### Refresh VM network gateways

1.	Get all the VM networks that are configured with VM network gateways by using the following cmdlet:
    ```powershell
$vmNetworks = Get-SCVMNetwork | Where-Object {$_.NetworkManager.Model -eq 'Microsoft Network Controller' -and $_.IsolationType -eq 'WindowsNetworkVirtualization'  -and $_.VMNetworkGateways.Count -gt 0}}
```
2.	Get the virtual gateways configured in NC using the following cmdlet. [Learn more](https://technet.microsoft.com/en-us/itpro/powershell/windows/networkcontroller/get-networkcontrollervirtualgateway):
    ```powershell
    Get-NetworkControllerVirtualGateway cmdlet.

    ```
3.	Validate all the properties of virtual gateway, VPN connections,  BGP routers, BGP peers and check if they are in sync between VMM and NC.

    > [!NOTE]

    > You can correlate the  VMM VM network and the virtual gateway in NC. Look for the virtual gateway whose gateway subnet resources contain the corresponding virtual network.

4.	Verify the VMM job logs for the result status and follow the recommendations from the job's log in case of any failures.




### Refresh gateway pools

1.	Get the gateway fabric role from the VMM server by using the following cmdlet:

    ```powershell
    $networkService =  Get-SCNetworkService  | Where-Object {$_.Model -eq 'Microsoft Network Controller'}
    $gatewayFabricRole = Get-SCFabricRole -NetworkService $networkService | Where-Object {$_. RoleType -eq ‘Gateway’}

    ```
2.	Get the gateway pool with ResourceId “Default” from NC using the Get-NetworkControllerGatewayPool cmdlet. [Learn more](https://technet.microsoft.com/en-us/itpro/powershell/windows/networkcontroller/get-networkcontrollergatewaypool)
3.	Verify all the properties of the gateway pool are in sync between VMM and NC and update the properties in VMM as required.
