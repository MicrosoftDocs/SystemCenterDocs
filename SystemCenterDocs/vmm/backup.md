---
ms.assetid: 2ebb4cfd-fd5e-4add-b75c-dcb932dbaa64
title: Back up and restore VMM
description: This article describes how to back up and restore the VMM database, and hosts and virtual machines in the VMM fabric
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 11/07/2017
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Back up and restore VMM

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

This article describes the backup and recovery process in a System Center - Virtual Machine Manager (VMM) environment, and provides some recommendations.

## Before you start

- Don't use checkpoints for disaster recovery. Checkpoints do not create full duplicates of the hard disk contents, nor do they copy data to a separate volume.
- You can use a checkpoint to serve as temporary backup, before updating an operating system on a virtual machine. This allows you to roll back the update if it has adverse effects.
- You should use a backup application to back up and recover your data in case of catastrophic data loss. One option is System Center Data Protection Manager (DPM).
- Data such as Remote Access Authorization (RAA) passwords and the product key can be entered when you reinstall VMM. However, some encrypted data such as Virtual Machine Roles cannot be reentered.
- You can't back up and restore such data if you use the Data Protection application programming interface (DPAPI) for backing up VMM.
- The data will be lost if the VMM management server fails.

## Create and implement a backup plan
Basic elements of a backup plan include a list of what needs to be backed up, and an outline of what is changed frequently (and therefore need to be backed up frequently) in your environment.

## Back up the VMM database
The VMM database contains information such as configurations, service templates, profiles, virtual machine templates, services, scale-out services, and other critical data that is required for VMM to function correctly. Back up the VMM database regularly.

The VMM database can be stored on the VMM management server or on a separate server running Microsoft SQL Server. To back up the VMM database, you can use one or more of the following:

