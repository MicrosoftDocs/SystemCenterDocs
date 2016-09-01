---
title: Upgrade to VMM in System Center Technical Preview
description: This article helps you to upgrade your existing VMM deployment to System Center Technical Preview
author:  rayne-wiselman
manager:  cfreemanwa
ms.date:  2016-08-30
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Upgrade to VMM in System Center Technical Preview

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

This article describes prerequisites for System Center 2016 - Virtual Machine Manager (VMM) upgrade. It includes upgrade steps, and describes tasks you should complete after the upgrade finishes.


## Before you begin

- Complete all jobs that are currently running in VMM. You can use the console to view the jobs’ status. All job history is deleted during the upgrade.
- Close any connections to the VMM management server, including the VMM console and the VMM command shell. Close any other programs that are running on the VMM management server.
- Ensure that there are no pending restarts on the computers on which the VMM roles are installed. For example, if you have installed a server role by using Server Manager or have applied a security update, you may need to restart the computer. After you have restarted the computer, sign in to the computer with the same user account to finish the installation of the server role or the security update.
- If you've deployed VMM with Azure Site Recovery make sure the latest version of the Microsoft Azure Site Recovery Provider is installed on the VMM management server. After the upgrade, you'll need to reinstall the Provider.
- Perform a full backup of the VMM database.
- Ensure that the server meets all requirements for VMM in System Center Technical Preview.
- If needed, upgrade SQL Server to a supported version. If the version you're using is supported in System Center Technical Preview you don't need to upgrade.
- Install Windows 8.1 Assessment and Deployment Kit (Windows ADK).
- If the current database is configured with AlwaysOn Availability Groups, complete the following tasks:
	- If the VMM database is included in the availability group, remove it. You can use the Microsoft SQL Management Studio tool to perform this task.
	- Initiate a failover to the computer that is running SQL Server and on which the VMM database is installed.

## Upgrade a standalone VMM server

1. Before you begin make sure you have at least local admin permissions on the computer on w which you're running the upgrade.
2. On the current VMM server start setup.
3. In the main setup page, click **Install**.
4. On the **Select features to install** page, select the **VMM management server** and then click **Next**. The VMM console will be automatically installed.
5. On the **Product registration information** page, provide the appropriate information, and then click **Next**. If you do not enter a product key, VMM will be installed as an evaluation version that expires 180 days after installation.
6. On the **Please read this license agreement** page, review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.
7. On the **Usage and Connectivity Data** page, select either option, and then click **Next**.
8. If the **Microsoft Update** page appears, select whether you want to use Microsoft Update, and then click **Next**. If you've already chosen to use Microsoft Update on this computer the page won't appear.
9. On the **Installation location** page, use the default path or type a different installation path for the VMM program files, and then click **Next**. The computer you're upgrading is checked to ensure prerequisites are in place. If the computer does not meet a prerequisite, a page that contains information about the prerequisite and how to resolve the issue appears.
10. On the **Database configuration** page:

	- If you're using a remote SQL instance specify the name of the computer that is running SQL Server.
	- If you are installing the VMM management server on the same computer that is running SQL Server, then in the **Server name** box, either type the name of the computer (for example, **vmmserver01**) or type **localhost**. If the SQL Server is in a cluster, type the cluster name.
	- Don't specify a **Port** value if you're using local SQL Server, or if your remote SQL Server uses the default port (1443).
	- Select **Existing Database** and select the database you backed up from your previous installation. Provide credentials with permissions to access the database. When you're prompted to upgrade the database click **Yes**.
13. On the **Configure service account and distributed key management** page, specify the account that the VMM service will use. You can't change the identity of the VMM service account after installation.
14. Under **Distributed Key Management**, select whether to store encryption keys in Active Directory. Choose settings careful for the service account and distributed key management. Depending on what you choose encrypted data such as passwords in templates might not be available after the upgrade and you'll need to enter them manually.
15. On the **Port configuration** page, use the default port number for each feature or provide a unique port number that is appropriate in your environment. You cannot change the ports that you assign during the installation of a VMM management server unless you uninstall and then reinstall the VMM management server. Also, do not configure any feature to use port 5986, because that port number is preassigned.
16. On the **Library configuration** page, select whether to create a new library share or to use an existing library share on the computer. The default library share that VMM creates is named MSSCVMMLibrary, and the folder is located at **%SYSTEMDRIVE%\ProgramData\Virtual Machine Manager Library Files**. **ProgramData** is a hidden folder, and you cannot remove it. After the VMM management server is installed, you can add library shares and library servers by using the VMM console or by using the VMM command shell.
17. In **Upgrade compatibility report** page, review settings and click **Next** to proceed with upgrade.
18. In **Installation Summary** review settings and click **Install** to upgrade the server. **Installing features** page appears and displays the installation progress.
18. On the **Setup completed successfully** page, click **Close** to finish the installation. To open the VMM console, you can ensure that **Open the VMM console when this wizard closes** is checked, or you can click the **Virtual Machine Manager Console** icon on the desktop.

During Setup, VMM enables the following firewall rules. These rules remain in effect even if you later uninstall VMM.

- Windows Remote Management
- Windows Standards-Based Storage Management

