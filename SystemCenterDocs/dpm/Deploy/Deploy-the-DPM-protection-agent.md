---
title: Deploy the DPM protection agent
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 502fff45-79b5-477b-af4f-3b8a39bdde1a
---
# Deploy the DPM protection agent
The DPM protection agent is software that you install on each computer that contains data you 
		  want to back up with DPM. It consists of two components \- the protection agent itself and an agent coordinator. 
		  Here's what it does:

-   Identifies data that DPM can protect and recover.

-   Allows the DPM server to browse the shares, volumes, and folders on the protected computer.

-   Creates a change journal for each protected volume and stores the journal in a hidden file on that volume. 
    it records any changes to protected data in the change journal, and transfers the journal from the protected computer to the 
    DPM server so that DPM can synchronize the primary data with the replica.

You'll set up the agent as follows:

-   If the computer containing data you want to back up is behind a firewall you'll need 
    	 to [Set up firewall exceptions](#BKMK_Firewall).

-   If the computer isn't behind a firewall, or you've configured firewall exceptions to allow access, you can [Install the agent from the DPM console](#BKMK_Console) .

-   Alternatively if you don't have access through the firewall, the computer you want to protect is in a workgroup or untrusted domain, or you simply need to use a different installation method, you can [Install the agent manually](#BKMK_Manual) and then [Attach the agent](#BKMK_Attach)

## <a name="BKMK_Firewall"></a>Set up firewall exceptions
For a protection agent to communicate with the DPM server through a firewall, firewall exceptions are required.

Configure an incoming exception for sqservr.exe for the DPM instance of SQL Server, to allow TCP on port 80.The report server listens for HTTP requests on port 80 for HTTP requests. The following table lists the protocols and ports required for communication between the DPM server and protected servers and clients.

|Protocol|Port|Details|
|------------|--------|-----------|
|DCOM|135\/TCP<br />Dynamic|The DPM control protocol uses DCOM. DPM issues commands to the protection agent by invoking DCOM calls on the agent. The protection agent responds by invoking DCOM calls on the DPM server.<br /><br />TCP port 135 is the DCE endpoint resolution point used by DCOM.<br /><br />By default, DCOM assigns ports dynamically from the TCP port range of 1024 through 65535. However, you can configure this range by using Component Services.<br /><br />Note that for DPM\-Agent communication you must open the upper ports 1024\-65535. To open the ports, perform the following steps:<br /><br />1.  In IIS 7.0 Manager, in the **Connections** pane, click the server\-level node in the tree.<br />2.  Double\-click the **FTP Firewall Support** icon in the list of features.<br />3.  Enter a range of values for the **Data Channel Port Range**.<br />4.  After you enter the port range for your FTP service, in the **Actions** pane, click **Apply** to save your configuration settings.|
|TCP|5718\/TCP<br />5719\/TCP|The DPM data channel is based on TCP. Both DPM and the protected computer initiate connections to enable DPM operations such as synchronization and recovery.<br /><br />DPM communicates with the agent coordinator on port 5718 and with the protection agent on port 5719.|
|DNS|53\/UDP|Used between DPM and the domain controller, and between the protected computer and the domain controller, for host name resolution.|
|Kerberos|88\/UDP 88\/TCP|Used between DPM and the domain controller, and between the protected computer and the domain controller, for authentication of the connection endpoint.|
|LDAP|389\/TCP<br />389\/UDP|Used between DPM and the domain controller for queries.|
|NetBIOS|137\/UDP<br />138\/UDP<br />139\/TCP<br />445\/TCP|Used between DPM and the protected computer, between DPM and the domain controller, and between the protected computer and the domain controller, for miscellaneous operations. Used for SMB directly hosted on TCP\/IP for DPM functions.|

## <a name="BKMK_Console"></a>Install the agent from the DPM console

### <a name="BKMK_Install"></a>

1.  In DPM Administrator Console, click **Management** > **Agents**. Click **Install** on the tool ribbon to open the Protection Agent Installation Wizard.

2.  On the **Select Agent Deployment Method** page, click **Install agents** > **Next**.

3.  On the **Select Computers** page, DPM displays a list of available computers that are in the same domain as the DPM server. Add the required computer.

    -   The first time you use the wizard DPM queries Active Directory to get a list of available computers. After the first installation, DPM stores the list of computers in its database, which is updated once each day by the auto\-discovery process.

    -   To find a computer in another domain that has a two\-way trust relationship with the domain that the DPM server is located in, you must type the fully qualified domain name of the computer that you want to protect \(for example, *<Computer1>***.Domain1.contoso.com**, where *Computer1* is the name of the computer that you want to protect, and *Domain1.contosa.com* is the domain to which the target computer belongs.

    -   The **Advanced** button page is enabled only when there is more than one version of a protection agent available for installation on the computers. You can use this option to install a previous version of the protection agent that was installed before you upgraded DPM server to a more recent version.

4.  On the **Enter Credentials** page, type the user name and password for a domain account that is a member of the local Administrators group on all selected computers.

    -   In the **Domain** box, accept or type the domain name of the user account that you are using to install the protection agent on the target computer. This account may belong to the domain that the DPM server is located in or to a domain that has a two\-way trust relationship with the domain that the DPM server is located in.

    -   If you’re installing a protection agent on a computer across a trusted domain, enter your current domain user credentials. You can be a member of any domain that has a two\-way trust relationship with the domain that the DPM server and you must be member of the local Administrators group on all selected computers on which you want to install an agent.

    -   If you select a node in a cluster, DPM detects all additional nodes in the cluster and displays the **Select Cluster Nodes** page.

5.  On the **Select Cluster Nodes** page,  select an option that you want DPM to use for installing agents on additional nodes in the cluster, and then click **Next**.

6.  On the **Choose Restart Method** page, select the method to use to restart the selected computers after the protection agent is installed. The computer must be restarted before you can start protecting data. A restart is necessary to load the volume filter that DPM uses to track and transfer block\-level changes between the DPM server and the protected computers.

    -   If you select to restart the computers later the protection agent installation status isn’t refreshed automatically on the **Agents** tab in the **Management** task area after the computer restart, and you’ll need to click **Refresh Information**.

    -   Note that you don’t need to restart the computer if you are installing a protection agent on another DPM  server.

    -   If any of the computers that you selected are nodes in a cluster, an additional **Choose Restart Method** page appears that you can use to select the method to restart the clustered computers. You’ll need to install a protection agent on all nodes in a cluster to successfully protect the clustered data. The computers must be restarted before you can start protecting data. Because of the time required to start services, it might take a few minutes after a restart before DPM  can contact the agent on the cluster.

    -   DPM will not automatically restart a computer that belongs to a Microsoft Cluster Server \(MSCS\) cluster. You must manually restart computers in an MSCS cluster.

7.  On the **Summary** page, click **Install** to begin the installation. If the EULA appears accept it for installation to start. On the **Task** tab of the Installation page you can see whether the installation is successful. You can click **Close** before the wizard is finished and monitor the installation progress in **Agents** tab in the **Management** task area. If the installation is unsuccessful, you can view the alerts in the **Monitoring** task area on the **Alerts** tab.

    Note: After you install a protection agent on a computer that is part of a Windows SharePoint Services farm, each of the computers in the farm will not appear as protected computers on the**Agents** tab in the **Management** task area, only the computer that you selected. However, if the Windows SharePoint Services farm has data on the selected computer, [!INCLUDE[dpm2012short](../../includes/dpm2012short_md.md)] protects the data on all of the computers in the farm, provided all of them have the protection agent installed.

## <a name="BKMK_Manual"></a>Install the agent manually

1.  If you install the agent on a computer behind a firewall, you need to make sure that the agent can be pushed out through the firewall.

    For example, you can run the following command on the computer to configure Windows Firewall: **netsh advfirewall firewall add rule name\="Allow DPM Remote Agent Push" dir\=in action\=allow service\=any enable\=yes profile\=any remoteip\=<IPAddress>**, where IPAddress is the address of the DPM server.

    To configure the ports exception on the firewall, see [Configure firewall exceptions for the agent](https://technet.microsoft.com/en-us/library/Hh758204.aspx).

2.  On the computer that you want to protect, open an elevated Command Prompt window, and then run the following commands:

    To assign a drive letter, type: 
    **net use *Z*: \\\\<DPMServerName>\\c$**
     where *Z* is the local drive letter that you want to assign and *<DPMServerName>* is the name of the DPM server that will protect the computer.

    To change the directory, do the following:

    -   For a 64\-bit computer type **cd \/d *<assigned drive letter>*:\\Program Files\\Microsoft DPM\\DPM\\ProtectionAgents\\RA\\3.0.*<build number>*.0\\amd64** where *<assigned drive letter>* is the drive letter that you assigned in the previous step and *<build number>* is the latest DPM build number. For example: **cd \/d X:\\Program Files\\Microsoft DPM\\DPM\\ProtectionAgents\\RA\\3.0.7696.0\\amd64**

    -   For a 32\-bit computer type: **cd \/d *<assigned drive letter>*:\\Program Files\\Microsoft DPM\\DPM\\ProtectionAgents\\RA\\3.0.*<build number>*.0\\i386**
         where *<assigned drive letter>* is the drive that you mapped in the previous step and *<build number>* is the latest DPM build number.

3.  To install the protection agent open an elevated Command Prompt window, and then run one of the following commands:

    -   For a 64\-bit computer type: **DpmAgentInstaller\_x64.exe *<DPMServerName>***
        where *<DPMServerName>* is the fully qualified domain name \(FQDN\) of the DPM server.For example: **DPMAgentInstaller\_x64.exe DPMserver1.contoso.com**

    -   For a 32\-bit computer type: **DpmAgentInstaller\_x86.exe *<DPMServerName>***
        where *<DPMServerName>* is the fully qualified domain name of the DPM server.

    Note:

    -   To perform a silent installation, you can use the **\/q** option after the **DpmAgentInstaller\_x64.exe** command.For example: **DpmAgentInstaller\_x64.exe \/q *<DPMServerName>***

    -   To accept the EULA manually in a silent installation use **DpmAgentInstaller\_x64.exe \/q <DPMServerName> \/IAcceptEULA**

    -   If you specify a DPM server name in the command line, it installs the protection agent, and automatically configures the security accounts, permissions, and firewall exceptions necessary for the agent to communicate with the specified DPM server. If you didn’t specify a server name, open an elevated Command Prompt on the targeted computer and do the following:

        1.  To change the directory type: **cd \/d *<system drive>*:\\Program Files\\Microsoft Data Protection Manager\\DPM\\bin**

        2.  Type: **SetDpmServer.exe –dpmServerName *<DPMServerName>***. This configure security accounts, permissions, and firewall exceptions for the agent to communicate with the server.

4.  If you added the computer to the DPM server before you installed the agent, the  server begins to create backups for the protected computer. If you installed the agent before you added the computer to the DPM server, you must attach the computer before the DPM server begins to create backups.

You can also install [DPM on an RODC](https://technet.microsoft.com/en-US/library/hh758186.aspx), [using a server image](https://technet.microsoft.com/en-US/library/hh758186.aspx), or  [with Configuration Manager](https://technet.microsoft.com/en-US/library/hh758186.aspx).

## <a name="BKMK_Attach"></a>Attach the agent
After you’ve installed the DPM agent manually you'll need to attach the agent to the DPM server.

1.  In DPM Administrator Console, on the navigation bar, click **Management** > **Agents**. In the **Actions**pane, click **Install**.

2.  On the **Select Agent Deployment Method**page, select **Attach agents** > **Computer on a trusted domain** > **Next**.  The Protection Agent Installation Wizard opens.

3.  On the Select Computers page, DPM displays a list of available computers in the same domain as the DPM server. Select one or more computers \(50 maximum\), from the **Computer name**list >**Add** > **Next**.

    -   If this is the first time you have used the wizard, DPM queries Active Directory to get a list of potential computers. After the first installation, DPM displays the list of computers in its database, which is updated once each day by the auto\-discovery process.

    -   To add multiple computers by using a text file, click the **Add From File**button, and in the **Add From File**dialog box, type the location of the text file or click Browse to navigate to its location.

4.  On the Enter Credentials page, type the user name and password for a domain account that is a member of the local Administrators group on all selected computers. In the **Domain** box, accept or type the domain name of the user account that you are using to install the protection agent on the target computer. This account may belong to the domain that the DPM server is located in or to a trusted domain. If you are installing a protection agent on a computer across a trusted domain, enter your current domain user credentials. You can be a member of any trusted domain, and you must be a member of the local Administrators group on all selected computers that you want to protect.

5.  On the Summary page, click **Attach**.


