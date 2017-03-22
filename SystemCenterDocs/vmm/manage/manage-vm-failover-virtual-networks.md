---
ms.assetid: 1e065bb4-b2a4-4632-a262-67bdfc23f0d1
title: Configure VM failover between virtual networks in VMM
description: This article describes how to fail over VMs between virtual networks without Azure Site Recovery
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  03/20/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---


# Configure VM failover between virtual networks

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to handle replication and failover of VMs between virtual networks when you're not using the Azure Site Recovery service to manage disaster recovery.

- We recommend that you use Azure Site Recovery for replicating VMs. VMM doesn't manage Hyper-V Replica without Site Recovery, and you need to use Hyper-V Replica PowerShell cmdlets to automate Hyper-V Replica operations.
- For disaster recovery, we recommend that you use separate primary and secondary virtual networks. Primary VMs connect to the primary network, and replica VMs to the secondary network. This ensures that both VMs can be connected to a network at the same time.
- If you have a single virtual network, use Site Recovery to automate network management using the network mapping feature. If you don't use Site Recovery, you need to carefully check prerequisites, and the order in which VMs are attached to the network. In particular, the replica VM and primary VM mustn't be connected to the single virtual network at the same time. Otherwise, CA-PA records might get deleted in VMM, and cause network connectivity loss.

## Sample solution

This sample solution describes the following environment:

- A single VMM server manages both primary and secondary sites.
- Primary and replica VMs are hosted on a single Hyper-V virtual network.
- You want to run a planned failover, and retain the IP address of the VM after the failover.
- VMs have IPv4 addresses.

## Before you start

- Make sure that the virtual switch and logical switch settings are valid and match in the VMM fabric. If they don't, network attach operations might not succeed after failover.
- The primary VM should be connected to a virtual network
- The replica VM shouldn't be connected to a network
- Only one IP address should be assigned to each network adapter of the primary VM. Run this command to ensure this. If there's more than one connected network adapter on the VM, run it for adapter by changing the array index.

        ``$VMOnPD = Get-SCVirtualMachine -Name "VM Name" | where {$_.IsPrimaryVM -eq $true}
        Get-SCIPAddress –GrantToObjectId $VMOnPD.VirtualNetworkAdapters[0].ID``

- Make sure that the IP address assigned to the VM by the operating system is the same as the IP address shown above. Log onto the VM and run **ipconfig** to check this.
- Check that lookup tables are correctly set on the primary and replica . To do this, run the following command on each server, and ensure that there is an entry that corresponds to the IP address returned above: **Get-NetVirtualizationLookupRecord**
- Check that the IP address is IPv4, and not IPv6
- Make sure both VMs are turned off before you run the scripts.
- Make sure that the replication state is enabled on both VMs.

## Run the planned failover script

Here's what this script does:

1. For each network adapter on a primary VM, it stores the IP address, VM network, and IP pool.
2. Revokes all of the IP addresses for each network adapter on the primary and secondary VMs.
3. Disconnects all network adapters.
4. Fails over the primary and secondary VMs.
5. Optionally starts reverse replication.
6. Gives the same IP address (for each network adapter) to the replica VM.
7. Attaches each network adapter on the replicate VM to the VM networks that were stored in step 1.

### Run the script

The script takes two arguments:

- $VMName – Name of the virtual machine
- $ReverseRep – Boolean argument to specify whether reverse replication should be performed or not.
    - If $true is passed then the reverse replication is started immediately, and you can't cancel failover later.
    - After this script is completed successfully with $ReverseRep as $true:
        - The primary VM should be in a **Prepared for planned failover** replication state.
        - The replica VM should be in a **Failover complete** replication state
    - If $false is passed, then reverse replication won't be performed. ReverseRepORCancelFO.ps1 can be used to either perform reverse replication or cancel the failover
    - After the script is completed successfully with $ReverseRep as $false:
        - The primary VM should be in a **Prepared for planned failover** replication state
        - The replica VM should be in a **Failover complete** replication state.

