---
ms.assetid: de545418-83e4-45f5-8809-27a5647d0aa7
title: include file
description: include file to summarize the release notes for VMM 2016.
author: jyothisuri
ms.author: jsuri
ms.date:  04/30/2018
ms.topic:  include
ms.service:  system-center
ms.subservice:  virtual-machine-manager
---

## VMM 2016 release notes

The following sections summarize the release notes for VMM 2016 and include the known issues, fixes, and the workarounds.

## VMM deployment

### VMM admin console import might fail
**Description**: If you import the VMM admin console add-in as a non-administrator, the console will crash. This occurs because the console add-in is stored in location “C:\Program Files\”, and only admins have access to this location.
**Workaround**: Store the console add-in at a location that doesn't need admin access, and then import it.


## Storage

### **Promoting a VM to highly available might fail**
**Description**: You create a VM on local storage, start it, and create checkpoints. If you try to migrate and promote the VM as highly available in a cluster, the migration might fail.
**Workaround**: Before you run the migration, delete the running checkpoint, and stop the VM.

### Migrating a VM from CSV to LUN storage might fail
**Description**: You create a highly available VM using CSV storage, add a LUN as available storage on the cluster, and migrate the VM from CSV to the LUN. If the VM and LUN storage are on the same node, the migration will succeed. If they're not, migration will fail.
**Workaround**: If the VM isn't located on the cluster node on which the LUN storage is registered, move it there. Then, migrate the VM to the LUN storage.

###  Capacity of NAS arrays is displayed as 0 GB.
**Description**: VMM shows **Total Capacity** and **Available Capacity** as 0 GB for existing file shares in the NAS arrays.
**Workaround**: None.


## Networking

### Logical networks managed by SDN network controller can't use dynamic IP addresses
**Description**: Using dynamic IP addresses for VMs connected to logical networks that are managed by SDN network controller in the VMM fabric isn't supported.
**Workaround**: Configure static IP addresses.

### SET switch shows as ‘Internal’ in VMM
**Description**: If you deploy an SET switch outside the VMM console, and then start managing it in the VMM fabric, The switch type will show as **internal**. This doesn't impact switch functionality.
**Workaround**: None.

### LACP teamed switch doesn't work after upgrade
**Description**: An LACP team configured in a logical switch doesn't work after upgrading to VMM 2016.
**Workaround**: Redeploy the switch, or remove and re-add a physical network adapter in the team.

### Backend adapter connectivity for SLB MUX doesn't work as expected
**Description**: Backend adapter connectivity of SLB MUX might not work as expected after VM migration.
**Workaround**: Use scale in/scale out in the SLB MUX VM as a workaround.

### CNG-based CA certificate isn't supported
**Description**: If you're using certificates from a CA, you can't use CNG certificates for SDN deployment in VMM.
**Workaround**: Use other certificate formats.

### A virtual adapter connected to a network managed by Network Controller must be restarted if you change the IP address
**Description**: If there's a change in the assigned IP address on any of the virtual network adapters connected to a VM network managed by Network Controller, you need to manually restart the associated adapters.
**Workaround**: No workaround.

### IPv6 isn't supported for a network infrastructure managed by Network Controller
**Description**: IPv6 isn't supported by Network Controller in the VMM fabric.
**Workaround:** Use IPv4.

### Connectivity issues for SLB addresses

**Description**: For frontend and backend IP addresses assigned to SLB MUX VMs, you might experience connectivity issues if **Register this connection's address in DNS** is selected.
**Workaround**: Clear the setting to avoid issues.

### Set-SCVMSubnet -RemovePortACL job completes in VMM without removing portACL association from NC VMSubnet object

**Description**: Set-SCVMSubnet -RemovePortACL job completes in VMM without removing portACL association from NC VMSubnet object, due to which Remove-PortACL job fails with NC Exception that is still in use.

**Workaround**: Remove the VMSubnet from VMM and then remove Port-ACL.

 Import-Module NetworkController

 #Replace the URI of the Network Controller with REST IP or FQDN

 ```
 $uri = "<NC FQDN or IP>"

 ```

 #Provide NC Admin credentials

 ```
 $cred = Get-Credential

 ```

 #Identify the virtual network that contains the subnet

 ```
 $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "Fabrikam_VNet1" -Credential $cred

 ```

 #Identify the subnet for which the ACL needs to be removed

 ```
 $vnet.Properties.Subnets[0].Properties = $vnet.Properties.Subnets[0].Properties | Select-Object -Property * -ExcludeProperty AccessControlList

 ```

 #Update

 ```
 New-NetworkControllerVirtualNetwork -ResourceId "Fabrikam_VNet1" -ConnectionUri $uri –Properties $vnet.Properties -Credential $cred

 ```


## Cluster management

### Upgrading the functional level of a cluster doesn't refresh file server information
**Description**: If you upgrade the functional level for a cluster that includes a file server, the platform information isn't automatically updated in the VMM database.
**Workaround**: After upgrading the cluster functional level, refresh the storage provider for the File Server.