> [!NOTE]
> If Setup does not finish successfully, consult the log files in the **%SYSTEMDRIVE%\ProgramData\VMMLogs** folder. **ProgramData** is a hidden folder.


## Upgrade a high availability deployment

Here's what you'll need to do:

1. Uninstall VMM from the cluster nodes that you want to upgrade, while choosing to retain the database.
2. We strongly recommend that you upgrade the operating system to Windows Server Technical Preview on the VMM management server.

	- If you choose to not upgrade Windows, delete the high availability VMM resource group from the failover cluster.
	- If you choose to upgrade Windows:
		- During the upgrade, choose the upgrade option, not a fresh installation, to retain data.
		- Note the name of your cluster, and then destroy the cluster.
		- Upgrade the operating system on all the nodes in the cluster that you want to upgrade.
		- Recreate the cluster by using its previous name.
3. Now run VMM setup on each cluster node.
4. In the main setup page, click **Install**.
4. On the **Select features to install** page, select the **VMM management server** and then click **Next**. The VMM console will be automatically installed.
5. On the **Product registration information** page, provide the appropriate information, and then click **Next**. If you do not enter a product key, VMM will be installed as an evaluation version that expires 180 days after installation.
6. On the **Please read this license agreement** page, review the license agreement, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.
7. On the **Usage and Connectivity Data** page, select either option, and then click **Next**.
8. If the **Microsoft Update** page appears, select whether you want to use Microsoft Update, and then click **Next**. If you've already chosen to use Microsoft Update on this computer the page won't appear.
9. On the **Installation location** page, use the default path or type a different installation path for the VMM program files, and then click **Next**. The computer you're upgrading is checked to ensure prerequisites are in place. If the computer does not meet a prerequisite, a page that contains information about the prerequisite and how to resolve the issue appears.
10. On the **Database configuration** page:

	- If you're using a remote SQL instance specify the name of the computer that is running SQL Server.
	- If you are installing the VMM management server on the same computer that is running SQL Server, then in the **Server name** box, either type the name of the computer (for example, **vmmserver01**) or type **localhost**. If the SQL Server is in a cluster, type the cluster name.
	- Don't specify a **Port** value if you're using local SQL Server, or if your remote SQL Server uses the default port (1443).
	- Select **Existing Database** and select the database you backed up from your previous installation. Provide credentials with permissions to access the database. When you're prompted to upgrade the database click **Yes**.
13. On the Cluster configuration page type a name for the VMM high availability deployment. Don't use the cluster name or the name of the computer on which you're installing VMM. This name is used when you connect to VMM using the VMM console.
14. If you are using static IPv4 addresses, specify the IP address to assign to the clustered service name. The clustered service name and its assigned IP address will be registered in DNS. If you are using IPv6 addresses or DHCP, you don't need to do this.
14. On the **Configure service account and distributed key management** page, specify the account that the VMM service will use. You can't change the identity of the VMM service account after installation.
14. Under **Distributed Key Management**, select whether to store encryption keys in Active Directory. Choose settings careful for the service account and distributed key management. Depending on what you choose encrypted data such as passwords in templates might not be available after the upgrade and you'll need to enter them manually.
15. On the **Port configuration** page, use the default port number for each feature or provide a unique port number that is appropriate in your environment. You cannot change the ports that you assign during the installation of a VMM management server unless you uninstall and then reinstall the VMM management server. Also, do not configure any feature to use port 5986, because that port number is preassigned.
16. On the **Library configuration** page, select whether to create a new library share or to use an existing library share on the computer. The default library share that VMM creates is named MSSCVMMLibrary, and the folder is located at **%SYSTEMDRIVE%\ProgramData\Virtual Machine Manager Library Files**. **ProgramData** is a hidden folder, and you cannot remove it. After the VMM management server is installed, you can add library shares and library servers by using the VMM console or by using the VMM command shell.
17. In **Upgrade compatibility report** page, review settings and click **Next** to proceed with upgrade.
18. In **Installation Summary** review settings and click **Install** to upgrade the server. **Installing features** page appears and displays the installation progress.
18. On the **Setup completed successfully** page, click **Close** to finish the installation. To open the VMM console, you can ensure that **Open the VMM console when this wizard closes** is checked, or you can click the **Virtual Machine Manager Console** icon on the desktop.

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

1. Click **Library **> **Templates** > **VM Templates**.
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
7. In the **Driver File Name Properties** > **Custom tags*,* enter custom tags separated by a semi-colon, or click **Select** to assign available tags or to create and assign new ones. If you click **Select**, and then click **New Tag**, you can change the name of the tag after you click **OK**. For example, if you added a network adapter driver file, you could create a tag that is named ServerModel NetworkAdapterModel, where ServerModel is the server model and NetworkAdapterModel is the network adapter model.


## Relocate the VMM library

- If you upgraded to a high availability VMM management server, we recommend that you relocate your VMM library to a high availability file server. 
- After you create a new VMM library, you will want to move the resources from the previous VMM library to the new VMM library.
- To preserve the custom fields and properties of saved virtual machines in the previous VMM library, deploy the saved virtual machines to a host and then save the virtual machines to the new VMM library.
-  Note that operating system and hardware profiles cannot be moved. You need to re-create these profiles.
