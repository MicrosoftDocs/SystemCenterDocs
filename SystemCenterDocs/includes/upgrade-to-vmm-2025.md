---
ms.assetid:
title: include file
description: include file to provide information about how to upgrade VMM servers and databases to VMM 2019.
author: jyothisuri
ms.author: jsuri
ms.date: 06/28/2024
ms.topic: include
ms.service: system-center
ms.subservice: virtual-machine-manager
---

## Upgrade to System Center 2025 - Virtual Machine Manager

The following sections provide information about how to upgrade to VMM 2025. These include prerequisites, upgrade instructions, and tasks to complete after the upgrade finishes.

> [!NOTE]
> - You can upgrade to VMM 2025 from VMM 2022; upgrade from 2019 and 2016 isn't supported.
> - During VMM Installation, ensure that SQL Database isn't part of any Availability Group.

## Requirements and limitations

- You should be running VMM on System Center 2022.
- Ensure that the server meets all the requirements for VMM 2025 and that prerequisites are in place. [Learn more](../vmm/install.md).
- Ensure that you're running a [supported version of SQL Server](../vmm/system-requirements.md).
- If your current VMM deployment is integrated with Azure Site Recovery, note that:
	- Site Recovery settings can't be upgraded. After the upgrade, you need to redeploy.
	- Verify Hyper-V host support for VMM 2025.

## Before you start

Ensure the following:

1. Complete any jobs that are currently running in VMM.

   > [!NOTE]
   > The jobs history is deleted during the upgrade.

2. Close any connections to the VMM management server, including the VMM console and the VMM command shell.
3. Close any other programs that are running on the VMM management server.
4. Ensure that there are no pending restarts on VMM servers.
5. Perform a full backup of the VMM database.
6.  If the current SQL Server database used Always On availability groups:

	- If the VMM database is included in the availability group, remove it in SQL Server Management Studio.
	- Initiate a failover to the computer that is running SQL Server on which the VMM database is installed.

7. If you're running Operations Manager with VMM, disconnect the connection between the VMM and the Operations Manager server.


## Upgrade sequence for System Center components
If you're running more than one System Center components, they should be upgraded in a specific order as shown below:

1. Service Management Automation
2. Orchestrator
3. Service Manager
4. Data Protection Manager
5. Operations Manager
6. Configuration Manager
7. Virtual Machine Manager

>[!Note]
>Service Provider Foundation (SPF) is discontinued from System Center 2025. However, SPF 2022 will continue to work with System Center 2025 components.

## Upgrade a standalone VMM server

>[!NOTE]
> When you're upgrading a standalone VMM server, we recommend that you install VMM 2025 on the same server that had VMM 2022.

If you're using Distributed Key Management, you can choose to install VMM 2025 on a different server.

Use the following procedures:

