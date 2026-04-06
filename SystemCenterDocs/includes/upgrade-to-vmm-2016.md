---
ms.assetid: 6aaf4c5c-db14-4c48-8c6d-8912ac333cab
title: include file
description: include file to provide information about how to upgrade VMM servers and databases to VMM 2016
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/20/2025
ms.topic: include
ms.service:  system-center
ms.subservice: virtual-machine-manager
ms.update-cycle: 1095-days
---

## Upgrade to System Center 2016 - VMM

The following sections describe how to upgrade to System Center Virtual Machine Manager (VMM) 2016. They include prerequisites, upgrade instructions, and tasks to complete after the upgrade finishes.

>[!NOTE]
>During VMM Installation, ensure that SQL Database isn't part of any Availability Group.

## Requirements and limitations

- VMM should be running on System Center 2012 R2 with update rollup 9 or later.
- The server on which you'll install VMM should meet VMM 2016 requirements. [Learn more](../vmm/install.md)
- Ensure that you're running a [supported version of SQL Server](../vmm/system-requirements.md).
- If your current VMM deployment is integrated with Azure Site Recovery, note that Site Recovery settings can't be upgraded. After the upgrade, you need to redeploy.
- Verify Hyper-V host [support requirements](https://azure.microsoft.com/blog/azure-site-recovery-windows-server-2016-asr/) for VMM 2016.

## Before you start

1. Complete any jobs that are currently running in VMM. All job history is deleted during the upgrade.
2. Close any connections to the VMM management server, including the VMM console and the VMM command shell.
3. Close any other programs that are running on the VMM management server.
4. Ensure that there are no pending restarts on VMM servers.
5. Perform a full backup of the VMM database.
6. If the current SQL Server database used Always On availability groups:

- If the VMM database is included in the availability group, remove it in SQL Server Management Studio.
- Initiate a failover to the computer that is running SQL Server and on which the VMM database is installed.

7. If you're running Operations Manager with VMM, disconnect the connection between VMM and Operations Manager server.
8. If the VMM 2012 R2 server is running update rollup 10 or 11 and you have a Citrix NetScalar load balancer deployed, run this SQL Server script before you start the upgrade, otherwise it might fail. The script isn't needed if you're running update rollup 12 or later.

  ``ALTER TABLE [dbo].[tbl_NetMan_HardwareModelSettings]  
  ALTER COLUMN Version NVARCHAR(255) NULL;  
  GO``

## Upgrade sequence for System Center components

If you're running more than one System Center component, they should be upgraded in a specific order:

1. Service Management Automation
2. Orchestrator
3. Service Manager
4. Data Protection Manager (DPM)
5. Operations Manager
6. Configuration Manager
7. Virtual Machine Manager (VMM)
8. App Controller
9. Service Provider Foundation
10. Windows Azure Pack for Windows Server
11. Service Bus Clouds
12. Windows Azure Pack
13. Service Reporting

## Upgrade a standalone VMM server

Back up and upgrade the operating system and then install VMM 2016.

### Back up and upgrade the operating system

1. Back up and retain the VMM database.
2. Uninstall VMM. To do this:
  a.  In **Add remove programs**, select **VMM** > **Uninstall**.
  b.  Select **Remove Features**, and then select **VMM management Server** and **VMM Console**.
  c.  In **Database Options**, select **Retain database**.
  d.  Review the summary and select **Uninstall**.
3. Upgrade the management operating system to Windows Server 2016.
4. Upgrade to the Windows 10 version of the ADK.

### Install VMM 2016

1. In the main setup page, select **Install**.
2. In **Select features to install**, select the VMM management server > **Next**. The VMM console will be automatically installed.
3. In **Product registration information**, provide the appropriate information, and then select **Next**. If you don't enter a product key, VMM will be installed as an evaluation version that expires after 180 days from the installation date.
4. In **Please read this license agreement**, review the license agreement, select **I have read, understood, and agree with the terms of the license agreement**, and then select **Next**.
5. In **Usage and Connectivity Data**, select either of the options, and then select **Next**.
6. If **Microsoft Update** page appears, select whether you want to use Microsoft Update, and then select **Next**. If you've already chosen to use Microsoft Update on this computer, this page won't appear.
7. In **Installation location**, use the default path or enter a different installation path for the VMM program files, and then select **Next**.
8. In **Database configuration**:
 - [Learn more](#upgrade-the-vmm-sql-server-database) if you need to upgrade the VMM SQL Server.
 - If you're using a remote SQL instance, specify the SQL server computer name.
 - If SQL server runs on the VMM server, enter the name of the VMM server or enter **localhost**. If the SQL Server is in a cluster, enter the cluster name.
 - Don't specify a port value if you're using local SQL server or if your remote SQL server uses the default port (1433).
 - Select **Existing Database** and select the database that you retained (backed up) from your previous installation. Provide credentials with permissions to access the database. When you're prompted to upgrade the database, select **Yes**.
11. In **Configure service account and distributed key management**, specify the account that the VMM service will use. You can't change the identity of the VMM service account after installation.
12. Under **Distributed Key Management**, select whether to store encryption keys in Active Directory.
>[!NOTE]
> Choose the settings for the service account and distributed key management carefully. Based on your selection, encrypted data such as passwords in templates might not be available after the upgrade and you'll need to enter them manually.
13. In **Port configuration**, use the default port number for each feature, or provide a unique port number that is appropriate in your environment. To change the ports you assigned during installation of a VMM management server, you need to uninstall and then reinstall the server. Don't configure any feature to use port 5986; this port number is preassigned.
14. In **Library configuration**, select whether to create a new library share or to use an existing library share on the computer. The default library share that VMM creates is named **MSSCVMMLibrary**, and the folder is located at **%SYSTEMDRIVE%\ProgramData\Virtual Machine Manager Library Files**. **ProgramData** is a hidden folder, and you can't remove it. After the VMM management server is installed, you can add library shares and library servers by using the VMM console or by using the VMM command shell.
15. In **Upgrade compatibility report**, review the settings, select **Next** to proceed with the upgrade.
16. In **Installation Summary**, review the settings and select **Install** to upgrade the server. **Installing features** page appears and displays the installation progress.
17. In **Setup completed successfully**, select **Close** to finish the installation. To open the VMM console, check  **Open the VMM console when this wizard closes**, or you can select the VMM console icon on the desktop.
18. After the upgrade, [upgrade the host agent manually](#update-vmm-agents).
19. During the setup, VMM enables the following firewall rules. These rules remain in effect even if you uninstall the VMM later:
 - Windows Remote Management
 - Windows Standards-Based Storage Management

if you experience any issues during setup, check the logs in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder.

## Upgrade a highly available VMM server

You can upgrade a highly available VMM 2012 R2 server (running at least update rollup 9) to VMM 2016.

The following modes of upgrade are supported:

- [Mixed mode with no additional VMM servers](#mixed-mode-upgrade-with-no-additional-vmm-servers)
- [Mixed mode with additional VMM servers](#mixed-mode-upgrade-with-additional-vmm-servers)

> [!NOTE]
> SQL Server upgrade can be performed any time, independent of VMM upgrade.

### Mixed mode upgrade with no additional VMM servers

This procedure requires no additional VMM servers but has increased risk for downtime in some scenarios. For example, when you have two node HA VMM and the active VMM node fails while you're upgrading the passive. In this scenario, your VMM server won't have a failover node available.

1. Back up and retain the VMM database.
2. Uninstall the VMM on the passive node.  
3. On the passive VMM node, upgrade the management OS to Windows Server 2016.
4. Upgrade to the Windows 10 version of the ADK.
5. Install VMM 2016 on the passive node by using the following steps:
  - In the main setup page, select **Install**.
  - In **Select features to install**, select  **VMM management server** and then select **Next**. The VMM console will be automatically installed.
  - When prompted, confirm that you want to add this server as a node to the highly available deployment.
  - On the **Database Configuration** page, if prompted, select to upgrade the database.
  - Review the summary and complete the installation.
6. Fail over the active VMM node to the newly upgraded VMM server.
7. Repeat the procedure on other VMM nodes.
8. Update the cluster functional level by using the
**Update-ClusterFunctionalLevel** [command](/powershell/module/failoverclusters/update-clusterfunctionallevel).
9. [Optional] Install the appropriate SQL command line utilities.

### Mixed mode upgrade with additional VMM servers

You need additional servers. However, there's almost no downtime in all the scenarios.

1. Back up and retain the VMM database.
2. Add the same number of additional servers (with Windows Server 2016 Management OS) that equals to the server number present in the HA cluster.
3. Install Windows 10 version of the ADK on the newly added 2016 servers.
4. Install VMM 2016 on one of the newly added servers by using the details in **step 5** in [Mixed mode upgrade with no additional VMM servers](#mixed-mode- upgrade-with-no-additional-VMM-servers).
5. Repeat the installation steps for all the other newly added servers.
6. Fail over the active VMM node to one of the newly added servers.
7. Uninstall VMM from the 2012 R2 nodes, and remove these nodes from the cluster after failover.
8. Update the cluster functional level by using the [Update-ClusterFunctionalLevelcommand](/powershell/module/failoverclusters/update-clusterfunctionallevel).
9. Optionally install the appropriate SQL Command line utilities.
10. After the upgrade, [upgrade the host agent manually](#update-vmm-agents).

## Upgrade the VMM SQL Server database

There are a couple of reasons you might want to upgrade the VMM SQL Server database:

- You're upgrading VMM to System Center 2016, and the current SQL Server database version isn't supported.
- You want to upgrade a VMM standalone server to a high availability server, and the SQL Server is installed locally.
- You want to move the SQL Server database to a different computer.

### Collect database information

Before you upgrade, collect information about the VMM database:

1. Record the database connection in the VMM console > **Settings** > **General** > **Database Connection**.
2. Record the account information in Server Manager > **Tools** > **Services**. Right-click **System Center Virtual Machine Manager** > **Properties** > **Log On**. This is the domain or local account that was assigned as the service account when VMM was installed. You can check if it's local in **Tools** > **Computer Manager** > **Local Users and Groups** > **Users**.
3. Check whether you used distributed key management when you installed VMM, or if encryption keys are stored locally on the VMM server.
4. If you're moving the VMM database but not upgrading the VMM, check which update rollups have been applied on the VMM server.

### Upgrade a standalone database

1. Back up the existing VMM database, and copy the backup to a computer running a supported version of the SQL Server.
2. Use SQL Server tools to restore the database.
    - If you're upgrading VMM, you'll specify the new SQL Server location in VMM setup > **Database Configuration**.
    - If you want to upgrade the database without upgrading VMM, you need to uninstall and then reinstall VMM. When you uninstall, on the **Database Options** page, select **Retain database**. Then, reinstall with the same settings you used for the original installation. On the **Database Configuration**, specify the new SQL Server details. After reinstall, apply the update rollups and check that the deployment is working as expected.

### Upgrade a highly available database

1. Record the source version of the existing database and the version you want to upgrade to.
2. Create a backup of the highly available SQL Server database from the active node of the SQL Server cluster.
3. Upgrade passive SQL Server nodes to the new version. After the upgrade, optionally install SQL Server Management Studio if you want to manage SQL Server from this node.
4. Fail over the highly available SQL server role from the currently active node to the upgraded node. After failover, you can use SQL Server Management Studio to validate the running database version.
5. Repeat the upgrade for the other nodes in the HA SQL cluster. As an additional validation, you can fail over the SQL Server database roles to ensure that everything works as expected.

### Migrate a SQL Server cluster as part of the VMM upgrade

1. Take a backup of the highly available VMM database from the active node of the existing SQL cluster.
2. Note the VMM role name to use when reinstalling the VMM server role. Uninstall VMM server from the existing VMM cluster nodes with the retain database option.
When uninstalling VMM server from the last node, you can get a message about unsuccessful SPN registration. This is a known issue with no functional impact.
3. Restore the backed-up DB into another SQL cluster running supported SQL version. Add the user on which VMM service is running as User to this new DB with membership to db_owner.
4. While upgrading VMM Server as part of SQL Cluster migration, give the Parameters corresponding to the new SQL Cluster.

## Update VMM agents

After the upgrade, you need to update the VMM agents on your Hyper-V hosts and in your VMM library servers.

1. Select **Fabric** >  **Servers** >  **All Hosts**.
2. In the **Hosts** pane, right-click a column heading, and then select **Agent Version Status**.
3. Select the host with the VMM agent that you want to update. On the **Hosts** tab, in the **Host** group, select **Refresh**. If a host needs to have its VMM agent updated, the **Host Status** column will display **Needs Attention** and the **Agent Version Status** column will display **Upgrade Available**.
4. Right-click the host with the VMM agent that you want to update, and then select **Update Agent**. In **Update Agent**, provide the necessary credentials and then select **OK**.
5. The **Agent Version Status** column will display a value of **Upgrading**. After the VMM agent is updated successfully on the host, the **Agent Version Status** column will display a value of **Up-to-date**, and the **Agent Version** column will display the updated version of the agent. After you refresh the host again, the **Host Status** column for the host will display a value of **OK**.
6. You can update the VMM agent on a VMM library server in a similar manner. To view a list of VMM library servers, select **Fabric** > **Servers** > **Library Servers**.

## Reassociate hosts and library servers

You might need to reassociate virtual machine hosts and VMM library servers with the VMM management server after the upgrade.

1. Select **Fabric** > **Servers** > **All Hosts**.
2. In the **Hosts** pane, ensure that the **Agent Status** column is displayed. If it isn't, right-click a column heading > **Agent Status**.
3. Select the host that you need to reassociate with the VMM management server.
4. In the host group, select **Refresh**. If a host needs to be reassociated, the **Host Status** column will display a value of **Needs Attention**, and the **Agent Status** column will display a value of **Access Denied**.
Right-click the host that you want to reassociate, and then select **Reassociate**. In **Reassociate Agent**, provide credentials and then select **OK**. The Agent Status column will display a value of Reassociating. After the host has been reassociated successfully, the **Agent Status** column will display a value of **Responding**. After you refresh the host again, the **Host Status** column for the host will display a value of **OK**.
After you've reassociated the host, you'll most likely have to update the VMM agent on the host.

## Redeploy Azure Site Recovery

If Azure Site Recovery was integrated into your VMM 2012 R2 deployment, you need to redeploy it with VMM 2016, for [replication to Azure](/azure/site-recovery/site-recovery-vmm-to-azure) or [replication to a secondary site](/azure/site-recovery/site-recovery-vmm-to-vmm).

Read this [blog entry](https://azure.microsoft.com/blog/azure-site-recovery-windows-server-2016-asr/) for details of Hyper-V host support when running VMM 2016.

## Connect to Operations Manager

After the upgrade, reconnect VMM to Operations Manager.

>[!NOTE]
>You shouldn't install any management pack on VMM 2016 RTM. Update Rollup 1 or later must be installed. If you've installed any management packs on the RTM version, uninstall them before you install Update Rollup 1.

## Configure Always On Availability Groups

If you upgraded a database that was configured with Always On Availability Groups, you need to complete a few tasks to ensure that the upgraded database is properly configured with Always On Availability Groups.

1. Add the VMM database to the availability group. You can use Microsoft SQL Server Management Studio to perform this task.
2. On the secondary node computer in the cluster that is running SQL Server, create a new sign-in account. Configure the sign-in name so that it's identical to the VMM service account name. Include user mapping to the VMM database, and configure the database owner credentials.
3. Initiate a failover to the secondary node computer that is running SQL Server, and verify that you can restart the VMM service (scvmmservice).
4. Repeat the last two steps for every secondary node in the cluster that is running SQL Server.
5. If this is a high availability VMM setup, continue to install other high availability VMM nodes.

## Update virtual machine templates

All the virtual machine templates that were upgraded need to correctly specify the virtual hard disk that contains the operating system.

1. Select **Library** > **Templates** > **VM Templates**.
2. Right-click the template > **Properties** > **Hardware Configuration**, and check disk settings.

## Renew certificates for PXE servers

If you have a PXE server in the VMM fabric, you need to remove it from the fabric and then add it again. This is to renew the PXE server certificate and avoid certificate errors.

## Update driver packages

Driver packages that were previously added to the VMM library must be removed and added again to be correctly discovered.

If you plan to assign custom drivers, the driver files must exist in the library. You can tag the drivers in the library so that you can later filter them by tag. After the files are added, when you configure a physical computer profile, you can specify the driver files. VMM installs the specified drivers when it installs the operating system on a physical computer.

In the physical computer profile, you can select to filter the drivers by tags or you can select to filter drivers with matching Plug and Play (PnP) IDs on the physical computer. If you select to filter the drivers by tags, VMM determines the drivers to apply by matching the tags that you assign to the drivers in the library to the tags that you assign in the profile. If you select to filter drivers with matching PnP IDs, you don't need to assign custom tags.

1. Locate a driver package that you want to add to the library.
2. In the library share that is located on the library server associated with the group where you want to deploy the physical computers, create a folder to store the drivers and then copy the driver package to the folder.
3. We strongly recommend that you create a separate folder for each driver package, and that you don't mix resources in the driver folders. If you include other library resources such as .iso images, .vhd files or scripts with an .inf file name extension in the same folder, the VMM library server won't discover those resources. Also, when you delete an .inf driver package from the library, VMM deletes the entire folder where the driver .inf file resides.
4. In the VMM console, open the Library workspace. In the **Library** > **Library Servers**, expand the library server where the share is located, right-click the share, and then select **Refresh**. After the library refreshes, the folder that you created to store the drivers appears.
5. Now assign tags if required. In **Library**, expand the folder that you created to store the drivers in the previous procedure, and then select the folder that contains the driver package.
6. In the **Physical Library Objects**, right-click the driver .inf file, and then select **Properties**.
7. In the **Driver File Name Properties** > **Custom tags**, enter custom tags separated by a semicolon or select **Select** to assign available tags or to create and assign new ones. If you select **Select**, and then select **New Tag**. You can change the name of the tag after you select **OK**. For example, if you added a network adapter driver file, you could create a tag that is named ServerModel NetworkAdapterModel, where ServerModel is the server model and NetworkAdapterModel is the network adapter model.

## Relocate the VMM library

- If you upgraded to a high availability VMM management server, we recommend that you relocate your VMM library to a high availability file server.
- After you create a new VMM library, you'll want to move the resources from the previous VMM library to the new VMM library.
- To preserve the custom fields and properties of saved virtual machines in the previous VMM library, deploy the saved virtual machines to a host and then save the virtual machines to the new VMM library.

> [!NOTE]
> The operating system and hardware profiles can't be moved. You need to re-create these profiles.