-   SQL Server tools. For more information, see [Create a Full Database Backup (SQL Server)](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

-   Other backup tools that are used in your environment.

-   The VMM console or a Windows PowerShell cmdlet, as described in the procedures that follow.

In addition to backing up the database, we recommend that you create a system state backup of the VMM management server so that you can re-create the server with the same security identifier (SID) in case of a catastrophic data loss. The SID is an integral part of how VMM is authorized on virtual machine hosts.

> [!IMPORTANT]
> -   There are several ways to recover the VMM database file that you create through either of the following backup procedures. One way, which requires the VMM management server to be functioning, is to use the **SCVMMRecover.exe** tool, as described in [Backup-SCVMMServer](/previous-versions/system-center/powershell/system-center-2012-r2/jj647705(v=sc.20)) (although **SCVMMRecover.exe** is not a cmdlet). Another way, which does not require the VMM management server to be functioning, is to restore by using SQL Server tools for restoring and attaching a database file.
> -   To use the following procedures, you must be a member of the Administrator user role.

### Back up the VMM database by using the VMM console

1.  In the **Settings** workspace, on the **Home** tab, in the **Backup** group, click **Backup**.

2.  In the **Virtual Machine Manager Backup** dialog box, specify the location for the backup file. Select a folder that is not a root directory and that SQL Server can access.

    You can check the status of the backup in the Jobs workspace.

    For information about how to recover the backup, see the **Important** note before this procedure.

### Back up the VMM database by using cmdlets in Windows PowerShell

1.  Start a Windows PowerShell session.

2.  At the Windows PowerShell command prompt, run the [Get-SCVMMServer](/previous-versions/system-center/powershell/system-center-2012-r2/jj613273(v=sc.20)) and [Backup-SCVMMServer](/previous-versions/system-center/powershell/system-center-2012-r2/jj647705(v=sc.20)) cmdlets, using the following syntax:

    ```
    get-scvmmserver <VMM management server name> | backup-scvmmserver -Path <BackupFileDir>
    ```

For information about how to recover the backup, see the **Important** note before these procedures.

## Back up hosts and virtual machines

Virtual machine hosts are Hyper-V hosts, VMware ESXi hosts, and host clusters on which virtual machines and services are deployed. To back up virtual machine hosts and clusters, use Microsoft System Center Data Protection Manager (DPM) or another backup application that takes advantage of Volume Shadow Copy Service (VSS) to copy host and virtual machine data to a remote file server share.

> [!IMPORTANT]
> We recommend that you back up virtual machine configuration files (.vmc) daily.

Inventory your hosts, and then back up all of the hosted virtual machines. To get the list of hosts that are being managed by VMM, run the following cmdlet from a Windows PowerShell command line:

```
$vmhost = get-scvmmserver <VMM management server name> | get-scvmhost
```

For more information, see [Get-SCVMMServer](/previous-versions/system-center/powershell/system-center-2012-r2/jj613273(v=sc.20)) and [Get-SCVMHost](/previous-versions/system-center/powershell/system-center-2012-r2/jj654380(v=sc.20)).

Back up all of the configuration and resource files on each VMM host by using backup software that supports the VMM VSS writer. Backup software that supports VMM can minimize the number of steps required to archive and restore virtual machines, help minimize downtime, and help ensure consistency of the data that is being archived or restored.

## Back up library servers
The VMM library includes file-based resources, such as virtual hard disks, ISO images, scripts, driver files, and application packages that are stored on library servers. These resources are closely associated with resources in the VMM database that are not file-based, such as virtual machine and service templates and profiles. All of these resources should be backed up.

To back up the data on library servers, use System Center Data Protection Manager (DPM) or another backup application that takes advantage of Volume Shadow Copy Service (VSS) to copy host and virtual machine data to a remote file server share. For a list of VMM library servers, run the following cmdlet from the Windows PowerShell command line:

```
$libraryservers = get-scvmmserver <VMM management server name> | get-sclibraryserver
```

For more information, see [Get-SCVMMServer](/previous-versions/system-center/powershell/system-center-2012-r2/jj613273(v=sc.20)) and [Get-SCLibraryServer](/previous-versions/system-center/powershell/system-center-2012-r2/jj647755(v=sc.20)).

Back up all files on library shares to a shared folder on a remote file server, including files with the following extensions:

- .vhd and .vhdx
- .iso
- .vmx
- .ps1
- .vmc
- .vsv

## Back up VMM private clouds

To orchestrate and automate the replication and failover of virtual machines located in VMM clouds, you can use [Azure Site Recovery Manager](/azure/site-recovery/). You can replicate in the following ways:

-   From one on-premises VMM site to another, using Hyper-V replication or SAN replication.

-   From an on-premises VMM site to Azure, using Hyper-V replication.


## Back up registry keys, encryption keys, and credentials
Use the following guidelines to back up registry keys, encryption keys, and non-VMM managed credentials:

-   **Registry keys**: VMM uses multiple registry keys to store important settings. Settings are stored in the following registry key and its subkeys: **HKLM\Software\Microsoft\Microsoft System Center Virtual Machine Manager Server\Settings**.

    You should back up this entire section of the registry, with the possible exception of the SQL subkey. If you back up the SQL subkey, you capture the database name, location, and other details at the time of backup, which might not match the VMM database details that you want at the time of recovery.

    To back up registry keys, you can use the Regedit **Export** function, or any other tool that is used in your environment to back up registry keys.

-   **Encryption keys in Active Directory Domain Services**: If distributed key management (DKM) is configured, then you are storing VMM-related encryption keys in Active Directory Domain Services (AD DS). To back up these keys, back up Active Directory on a regular basis.

-   **Non-VMM managed credentials**: Some credentials that are related to VMM are managed by the Windows Credential Manager on the VMM management server. To access the Credential Manager, in Control Panel, select **All Control Panel Items**, and then click **Credential Manager**. Click **Back up Credentials** to back up any VMM-related credentials.

## Back up non-Microsoft user interface add-ins and other non-Microsoft applications
You can use non-Microsoft user interface (UI) add-ins to extend the functionality of the VMM console. The data that is used by a UI add-in might be stored on the local server or on a remote computer, and it might be configured with a specific set of permissions. Consult the backup guidelines of your specific UI add-in.

For any other non-Microsoft applications, refer to the applications" specific backup guidelines.

## Restore the VMM environment

### Restore the VMM database if necessary
If the VMM database must be restored, restore it first, using the process that corresponds to your backup method. For example, to restore using SQL Server tools, see [Restore and Recovery Overview (SQL Server)](/sql/relational-databases/backup-restore/restore-and-recovery-overview-sql-server).

If the VMM database is the only element that you need to restore, and you want information about the **SCVMMRecover.exe** tool, see [Backup-SCVMMServer](/previous-versions/system-center/powershell/system-center-2012-r2/jj647705(v=sc.20)).

### Restore the VMM server on the same computer
If you are using the same computer for the VMM server, perform a system state restore on that computer (otherwise, skip this section). If you do this, the SID of the VMM server remains the same, and fewer steps are required to restore your VMM environment.

After you have restored the VMM server, take the following steps:

1.  Remove any hosts or virtual machines from the VMM console that were removed after the last backup. If a host has been removed after the last backup, then it appears as "Not Responding" and all virtual machines on the host appear as "Host Not Responding". If the host is present but a virtual machine has been removed after the last backup, then the virtual machine appears as "Missing."

2.  Add any hosts or virtual machines that were added after the last backup.

### Restore the VMM server on a different computer
If you plant to restore the VMM management server onto a different physical computer, first review the hardware requirements in System Requirements.

Next, re-install VMM on the selected server, and point this VMM server to the VMM database. Because this server will have a different SID than the original computer, a few steps are necessary to bring it current with your environment. These steps include reassociating hosts with the new VMM server (otherwise, they remain mapped to the original computer's machine account).

#### Update hosts with the new VMM management server

1.  Open the VMM console.

2.  Review the lists of hosts and virtual machines, as needed, to prepare for later steps in this procedure:

    -   To review the list of servers, in the **Fabric** workspace, on the left, click **Servers**.

    -   To review the list of virtual machines, in the **VMs and Services** workspace, on the left, click **All Hosts**.

3.  Remove any hosts or virtual machines from the VMM console that were removed after the last backup. If a host has been removed after the last backup, then it appears as "Not Responding" and all virtual machines on the host appear as "Host Not Responding". If the host is present but a virtual machine has been removed after the last backup, then the virtual machine appears as "Missing."

4.  Add any hosts or virtual machines that were added after the last backup.

5.  Identify managed computers that are marked as "Access Denied," right-click each one, click **Reassociate**, and then provide the administrative credentials.

6.  If you are restoring a VMM management server that was also a library server, then the new computer lists the original VMM server as the default library server. From the **Library** view, remove the original library server, and then add the new computer as a library server.

You might also need to reassociate servers in the perimeter network (also known as DMZ, demilitarized zone, and screened subnet), as described in the next section.

### Reassociate servers in a perimeter network
After you restore a VMM server, servers on a perimeter network might initially appear as "Not Responding." In that case, perform the following steps.



1.  Sign in to each server on the perimeter network, and then locate the VMM account. The VMM account is a local administrator account with a 10-character user name of **scvmm** plus 5 random characters.

2.  Change the password of the VMM account on each server.

3.  On the VMM management server, in the **Host Properties** dialog box, click the **Options** tab, and then assign each server the same password that you created in step 2.

### Restore VMM library servers
To restore a library server after data loss, restore the file server shares, and then restore the data back onto the shares.

After you restore the VMM management server and the VMM database, library servers are listed in the VMM console. As needed, reassociate these listings with the physical library servers.


1.  If the newly restored computer has the same name as the original computer, install the Virtual Machine Manager agent locally on that computer and then reassociate that computer with the VMM management server.
2.  If the newly restored computer has a different name than the original computer, use the VMM console to remove the original computer from the list of managed computers, and then add the new computer.

## Restore registry keys, Active Directory objects, and non-VMM managed credentials

Use the following guidelines to restore registry keys, Active Directory objects, and non-VMM managed credentials:

-   **Registry keys**: To restore registry keys that were previously backed up, you can use the Regedit **Import** function or any other tool that is used in your environment to back up and restore registry keys. However, do not restore the SQL subkey if the database name, location, and other details that it contains do not match what you want for the VMM database at the time you are restoring the registry keys.

-   **Active Directory objects**: If distributed key management (DKM) is enabled in your VMM environment, VMM stores some data in Active Directory, such as RAA passwords, product key information, and Virtual Machine Role data. After re-installing VMM, if needed, you can re-enter some of the data that was stored in Active Directory, such as RAA passwords and product key information. After you re-install VMM and (if necessary) restore Active Directory, the data in Active Directory continues to be accessible to VMM.

-   **Non-VMM managed credentials**: In Control Panel, select **All Control Panel Items**, and then click **Credential Manager**. Click **Restore Credentials** to restore any VMM-related credentials that were previously backed up.

## Post-restore tasks
Depending on your VMM configuration, you might need to do some of the following tasks after you restore your VMM environment:

## Configure Always On Availability Groups

If the VMM database was configured by using SQL Server Always On Availability Groups, you must complete a few tasks to ensure that the database is correctly configured with an availability group.

::: moniker range="<sc-vmm-2019"

## Reinstall Windows Azure Pack
If Windows Azure Pack (WAP) was deployed in your environment to support tenants by using VMM, then you"ll have to reinstall it after you restore the VMM environment. For more information about Windows Azure Pack for Windows Server, see [Windows Azure Pack for Windows Server](/previous-versions/azure/windows-server-azure-pack/dn296435(v=technet.10)).

::: moniker-end

## Install additional VMM consoles
If you had to replace any servers on which VMM consoles were installed, re-install the consoles on those servers.


### Update virtual machine templates

All virtual machine templates that were restored must correctly specify the virtual hard disk that contains the operating system.


1.  In the VMM console, open the **Library** workspace, expand **Templates**, and then click **VM Templates**.

2.  In the **Templates** pane, right-click the virtual machine template that you want to update, click **Properties**, and click the **Hardware Configuration** page to update the settings.

### Restore Windows Azure Hyper-V Recovery Manager

If Windows Azure Hyper-V Recovery Manager is implemented in the VMM environment, then you must perform a few steps to restore the Windows Azure Hyper-V Recovery Manager Provider.



### Review add-ins, driver packages, and certificates

After you restore VMM, review the following items to ensure that you have taken necessary steps for your add-ins, driver packages, and certificates:

-   **Non-Microsoft user interface add-ins**: To restore any non-Microsoft user interface add-ins or any other non-Microsoft party applications, consult the respective application"s restore guidelines.

-   **Driver packages**: Driver packages that were previously added to the VMM library might not be discovered correctly after a restore. They might have to be removed and be re-added.

-   **Certificates**: Any VMM-related certificates on hosts must be updated with the information of the new VMM management server.

> [!NOTE]
> After you re-install VMM, VMM updates the account control lists (ACLs) that became outdated due to the failure. No further intervention is required.
