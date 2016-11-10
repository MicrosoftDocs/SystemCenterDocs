---
ms.assetid: ecaa876d-d376-48a0-a20c-15f0c266e616
title: Upgrade VMM
description: This article helps you to upgrade your existing VMM servers and databases to System Center 2016 - VMM
author: rayne-wiselman
ms.author: raynew
manager: cfreemanwa
ms.date: 11/09/2016
ms.topic: article
ms.prod:  system-center-threshold
ms.technology: virtual-machine-manager
---

# Upgrade to System Center 2016 - VMM

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes prerequisites for upgrading to System Center 2016 - Virtual Machine Manager (VMM). It includes upgrade steps, and describes tasks you should complete after the upgrade finishes.


## Before you start

- Complete all jobs that are currently running in VMM. You can use the console to view the jobs’ status. All job history is deleted during the upgrade.
- Close any connections to the VMM management server, including the VMM console and the VMM command shell. Close any other programs that are running on the VMM management server.
- Ensure that there are no pending restarts on the computers on which the VMM roles are installed. For example, if you have installed a server role by using Server Manager or have applied a security update, you may need to restart the computer. After you have restarted the computer, sign in to the computer with the same user account to finish the installation of the server role or the security update.
- If you've deployed VMM with Azure Site Recovery make sure the latest version of the Microsoft Azure Site Recovery Provider is installed on the VMM management server. After the upgrade, you'll need to reinstall the Provider.
- Perform a full backup of the VMM database.
- Ensure that the server meets all requirements for VMM, and that prerequisites are in place [Learn more](../plan/plan-install.md)
- If needed, upgrade SQL Server to a supported version.
- Verify the [supported SQL Server versions](https://technet.microsoft.com/system-center-docs/system-requirements/sql-server-version-compatibility). Currently for best performance, we recommend SQL 2014 with SP1.
- Note that if you're upgrading a high availability SQL Server database, remote connectivity to the console sessions will be broken while the SQL Server role fails over. Connectivity is automatically restored after failover completes.
- If the current database is configured with AlwaysOn availability groups:
	- If the VMM database is included in the availability group, remove it in SQL Server Management Studio.
	- Initiate a failover to the computer that is running SQL Server, and on which the VMM database is installed.
- Make sure your VMM server running System Center 2012 R2 is running update rollup 9 or later.
- If you're running Operations Manager with VMM, disconnect the connection between VMM and Operations Manager before you begin the upgrade. Enable the connection again after both VMM and Operations Manager are running on System Center 2016.


## Upgrade a standalone VMM server

1. Uninstall VMM and select to retain the database. Make sure you remove both the VMM management server and the console.
2. On the current VMM server, upgrade the operating system to Windows Server 2016.
3. Start setup to install VMM 2016. In the main setup page, click **Install**.
4. In **Select features to install**, select **VMM management server** >  **Next**. The VMM console is automatically installed.
5. In **Product registration information**, provide the appropriate information > **Next**. If you don't enter a product key, VMM will be installed as an evaluation version that expires 180 days after installation.
6. In **Please read this license agreement** page, review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** > **Next**.
7. In **Usage and Connectivity Data** page, select either option > **Next**.
8. If **Microsoft Update** appears, select whether you want to use Microsoft Update >  **Next**.
9. In **Installation location**, use the default path or type a different installation path for the VMM program files, and then click **Next**. The computer you're upgrading is checked to ensure it complies with prerequisites.
10. In **Database configuration**:

	- If you're using a remote SQL Server instance, specify the name of the remote SQL Server computer.
	- If SQL Server will run on the VMM server, type the VMM server name, or type **localhost**. If the SQL Server is in a cluster, type the cluster name.
	- Don't specify a **Port** value if you're using local SQL Server, or if your remote SQL Server uses the default port (1443).
	- Select **Existing Database** and select the database you backed up from your previous installation. Provide credentials with permissions to access the database. Click **Yes** to upgrade.
13. In **Configure service account and distributed key management**, specify the account that the VMM service will use. You can't change the identity of the VMM service account after installation.
14. Under **Distributed Key Management**, select whether to store encryption keys in Active Directory. Choose settings carefully for the service account and distributed key management. Depending on what you choose encrypted data such as passwords in templates might not be available after the upgrade and you'll need to enter them manually.
15. In **Port configuration**, use the default port number for each feature or provide a unique port number that is appropriate in your environment. To change the ports that you assign during the VMM installation, you need to uninstall and reinstall the VMM server.  Don't configure port 5986, because it's preassigned.
16. In **Library configuration**, select whether to create a new library share or to use an existing library share on the computer. The default library share that VMM creates is named MSSCVMMLibrary, and the folder is located at **%SYSTEMDRIVE%\ProgramData\Virtual Machine Manager Library Files**. **ProgramData** is a hidden folder, and you cannot remove it. After the VMM management server is installed, you can add library shares and library servers.
17. In **Upgrade compatibility report**, review settings > **Next**.
18. In **Installation Summary**, review settings and click **Install** to upgrade the server. **Installing features** page appears and displays the installation progress.
18. In  **Setup completed successfully** page, click **Close** to finish the installation. If there's an issue with setup, check the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.

During Setup, VMM enables the following firewall rules. These rules remain in effect even if you later uninstall VMM.

- Windows Remote Management
- Windows Standards-Based Storage Management


## Upgrade a highly available VMM server

Here's what you'll need to do:

1. Uninstall VMM from the cluster nodes that you want to upgrade, while choosing to retain the database.
2. We strongly recommend that you upgrade the operating system to Windows Server 2016 on the VMM management server.

	- If you choose to not upgrade Windows, delete the high availability VMM resource group from the failover cluster.
	- If you choose to upgrade Windows:
		- During the upgrade, choose the upgrade option, not a fresh installation, to retain data.
		- Note the name of your cluster, and then destroy the cluster.
		- Upgrade the operating system on all the nodes in the cluster that you want to upgrade.
		- Recreate the cluster by using its previous name.
3. Now run VMM setup on each cluster node.
4. In the main setup page, click **Install**.
5. In **Select features to install**, select the **VMM management server** and then click **Next**. The VMM console will be automatically installed.
6. In **Product registration information**, provide the appropriate information, and then click **Next**. If you do not enter a product key, VMM will be installed as an evaluation version that expires 180 days after installation.
7. In **Please read this license agreement**, review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.
8. In **Usage and Connectivity Data**, select either option, and then click **Next**.
9. If **Microsoft Update** appears, select whether you want to use Microsoft Update > **Next**. If you've already chosen to use Microsoft Update on this computer the page won't appear.
10. In **Installation location**, use the default path or type a different installation path for the VMM program files, and then click **Next**. The computer you're upgrading is checked to ensure prerequisites are in place. If the computer does not meet a prerequisite, a page that contains information about the prerequisite and how to resolve the issue appears.
11. In **Database configuration**:

	- If you're using a remote SQL instance specify the SQL Server computer name.
	- If SQL Server runs on the VMM server, type the name of the VMM server, or type **localhost**. If the SQL Server is in a cluster, type the cluster name.
	- Don't specify a **Port** value if you're using local SQL Server, or if your remote SQL Server uses the default port (1443).
	- Select **Existing Database** and select the database you backed up from your previous installation. Provide credentials with permissions to access the database. When you're prompted to upgrade the database click **Yes**.
12. In **Cluster configuration** page type a name for the VMM high availability deployment. Don't use the cluster name or the name of the computer on which you're installing VMM. This name is used when you connect to VMM using the VMM console.
13. If you are using static IPv4 addresses, specify the IP address to assign to the clustered service name. The clustered service name and its assigned IP address will be registered in DNS. If you are using IPv6 addresses or DHCP, you don't need to do this.
14. In **Configure service account and distributed key management**, specify the account that the VMM service will use. You can't change the identity of the VMM service account after installation.
15. Under **Distributed Key Management**, select whether to store encryption keys in Active Directory. Choose settings careful for the service account and distributed key management. Depending on what you choose encrypted data such as passwords in templates might not be available after the upgrade and you'll need to enter them manually.
16. In **Port configuration**, use the default port number for each feature or provide a unique port number that is appropriate in your environment. You cannot change the ports that you assign during the installation of a VMM management server unless you uninstall and then reinstall the VMM management server. Also, do not configure any feature to use port 5986, because that port number is preassigned.
17. In **Library configuration**, select whether to create a new library share or to use an existing library share on the computer. The default library share that VMM creates is named MSSCVMMLibrary, and the folder is located at **%SYSTEMDRIVE%\ProgramData\Virtual Machine Manager Library Files**. **ProgramData** is a hidden folder, and you cannot remove it. After the VMM management server is installed, you can add library shares and library servers by using the VMM console or by using the VMM command shell.
18. In **Upgrade compatibility report**, review settings > **Next** to proceed with upgrade.
19. In **Installation Summary**, review settings and click **Install** to upgrade the server. **Installing features** page appears and displays the installation progress.
20. In **Setup completed successfully**, click **Close** to finish the installation. To open the VMM console, you can ensure that **Open the VMM console when this wizard closes** is checked, or you can click the **Virtual Machine Manager Console** icon on the desktop.

## Upgrade the VMM SQL Server database

There are a couple of reasons you might want to upgrade the VMM SQL Server database:

- You're upgrading VMM to System Center 2016, and the current SQL Server database version isn't supported.
- You want to upgrade a VMM standalone server to a high availability server, and SQL Server is installed locally.
- You want to move the SQL Server database to a different computer.

### Collect database information

Before you upgrade, collect information about the VMM database:

1. Record the database connection in the VMM console > **Settings** > **General** > **Database Connection**.
2. Record the account information in Server Manager > **Tools** > **Services**. Right-click **System Center Virtual Machine Manager** > **Properties** > **Log On**. This is the domain or local account that was assigned as the service account when VMM was installed. You can check if it's local in **Tools** > **Computer Manager** > **Local Users and Groups** > **Users**.
3. Check whether you used distributed key management when you installed VMM, or if encryption keys are stored locally on the VMM server.
4. If you're moving the VMM database, but not upgrading VMM, check which update rollups have been applied on the VMM server.

### Standalone database

1. Back up the existing VMM database, and copy the backup to a computer running a supported version of SQL Server.
2. Use SQL Server tools to restore the database.
3. If you are upgrading VMM, specify the new SQL Server location in VMM setup > **Database Configuration**.
4. If you're not upgrading VMM, you need to uninstall and then reinstall. To do this, close all connections to the VMM management server, and uninstall VMM. On the **Database Options** page, select **Retain database**.
5. Reinstall with the same settings you used for the original installation, but on the **Database Configuration** page:

	- Specify the name of the computer on which the VMM database is now located.
	- Specify the availability group listener if the database is configured with AlwaysOn.
	- Specify the port to use for communicating with the SQL Server computer if SQL Server is remote, the SQL Server browser service isn't started on the computer, and SQL Server isn't using the default port (1433). Otherwise, you don't need to specify a port setting.
	After reinstallation apply the same update rollups, and check that the VMM deployment is working. Then, apply any new update rollups if needed.


### Highly available database

1. Record the source version of the existing database, and the version you want to upgrade to. Check that the version is supported. VMM supports all SQL Server versions that are in mainstream support.
2. Create a backup of the highly available SQL Server database, from the active node of the SQL Server cluster.
3. Upgrade passive SQL Server nodes to the new version. After the upgrade, optionally install SQL Server Management Studio if you want to manage SQL Server from this node.
4. Fail over the highly available SQL server role, from the currently active node to the upgraded node. After failover, you can use SQL Server Management Studio to validate the running database version.
5. Repeat the upgrade for the other nodes in the HA SQL cluster. As an additional validation, you can fail over the SQL Server database roles, to ensure that everything works as expected.



## Post-upgrade tasks

After you complete the VMM upgrade, you might need to make additional configuration changes to your VMM environment.


## Reassociate hosts and library servers

In some upgrade scenarios, you need to reassociate virtual machine hosts and VMM library servers with the VMM management server after the upgrade.

1. Click **Fabric** > **Servers **> **All Hosts**.
2. In the **Hosts** pane, ensure that the **Agent Status** column is displayed. If it isn't right-click a column heading > **Agent Status**.
3. Select the host that you need to reassociate with the VMM management server.
4. In **Hosts** > **Host** group, click R**efresh**. If a host needs to be reassociated, the **Host Status** column  will display a value of **Needs Attention**, and the **Agent Status** column will display a value of **Access Denied**.
Right-click the host that you want to reassociate, and then click **Reassociate**. In **Reassociate Agent** provide credentials, and then click **OK**. The Agent Status column will display a value of Reassociating. After the host has been reassociated successfully, the **Agent Status** column will display a value of **Responding**. And after you refresh the host again, the **Host Status** column for the host will display a value of **OK**.
After you have reassociated the host, you will most likely have to update the VMM agent on the host.


## Update VMM agents

After the upgrade, you need to update the VMM agents on your Hyper-V hosts and in your VMM library servers.

1. Click **Fabric** >  **Servers** >  **All Hosts**.
2. In the **Hosts** pane, right-click a column heading, and then click **Agent Version Status**.
3. Select the host with the VMM agent that you want to update. On the **Hosts** tab, in the **Host** group, click **Refresh**. If a host needs to have its VMM agent updated, the **Host Status** column will display **Needs Attention**, and the **Agent Version Status** column will display **Upgrade Available**.
4. Right-click the host with the VMM agent that you want to update, and then click **Update Agent**. In **Update Agent** provide the necessary credentials, and then click **OK**.
5. The **Agent Version Status** column will display a value of **Upgrading**. After the VMM agent is updated successfully on the host, the **Agent Version Status** column will display a value of **Up-to-date**, and the **Agent Version** column will display the updated version of the agent. After you refresh the host again, the **Host Status** column for the host will display a value of **OK**.
6. You can update the VMM agent on a VMM library server in a similar manner. To view a list of VMM library servers, click **Fabric** > **Servers** > **Library Servers**.

## Configure AlwaysOn Availability Groups

If you upgraded a database that was configured with AlwaysOn Availability Groups, you need to complete a few tasks to ensure that the upgraded database is properly configured with AlwaysOn Availability Groups.

1. Add the VMM database to the availability group. You can use Microsoft SQL Server Management Studio to perform this task.
2. On the secondary node computer in the cluster that is running SQL Server, create new sign-in account. Configure the sign-in name so that it is identical to the VMM service account name. Include user mapping to the VMM database, and configure the database owner credentials.
3. Initiate a failover to the secondary node computer that is running SQL Server, and verify that you can restart the VMM service (scvmmservice).
4. Repeat the last two steps for every secondary node in the cluster that is running SQL Server.
5. If this is a high availability VMM setup, continue to install other high availability VMM nodes.







## Restore Azure Site Recovery

If you've deployed Azure Site Recovery to replicate VMs in VMM private clouds, you need to perform a few steps to restore the Windows Azure Hyper-V Recovery Manager Provider.

1. Reinstall the latest version of Microsoft Azure Site Recovery Provider. This restores the Provider registration information that was removed during the VMM upgrade.
2. In the Azure portal > **Jobs** wait for the Repair Provider job to complete.


## Update virtual machine templates

All virtual machine templates that were upgraded need to correctly specify the virtual hard disk that contains the operating system.

1. Click **Library** > **Templates** > **VM Templates**.
2. Right-click the template > **Properties** > **Hardware Configuration** and check disk settings.


## Update driver packages

Driver packages that were previously added to the VMM library must be removed and added again to be correctly discovered.

If you plan to assign custom drivers, the driver files must exist in the library. You can tag the drivers in the library, so that you can later filter them by tag.  After files are added, when you configure a physical computer profile, you can specify the driver files. VMM installs the specified drivers when it installs the operating system on a physical computer.

In the physical computer profile, you can select to filter the drivers by tags, or you can select to filter drivers with matching Plug and Play (PnP) IDs on the physical computer. If you select to filter the drivers by tags, VMM determines the drivers to apply by matching the tags that you assign to the drivers in the library to the tags that you assign in the profile. If you select to filter drivers with matching PnP IDs, you don't need to assign custom tags.


1. Locate a driver package that you want to add to the library.
2. In the library share that is located on the library server that is associated with the group where you want to deploy the physical computers, create a folder to store the drivers, and then copy the driver package to the folder.
3. We strongly recommend that you create a separate folder for each driver package, and that you do not mix resources in the driver folders. If you include other library resources such as .iso images, .vhd files or scripts with an .inf file name extension in the same folder, the VMM library server will not discover those resources. Also, when you delete an .inf driver package from the library, VMM deletes the entire folder where the driver .inf file resides.
4. In the VMM console, open the Library workspace. In the **Library** > **Library Servers**, expand the library server where the share is located, right-click the share, and then click **Refresh**. After the library refreshes, the folder that you created to store the drivers appears.
5. Now assign tags if required. In **Library**, expand the folder that you created to store the drivers in the previous procedure, and then click the folder that contains the driver package.
6. In the **Physical Library Objects**, right-click the driver .inf file, and then click **Properties**.
7. In the **Driver File Name Properties** > **Custom tags**, enter custom tags separated by a semi-colon, or click **Select** to assign available tags or to create and assign new ones. If you click **Select**, and then click **New Tag**, you can change the name of the tag after you click **OK**. For example, if you added a network adapter driver file, you could create a tag that is named ServerModel NetworkAdapterModel, where ServerModel is the server model and NetworkAdapterModel is the network adapter model.


## Relocate the VMM library

- If you upgraded to a high availability VMM management server, we recommend that you relocate your VMM library to a high availability file server.
- After you create a new VMM library, you will want to move the resources from the previous VMM library to the new VMM library.
- To preserve the custom fields and properties of saved virtual machines in the previous VMM library, deploy the saved virtual machines to a host and then save the virtual machines to the new VMM library.
-  Note that operating system and hardware profiles cannot be moved. You need to re-create these profiles.