If the script doesn't complete any of the  steps, you need to manually complete the failed steps, and then return to the PowerShell window. The script steps include failover of the primary VM, failover of the replica VM, and optionally, reverse replication.

Run the script:

``Param(
 [Parameter(Mandatory=$True)]
   [string]$VMName,
 [Parameter(Mandatory=$true)]
   [boolean]$ReverseRep
)

# the script running on system with SCVMM Console/PowerShell installed. Also, requires Hyper-V powershell module.

Import-Module hyper-v

## Refresh VM configuration and initialize
Write-Host -ForegroundColor Green (Get-Date) ".....Refreshing the VMs..."
Get-SCVirtualMachine -Name $VMName | Read-SCVirtualMachine

$VMOnPD = Get-SCVirtualMachine -Name $VMName | where {$_.IsPrimaryVM -eq $true}
$VMOnDR = Get-SCVirtualMachine -Name $VMName | where {$_.IsPrimaryVM -eq $false}

if ($VMOnPD.StatusString -ne "Stopped")
{
    write-host -ForegroundColor Red (Get-Date) "....VM is not in stopped state. Actual State " $VMOnPD.StatusString
    write-host -ForegroundColor Red (Get-Date) "....Exiting"
    exit 1
}

$error.Clear()
$VMRepConfig = Get-VMReplication -ComputerName $VMOnPD.HostName -VMName $VMOnPD.Name
$VMRepConfig = Get-VMReplication -ComputerName $VMOnDR.HostName -VMName $VMOnPD.Name

if ($error -ne 0)
{
    $temp = $VMOnPD.HostName.Split(".")
    $primaryHostName = $temp[0]

    $temp = $VMOnDR.HostName.Split(".")
    $recoveryHostName = $temp[0]

    write-host -ForegroundColor Red (Get-Date) "....Error in getting VM Replication state using FQDN, switching to Hostname"
    write-host -ForegroundColor Yellow (Get-Date) "....Primary Hostname: " $primaryHostName " Replica Hostname: " $recoveryHostName

    $error.Clear()
    $VMRepConfig = Get-VMReplication -ComputerName $primaryHostName -VMName $VMOnPD.Name
    $VMRepConfig = Get-VMReplication -ComputerName $recoveryHostName -VMName $VMOnPD.Name

    if ($error -ne 0)
    {
        write-host -ForegroundColor Red (Get-Date) "....Error in getting VM Replication state using Hostname"
        write-host -ForegroundColor Red (Get-Date) "....Exiting"
        exit 1
    }

    write-host -ForegroundColor Green (Get-Date) "....Successful in getting VM Replication state using Hostname"
}
else
{
    $primaryHostName = $VMOnPD.HostName
    $recoveryHostName = $VMOnDR.HostName
}

$VMOnPDAdapter = Get-SCVirtualNetworkAdapter -VM $VMonPD
$VMOnDRAdapter = Get-SCVirtualNetworkAdapter -VM $VMonDR

$fileName = $VMName + (Get-Date).ToString() + ".txt"
$fileName = $fileName.Replace("/","_")
$fileName = $fileName.Replace(":","_")

Write-Host -ForegroundColor Yellow (Get-Date) "....Dumping network information for $VMName to file $fileName"
Write-Host -ForegroundColor Yellow (Get-Date) "....Number of Network adapters found: " $VMOnPDAdapter.count

$VMNetwork = @()
$VMSubnet = @()
$Pools = @()

