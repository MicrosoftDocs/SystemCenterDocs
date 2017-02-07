---
description: Prerequite and set up instructions for DPM 2016. Includes attended and unattended instructions.
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  Get DPM installed
ms.technology:  data-protection-manager
ms.assetid:  85d424ba-123b-4158-8833-5bc04ea145db
ms.author: markgal
---

# Get DPM installed

>Applies To: System Center 2016 - Data Protection Manager

Here's what you'll need to do to get DPM set up:

1.  Read the [Setup prerequisites](#setup-prerequisites)

2.  [Set up a SQL Server database](#BKMK_SQL) to store DPM settings and configuration information.

3.  Set up DPM. You can [Install DPM](#BKMK_Install) from the user interface, or [Run an unattended install](#BKMK_Unattend). Follow these instructions if you want to [Install DPM on a domain controller](#BKMK_DC)

## Setup prerequisites

|Environment|Details or specifics for the installation|
|-----------|-----------------------------------------|
|Basic DPM installation prerequisites|A number of components are needed on the DPM server. These are installed automatically during setup:<br /><br />-   .NET Framework 4.0 or 4.5 (DPM 2016); .NET Framework 3.5 required for SQL installation (Before SQL 2016); .NET Framework 4.6 required for SQL installation (SQL 2016 onwards) . Install with Add Features in Server Manager if it doesn't install automatically.<br />-   Windows Installer 4.5 (or later). Installed as part of the operating system but can also be installed as an administrator from <root directory>DPM2012\setup\redist\WindowsInstaller\INSTMSI45.EXE.<br />-   Microsoft Visual C++ 2012 Redistributable; Microsoft Visual C++ 2010 Redistributable; Microsoft Visual C++ 2008 Redistributable. <br />-   PowerShell 3.0 (included with Windows Server 2012 R2 or 2012) or PowerShell 2.0 (included with Windows Server 2008 R2)<br />|
|SQL Server prerequisites<br />|You'll need:<br /><br />-   64-bit SQL Server 2016, SQL Server 2014, or SQL Server 2012  <br />-   You can install SQL Server  on the DPM server or on a remote server.  If you install remotely the server remote instance must be in the same domain and time zone as the DPM server. You can't run SQL Server on a domain controller.<br />-   Get the local or remote SQL Server up and running before you install DPM.<br />-   SQL Server can be standalone or running in a cluster.<br />-   You can't use a SQL Server AlwaysOn deployment.<br />-   If you're deploying DPM as an Azure virtual machine you can use an Azure virtual machine running SQL Server as a remote SQL Server instance. You can't use an on-premises SQL Server when in this deploying, and using an Azure SQL Database isn't currently supported.<br />-   If SQL Server is clusterd, Reporting Server and SQL Server should be on different machines.|
|DPM installed as Hyper-V VM|If you're installing DPM as a Hyper-V virtual machine note that:<br /><br /><ul><li>Virtual DPM installation isn't for scaled up environments. Instead, use direct attach/SAN-based storage. Performance can suffer in scaled up (Hyper-V on CSV) environments using VHDX files compared to SAN. Therefore, for scaled up environments we don't recommend using VHDX.</li><li>There's no size limit for VHDX.<br />    Both fixed and dynamically expanding VHDX files are supported.</li><li>Both VHD and VHDX files are supported in the DPM storage pool.<br />     A virtual DPM installation is required to support adding virtual hard drives to the storage pool.</li><li>For dynamic and fixed virtual hard drives, VHD and VHDX files are supported on remote SMB shares.</li><li>From DPM 2012 R2 with Update 3 onwards you can run DPM as a Hyper-V virtual machine with support for tape drives using synthetic FC.</li><li>For high availability DPM storage, virtual hard drives should be placed on scaled-out file servers (SOFS).  SMB 3.0 is required for scaled-out file servers.</li><li>Virtual DPM installations don't support:<br /><br /><ul><li>Windows 2012 Storage Spaces or virtual hard drives built on top of storage spaces.<br />        Local or remote hosting of VHDX files on Windows 2012 storage space also isn't supported.</li><li>Enabling Disk Dedupe on volumes hosting virtual hard drives.</li><li>Windows 2012 iSCSI targets (which use virtual hard drives) as a DPM storage pool.</li><li>NTFS compression for volumes hosting VHD files used in the DPM storage pool.</li><li>Bitlocker on volumes hosting VHD files used for the storage pool.</li><li>A native 4K sector size of physical disks for VHDX files in the DPM storage pool.</li><li>Virtual hard drives hosted on Windows 2008 servers.</li></ul></li></ul>|
|DPM as an Azure virtual machine|<ul><li>DPM is supported on any Azure IaaS virtual machine of size A2 or higher.<br />     You can select a size for the DPM virtual machine using the[DPM Azure virtual machine size calculator](http://go.microsoft.com/fwlink/?LinkId=512026).  When you set up the virtual machine create an instance in the Standard compute tier because the maximum IOPS per attached disk is higher in the Standard tier than in the Basic tier.</li><li>DPM can protect the following workloads running as Azure virtual machines:<br /><br /><ul><li>Windows Server 2016 - Datacenter/Standard<li>Windows Server 2012 R2 - Datacenter/Standard; Windows Server 2012 Datacenter/Standard; Windows Server 2008 R2 SP1 Enterprise/Standard</li><li>SQL Server 2014 and SQL Server 2012 with SP2 (from DPM 2012 R2 with Update rollup 4 onwards); SQL Server 2012 with SP1; SQL Server 2012; SQL Server 2008 R2; SQL Server 2008</li></ul></li><li>DPM can protect workloads that run across multiple Azure cloud services that have the same Azure virtual network and Azure subscription.<br />    DPM running as an Azure virtual machine can't protect on-premises data.</li><li>Use a separate storage account for the DPM virtual machine, because there are size and IOPS limits on a storage account that might impact the performance of the DPM virtual machine if shared with other running virtual machines. The DPM virtual machine and the protected workloads should be part of the same Azure virtual network.</li><li>The number of disks that can be used for the target storage (DPM storage pool) is limited by the size of the virtual machine (maximum of 16).  The Azure Backup agent running on the DPM server needs temporary storage for its own use (a cache location), and for data restored from the cloud (local staging area). Note that each Azure virtual machine comes with some temporary disk storage. This is available to the user as the volume D:\\. The local staging area needed by Azure Backup can be configured to reside in D:\\, and the cache location can be placed on C:\\. In this way, no space needs to be carved out from the data disks attached to the DPM virtual machine.</li><li>You store data on Azure disks attached to the DPM virtual machine. Once attached to the virtual machine, the disks and the storage space are managed from within DPM. The amount of data you can back up depends on the number and size of disks attached to the DPM virtual machine. There is a maximum number of disks that can be attached to each Azure virtual machine (4 disks for A2 size, 8 disks for A3 size, and 16 disks for A4 size), and maximum size of each disk (1 TB). This determines the total backup storage pool available. We recommend you retain data for one day on DPM-attached Azure disk, and store data older than one day in the Azure Backup service. This provides data store for a longer retention range, and allows you to protect a larger amount of data by offloading it to Azure Backup.</li><li>If you want to scale your deployment you have the following options:<br /><br /><ul><li>Option 1, Scale up: Increase the size of the DPM virtual machine from A2 to A3 to A4 and add more local storage.</li><li>Option 2, Offload data: Send older data to Azure Backup, and retain only the newest data on the storage attached to the DPM server.</li><li>Option 3, Scale out: Add more DPM servers to protect the workloads.</li></ul></li><li>The maximum number of protected workloads for each DPM virtual machine size is summarized in Table A below.</li></ul>|

Table A

|VM size|Max protected workloads|Avg workload size|Avg workload churn (daily)|Sample workload|
|-----------|---------------------------|---------------------|--------------------------------|-------------------|
|A2|20|100 GB|Net 5% churn|SQL Server, file server|
|A3|40|150 GB|Net 10% churn|SQL Server, file server|
|A4|60|200 GB|Net 15% churn|SQL Server, file server|

## <a name="BKMK_SQL"></a>Set up a SQL Server database
You'll need to set up a SQL Server database if:

-   You're running DPM 2016 or DPM 2012 R2.

-   You're running an earlier version of DPM but you don't want to use the local SQL Server 2008 R2 installation that's included in DPM setup.

To set up a SQL Server database:

1.  Run SQL Server setup on the local server on which you'll install DPM, or on a remote server.

2.  On the **Installation** tab, click **New SQL Server stand-alone installation** or **add features to an existing installation**.

3.  On the **Product Key** tab enter a valid license key. On the **Setup Support Rules** tab, correct any failures before proceeding.
     On the **Setup Role** tab select **SQL Server Feature Installation**

4.  On the **Feature Selection** tab select **Database Engine Services**. In **Instance Features**, select **Reporting Service - Native**.
     On the  **Installation Rules** tab review the rules.

5.  On the **Instance Configuration** tab specify the name of SQL Server instance you'll use for DPM.  Don't use an underscore or localized characters in the name. In **Disk Space Requirements** review the information.

6.  In **Server Configuration** -> **Service Accounts** specify the domain accounts under which the SQL Server services should run:

    -   We recommend you use a single, dedicated domain user account to run SQL Server services, SQL Server agent, SQL Server Database Engine, and SQL Server Reporting services.

    -   If you're installing DPM on an RODC then use the DPMSQLSvcsAcctaccount you created there.  Note that the user account  must be a member of the local Administrators group on the domain controller where the remote instance is installed. After setup is complete, you can remove the user account from the local Administrators group.  In addition for installation on an RODC you'll need to enter the password you selected when you set up RODC for DPM and crated the  DPMR$MACHINENAME account.

    -   When you create a domain user account give it the lowest possible privileges, assign it a strong password that does not expire, and give it a name that's easily identifiable. You'll add this account to the local Administrators group and to the SQL Server Sysadmin fixed server role later in the wizard.

    -   All services except the SQL Full-text Filter Daemon Launcher should be set to Automatic.

7.  On the **Database Engine Configuration** tab, accept the Windows authentication mode setting. In **Specify SQL Server administrators**, add the user account you'll use to connect to the remote instance when you install DPM. You can add additional accounts if you need to. Complete the rest of the wizard with the default settings and click **Ready to Install** -> **Install**.

8.  If you're installing SQL Server on a remote computer do the following:

    -   Install the DPM support files (SQLPrep). To do this, on the SQL Server computer insert the DPM DVD and start setup.exe. Follow the wizard to install the Microsoft Visual C++ 2012 redistributable. The DPM support files will be installed automatically.

    -   Set up firewall rules so that the DPM server can communicate with the SQL Server computer:

        -   Make sure TCP/IP is enabled with **default failure audit** and **enable password policy checking**.

        -   To allow TCP on port 80, configure an incoming exception for sqlservr.exe for the DPM instance of SQL Server.
            The report server listens for HTTP requests on port 80.

        -   Enable RPC on the remote SQL Server.

        -   The default instance of the database engine listens on TCP port 1443. This setting can be modified. To use the SQL Server Browser service to connect to instances that don't listen on the default 1433 port, you'll need UDP port 1434.

        -   Named instance of SQL Server uses Dynamic ports by default. This setting can be modified.

        -   You can see the current port number used by the database engine in the SQL Server error log. You can view the error logs by using SQL Server Management Studio and connecting to the named instance. You can view the current log under the Management - SQL Server Logs in the entry Server is listening on ['any' <ipv4> port_number].

## <a name="BKMK_Install"></a>Install DPM

1.  If required, extract the DPM 2016 .exe file onto the machine on which you want to run DPM. To do this, run the exe file and on the **Welcome** screen, click **Next**. In  **Select Destination Location** specify where you want to extract the installation files to. In **Ready to Extract** click **Extract.**. After the extraction finishes go to the specified location and run **Setup.exe**.

2.  On the **Welcome** page of DPM Setup click **Next**. On the **License Terms** page accept the agreement > **OK**.

3.  On the **Prerequisites Check** page, wait for the check and resolve any issues before proceeding.

4.  On the **Product Registration** page click **Next**. On the **Microsoft Update Opt-In** page, choose whether you want to include DPM in your Microsoft Updates.

5.  On **Summary of Settings** page check the settings and click **Install**. After install is complete click **Close**. It will automatically launch Windows update to check for changes.

## <a name="BKMK_Unattend"></a>Run an unattended install
Run an unattended install as follows:

1.  Make sure you have the prerequisites installed before you start.

2.  On the remote SQL Server, have to make sure .NET 3.5 is installed on Windows 2016 BEFORE installing SQL.

3.  Use the following code to make sure the firewall is opened:

    ```
    netsh advfirewall firewall add rule name=DPM_SqlServr.exe dir=in action=allow program=\"%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe\" profile=Domain  
    netsh advfirewall firewall add rule name=DPM_UDP_Port_1434 dir=in action=allow protocol=UDP localport=1434 profile=Domain
    ```

4.  Install SQL Server on the local or remote server.

5.  Copy the following text into Notepad (or another text editor) and save the script on the DPM server as DPMSetup.ini. You use the same script whether the SQL Server instance is installed on the DPM server or on a remote server.

  When creating DPMSetup.ini, replace the text inside <> with values from your own environment. Lines beginning with the hash (#) are commented out, and DPM setup uses the default values. To specify your own values, type the values within the <> and delete the hash (#).

    ```
    [OPTIONS]
    UserName = <A user with credentials to install DPM>
    CompanyName = <Name of your company>
    ProductKey = <The 25-character DPM product key in the format xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>
    # SqlAccountPassword = <The password to the DPM$ account>
    # StandardAgentLicenses = <No. of standard agent licenses you have purchased>
    # EnterpriseAgentLicenses = <No. of enterprise agent licenses you have purchased>
    # ProgramFiles = C:\Program Files\Microsoft Data Protection Manager
    # DatabaseFiles = C:\Program Files\Microsoft Data Protection Manager\DPM\DPMDB
    # IntegratedInstallSource = <Location of the DPM setup files>
    # ---For using a remote SQL Server instance ---
    # SQLMachineName = <Name of the SQL Server computer> OR <SQL Cluster Name>
    # SQLInstanceName = <Name of the instance of SQL Server that Setup must use>
    # SQLMachineUserName = <User name that Setup must user>
    # SQLMachinePassword = <Password for the user name Setup must use>
    # SQLMachineDomainName = <Domain to which the SQL Server computer is attached>
    # ---For using a reporting SQL Server instance in case of DPMDB in SQL Cluster ---
    # ReportingMachineName = <Name of the SQL Server computer>
    # ReportingInstanceName = <Name of the instance of SQL Server that Setup must use>
    # ReportingMachineUserName = <User name that Setup must user>
    # ReportingMachinePassword = <Password for the user name Setup must use>
    # ReportingMachineDomainName = <Domain to which the SQL Server computer is attached>
    ```

6.  After saving the file, at an elevated command prompt on the installation server, type: `start /wait [media location]\setup.exe /i /f <path>\DPMSetup.ini /l <path>\dpmlog.txt`. [media location] indicates where you'll run setup.exe from. `<path>` is the location of the .ini file.

## <a name="BKMK_DC"></a>Install DPM on a domain controller
If you want to set up DPM on an RODC you'll need to do a couple of steps before you set up SQL Server and install DPM.

1.  Create the security groups and accounts needed for DPM. To do this click **Start** > **Administrative Tools** > **Active Directory Users and Computers** > **Domain/Builtin** and create these security groups. For each group use the default setting for Scope (Global) and Group type (Security):

    -   DPMDBReaders$<*Computer Name*>; MSDPMTrustedMachines$<*Computer Name*>;
        DPMRADCOMTrustedMachines$<*Computer Name*>;
        DPMRADmTrustedMachines$<*Computer Name*>; DPMDBAdministrators$<*Computer Name*>;
        MSDPMTrustedUsers$<*Computer Name*>;
        DPMSCOM$<*Computer Name*>;
        DPMRATrustedDPMRAs$<*Computer Name*>, where <*Computer Name*> is the name of the domain controller.

2.  Add the local machine account for the domain controller (<*Computer Name*>) to the MSDPMTrustedMachines$<*Computer Name*> group. Then on the primary domain controller create a domain user account with the lowest possible credentials. Assign it a strong password  that doesn't expire and add it to the local administrators group.

    > [!NOTE]
    > Make a note of this account because you need to configure the SQL Server services during the installation of SQL Server. You can name this user account anything that you want; however, for the purposes of easily identifying the account's purpose, you might want to give it a significant name, such as DPMSQLSvcsAcct. For the purposes of these procedures, this account is referred as the DPMSQLSvcsAcct account.

3.  On the primary domain controller, create another domain user account with the lowest possible credentials and name the account DPMR$MACHINENAME, assign it a strong password that does not expire, and then add this account to the DPMDBReaders$<*Computer Name*> group.

4.  Then create the security groups and user accounts needed for the SQL Server database with scope: global and Group type: security. The group or account should be in this format <*grouporaccountname**ComputerName*>.

    -   SQLServerSQL2005BrowserUser$<*Computer Name*>

    -   SQLServerMSSQLServerADHelperUser$<*Computer Name*>

    -   SQLServerReportServerUser$<*Instance ID*><*Instance Name*>

    -   SQLServerMSASUser$<*Computer Name*><*Instance Name*>

    -   SQLServerDTSUser$<*Computer Name*>

    -   SQLServerFDHostUser<*Computer Name*><*Instance Name*>

    -   where <*Computer Name*> is the computer name of the domain controller on which SQL Server 2008 will be installed.
         - <*Instance Name*> is the name of the instance of SQL Server that you plan to create on the domain controller. The instance name can be any name other than the default DPM instance name (MSDPM2010).
         - <*Instance ID*> by default is assigned by SQL Server Setup and indicates that the group applies to Reporting Services (MSRS) for the major version of the instance (10) of SQL Server. For this release, this value is MSRS1A0_50.

5.  On the primary domain controller, add the domain user account that you created earlier (the DPMSQLSvcsAcct account) to the following groups:
    SQLServerReportServerUser$<*ComputerName*>$MSRS10.<*InstanceID*>
    SQLServerMSASUser$<*ComputerName*>$<*InstanceID*>

6.  After you've complete these steps you can install SQL Server:

    -   Log onto the domain controller on which you want to install DPM using the  domain user account that you created earlier. Let's refer to this account as DPMSQLSvcsAcct.

    -   Start to install SQL Server. On the **Server Configuration - Service Accounts** page of Setup you specify the login account for the SQL Server services (SQL Server Agent, SQL Server Database Engine, SQL Server Reporting services) to run under the user account DPMSQLSvcsAcct.

    -   After SQL Server is installed, open **SQL Server Configuration Manager** > **SQL Server Network Configuration** > **Protocols**, right-click **Named Pipes** > **Enable**. You'll need to stop and restart the SQL Server service.

7.  Then you can install DPM:

    -   On the **SQL Server Settings** page  type the name of the instance of SQL Server that you installed in procedure as localhost\\&lt;Instance Name&gt;, and then type the credentials for the first domain user account you created (the DPMSQLSvcsAcct account).  This account must be a member of the local Administrators group on the domain controller where the remote instance is installed. After setup is complete, you can remove the user account from the local Administrators group.

    -   On the **Security Settings** page you'll need to enter the same password that you used when you created the DPMR$MACHINENAME user account earlier.

    -   Open SQL Server Management Studio and connect to the instance of SQL Server that DPM is configured to use. Click New Query, copy the text below to the right pane, and then press F5 to run the query.

        ```
        use DPMDB
        declare @refresh_jobid uniqueidentifier
        select @refresh_jobid = ScheduleId from tbl_SCH_ScheduleDefinition where JobDefinitionId in
        (select JobDefinitionId from tbl_JM_TaskDefinition where TaskDefinitionId in (select distinct TaskDefinitionID from tbl_TE_TaskTrail
        where VerbID = '53603503-C4C8-4D0E-8F1E-D2F3868E51E3')) and IsDeleted=0
        exec msdb.dbo.sp_update_job @job_name =@refresh_jobid, @enabled=0
        update tbl_SCH_ScheduleDefinition
        set IsDeleted=1
        where ScheduleId = @refresh_jobid
        ```