### Updating a Storage Spaces Direct cluster in VMM will fail
**Description**: Updating a Storage Spaces Direct cluster (hyper-converged or disaggregated) using VMM isn't supported, and might cause data loss.
**Workaround**: Update the clusters outside VMM, using cluster-aware updating (CAU) in Windows.

### A cluster rolling upgrade of a Windows Server 2012 R2 host cluster to a Windows Server 2016 Nano Server host cluster will fail
**Description**: When you try to upgrade the host nodes of a Windows Server 2012 R2 cluster to Windows Server 2016 - Nano Server using cluster rolling upgrade functionality in VMM, the upgrade will fail with error 20406: **VMM could not enumerate instances of class MSFT_StorageNodeToDisk on the server \<servername\>. Failed with error MI RESULT 7 The requested operation isn't supported**.
**Workaround**: Manually upgrade the Windows Server 2012 R2 host cluster to Nano outside of VMM.

> [!NOTE]
> The rolling upgrade from Windows Server 2012 R2 to Windows Server 2016 Full Server works fine. This issue is specific to Nano.

### Adding a cluster in the VMM Admin console might cause an error
**Description**: When you add a cluster as a resource in the VMM Administrative console, you might receive an error stating **There were no computers discovered based on your inputs**.
**Workaround**: Select **OK**, and close the error dialog. Then try to add the cluster again.

### A cluster rolling upgrade doesn't do live migration of VMs that aren't highly available
**Description**: When you run a rolling upgrade of Windows Server 2012 R2 clusters to Windows Server 2016 using VMM, it doesn't perform live migration of VMs that aren't highly available. They're moved to a saved state.
**Workaround**: Either make all cluster VMs highly available before the upgrade, or do a manual live migration for the specific VMs.

### You need manual steps to add a Nano Server-based host located in an untrusted domain
**Description**: You can't add a Nano Server-based host in an untrusted domain.
**Workaround**: Perform these steps on the host and then add it to the VMM fabric as an untrusted host.

1.  Enable WINRM over HTTPS:

      ``
      New-Item -Path WSMan:\LocalHost\Listener -Transport HTTPS -Address * -CertificateThumbPrint $cert.Thumbprint –Force
      ``

2.  Create a firewall exception on the host to allow WINRM over HTTPS:

      ``
      New-NetFirewallRule -DisplayName 'Windows Remote Management (HTTPS-In)' -Name 'Windows Remote Management (HTTPS-In)' -Profile Any -LocalPort 5986 -Protocol TCP
      ``


### You can't add Nano Server-based hosts located in a perimeter network
**Description**: Trying to add a Nano Server-based host located in a perimeter network using the Add Resource Wizard fails.
**Workaround**: Perform these steps on the host, and then add it as an untrusted host to the VMM fabric.

1.  Enable WINRM over HTTPS on the host:

    ``
    New-Item -Path WSMan:\LocalHost\Listener -Transport HTTPS -Address * -CertificateThumbPrint $cert.Thumbprint –Force
    ``

2.  Create a firewall exception on the host, to allow WINRM over HTTPS:

    ``
    New-NetFirewallRule -DisplayName 'Windows Remote Management (HTTPS-In)' -Name 'Windows Remote Management (HTTPS-In)' -Profile Any -LocalPort 5986 -Protocol TCP
    ``

### Bare metal deployment of hosts might fail during a highly available upgrade
**Description**: After a highly available upgrade to VMM 2016, VMM might incorrectly update the Windows Deployment Services (WDS) registry key, HKLM\SYSTEM\CCS\SERVICES\WDSSERVER\PROVIDER\WDSPXE\PROVIDES\VMMOSDPROVIDER, to 'HOST/VIRT-VMM-1', instead of 'SCVMM/VIRT-VMM-1'. This will cause failures in bare metal deployment.
**Workaround**: Manually change the registry entry for HKLM\SYSTEM\CCS\SERVICES\WDSSERVER\PROVIDER\WDSPXE\PROVIDES\VMMOSDPROVIDER to 'SCVMM/VIRT-VMM-1'.

### Host agent status mismatch after upgrade
**Description**: When VMM updates the host agent, it generates a new certificate for the host. Because of this update, the Network Controller server certificate and the host certificate don't match.
**Workaround**: Repairing the host on the **Host Status** page

### SAN migration fails for a Nano Server-based host
**Description**: If you do a SAN migration between two standalone Nano Server-based hosts, an error is issued.
**Workaround**: Install the latest VMM update rollup (issue fixed in Update Rollup 2).

## Storage Spaces Direct

### Adding a host with Storage Spaces Direct enabled to the VMM fabric issues a warning
**Description**: When you add a host to a cluster with Storage Spaces Direct enabled, the warning "Multipath I/O is not enabled for known storage arrays on host <\hostname>" is generated.
**Workaround**: Install the latest VMM update rollup (issue fixed in Update Rollup 2).