$counter = 0
foreach($vmAdapter in $VMOnPDAdapter)
{
    if ($vmAdapter.VMNetwork -eq $null)
    {
        $VMNetwork = $VMNetwork + $null
        $VMSubnet = $VMSubnet + $null
        $Pools = $Pools + $null
        $counter = $counter + 1
        continue
    }

    $VMNetwork = $VMNetwork + (Get-SCVMNetwork -Name $vmAdapter.VMNetwork.Name -ID $vmAdapter.VMNetwork.ID)
    $VMSubnet = $VMSubnet + (Get-SCVMSubnet -Name $vmAdapter.VMSubnet.Name | where {$_.VMNetwork.ID -eq $vmAdapter.VMNetwork.ID})
    #$PortClassification = Get-SCPortClassification | where {$_.Name -eq "Guest Dynamic IP"}
    $Pools = $Pools + (Get-SCStaticIPAddressPool -IPv4 | where {$_.VMsubnet.name -eq $vmAdapter.VMSubnet.Name})

    Out-File -FilePath $fileName -InputObject $VMNetwork[$counter] -Append
    Out-File -FilePath $fileName -InputObject $VMSubnet[$counter] -Append
    Out-File -FilePath $fileName -InputObject $Pools[$counter] -Append

    $counter = $counter + 1
}

if ($error.Count -ne 0)
{    
    write-host -ForegroundColor Red (Get-Date) "....Error is gathering information for $VMName. No changes made"
    write-host -ForegroundColor Red (Get-Date) "....Exiting"
    exit 1   
}

$IP = @()
$counter = 0
foreach($vmAdapter in $VMOnPDAdapter)
{

    if ($VMNetwork[$counter] -eq $null)
    {
        Write-Host -ForegroundColor Yellow (Get-Date) ".....Network Adapter '" $counter "' not connected"
        $IP = $IP + $null
        $counter = $counter + 1
        continue
    }

    ## Revoke IP
    $error.Clear()
    $IP = $IP +(Get-SCIPAddress –GrantToObjectId $VMOnPD.VirtualNetworkAdapters[$counter].ID)        
    Write-Host -ForegroundColor Yellow (Get-Date) "....Revoking IP " $IP[$counter] "from Primary VM"
    Revoke-SCIPAddress $IP[$counter]
    if ($error.count -eq 0)
    {
        Write-Host -ForegroundColor Green (Get-Date) "....." $IP[$counter] "revoke completed"
    }

    ## Disconnect Primary VM
    Write-Host -ForegroundColor Yellow (Get-Date) "....Disconnecting Primary VM from Network " $VMNetwork[$counter]
    Set-SCVirtualNetworkAdapter -VirtualNetworkAdapter $VMOnPD.VirtualNetworkAdapters[$counter] -NoLogicalNetwork -NoConnection -NoPortClassification
    Write-Host -ForegroundColor Green (Get-Date) "....Network Adapter '" $counter "' of Primary VM Disconnected"

    $counter = $counter + 1
}

## Start failover
Write-Host -ForegroundColor Yellow (Get-Date) ".....We are going to Failover " $VMName " from " $primaryHostName " to " $recoveryHostName

$error.Clear()
Start-VMFailover -ComputerName $primaryHostName -VMName $VMOnPD.Name -Prepare -Confirm:$false

start-sleep 5

Write-Host -ForegroundColor Yellow (Get-Date) ".....Completing Failover on Replica site..."
Start-VMFailover -ComputerName $recoveryHostName -VMName $VMOnDR.Name -Confirm:$false
if ($ReverseRep)
{
    write-host -ForegroundColor Green (Get-Date) ".....Starting Reverse Replication..."
    Set-VMReplication -ComputerName $recoveryHostName -reverse -VMName $VMOnDR.Name
}

if ($error -ne 0)
{
    write-host -ForegroundColor Red (Get-Date) ".....Error occured during Planned Failover for VM $VMName"
    write-host -ForegroundColor Red (Get-Date) ".....Please manually complete Failover before continuing"
    Write-Host -ForegroundColor Red (Get-Date) ".....Press any key to continue..."
    $ignoreKey = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
}

Write-Host -ForegroundColor Green (Get-Date) ".....Connecting Network(s) to Failed-over VM"

