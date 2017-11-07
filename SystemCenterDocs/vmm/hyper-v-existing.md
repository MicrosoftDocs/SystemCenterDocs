---
ms.assetid: e72332a9-7f1b-477d-8d2c-34ea4ba137fa
title: Add Windows servers as Hyper-V hosts or clusters in the VMM fabric
description: This article describes how to provision Windows server as Hyper-V hosts and cluster in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---


# Add Windows servers as Hyper-V hosts or clusters in the VMM compute fabric



Read this article to learn about adding an existing Windows server as a Hyper-V host server or cluster to the System Center - Virtual Machine Manager (VMM) fabric, and configuring the host and cluster properties.

The article is relevant for adding Windows server computers with or without the Hyper-V role. If you add a Windows server that doesn't have Hyper-V installed, VMM will install the Hyper-V role as long as the server meets the prerequisites.


## Before you start

The prerequisites for adding an existing Hyper-V host server or cluster depend on whether Hyper-V is installed and where the server is located.

**Host location** | **Prerequisite**
--- | ---
**Server without Hyper-V** | If you want to add a server that doesn't have Hyper-V installed it must meet the [prerequisites](https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/System-requirements-for-Hyper-V-on-Windows) for Hyper-V installation.<br/><br/> The server must be running Windows Server 2012 R2 or later.<br/><br/>  If you want to add the VMM management server as a managed Hyper-V host the Hyper-V role must be installed on the server before you add it. You can't add a highly available VMM server as a managed Hyper-V host cluster.<br/></br> If you want to add a Hyper-V cluster the instructions in this article presume that the cluster already exists. Read this article if you want to create a cluster from existing Hyper-V hosts in the VMM fabric.<br/><br/>This article assumes that the server you want to add already has an operating system running on it. If you want to add a bare-metal computer as a Hyper-V host or cluster read this article.
**Same domain as VMM server, or two-way trusted domain** | You must specify account credentials for an account that has administrative rights on the computers that you want to add. You can enter a user name and password or specify a RunAs account. <br/><br/> If you use Group Policy to configure Windows Remote Management (WinRM) settings, note these settings:<br/><br/> WinRM Service settings must be configured through Group Policy, and can only apply to hosts that are in a trusted Active Directory domain. Specifically, VMM supports the configuration of the Allow automatic configuration of listeners, Turn On Compatibility HTTP Listener, and Turn on Compatibility HTTPS Listener Group Policy settings. VMM does not support other WinRM Service policy settings. <br/><br/> If you enable the **Allow automatic configuration of listeners** policy setting, you must configure it to allow messages from any IP address. In other words, in the policy setting, the IPv4 filter and IPv6 filter (depending on whether you use IPv6) must be set to *****.<br/><br/> WinRM Client settings cannot be configured through Group Policy. These policy settings might override client properties that VMM requires for the VMM agent to work correctly.<br/><br/> If you enable any unsupported WinRM Group Policy settings, installation of the VMM agent may fail.
**Untrusted domain** | VMM doesn't support configuring Windows Remote Management (WinRM) Group Policy settings (Service or Client) on hosts that are in an untrusted Active Directory domain. If WinRM Group Policy settings are enabled, installation of the VMM agent—required on the hosts might fail.<br/><br/> In an untrusted domain, when VMM  installs the agent on the servers or clusters, it also generates a certificate. The certificate is used to help secure communications with the host. When VMM adds the host or cluster, the certificate is automatically imported into the VMM management server trusted certificate store.
**Disjoined namespace (DNS suffix doesn't match the domain of which it's a member)** | The System Center Virtual Machine Manager service must be running as the local system account or as a domain account that has permission to register a Service Principal Name (SPN) in Active Directory.<br/><br/> When you try to add a computer that is in a disjointed namespace, VMM checks Active Directory to see if an SPN exists. If it doesn't VMM tries to create one. If the permissions are OK VMM adds the missing SPN automatically. Otherwise, host addition fails and you'll need to add the SPN manually. To do this type: **setspn -A HOST/**. For example, setspn –A HOST/hypervhost03.contosocorp.com hypervhost03. <br/><br/> If the host cluster is in a disjointed namespace and the VMM management server is not, add the DNS suffix for the host cluster to the TCP/IP connection settings on the VMM management server.<br/><br/> If you use Group Policy to configure Windows Remote Management (WinRM) settings, review the following requirements:<br/><br/> WinRM Service settings must be configured through Group Policy, and can only apply to hosts that are in a trusted Active Directory domain. Specifically, VMM supports the configuration of the Allow automatic configuration of listeners, Turn On Compatibility HTTP Listener, and Turn on Compatibility HTTPS Listener Group Policy settings. VMM does not support other WinRM Service policy settings.<br/><br/> If you enable the Allow automatic configuration of listeners policy setting, you must configure it to allow messages from any IP address. In other words, in the policy setting, the IPv4 filter and IPv6 filter (depending on whether you use IPv6) must be set to *****.<br/><br/> WinRM Client settings cannot be configured through Group Policy. These policy settings might override client properties that VMM requires for the VMM agent to work correctly.<br/><br/> If you enable any unsupported WinRM Group Policy settings, installation of the VMM agent may fail.
**Perimeter network or workgroup** | You'll need to install the VMM agent locally on the target host. To do this run VMM setup as an administrator and click **Optional Installations** > **Local Agent**. In **Security File Folder** select **This host in on a perimeter network** and enter an encryption key. In **Host network name** specify how the VMM server will contact the host server and note the computer name or IP address. Finish the wizard.<br/><br/> Check that a file SecurityFile.txt is located on the VMM server. By default it's located in C:\Program Files\Microsoft System Center version\Virtual Machine Manager.


## Add servers

1. In the VMM console open **Fabric** > **Servers**.
2. Click **Add group** > **Add Resources** > **Hyper-V hosts and Clusters**.
3. In the **Add Resource Wizard** > **Resource location**, select where the server you want to add is located.
	- If you're adding a host in a perimeter network select **Windows Server computer in a perimeter network**.
4. In **Credentials**, specify credentials for a domain account that has administrative permissions on all hosts that you want to add. (For computers in an untrusted domain, you must use a RunAs account.)
5. In **Discovery scope** specify:

	- **Same domain or domains with two-way trust**:
		- If you click **Specify Windows Server** computers by names, in **Computer names** enter names or IP addresses, one per line. If you are adding a Hyper-V host cluster, specify the name or IP address of the cluster or of any cluster node.
		- If you click **Specify an Active Directory** query to search for Windows Server computers, you can type or generate a query.
	- **Untrusted domain**: Discovery page dooesn't appear
	- **Disjointed namespace**: Enter the hos FQDN and select **Skip AD verification**.

6. In **Target resources**, specify the computers you want to add. Repeat for all hosts. If discovery succeeds the host will be listed under **Computer name**. Add as follows:

	- **Trusted domain or disjointed namespace**: Select the check box next to each computer that you want to add, and then click Next. If you specified a cluster name or cluster node in the previous step, select the check box next to the cluster name. (The cluster name is listed together with the associated cluster nodes.)
	- **Untrusted domain**: Enter the FQDN or IP address of the server or cluster that you want to add, and then click Add. For a cluster, you can enter an FQDN or IP address of the cluster or of one of the cluster nodes.
	- **Perimeter network/workgroup**: Enter the NETBIOS name or IP address of the host in the perimeter network. Enter the encryption key you created when you installed the agent on the host, and in Security file path enter the path to the SecurityFile.txt file.

7. In the **Host settings** > **Host group** list, click the host group to which you want to assign the host or host cluster. If the host is already associated with a different VMM management server, select  **Reassociate this host with this VMM environment**. If the host was associated with a different VMM management server, it will stop working on that server.

	- For a standalone host, in **Add the following path**, enter a path on the host for storing files for virtual machines that are deployed on the host, and then click **Add**. Repeat to add more than one path. If the path doesn't exist it's created automatically. If you leave the box empty, the default is %SystemDrive%\ProgramData\Microsoft\Windows\Hyper-V. As a  best practice don't add default paths that are on the same drive as the operating system files.
	- For a cluster don't specify default virtual machine paths. VMM automatically manages the paths that are available for virtual machines, based on the shared storage that is available to the host cluster

9. On the **Summary** page, confirm the settings, and then click **Finish**. The **Jobs** dialog box appears to show the job status. Wait for a Completed status. Verify that the host or cluster was added in the host group > host or cluster name. The status should be **OK**.


## Configure properties for Hyper-V hosts

After you've added Hyper-V hosts and servers in the VMM fabric there are a number of properties you can configure for standalone hosts and clusters.

**Tab** | **Settings**
--- | ---
**General** | View identity and system information for the host. This includes information such as processor information, total and available memory and storage, the operating system, the type of hypervisor, and the VMM agent version.<br/><br/>Enter a host description.<br/><br/> Configure whether the host is available for placement.<br/><br/> Configure the remote connection port. By default, the port is set to 2179.
**Hardware** | View or modify settings for CPU, memory, graphics processing units \(GPUs\), storage \(including whether the storage is available for placement\), network adapters, DVD\/CD\-ROM drives and Baseboard Management Controller \(BMC\) settings.
**Status** | Lists health status information for the host. Includes areas such as overall health, Hyper\-V role health and VMM agent health. In the **Status** pane, you can also do the following:<br/><br/> View error details.<br/><br/> Refresh the health status.<br/><br/> Click **Repair all**. VMM will try to automatically fix any errors.
**Virtual Machine Paths**/**Virtual Machines** | Shows the virtual machines that reside on the host, together with status information. Also enables you to register virtual machines on the host.
**Reserves** | Enables you to override host reserve settings from the parent host group, and configure reserved resources for the host. Configurable resources include CPU, memory, disk space, disk I\/O and network capacity.
**Storage** | Shows storage allocated to a host, and enables you to add and remove storage logical units or file shares.
**Virtual Switches** | Enables you to configure virtual switches.
**Placement Paths**/**Placement** | Enables you to configure the default virtual machine paths and default parent disk paths that will be used during virtual machine placement on the host.
**Servicing Windows** | Enables you to select servicing windows.
**Custom Properties** | Enables you to assign and manage custom properties.

## Properties for Hyper-V clusters

**Tab** | **Settings**
--- |---
**General** | View the name, host group and description. You can also configure the **Cluster reserve \(nodes\)** setting, and view the cluster reserve state.<br /><br/> The **Cluster reserve \(nodes\)** setting specifies the number of node failures a cluster must be able to sustain while still supporting all virtual machines deployed on the host cluster. If the cluster cannot withstand the specified number of node failures and still keep all of the virtual machines running, the cluster is placed in an over\-committed state. When over\-committed, the clustered hosts receive a zero rating during virtual machine placement. An administrator can override the rating and place a highly\-available virtual machine on an over\-committed cluster during a manual placement.
**Status** | View detailed status information for the host cluster:<br/><br/> Cluster validation test runs and successes. Includes a link to the latest validation report \(if available\). Note that accessing the report requires administrative permissions on the cluster node where the report is located.  For host clusters, you can perform an on\-demand cluster validation through VMM. To do this, in the **Fabric** workspace, locate and click the host cluster. Then, on the **Host Cluster** tab, click **Validate Cluster**. Cluster validation begins immediately.<br/><br/>  Online elements in the cluster: cluster core resources, disk witness in quorum, and the cluster service on each node.
**Available Storage** | Shows available storage, that is, storage logical units that are assigned to the host cluster but are not Cluster Shared Volumes \(CSV\).<br/><br/> You can also do the following:<br/><br/> Add and remove storage logical units that are managed by [VMM.<br/><br/> Convert available storage to shared storage \(CSV\).
**Shared Volumes** | Shows the shared volumes \(CSVs\) that are allocated to the host cluster. You can also do the following:<br/><br/> Add and remove CSVs that are managed by VMM. <br/><br/> Convert CSVs to available \(non\-CSV\) storage.|
**Custom Properties** | Custom properties that you manage.