### Deploying a VM on SOFS using fast file copy issues a warning
**Description**: If you deploy a VM on an SOFS using fast file copy, the action completes successfully with the following warning: **VMM could not transfer the file \<source location\> to \<destination location\> using fast file copy. The VMM agent on \<host\> returned an error**.
**Workaround**: None.

### Cluster validation always runs
**Description**: When you add a node to a cluster (or create a Storage Spaces Direct hyper-converged cluster), cluster validation is always performed, even when the skip cluster validation option is selected.
**Workaround**: Install the latest VMM update rollup. The issue was fixed in Update Rollup 2.

###  A classification change on a Cluster Shared Volume (CSV) isn't applied
**Description**: If you change the classification on a Cluster Shared Volume (CSV) in a Storage Spaces Direct hyper-converged cluster, only the classification of the owner node is updated. The other nodes still have the older classification assigned.
**Workaround**: Install the latest VMM update rollup. The issue was fixed in update rollup 2.

###  Creating tiered file share on SOFS doesn't work as expect o
**Description**: When you successfully create a tiered fileshare on SOFS, an error (43020 [SM_RC_DEDUP_NOT_AVAILABLE]) is issued even if dedup option isn't selected.
**Workaround**: Ignore the error.

###  VMM doesn't show correct information for a hyper-converged  cluster, or Storage Spaces Direct SOFS
**Description**: After you add an existing hyper-converged cluster or Storage Spaces Direct SOFS cluster to the VMM fabric, the Storage Provider isn't added, and some properties aren't available.
**Workaround**: Install the latest VMM update rollup. The issue was fixed in update rollup 2.


## VM management

### Shielding a VM causes an error
**Description**: If you enable shield for an existing VM in the VMM fabric, or if you create a shielded VM from a non-shielded template, the job might fail with the error 1730: **The selected action could not be completed because the virtual machine is not in a state in which the action is valid**. The failure happens during the last step of the job, when the VM is shut down after the shielding is completed. The VM is shielded properly, and is usable.
**Workaround**: Repair the VM with the **Ignore** option.

### VMM doesn't show changes to VM security properties
**Description**: If you change the secure boot properties of a generation 2 VM, or enable/disable vTPM for a shielded VM, outside the VMM console, the change isn't immediately shown in VMM.
**Workaround**: Manually refresh the VM to show the changes.

### Storing a VM in the VMM library fails if you change the default port for BITS (443)
**Description**: If you change the default BITS port when configuring VMM, and error is issued when you store a VM in the VMM library. Error 2940: **VMM is unable to complete the requested file transfer. The connection to the HTTP Server \<name> could not be established**.
**Workaround**: Manually add the new port number to the Windows Firewall exceptions list of the host:
``
netsh advfirewall firewall add rule name="VMM" dir=in action=allow localport=<port no.> protocol=TCP
``

### You can't create VM templates from a Nano Server-based VM.
**Description**: When you try to create a VM template from a Nano Server-based VM, error 2903 is issued: **VMM could not locate the specified file/folder '' on the '\<server name\>' server. This file/folder might be required as part of another object**.
**Workaround**: Create a VM template from scratch using a Nano Server VHD.

### Service deployments from service templates might fail on a Nano Server/Core-based guest OS.
**Description**: When selecting roles and features for a service template, the guest OS profile doesn't differentiate between Core, Nano Server, and Desktop. If you select roles and features (such as Desktop Experience or other GUI-related features) that don't apply to a Core/Nano Server-based guest OS, deployment failure might occur.
**Workaround**: Don't include these roles and features in the service template.

### VMM 2016 doesn't update the VMM guest agents after an upgrade
**Description**: When you upgrade VMM to 2016 with existing service deployments, and then service those services, VMM 2016 guest agents aren't updated on the VMs that were part of the service deployment. This doesn't affect functionality.
**Workaround**: Manually install the VMM 2016 guest agent.

### Nano Server-based VM fails to join a domain
**Description**: During Nano Server VM deployment, if you join the VM to a domain by specifying the domain join information on the **OS Configuration** page of the VM deployment Wizard, VMM deploys the VM but doesn't add it to the specified domain.
**Workaround**: After the VM is deployed, manually join the VM to the domain. [Learn more](/windows-server/get-started/getting-started-with-nano-server).


### Error when starting a VM with Start Ordering
**Description**: Windows Server 2016 includes the VM Start Ordering feature, which defines the order in which dependent VMs are started. This functionality isn't available in VMM, but if you've configured the feature outside the VMM, VMM understands the order in which the VMs will start. However, VMM throws a false positive error (12711): **VMM cannot complete the WMI operation on the server \<servername\> because of an error: [MSCluster_ResourceGroup.Name=\<name\>] The group or resource isn't in the correct state to perform the requested operation**.
**Workaround**: Ignore the error. The VMs will start in the correct order.



## Integration

## SQL Server Analysis Services (SSAS) integration doesn't work in VMM and Operations Manager Update Rollup 1.
**Description**: If you're running Update Rollup 1, you can't configure SSAS for SQL Server.
**Workaround**: Download the latest Update Rollups. The issue was fixed in Update Rollup 2.