- [Back up and upgrade the OS](#back-up-and-upgrade-os)
- [Install VMM 2025](#install-vmm-2025)

### Back up and upgrade OS
1. Back up and retain the VMM database.
2. [Uninstall the VMM](#uninstall-the-vmm). Ensure to remove both the management server and the console.
3. Upgrade the management OS to Windows Server 2025.
4. Install Windows 11 or Windows Server 2025 version of [ADK](/windows-hardware/get-started/adk-install).

#### Uninstall the VMM
1. Go to **Control Panel** > **Programs** > **Program and Features**, select **Virtual Machine Manager** and select **Uninstall**.
2. On the **Uninstall wizard,** select **Remove Features**, then select both **VMM management Server** and **VMM Console** under the features to remove list.  
3. On the database options page, select **Retain database**.
4. Review the summary and select **Uninstall**.

### Install VMM 2025

1.	In the main setup page, select **Install**.
2.	In **Select features to install**, select the VMM management server, and then select **Next**. The VMM console will be automatically installed.
3.	In **Product registration information**, provide the appropriate information and then select **Next**. If you don't enter a product key, VMM will be installed as an evaluation version that expires after 180 days from the installation date.
4.	In **Please read this license agreement**, review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** checkbox, and then select **Next**.
5.	In **Usage and Connectivity Data**, select either of the options, and then select **Next**.
6.	If the **Microsoft Update** page appears, select whether you want to use Microsoft Update and select **Next**. If you have already chosen to use Microsoft Update on this computer, this page won't appear.
7.	In **Installation location**, use the default path or enter a different installation path for the VMM program files and then select **Next**.
8.	In **Database configuration**:
	- [Learn more](#upgrade-the-vmm-sql-server-database) if you need to upgrade the VMM SQL Server.
	- If you're using a remote SQL instance, specify the SQL server computer name.
	- If SQL server runs on the VMM server, enter the name of the VMM server, or enter **localhost**. If the SQL Server is in a cluster, enter the cluster name.
	- Don't specify a port value if you're using a local SQL server or if your remote SQL server uses the default port (1433).
	- Select **Existing Database** and select the database that you retained (backed up) from your previous installation. Provide credentials with permissions to access the database. When you're prompted to upgrade the database, select **Yes**.
9.	In **Configure service account and distributed key management**, specify the account that the VMM service will use.

   >[!NOTE]
   >You can't change the identity of the VMM service account after installation.

10.	Under **Distributed Key Management**, select whether to store encryption keys in Active Directory.

   >[!NOTE]
   >Choose the settings for the service account and distributed key management carefully. Based on your selection, encrypted data, such as passwords in templates, might not be available after the upgrade and you'll need to enter them manually.

11.	In **Port configuration**, use the default port number for each feature or provide a unique port number that is appropriate in your environment.

   >[!NOTE]
   >You can't change the ports that you assign during the installation of a VMM management server unless you uninstall and then reinstall the VMM management server. Also, don't configure any feature to use port 5986; this port number is preassigned.

12.	In **Library configuration**, select whether to create a new library share or to use an existing library share on the computer. The default library share that VMM creates is named **MSSCVMMLibrary**, and the folder is located at **%SYSTEMDRIVE%\ProgramData\Virtual Machine Manager Library Files**. **ProgramData** is a hidden folder, and you can't remove it. After the VMM management server is installed, you can add library shares and library servers by using the VMM console or by using the VMM command shell.
13.	In **Upgrade compatibility report**, review the settings and select **Next** to proceed with the upgrade.
14.	In **Installation Summary**, review the settings and select **Install** to upgrade the server. **Installing features** page appears and displays the installation progress.
15.	In **Setup completed successfully**, select **Close** to finish the installation. To open the VMM console, check **Open the VMM console when this wizard closes** or you can select the Virtual Machine Manager Console icon on the desktop.

>[!NOTE]
>Once the upgrade is successful, [upgrade the host agent manually](#update-vmm-agents) by using the VMM. It is recommended to maintain the server and the agent in the same version.

If there's any issue with the setup, check the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder.

During the setup, VMM enables the following firewall rules. These rules remain in effect even if you uninstall the VMM later.

- Windows Remote Management
- Windows Standards-Based Storage Management

## Upgrade a highly available VMM server

You can upgrade a highly available (HA) VMM server 2022 to 2025.

The following two modes of upgrade are supported:

- [Mixed mode with no additional VMM servers](#mixed-mode-upgrade-with-no-additional-vmm-servers)
- [Mixed mode with additional VMM servers](#mixed-mode-upgrade-with-additional-vmm-servers)

>[!NOTE]
>SQL Server upgrade can be performed any time, independent of VMM upgrade.

### Mixed mode upgrade with no additional VMM servers
This procedure requires no additional VMM servers, but has increased risk for downtime in some scenarios. For example, when you have two node HA VMM and the active VMM node fails while you're upgrading the passive. In this scenario, your VMM server won't have a failover node available.

**Follow these steps**:  

1. Back up and retain the VMM database.
2. [Uninstall the VMM](#uninstall-the-vmm) on the passive node.  
3. On the passive VMM node, upgrade the management OS to Windows Server 2025.
4. Upgrade to the Windows 11 or Windows Server 2025 version of the [ADK](/windows-hardware/get-started/adk-install).
5. Install VMM 2025 on the passive node by using the following steps:
   -  In the main setup page, select **Install**.
   -  In **Select features to install**, select **VMM management server** and then select **Next**. The VMM console will be automatically installed.
   -  When prompted, confirm that you want to add this server as a node to the highly available deployment.
   -  On **Database Configuration** page, if prompted, select to upgrade the database.
   -  Review the summary and complete the installation.
6.	Fail over the active VMM node to the newly upgraded VMM server.
7.	Repeat the procedure on other VMM nodes.
8.  Update the cluster functional level by using the
**Update-ClusterFunctionalLevel** [command](/powershell/module/failoverclusters/update-clusterfunctionallevel).
9.	[Optional] Install the appropriate SQL Command line utilities.

### Mixed mode upgrade with additional VMM servers
This procedure requires additional VMM servers; however, it ensures almost no downtime in all the scenarios.

**Follow these steps**:

1. Back up and retain the VMM database.
2. Add the same number of additional servers (with Windows Server 2025 Management OS) that equals to the server number present in the HA cluster.
3. Install Windows 11/Windows Server 2025 version of the [ADK](/windows-hardware/get-started/adk-install) on the newly added 2025 servers.
4. Install VMM 2025 on one of the newly added servers by using the details in **step 5** in [Mixed mode upgrade with no additional VMM servers](#mixed-mode-upgrade-with-no-additional-vmm-servers).
5. Repeat the installation steps for all the other newly added servers.
6. Fail over the active VMM node to one of the newly added servers.
7. Uninstall VMM from the 2022 nodes, and remove these nodes from the cluster after failover.
8. Update the cluster functional level by using the
**Update-ClusterFunctionalLevel** [command](/powershell/module/failoverclusters/update-clusterfunctionallevel).
9.	[Optional] Install the appropriate SQL Command line utilities.


>[!NOTE]
>Once the HA VMM upgrade is successful, [upgrade the host agent manually](#update-vmm-agents) by using the VMM.  

## Update VMM agents

 After the upgrade, you need to update the VMM agents on your Hyper-V hosts and in your VMM library servers.

 1. Select **Fabric** >  **Servers** >  **All Hosts**.
 2. In the **Hosts** pane, right-click a column heading and then select **Agent Version Status**.
 3. Select the host with the VMM agent that you want to update. On the **Hosts** tab, in the **Host** group, select **Refresh**. If a host needs to have its VMM agent updated, the **Host Status** column will display **Needs Attention**, and the **Agent Version Status** column will display **Upgrade Available**.
 4. Right-click the host with the VMM agent that you want to update, and then select **Update Agent**. In **Update Agent**, provide the necessary credentials and then select **OK**.
 5. The **Agent Version Status** column will display a value of **Upgrading**. After the VMM agent is updated successfully on the host, the **Agent Version Status** column will display a value of **Up-to-date**, and the **Agent Version** column will display the updated version of the agent. After you refresh the host again, the **Host Status** column for the host will display a value of **OK**.
 6. You can update the VMM agent on a VMM library server in a similar manner. To view a list of VMM library servers, select **Fabric** > **Servers** > **Library Servers**.


## Reassociate hosts and library servers

 After the upgrade, you might need to reassociate virtual machine hosts and VMM library servers with the VMM management server.

 Follow these steps:

1. Select **Fabric** > **Servers** > **All Hosts**.
2. In the **Hosts** pane, ensure that the **Agent Status** column is displayed. If it isn't displayed, right-click a column heading and select **Agent Status**.
3. In the host group, select **Refresh**. If a host needs to be reassociated, the Host Status column displays **Needs Attention**, and the **Agent Status** column displays **Access Denied**. Right-click the host that you want to reassociate and then select **Reassociate**.
4. In **Reassociate Agent** page, provide credentials and then select **OK**. The Agent Status displays the status as **Reassociating**. After the host is reassociated successfully, the status changes to **Responding**.
5. Refresh the host; the host status columns now display **OK**. After you've reassociated the host, you might need to update the VMM agent on the host.

## Upgrade the VMM SQL Server database

There are a couple of reasons you might want to upgrade the VMM SQL Server database:

- You're upgrading VMM to System Center 2025, and the current SQL Server database version isn't supported.
- You want to upgrade a VMM standalone server to a high availability server, and SQL Server is installed locally.
- You want to move the SQL Server database to a different computer.

### Collect database information

Before you upgrade, collect information about the VMM database:

1. Record the database connection in the VMM console > **Settings** > **General** > **Database Connection**.
2. Record the account information in Server Manager > **Tools** > **Services**. Right-click **System Center Virtual Machine Manager** > **Properties** > **Log On**. This is the domain or local account that was assigned as the service account when VMM was installed. You can check if it's local in **Tools** > **Computer Manager** > **Local Users and Groups** > **Users**.
3. Check whether you used distributed key management when you installed VMM, or if encryption keys are stored locally on the VMM server.
4. If you're moving the VMM database, but not upgrading the VMM, check which update rollups have been applied on the VMM server.

### Upgrade a standalone database

1. Back up the existing VMM database, and copy the backup to a computer running a supported version of SQL Server.
2. Use SQL Server tools to restore the database.
   - If you're upgrading VMM, you'll specify the new SQL Server location in VMM setup > **Database Configuration**.
   - If you want to upgrade the database without upgrading VMM, you need to uninstall, and then reinstall VMM. When you uninstall, on the **Database Options** page, select **Retain database**. Then reinstall with the same settings you used for the original installation. On the **Database Configuration**, specify the new SQL Server details. After reinstall, apply the update rollups and check that the deployment is working as expected.

### Upgrade a highly available database

1. Record the source version of the existing database and the version you want to upgrade to.
2. Create a backup of the highly available SQL Server database from the active node of the SQL Server cluster.
3. Upgrade passive SQL Server nodes to the new version. After the upgrade, optionally install SQL Server Management Studio if you want to manage the SQL Server from this node.
4. Fail over the highly available SQL server role from the currently active node to the upgraded node. After failover, you can use SQL Server Management Studio to validate the running database version.
5. Repeat the upgrade for the other nodes in the HA SQL cluster. As an additional validation, you can fail over the SQL Server database roles to ensure that everything works as expected.

### Migrate a SQL Server cluster as part of the VMM upgrade

1. Take a backup of the highly available VMM database from the active node of the existing SQL cluster.
2. Note the VMM role name to use when reinstalling the VMM server role. Uninstall VMM server from the existing VMM cluster nodes with the retain database option.
When uninstalling VMM server from last node, you can get a message about unsuccessful SPN registration. This is a known issue with no functional impact.
3. Restore the backed-up DB into another SQL cluster running supported SQL version. Add the user on which VMM service is running as User to this new DB with membership to db_owner.
4. While upgrading VMM Server as part of SQL Cluster migration, give the Parameters corresponding to the new SQL Cluster.


## Redeploy Azure Site Recovery

If Azure Site Recovery was integrated into your VMM 2022 deployment, you need to redeploy it with VMM 2025 for [replication to Azure](/azure/site-recovery/site-recovery-vmm-to-azure) or [replication to a secondary site](/azure/site-recovery/site-recovery-vmm-to-vmm).


## Connect to Operations Manager

After the upgrade, reconnect VMM to the Operations Manager.

## Renew certificates for PXE servers

If you have a PXE server in the VMM fabric, you need to remove it from the fabric, and then add it again. This is to renew the PXE server certificate and avoid certificate errors.