$counter = 0
foreach($vmAdapter in $VMOnPDAdapter)
{

    if ($VMNetwork[$counter] -eq $null)
    {
        Write-Host -ForegroundColor Yellow (Get-Date) ".....Network Adapter '" $counter "' not connected"
        $counter = $counter + 1
        continue
    }

    Write-Host -ForegroundColor Yellow (Get-Date) "Granting " $IP[$counter] "to Failed-over VM"
    Grant-SCIPAddress -GrantToObjectType "VirtualNetworkAdapter" -GrantToObjectID $VMOnDRAdapter[$counter].ID -StaticIPAddressPool $Pools[$counter] –IPAddress $IP[$counter]
    Write-Host -ForegroundColor Green (Get-Date) "Granting IP completed"

    Write-Host -ForegroundColor Yellow (Get-Date) "Connecting Replica VM to " $VMNetwork[$counter]
    Set-SCVirtualNetworkAdapter -VirtualNetworkAdapter $VMOnDRAdapter[$counter] -IPv4AddressType static -VMNetwork $VMNetwork[$counter] -VMSubnet $VMSubnet[$counter]
    Write-Host -ForegroundColor Green (Get-Date) "Network Adapter '" $counter "' of Failed-over VM connected to " $VMNetwork[$counter]

    $counter = $counter + 1
}``


## Run the reverse replication/cancel script

Here's what this script does:

1.	If you didn't run reverse replication in the failover script, you can use this script for reverse replication, or to cancel the failover.
2.	If you cancel, the script reverses the networking steps, and restores the primary VM connections, after disconnecting the replica VM networks.

### Run the script

This script should be run for the failover script was run with $ReverseRep set to **$false** .This script takes three arguments:

- $VMName: VM name
- $ReverseRep: Boolean argument to specify whether reverse replication should be performed. $true indicates that reverse replication runs.
- $CancelFO - Boolean argument to specify whether the failover is cancelled. $true indicates cancellation on primary and recovery sites.
- One and only one of $ReverseRep and $CancelFO can be passed $true at a time
- After the script runs successfully, the state on both VMs should be **Replication enabled’**.

Run the script:

``Param(
 [Parameter(Mandatory=$True)]
   [string]$VMName,
 [Parameter(Mandatory=$true)]
   [boolean]$ReverseRep,   
 [Parameter(Mandatory=$true)]
   [boolean]$CancelFO
)

# the script running on system with SCVMM Console/PowerShell installed. Also, requires Hyper-V powershell module.

Import-Module hyper-v

if ($ReverseRep -eq $CancelFO)
{
    write-host -ForegroundColor Red (Get-Date) "....Please ensure that one and only one of the parameters -ReverseRep and -CancelFO is passed as $True"
    write-host -ForegroundColor Red (Get-Date) "....Exiting"
    exit 1
}

## Refresh VM configuration and initialize
Write-Host -ForegroundColor Green (Get-Date) ".....Refreshing the VMs..."
Get-SCVirtualMachine -Name $VMName | Read-SCVirtualMachine

$VMOnPD = Get-SCVirtualMachine -Name $VMName | where {$_.IsPrimaryVM -eq $true}
$VMOnDR = Get-SCVirtualMachine -Name $VMName | where {$_.IsPrimaryVM -eq $false}

$error.Clear()
$VMRepConfig = Get-VMReplication -ComputerName $VMOnPD.HostName -VMName $VMOnPD.Name
$VMRepConfig = Get-VMReplication -ComputerName $VMOnDR.HostName -VMName $VMOnPD.Name

