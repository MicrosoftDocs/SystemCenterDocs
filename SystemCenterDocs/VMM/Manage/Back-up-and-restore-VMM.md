---
title: Back up and restore VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ebb4cfd-fd5e-4add-b75c-dcb932dbaa64
---
# Back up and restore VMM
This topic describes the backup and recovery process in a [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] environment, and provides some recommendations.

> [!IMPORTANT]
> Do not use checkpoints for disaster recovery. Checkpoints do not create full duplicates of the hard disk contents nor do they copy data to a separate volume. A checkpoint can serve as temporary backup before updating an operating system on a virtual machine so that you can roll back the update if the update has any adverse effects. You should use a backup application to back up and recover your data in case of catastrophic data loss.

One option for backing up and recovering [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] is [!INCLUDE[dpm2012sp1long](../../Token/dpm2012sp1long_md.md)]. For more information, see [Data Protection Manager](http://technet.microsoft.com/library/hh758173.aspx).

Data such as Remote Access Authorization \(RAA\) passwords and the product key can be entered when you re\-install [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]. However, some encrypted data such as Virtual Machine Roles cannot be re\-entered. You cannot back up and restore such data if you use the Data Protection application programming interface \(DPAPI\) for backing up [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]—the data will be lost if the VMM management server fails.

## Creating and implementing a backup plan
Two basic elements of a backup plan are a list of what needs to be backed up, and an outline of what is changed frequently \(and therefore need to be backed up frequently\) in your environment. The following sections in this topic can help you create and implement your backup plan:

-   [Back up the VMM database](Back-up-and-restore-VMM.md#BKMK_b_database)

-   [Back up hosts and virtual machines](Back-up-and-restore-VMM.md#BKMK_b_hosts)

-   [Back up library servers](Back-up-and-restore-VMM.md#BKMK_b_library) \(including virtual hard disk files and ISO images\)

-   [Back up VMM private clouds](Back-up-and-restore-VMM.md#BKMK_b_clouds)

-   [Back up registry keys, encryption keys, and credentials](Back-up-and-restore-VMM.md#BKMK_b_misc)

-   [Back up non-Microsoft user interface add-ins and other non-Microsoft applications](Back-up-and-restore-VMM.md#BKMK_b_addins)

### <a name="BKMK_b_database"></a>Back up the VMM database
The [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database contains information such as configurations, service templates, profiles, virtual machine templates, services, scale\-out services, and other critical data that is required for [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to function correctly. Back up the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database regularly.

The [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database can be stored on the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server or on a separate server running Microsoft SQL Server. To back up the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database, you can use one or more of the following:

-   SQL Server tools. For more information, see [Create a Full Database Backup (SQL Server)](http://technet.microsoft.com/library/ms187510.aspx).

-   Other backup tools that are used in your environment.

-   The [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console or a [!INCLUDE[wps_2](../../Token/wps_2_md.md)] cmdlet, as described in the procedures that follow.

In addition to backing up the database, we recommend that you create a system state backup of the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server so that you can re\-create the server with the same security identifier \(SID\) in case of a catastrophic data loss. The SID is an integral part of how [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] is authorized on virtual machine hosts.

> [!IMPORTANT]
> -   There are several ways to recover the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database file that you create through either of the following backup procedures. One way, which requires the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server to be functioning, is to use the **SCVMMRecover.exe** tool, as described in [Backup-SCVMMServer](http://technet.microsoft.com/library/jj647705.aspx) \(although **SCVMMRecover.exe** is not a cmdlet\). Another way, which does not require the VMM management server to be functioning, is to restore by using SQL Server tools for restoring and attaching a database file.
> -   To use the following procedures, you must be a member of the Administrator user role.

##### To back up the VMM database by using the VMM console

1.  In the **Settings** workspace, on the **Home** tab, in the **Backup** group, click **Backup**.

2.  In the **Virtual Machine Manager Backup** dialog box, specify the location for the backup file. Select a folder that is not a root directory and that SQL Server can access.

    You can check the status of the backup in the Jobs workspace.

    For information about how to recover the backup, see the **Important** note before this procedure.

##### To back up the VMM database by using cmdlets in Windows PowerShell

1.  Start a [!INCLUDE[wps_2](../../Token/wps_2_md.md)] session.

2.  At the [!INCLUDE[wps_2](../../Token/wps_2_md.md)] command prompt, run the [Get-SCVMMServer](http://technet.microsoft.com/library/jj613273.aspx) and [Backup-SCVMMServer](http://technet.microsoft.com/library/jj647705.aspx) cmdlets, using the following syntax:

    ```
    get-scvmmserver <VMM management server name> | backup-scvmmserver -Path <BackupFileDir>
    ```

For information about how to recover the backup, see the **Important** note before these procedures.

### <a name="BKMK_b_hosts"></a>Back up hosts and virtual machines
Virtual machine hosts are Hyper\-V hosts, VMware ESXi hosts, and host clusters on which virtual machines and services are deployed. To back up virtual machine hosts and clusters, use Microsoft System Center [!INCLUDE[dpm2012sp1long](../../Token/dpm2012sp1long_md.md)] or another backup application that takes advantage of Volume Shadow Copy Service \(VSS\) to copy host and virtual machine data to a remote file server share.

> [!IMPORTANT]
> We recommend that you back up virtual machine configuration files \(.vmc\) daily.

Inventory your hosts, and then back up all of the hosted virtual machines. To get the list of hosts that are being managed by [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], run the following cmdlet from a [!INCLUDE[wps_2](../../Token/wps_2_md.md)] command line:

```
$vmhost = get-scvmmserver <VMM management server name> | get-scvmhost
```

For more information, see [Get-SCVMMServer](http://technet.microsoft.com/library/jj613273.aspx) and [Get-SCVMHost](http://technet.microsoft.com/library/jj654380.aspx).

Back up all of the configuration and resource files on each [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] host by using backup software that supports the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] VSS writer. Backup software that supports [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] can minimize the number of steps required to archive and restore virtual machines, help minimize downtime, and help ensure consistency of the data that is being archived or restored.

### <a name="BKMK_b_library"></a>Back up library servers
The [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library includes file\-based resources, such as virtual hard disks, ISO images, scripts, driver files, and application packages that are stored on library servers. These resources are closely associated with resources in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database that are not file\-based, such as virtual machine and service templates and profiles. All of these resources should be backed up.

To back up the data on library servers, use System Center [!INCLUDE[dpm2012sp1long](../../Token/dpm2012sp1long_md.md)] or another backup application that takes advantage of Volume Shadow Copy Service \(VSS\) to copy host and virtual machine data to a remote file server share. For a list of [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library servers, run the following cmdlet from the [!INCLUDE[wps_2](../../Token/wps_2_md.md)] command line:

```
$libraryservers = get-scvmmserver <VMM management server name> | get-sclibraryserver
```

For more information, see [Get-SCVMMServer](http://technet.microsoft.com/library/jj613273.aspx) and [Get-SCLibraryServer](http://technet.microsoft.com/library/jj647755.aspx).

Back up all files on library shares to a shared folder on a remote file server, including files with the following extensions:

|||
|-|-|
|-   .vhd and .vhdx<br />-   .iso<br />-   .inf<br />-   .vmx|-   .ps1<br />-   .vmc<br />-   .vsv|

### <a name="BKMK_b_clouds"></a>Back up VMM private clouds
To orchestrate and automate the replication and failover of virtual machines located in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] clouds, you can use Azure Site Recovery Manager. You can replicate in the following ways:

-   From one on\-premises [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] site to another, using Hyper\-V replication or SAN replication.

-   From an on\-premises [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] site to Azure, using Hyper\-V replication.

For more information about Azure Site Recovery, see [Azure Site Recovery Overview](http://azure.microsoft.com/documentation/articles/hyper-v-recovery-manager-overview/).

### <a name="BKMK_b_misc"></a>Back up registry keys, encryption keys, and credentials
Use the following guidelines to back up registry keys, encryption keys, and non\-[!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] managed credentials:

-   **Registry keys**: [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] uses multiple registry keys to store important settings. Settings are stored in the following registry key and its subkeys: **HKLM\\Software\\Microsoft\\Microsoft System Center Virtual Machine Manager Server\\Settings**.

    You should back up this entire section of the registry, with the possible exception of the SQL subkey. If you back up the SQL subkey, you capture the database name, location, and other details at the time of backup, which might not match the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database details that you want at the time of recovery.

    To back up registry keys, you can use the Regedit **Export** function, or any other tool that is used in your environment to back up registry keys.

-   **Encryption keys in Active Directory Domain Services**: If distributed key management \(DKM\) is configured, then you are storing [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]\-related encryption keys in Active Directory Domain Services \(AD DS\). To back up these keys, back up Active Directory on a regular basis.

-   **Non\-VMM managed credentials**: Some credentials that are related to [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] are managed by the Windows Credential Manager on the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server. To access the Credential Manager, in Control Panel, select **All Control Panel Items**, and then click **Credential Manager**. Click **Back up Credentials** to back up any [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]\-related credentials.

### <a name="BKMK_b_addins"></a>Back up non\-Microsoft user interface add\-ins and other non\-Microsoft applications
You can use non\-Microsoft user interface \(UI\) add\-ins to extend the functionality of the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console. The data that is used by a UI add\-in might be stored on the local server or on a remote computer, and it might be configured with a specific set of permissions. Consult the backup guidelines of your specific UI add\-in.

For any other non\-Microsoft applications, refer to the applications’ specific backup guidelines.

## Restoring the VMM environment
The following sections describe the process for restoring the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] environment, including data recovery and reassociating servers in your [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] environment.

-   [Restore the VMM database if necessary](Back-up-and-restore-VMM.md#BKMK_r_database)

-   Either:

    -   [Restore the VMM server on the same computer](Back-up-and-restore-VMM.md#BKMK_r_same)

    -   [Restore the VMM server on a different computer](Back-up-and-restore-VMM.md#BKMK_r_different)

    > [!NOTE]
    > To restore the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] server on a different computer, you will re\-install it and point it to the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database you're using.

-   [Reassociate servers in a perimeter network](Back-up-and-restore-VMM.md#BKMK_r_perimeter)

-   [Restore VMM library servers](Back-up-and-restore-VMM.md#BKMK_r_hosts)

-   [Restore registry keys, Active Directory objects, and non-VMM managed credentials](Back-up-and-restore-VMM.md#BKMK_r_misc)

After restoring the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] environment, perform any necessary [Post-restore tasks](Back-up-and-restore-VMM.md#BKMK_r_post).

### <a name="BKMK_r_database"></a>Restore the VMM database if necessary
If the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database must be restored, restore it first, using the process that corresponds to your backup method. For example, to restore using SQL Server tools, see [Restore and Recovery Overview (SQL Server)](http://technet.microsoft.com/library/ms191253.aspx).

If the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database is the only element that you need to restore, and you want information about the **SCVMMRecover.exe** tool, see [Backup-SCVMMServer](http://technet.microsoft.com/library/jj647705.aspx).

### <a name="BKMK_r_same"></a>Restore the VMM server on the same computer
If you are using the same computer for the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] server, perform a system state restore on that computer \(otherwise, skip this section\). If you do this, the SID of the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] server remains the same, and fewer steps are required to restore your [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] environment.

After you have restored the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] server, take the following steps:

1.  Remove any hosts or virtual machines from the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console that were removed after the last backup. If a host has been removed after the last backup, then it appears as "Not Responding" and all virtual machines on the host appear as "Host Not Responding". If the host is present but a virtual machine has been removed after the last backup, then the virtual machine appears as "Missing."

2.  Add any hosts or virtual machines that were added after the last backup.

### <a name="BKMK_r_different"></a>Restore the VMM server on a different computer
If you plant to restore the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server onto a different physical computer, first review the hardware requirements in System Requirements.

Next, re\-install [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] on the selected server, and point this [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] server to the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database. Because this server will have a different SID than the original computer, a few steps are necessary to bring it into synchrony with your environment. These steps include reassociating hosts with the new [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] server \(otherwise, they remain mapped to the original computer's machine account\).

##### To update the list of hosts and reassociate hosts with the new VMM management server

1.  Open the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console.

2.  Review the lists of hosts and virtual machines, as needed, to prepare for later steps in this procedure:

    -   To review the list of servers, in the **Fabric** workspace, on the left, click **Servers**.

    -   To review the list of virtual machines, in the **VMs and Services** workspace, on the left, click **All Hosts**.

3.  Remove any hosts or virtual machines from the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console that were removed after the last backup. If a host has been removed after the last backup, then it appears as "Not Responding" and all virtual machines on the host appear as "Host Not Responding". If the host is present but a virtual machine has been removed after the last backup, then the virtual machine appears as "Missing."

4.  Add any hosts or virtual machines that were added after the last backup.

5.  Identify managed computers that are marked as "Access Denied," right\-click each one, click **Reassociate**, and then provide the administrative credentials.

6.  If you are restoring a [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server that was also a library server, then the new computer lists the original [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] server as the default library server. From the **Library** view, remove the original library server, and then add the new computer as a library server.

You might also need to reassociate servers in the perimeter network \(also known as DMZ, demilitarized zone, and screened subnet\), as described in the next section.

### <a name="BKMK_r_perimeter"></a>Reassociate servers in a perimeter network
After you restore a [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] server, servers on a perimeter network might initially appear as "Not Responding." In that case, perform the following steps.

##### To reassociate servers in a perimeter network

1.  Sign in to each server on the perimeter network, and then locate the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] account. The [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] account is a local administrator account with a 10\-character user name of **scvmm** plus 5 random characters.

2.  Change the password of the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] account on each server.

3.  On the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server, in the **Host Properties** dialog box, click the **Options** tab, and then assign each server the same password that you created in step 2.

### <a name="BKMK_r_hosts"></a>Restore VMM library servers
To restore a library server after data loss, restore the file server shares, and then restore the data back onto the shares.

After you restore the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server and the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database, library servers are listed in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console. As needed, reassociate these listings with the physical library servers.

##### To reassociate library servers with physical computers

1.  If the newly restored computer has the same name as the original computer, install the Virtual Machine Manager agent locally on that computer and then reassociate that computer with the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server. For more information, see [How to Reassociate a Host or Library Server](How-to-Reassociate-a-Host-or-Library-Server.md).

2.  If the newly restored computer has a different name than the original computer, use the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console to remove the original computer from the list of managed computers, and then add the new computer.

### <a name="BKMK_r_misc"></a>Restore registry keys, Active Directory objects, and non\-VMM managed credentials
Use the following guidelines to restore registry keys, Active Directory objects, and non\-[!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] managed credentials:

-   **Registry keys**: To restore registry keys that were previously backed up, you can use the Regedit **Import** function or any other tool that is used in your environment to back up and restore registry keys. However, do not restore the SQL subkey if the database name, location, and other details that it contains do not match what you want for the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database at the time you are restoring the registry keys.

-   **Active Directory objects**: If distributed key management \(DKM\) is enabled in your [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] environment, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] stores some data in Active Directory, such as RAA passwords, product key information, and Virtual Machine Role data. After re\-installing [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], if needed, you can re\-enter some of the data that was stored in Active Directory, such as RAA passwords and product key information. After you re\-install [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] and \(if necessary\) restore Active Directory, the data in Active Directory continues to be accessible to [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)].

-   **Non\-VMM managed credentials**: In Control Panel, select **All Control Panel Items**, and then click **Credential Manager**. Click **Restore Credentials** to restore any [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]\-related credentials that were previously backed up.

## <a name="BKMK_r_post"></a>Post\-restore tasks
Depending on your [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] configuration, you might need to do some of the following tasks after you restore your [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] environment:

-   [Configure AlwaysOn Availability Groups](Back-up-and-restore-VMM.md#BKMK_post_AlwaysOn)

-   [Reinstall Windows Azure Pack](Back-up-and-restore-VMM.md#BKMK_post_WAP)

-   [Install additional VMM consoles](Back-up-and-restore-VMM.md#BKMK_Additional)

-   [Update virtual machine templates](Back-up-and-restore-VMM.md#BKMK_Templates)

-   [Restore Windows Azure Hyper-V Recovery Manager](Back-up-and-restore-VMM.md#BKMK_post_RM)

-   [Review add-ins, driver packages, and certificates](Back-up-and-restore-VMM.md#BKMK_post_misc)

### <a name="BKMK_post_AlwaysOn"></a>Configure AlwaysOn Availability Groups
If the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] database was configured by using SQL Server AlwaysOn Availability Groups, you must complete a few tasks to ensure that the database is correctly configured with Availability Groups. For more information, see [How to Complete the Configuration of AlwaysOn Availability Groups for the Database](How-to-Complete-the-Configuration-of-AlwaysOn-Availability-Groups-for-the-Database.md).

### <a name="BKMK_post_WAP"></a>Reinstall Windows Azure Pack
If Windows Azure Pack \(WAP\) was deployed in your environment to support tenants by using [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], then you’ll have to reinstall it after you restore the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] environment. For more information about Windows Azure Pack for Windows Server, see [Windows Azure Pack for Windows Server](http://technet.microsoft.com/library/dn296435.aspx).

### <a name="BKMK_Additional"></a>Install additional VMM consoles
If you had to replace any servers on which [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] consoles were installed, re\-install the consoles on those servers.

For more information, see [Installing and Opening the VMM Console](../Deploy/Installing-and-Opening-the-VMM-Console.md).

### <a name="BKMK_Templates"></a>Update virtual machine templates
All virtual machine templates that were restored must correctly specify the virtual hard disk that contains the operating system.

##### To update a virtual machine template

1.  In the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console, open the **Library** workspace, expand **Templates**, and then click **VM Templates**.

2.  In the **Templates** pane, right\-click the virtual machine template that you want to update, click **Properties**, and click the **Hardware Configuration** page to update the settings.

### <a name="BKMK_post_RM"></a>Restore Windows Azure Hyper\-V Recovery Manager
If Windows Azure Hyper\-V Recovery Manager is implemented in the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] environment, then you must perform a few steps to restore the Windows Azure Hyper\-V Recovery Manager Provider.

For more information, see [How to Restore Windows Azure Hyper-V Recovery Manager Provider](How-to-Restore-Windows-Azure-Hyper-V-Recovery-Manager-Provider.md).

### <a name="BKMK_post_misc"></a>Review add\-ins, driver packages, and certificates
After you restore [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], review the following items to ensure that you have taken necessary steps for your add\-ins, driver packages, and certificates:

-   **Non\-Microsoft user interface add\-ins**: To restore any non\-Microsoft user interface add\-ins or any other non\-Microsoft party applications, consult the respective application’s restore guidelines.

-   **Driver packages**: Driver packages that were previously added to the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] library might not be discovered correctly after a restore. They might have to be removed and be re\-added. For more information, see [How to add driver files to the VMM library](How-to-add-driver-files-to-the-VMM-library.md).

-   **Certificates**: Any [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]\-related certificates on hosts must be updated with the information of the new [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] management server.

> [!NOTE]
> After you re\-install [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] updates the account control lists \(ACLs\) that became outdated due to the failure. No further intervention is required.

## See Also
[Performing maintenance tasks in VMM](Performing-maintenance-tasks-in-VMM.md)
[Maintaining resources with VMM](Maintaining-resources-with-VMM.md)