if ($error -ne 0)
{
    $temp = $VMOnPD.HostName.Split(".")
    $primaryHostName = $temp[0]

    $temp = $VMOnDR.HostName.Split(".")
    $recoveryHostName = $temp[0]

    write-host -ForegroundColor Red (Get-Date) "....Error in getting VM Replication state using FQDN, switching to Hostname"
    write-host -ForegroundColor Yellow (Get-Date) "....Primary Hostname: " $primaryHostName " Replica Hostname: " $recoveryHostName

    $error.Clear()
    $VMRepConfig = Get-VMReplication -ComputerName $primaryHostName -VMName $VMOnPD.Name
    $VMRepConfig = Get-VMReplication -ComputerName $recoveryHostName -VMName $VMOnPD.Name

    if ($error -ne 0)
    {
        write-host -ForegroundColor Red (Get-Date) "....Error in getting VM Replication state using Hostname"
        write-host -ForegroundColor Red (Get-Date) "....Exiting"
        exit 1
    }

    write-host -ForegroundColor Green (Get-Date) "....Successful in getting VM Replication state using Hostname"
}
else
{
    $primaryHostName = $VMOnPD.HostName
    $recoveryHostName = $VMOnDR.HostName
}

if ($VMOnDR.ReplicationStatus.ReplicationState -ne "Recovered")
{
    write-host -ForegroundColor Red (Get-Date) "....Replica VM is not in Failed over state. Actual State " $VMOnDR.ReplicationStatus.ReplicationState
    write-host -ForegroundColor Red (Get-Date) "....Exiting"
    exit 1
}

$error.Clear()

if ($ReverseRep -eq $true)
{
    write-host -ForegroundColor Green (Get-Date) ".....Starting Reverse Replication..."
    Set-VMReplication -ComputerName $recoveryHostName -reverse -VMName $VMOnDR.Name

    if ($error -ne 0)
    {
        write-host -ForegroundColor Red (Get-Date) ".....Error occured during Reverse Replication for VM $VMName"
        write-host -ForegroundColor Red (Get-Date) ".....Please manually complete Reverse replication"
        exit 1
    }

    write-host -ForegroundColor Green (Get-Date) ".....Reverse Replication completed..."
    exit 0
}

if ($VMOnDR.StatusString -ne "Stopped")
{
    write-host -ForegroundColor Red (Get-Date) "....VM is not in stopped state. Actual State " $VMOnDR.StatusString
    write-host -ForegroundColor Red (Get-Date) "....Exiting"
    exit 1
}

$VMOnPDAdapter = Get-SCVirtualNetworkAdapter -VM $VMonPD
$VMOnDRAdapter = Get-SCVirtualNetworkAdapter -VM $VMonDR

$fileName = $VMName + (Get-Date).ToString() + ".txt"
$fileName = $fileName.Replace("/","_")
$fileName = $fileName.Replace(":","_")

Write-Host -ForegroundColor Yellow (Get-Date) "....Dumping network information for $VMName to file $fileName"
Write-Host -ForegroundColor Yellow (Get-Date) "....Number of Network adapters found on Failed-over VM: " $VMOnDRAdapter.count

$VMNetwork = @()
$VMSubnet = @()
$Pools = @()

$counter = 0
foreach($vmAdapter in $VMOnDRAdapter)
{
    if ($vmAdapter.VMNetwork -eq $null)
    {
        $VMNetwork = $VMNetwork + $null
        $VMSubnet = $VMSubnet + $null
        $Pools = $Pools + $null
        $counter = $counter + 1
        continue
    }

    $VMNetwork = $VMNetwork + (Get-SCVMNetwork -Name $vmAdapter.VMNetwork.Name -ID $vmAdapter.VMNetwork.ID)
    $VMSubnet = $VMSubnet + (Get-SCVMSubnet -Name $vmAdapter.VMSubnet.Name | where {$_.VMNetwork.ID -eq $vmAdapter.VMNetwork.ID})
    #$PortClassification = Get-SCPortClassification | where {$_.Name -eq "Guest Dynamic IP"}
    $Pools = $Pools + (Get-SCStaticIPAddressPool -IPv4 | where {$_.VMsubnet.name -eq $vmAdapter.VMSubnet.Name})

    Out-File -FilePath $fileName -InputObject $VMNetwork[$counter] -Append
    Out-File -FilePath $fileName -InputObject $VMSubnet[$counter] -Append
    Out-File -FilePath $fileName -InputObject $Pools[$counter] -Append

    $counter = $counter + 1
}

if ($error.Count -ne 0)
{    
    write-host -ForegroundColor Red (Get-Date) "....Error is gathering information for $VMName. No changes made"
    write-host -ForegroundColor Red (Get-Date) "....Exiting"
    exit 1   
}

$IP = @()
$counter = 0
foreach($vmAdapter in $VMOnDRAdapter)
{

    if ($VMNetwork[$counter] -eq $null)
    {
        Write-Host -ForegroundColor Yellow (Get-Date) ".....Network Adapter '" $counter "' not connected"
        $IP = $IP + $null
        $counter = $counter + 1
        continue
    }

    ## Revoke IP
    $error.Clear()
    $IP = $IP +(Get-SCIPAddress –GrantToObjectId $VMOnDR.VirtualNetworkAdapters[$counter].ID)        
    Write-Host -ForegroundColor Yellow (Get-Date) "....Revoking IP " $IP[$counter] "from Replica VM"
    Revoke-SCIPAddress $IP[$counter]
    if ($error.count -eq 0)
    {
        Write-Host -ForegroundColor Green (Get-Date) "....." $IP[$counter] "revoke completed"
    }

    ## Disconnect Replica VM
    Write-Host -ForegroundColor Yellow (Get-Date) "....Disconnecting Replica VM from Network " $VMNetwork[$counter]
    Set-SCVirtualNetworkAdapter -VirtualNetworkAdapter $VMOnDR.VirtualNetworkAdapters[$counter] -NoLogicalNetwork -NoConnection -NoPortClassification
    Write-Host -ForegroundColor Green (Get-Date) "....Network Adapter '" $counter "' of Replica VM Disconnected"

    $counter = $counter + 1
}

## Cancel failover
Write-Host -ForegroundColor Yellow (Get-Date) ".....We are going to Cancel Failover " $VMName " on both " $primaryHostName " and " $recoveryHostName

$error.Clear()
Stop-VMFailover -ComputerName $recoveryHostName -VMName $VMName
Start-Sleep -Seconds 10
Stop-VMFailover -ComputerName $primaryHostName -VMName $VMName

if ($error -ne 0)
{
    write-host -ForegroundColor Red (Get-Date) ".....Error occured during Cancel Failover for VM $VMName"
    write-host -ForegroundColor Red (Get-Date) ".....Please manually Cancel Failover on both Primary and Recovery Server"
    Write-Host -ForegroundColor Red (Get-Date) ".....Press any key to continue..."
    $ignoreKey = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
}

Write-Host -ForegroundColor Yellow (Get-Date) ".....Connecting Network(s) back to the Primary VM"

$counter = 0
foreach($vmAdapter in $VMOnDRAdapter)
{

    if ($VMNetwork[$counter] -eq $null)
    {
        Write-Host -ForegroundColor Yellow (Get-Date) ".....Network Adapter '" $counter "' not connected"
        $counter = $counter + 1
        continue
    }

    Write-Host -ForegroundColor Yellow (Get-Date) "Granting " $IP[$counter] "to Primary VM"
    Grant-SCIPAddress -GrantToObjectType "VirtualNetworkAdapter" -GrantToObjectID $VMOnPDAdapter[$counter].ID -StaticIPAddressPool $Pools[$counter] –IPAddress $IP[$counter]
    Write-Host -ForegroundColor Green (Get-Date) "Granting IP completed"

    Write-Host -ForegroundColor Yellow (Get-Date) "Connecting Primary VM to " $VMNetwork[$counter]
    Set-SCVirtualNetworkAdapter -VirtualNetworkAdapter $VMOnPDAdapter[$counter] -IPv4AddressType static -VMNetwork $VMNetwork[$counter] -VMSubnet $VMSubnet[$counter]
    Write-Host -ForegroundColor Green (Get-Date) "Network Adapter '" $counter "' of Primary VM connected to " $VMNetwork[$counter]

    $counter = $counter + 1
}``
