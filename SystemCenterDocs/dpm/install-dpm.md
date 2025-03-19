---
description: This article contains prerequisites and setup instructions for DPM and it includes attended and unattended instructions
ms.topic: article
ms.date: 03/19/2025
title: Install Data Protection Manager
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.service: system-center
ms.subservice: data-protection-manager
ms.custom: UpdateFrequency.5, intro-installation, engagement-fy23, engagement-fy24
---

# Get DPM installed

Here's what you need to do to set up System Center Data Protection Manager (DPM):

1. Read the [Setup prerequisites](#setup-prerequisites).
2. Verify the [DPM operating system](prepare-environment-for-dpm.md#dpm-server) is compatible.
3. [Set up a SQL Server database](#BKMK_SQL) to store DPM settings and configuration information.
4. Set up DPM. You can [Install DPM](#BKMK_Install) from the user interface or [Run an unattended install](#BKMK_Unattend). Follow these instructions if you want to [Install DPM on a domain controller](#BKMK_DC).

::: moniker range="sc-dpm-2019"

> [!NOTE]
> With DPM 2019 UR4, a fresh installation of the Update Rollup agent might restart the protected server.

::: moniker-end

## Setup prerequisites

::: moniker range="<=sc-dpm-2022"

|Environment |Details or specifics for the installation|
|----------- |-----------------------------------------|
|Basic DPM installation prerequisites|Many components are needed on the DPM server. These are installed automatically during setup:<br /><br />-   .NET Framework 4.0 or 4.5 (DPM 2016/2019); .NET Framework 3.5 required for SQL installation (Before SQL 2016); .NET Framework 4.6 required for SQL installation (SQL 2016 onwards). Install with Add Features in Server Manager if it doesn't install automatically.<br />-   Windows Installer 4.5 (or later). Installed as part of the operating system but can also be installed as an administrator from \<root directory\>DPM\setup\redist\WindowsInstaller\INSTMSI45.EXE.<br />-   Microsoft Visual C++ 2012 Redistributable; Microsoft Visual C++ 2010 Redistributable; Microsoft Visual C++ 2008 Redistributable. <br />-   PowerShell 3.0 (included with Windows Server 2012 R2 or 2012). <br /> - Microsoft Hyper-V Management PowerShell|
|DPM database<br />|- [Verify supported SQL server versions](prepare-environment-for-dpm.md#sql-server-database) for the DPM database. <br /> - You can install the SQL server on the DPM server or a remote server.<br /> - Have SQL installed locally or remotely before you install DPM. <br />- If you plan to use SQL server 2022 with DPM 2022, ensure to install [SQL server Native Client (SQLNCLI)](https://www.microsoft.com/download/details.aspx?id=50402) on the SQL server machine before you install DPM 2022 RTM as SQL 2022 doesn't ship with SQLNCLI.  <br />- If you install the database remotely, the computer running the remote instance must be in the same domain and time zone as the DPM server. <br />- If you're running a remote database, make sure to run the SQL Prep tool on the remote SQL computer before installing DPM. <br />- SQL server can be standalone or running in a cluster.<br />- If the SQL server is clustered, Reporting server and SQL server should be on different computers. <br />- You can't run a SQL server on a domain controller. <br />- You can't use a SQL server Always-On deployment.<br />- If you deploy DPM as an Azure virtual machine (VM), use an Azure VM running SQL server as a remote SQL server instance. You can't use an on-premises SQL server in this deployment, and the Azure SQL database isn't currently supported.|
|DPM installed as Hyper-V VM|If you're installing DPM as a Hyper-V virtual machine note that:<br /><br /><ul><li>Virtual DPM installation isn't for scaled-up environments. Instead, use direct attach/SAN-based storage. Performance can suffer in scaled-up (Hyper-V on CSV) environments using VHDX files compared to SAN. Therefore, for scaled-up environments, we don't recommend using VHDX.</li><li>There's no size limit for VHDX.<br />    Both fixed and dynamically expanding VHDX files are supported.</li><li>Both VHD and VHDX files are supported in the DPM storage pool.<br />     A virtual DPM installation is required to support adding virtual hard drives to the storage pool.</li><li>For dynamic and fixed virtual hard drives, VHD and VHDX files are supported on remote SMB shares.</li><li>From DPM 2012 R2 with Update 3 onwards, you can run DPM as a Hyper-V virtual machine with support for tape drives using synthetic FC.</li><li>For high-availability DPM storage, virtual hard drives should be placed on scaled-out file servers (SOFS).  SMB 3.0 is required for scaled-out file servers.</li><li>Virtual DPM installations don't support:<br /><br /><ul><li>Windows 2012 Storage Spaces or virtual hard drives built on top of storage spaces.<br /> Local or remote hosting of VHDX files on Windows 2012 storage space also isn't supported.</li><li>Enabling Disk Dedupe on volumes hosting virtual hard drives.</li><li>Windows 2012 iSCSI targets (which use virtual hard drives) as a DPM storage pool.</li><li>NTFS compression for volumes hosting VHD files used in the DPM storage pool.</li><li>BitLocker on volumes hosting VHD files used for the storage pool.</li><li>A native 4K sector size of physical disks for VHDX files in the DPM storage pool.</li><li>Virtual hard drives hosted on Windows 2008 servers.</li></ul></li></ul>|
|DPM as an Azure virtual machine|<ul><li>DPM is supported on any Azure IaaS virtual machine of size A2 or higher.<br />     You can select a size for the DPM virtual machine using the [DPM Azure virtual machine size calculator](/samples/browse/?redirectedfrom=TechNet-Gallery).  When you set up the virtual machine create an instance in the Standard compute tier because the maximum IOPS per attached disk are higher in the Standard tier than in the Basic tier.</li><li>DPM can protect the workloads as detailed here in the [protection matrix](~/dpm/dpm-protection-matrix.md).</li><li>DPM can protect workloads that run across multiple Azure cloud services that have the same Azure virtual network and Azure subscription.<br /> DPM running as an Azure virtual machine can't protect on-premises data.</li><li>Use a separate storage account for the DPM virtual machine, because there are size and IOPS limits on a storage account that might impact the performance of the DPM virtual machine if shared with other running virtual machines. The DPM virtual machine and the protected workloads should be part of the same Azure virtual network.</li><li>The number of disks that can be used for the target storage (DPM storage pool) is limited by the size of the virtual machine (maximum of 16).  The Azure Backup agent running on the DPM server needs temporary storage for its use (a cache location), and data restored from the cloud (local staging area). Note that each Azure virtual machine comes with some temporary disk storage. This is available to the user as the volume D:\\. The local staging area needed by Azure Backup can be configured to reside in D:\\, and the cache location can be placed on C:\\. In this way, no space needs to be carved out from the data disks attached to the DPM virtual machine.</li><li>You store data on Azure disks attached to the DPM virtual machine. Once attached to the virtual machine, the disks and the storage space are managed from within DPM. The amount of data you can back up depends on the number and size of disks attached to the DPM virtual machine. There's a maximum number of disks that can be attached to each Azure virtual machine (4 disks for A2V2, A4V2, and A8V2), and the maximum size of each disk (1 TB). This determines the total backup storage pool available. We recommend you retain data for one day on the DPM-attached Azure disk, and store data older than one day in the Azure Backup service. This provides data storage for a longer retention range and allows you to protect a larger amount of data by offloading it to Azure Backup.</li><li>If you want to scale your deployment you have the following options:<br /><br /><ul><li>Option 1, Scale up: Increase the size of the DPM virtual machine from A2V2, A4V2, A8V2, and add more local storage.</li><li>Option 2, Offload data: Send older data to Azure Backup, and retain only the newest data on the storage attached to the DPM server.</li><li>Option 3, Scale-out: Add more DPM servers to protect the workloads.</li></ul></li><li>The maximum number of protected workloads for each DPM virtual machine size is summarized in Table A below.</li></ul>|

::: moniker-end

::: moniker range="sc-dpm-2025"

|Environment |Details or specifics for the installation|
|----------- |-----------------------------------------|
|Basic DPM installation prerequisites|Many components are needed on the DPM server. These are installed automatically during setup:<br /><br />-   .NET Framework 4.0 or 4.5 (DPM 2016/2019); .NET Framework 3.5 required for SQL installation (Before SQL 2016); .NET Framework 4.6 required for SQL installation (SQL 2016 onwards). Install with Add Features in Server Manager if it doesn't install automatically.<br />-   Windows Installer 4.5 (or later). Installed as part of the operating system but can also be installed as an administrator from \<root directory\>DPM\setup\redist\WindowsInstaller\INSTMSI45.EXE.<br />-   Microsoft Visual C++ 2015 Redistributable; Microsoft Visual C++ 2013 Redistributable; Microsoft Visual C++ 2012 Redistributable. <br />-   PowerShell 3.0 (included with Windows Server 2012 R2 or 2012). <br /> - Microsoft Hyper-V Management PowerShell|
|DPM database<br />|- [Verify supported SQL server versions](prepare-environment-for-dpm.md#sql-server-database) for the DPM database. <br /> - You can install the SQL server on the DPM server or a remote server.<br /> - Have SQL installed locally or remotely before you install DPM. <br />- If you plan to use SQL server 2022 with DPM 2025, ensure to install [SQL OLEDB 19](/sql/connect/oledb/download-oledb-driver-for-sql-server?view=sql-server-ver16#download). <br />- If you install the database remotely, the computer running the remote instance must be in the same domain and time zone as the DPM server. <br />- If you're running a remote database, make sure to run the SQL Prep tool on the remote SQL computer before installing DPM. <br />- SQL server can be standalone or running in a cluster.<br />- If the SQL server is clustered, Reporting server and SQL server should be on different computers. <br />- You can't run a SQL server on a domain controller. <br />- You can't use a SQL server Always-On deployment.<br />- If you deploy DPM as an Azure virtual machine (VM), use an Azure VM running SQL server as a remote SQL server instance. You can't use an on-premises SQL server in this deployment, and the Azure SQL database isn't currently supported.|
|DPM installed as Hyper-V VM|If you're installing DPM as a Hyper-V virtual machine note that:<br /><br /><ul><li>Virtual DPM installation isn't for scaled-up environments. Instead, use direct attach/SAN-based storage. Performance can suffer in scaled-up (Hyper-V on CSV) environments using VHDX files compared to SAN. Therefore, for scaled-up environments, we don't recommend using VHDX.</li><li>There's no size limit for VHDX.<br />    Both fixed and dynamically expanding VHDX files are supported.</li><li>Both VHD and VHDX files are supported in the DPM storage pool.<br />     A virtual DPM installation is required to support adding virtual hard drives to the storage pool.</li><li>For dynamic and fixed virtual hard drives, VHD and VHDX files are supported on remote SMB shares.</li><li>DPM can run as a Hyper-V virtual machine with support for tape drives using synthetic FC.</li><li>For high-availability DPM storage, virtual hard drives should be placed on scaled-out file servers (SOFS).  SMB 3.0 is required for scaled-out file servers.</li><li>Virtual DPM installations don't support:<br /><br /><ul><li>Windows 2012 Storage Spaces or virtual hard drives built on top of storage spaces.<br /> Local or remote hosting of VHDX files on Windows 2012 storage space also isn't supported.</li><li>Enabling Disk Dedupe on volumes hosting virtual hard drives.</li><li>Windows 2012 iSCSI targets (which use virtual hard drives) as a DPM storage pool.</li><li>NTFS compression for volumes hosting VHD files used in the DPM storage pool.</li><li>BitLocker on volumes hosting VHD files used for the storage pool.</li><li>A native 4K sector size of physical disks for VHDX files in the DPM storage pool.</li><li>Virtual hard drives hosted on Windows 2008 servers.</li></ul></li></ul>|
|DPM as an Azure virtual machine|<ul><li>DPM is supported on any Azure IaaS virtual machine of size A2 or higher.<br />     You can select a size for the DPM virtual machine using the [DPM Azure virtual machine size calculator](/samples/browse/?redirectedfrom=TechNet-Gallery).  When you set up the virtual machine create an instance in the Standard compute tier because the maximum IOPS per attached disk are higher in the Standard tier than in the Basic tier.</li><li>DPM can protect the workloads as detailed here in the [protection matrix](~/dpm/dpm-protection-matrix.md).</li><li>DPM can protect workloads that run across multiple Azure cloud services that have the same Azure virtual network and Azure subscription.<br /> DPM running as an Azure virtual machine can't protect on-premises data.</li><li>Use a separate storage account for the DPM virtual machine, because there are size and IOPS limits on a storage account that might impact the performance of the DPM virtual machine if shared with other running virtual machines. The DPM virtual machine and the protected workloads should be part of the same Azure virtual network.</li><li>The number of disks that can be used for the target storage (DPM storage pool) is limited by the size of the virtual machine (maximum of 16).  The Azure Backup agent running on the DPM server needs temporary storage for its use (a cache location), and data restored from the cloud (local staging area). Note that each Azure virtual machine comes with some temporary disk storage. This is available to the user as the volume D:\\. The local staging area needed by Azure Backup can be configured to reside in D:\\, and the cache location can be placed on C:\\. In this way, no space needs to be carved out from the data disks attached to the DPM virtual machine.</li><li>You store data on Azure disks attached to the DPM virtual machine. Once attached to the virtual machine, the disks and the storage space are managed from within DPM. The amount of data you can back up depends on the number and size of disks attached to the DPM virtual machine. We recommend you retain data for one day on the DPM-attached Azure disk, and store data older than one day in the Azure Backup service. This provides data storage for a longer retention range and allows you to protect a larger amount of data by offloading it to Azure Backup.</li><li>If you want to scale your deployment you have the following options:<br /><br /><ul><li>Option 1, Scale up: Increase the size of the DPM virtual machine from A2V2, A4V2, A8V2, and add more local storage.</li><li>Option 2, Offload data: Send older data to Azure Backup, and retain only the newest data on the storage attached to the DPM server.</li><li>Option 3, Scale-out: Add more DPM servers to protect the workloads.</li></ul></li><li>The maximum number of protected workloads for each DPM virtual machine size is summarized in Table A below.</li></ul>|

::: moniker-end

Table A

|VM size|Max protected workloads|Avg workload size|Avg workload churn (daily)|
|-----------|---------------------------|---------------------|--------------------------------|-------------------|
|A2V2|20|100 GB|Net 5% churn|
|A4V2|40|150 GB|Net 10% churn|
|A8V2|60|200 GB|Net 15% churn|

:::moniker range=">=sc-dpm-2022"
>[!NOTE]
>As a Windows virtual machine in VMware - You can install DPM 2022 on a Windows virtual machine in a VMware environment. In this configuration, DPM can protect Microsoft workloads running as Windows virtual machines in VMware.
:::moniker-end

:::moniker range="<=sc-dpm-2019"
>[!NOTE]
>As a Windows virtual machine in VMware - You can install DPM 2019 on a Windows virtual machine in a VMware environment. In this configuration, DPM can protect Microsoft workloads running as Windows virtual machines in VMware.
:::moniker-end

## <a name="BKMK_SQL"></a>Set up a SQL Server database

You'll need to set up a SQL Server database if:

::: moniker range="<=sc-dpm-2019"

- You're running DPM 2019, 2016

::: moniker-end

::: moniker range="sc-dpm-2022"

- You're running DPM 2022, 2019, 2016

::: moniker-end

::: moniker range="sc-dpm-2025"

- You're running DPM 2025, 2022, 2019

::: moniker-end

To set up a SQL Server database:

1. Run SQL Server setup on the local server on which you'll install DPM or on a remote server.

1. On the **Installation**, select **New SQL Server stand-alone installation** or **add features to an existing installation**.

1. On the **Product Key**, enter a valid license key. On the **Setup Support Rules**, correct any failures before proceeding.
     On the **Setup Role**, select **SQL Server Feature Installation**.

1. On the **Feature Selection**, select **Database Engine Services**. In **Instance Features**, select **Reporting Service - Native**.
     On the **Installation Rules**, review the rules.

1. On the **Instance Configuration**, specify the name of the SQL Server Instance you'll use for DPM.  Don't use underscore or localized characters in the name. In **Disk Space Requirements**, review the information.

1. In **Server Configuration** > **Service Accounts**, specify the domain accounts under which the SQL Server Services should run:

    - We recommend you use a single, dedicated domain user account to run SQL Server Services, SQL Server Agent, SQL Server Database Engine, and SQL Server Reporting Services.

    - If you're installing DPM on an RODC, then use the *DPMSQLSvcsAcctaccount* you created there. Note that the user account must be a member of the local Administrators group on the domain controller where the remote instance is installed. After the setup is complete, you can remove the user account from the local Administrators group.  In addition, for installation on an RODC, you'll need to enter the password you selected when you set up RODC for DPM and create the *DPMR$MACHINENAME* account.

    - When you create a domain user account, give it the lowest possible privileges, assign it a strong password that doesn't expire, and give it an easily identifiable name. You'll add this account to the local Administrators group and the SQL Server Sysadmin fixed server role later in the wizard.

    - All services except the SQL Full-text Filter Daemon Launcher should be set to Automatic.

::: moniker range="sc-dpm-2022"

7. On the **Database Engine Configuration**, accept the Windows authentication mode setting. DPM admins need *SQL Server administrator* permissions. In **Specify SQL Server administrators**, add DPM Admins. You can add additional accounts if you need to. Complete the rest of the wizard with the default settings and select **Ready to Install** > **Install**.
    
    If you use SQL Server 2022, you need to install [SQL Server Native Client (SQLNCLI)](https://www.microsoft.com/download/details.aspx?id=50402) on the SQL Server 2022 machine.

    SQLNCLI is a pre-requisite for DPM 2022 RTM installation but isn't available in SQL Server 2022. Hence, after SQL Server 2022 installation you would also need to install SQL Server Native Client separately on the SQL Server machine.  After that, ensure that you install DPM 2022 RTM and update to UR1 or later, which supports SQL Server 2022 as the DPM Database and uses OLEDB 18.0 instead of SQLNCLI.

8. If you're installing SQL Server on a remote computer, do the following:

    - If you use a MSCS clustered SQL server for DPM database, the Cluster Group Resource name for the SQL Server role must be named SQL Server (**InstanceName**). For example., SQL Server (MSSQLSERVER).
    - If you use a MSCS clustered SQL server for DPM database, SQL Server Reporting Service (SSRS) must be installed on a separate standalone SQL server computer or installed on the DPM server itself.
    - Install the DPM support files (SQLPrep). To do this, on the SQL Server computer, insert the DPM DVD and start setup.exe. Follow the wizard to install the Microsoft Visual C++ 2012 Redistributable. The DPM support files will be installed automatically.

    - Set up firewall rules so that the DPM server can communicate with the SQL Server computer:

        - Ensure TCP/IP is enabled with **default failure audit** and **enable password policy checking**.

        - To allow TCP on port 80, configure an incoming exception for sqlservr.exe for the DPM instance of SQL Server.
            The report server listens for HTTP requests on port 80.

        - Enable RPC on the remote SQL Server.

        - The default instance of the database engine listens on TCP port 1443. This setting can be modified. To use the SQL Server Browser service to connect to instances that don't listen on the default 1433 port, you'll need UDP port 1434.

        - Named instance of SQL Server uses Dynamic ports by default. This setting can be modified.

        - You can see the current port number used by the database engine in the SQL Server error log. You can view the error logs by using SQL Server Management Studio and connecting to the named instance. You can view the current log under the Management - SQL Server Logs in the entry Server is listening on ['any' \<ipv4\> port_number].

::: moniker-end

::: moniker range="sc-dpm-2025"

7. On the **Database Engine Configuration**, accept the Windows authentication mode setting. DPM admins need *SQL Server administrator* permissions. In **Specify SQL Server administrators**, add DPM Admins. You can add additional accounts if you need to. Complete the rest of the wizard with the default settings and select **Ready to Install** > **Install**.
    
    After the SQL installation is completed, ensure to install [SQL OLEDB 19](/sql/connect/oledb/download-oledb-driver-for-sql-server?view=sql-server-ver16#download).


8. If you're installing SQL Server on a remote computer, do the following:

    - If you use a MSCS clustered SQL server for DPM database, the Cluster Group Resource name for the SQL Server role must be named SQL Server (**InstanceName**). For example., SQL Server (MSSQLSERVER).
    - If you use a MSCS clustered SQL server for DPM database, SQL Server Reporting Service (SSRS) must be installed on a separate standalone SQL server computer or installed on the DPM server itself.
    - Install the DPM support files (SQLPrep). To do this, on the SQL Server computer, insert the DPM DVD and start setup.exe. Follow the wizard to install the Microsoft Visual C++ 2012 Redistributable. The DPM support files will be installed automatically.

    - Set up firewall rules so that the DPM server can communicate with the SQL Server computer:

        - Ensure TCP/IP is enabled with **default failure audit** and **enable password policy checking**.

        - To allow TCP on port 80, configure an incoming exception for sqlservr.exe for the DPM instance of SQL Server.
            The report server listens for HTTP requests on port 80.

        - Enable RPC on the remote SQL Server.

        - The default instance of the database engine listens on TCP port 1443. This setting can be modified. To use the SQL Server Browser service to connect to instances that don't listen on the default 1433 port, you'll need UDP port 1434.

        - Named instance of SQL Server uses Dynamic ports by default. This setting can be modified.

        - You can see the current port number used by the database engine in the SQL Server error log. You can view the error logs by using SQL Server Management Studio and connecting to the named instance. You can view the current log under the Management - SQL Server Logs in the entry Server is listening on ['any' \<ipv4\> port_number].

::: moniker-end

::: moniker range="= sc-dpm-2019"

7. On the **Database Engine Configuration**, accept the Windows authentication mode setting. DPM admins need *SQL Server administrator* permissions. In **Specify SQL Server administrators**, add DPM Admins. You can add additional accounts if you need to. Complete the rest of the wizard with the default settings and select **Ready to Install** > **Install**.

8. If you're installing SQL Server on a remote computer, do the following:

    - If you use a MSCS clustered SQL server for DPM database, the Cluster Group Resource name for the SQL Server role must be named SQL Server (**InstanceName**). For example., SQL Server (MSSQLSERVER).
    - If you use a MSCS clustered SQL server for DPM database, SQL Server Reporting Service (SSRS) must be installed on a separate standalone SQL server computer or installed on the DPM server itself.
    - Install the DPM support files (SQLPrep). To do this, on the SQL Server computer, insert the DPM DVD and start setup.exe. Follow the wizard to install the Microsoft Visual C++ 2012 Redistributable. The DPM support files will be installed automatically.

    - Set up firewall rules so that the DPM server can communicate with the SQL Server computer:

        - Ensure TCP/IP is enabled with **default failure audit** and **enable password policy checking**.

        - To allow TCP on port 80, configure an incoming exception for sqlservr.exe for the DPM instance of SQL Server.
            The report server listens for HTTP requests on port 80.

        - Enable RPC on the remote SQL Server.

        - The default instance of the database engine listens on TCP port 1443. This setting can be modified. To use the SQL Server Browser service to connect to instances that don't listen on the default 1433 port, you'll need UDP port 1434.

        - Named instance of SQL Server uses Dynamic ports by default. This setting can be modified.

        - You can see the current port number used by the database engine in the SQL Server error log. You can view the error logs by using SQL Server Management Studio and connecting to the named instance. You can view the current log under the Management - SQL Server Logs in the entry Server is listening on ['any' \<ipv4\> port_number].

::: moniker-end

::: moniker range="= sc-dpm-2016"

7. On the **Database Engine Configuration**, accept the Windows authentication mode setting. DPM admins need *SQL Server administrator* permissions. In **Specify SQL Server administrators**, add DPM Admins. You can add additional accounts if you need to. Complete the rest of the wizard with the default settings and select **Ready to Install** > **Install**.

8. If you're installing SQL Server on a remote computer, do the following:

    - Install the DPM support files (SQLPrep). To do this, on the SQL Server computer, insert the DPM DVD and start setup.exe. Follow the wizard to install the Microsoft Visual C++ 2012 Redistributable. The DPM support files will be installed automatically.

    - Set up firewall rules so that the DPM server can communicate with the SQL Server computer:

        - Ensure TCP/IP is enabled with **default failure audit** and **enable password policy checking**.

        - To allow TCP on port 80, configure an incoming exception for sqlservr.exe for the DPM instance of SQL Server.
            The report server listens for HTTP requests on port 80.

        - Enable RPC on the remote SQL Server.

        - The default instance of the database engine listens on TCP port 1443. This setting can be modified. To use the SQL Server Browser service to connect to instances that don't listen on the default 1433 port, you'll need UDP port 1434.

        - Named instance of SQL Server uses Dynamic ports by default. This setting can be modified.

        - You can see the current port number used by the database engine in the SQL Server error log. You can view the error logs by using SQL Server Management Studio and connecting to the named instance. You can view the current log under the Management - SQL Server Logs in the entry Server is listening on ['any' \<ipv4\> port_number].

::: moniker-end


::: moniker range="<=sc-dpm-2019"

> [!NOTE]
>- With SQL 2017 and later, SSRS doesn't get installed as a part of SQL installation. You need to install SQL SSRS separately. For more information, see [Install SQL Server Reporting Services (2017 and later)](/sql/reporting-services/install-windows/install-reporting-services?preserve-view=true&view=sql-server-2017).
>- For remote clustered SQL Instance, Database Engine must be on the cluster and SSRS must be on a separate computer (which can be the DPM server or any other computer).
>- In both local or remote SQL Server scenarios, the following components must be installed on the DPM server.<br>
     - [SQL Server Management Studio (SSMS)](/sql/ssms/download-sql-server-management-studio-ssms) is no longer installed with SQL Server; you must install an equivalent version of SSMS separately.<br>
     - For SQL Server 2019, along with SSMS you should also install [SQLCMD](/sql/tools/sqlcmd-utility), [Visual C++ 2017 Redistributable](/cpp/windows/latest-supported-vc-redist?preserve-view=true&view=msvc-170), and [Microsoft ODBC Driver 17 for SQL Server](/sql/connect/odbc/download-odbc-driver-for-sql-server#version-17) on the DPM server separately.

::: moniker-end

::: moniker range=">=sc-dpm-2022"

> [!NOTE]
>- With SQL 2017 and later, SSRS doesn't get installed as a part of SQL installation. You need to install SQL SSRS separately. For more information, see [Install SQL Server Reporting Services (2017 and later)](/sql/reporting-services/install-windows/install-reporting-services?preserve-view=true&view=sql-server-2017).
>- For remote clustered SQL Instance, Database Engine must be on the cluster and SSRS must be on a separate computer (which can be the DPM server or any other computer).
>- In both local or remote SQL Server scenarios, the following components must be installed on the DPM server.<br>
         - [SQL Server Management Studio (SSMS)](/sql/ssms/download-sql-server-management-studio-ssms) is no longer installed with SQL Server; you must install an equivalent version of SSMS separately.<br>
         - For SQL Server 2019, along with SSMS you should also install [SQLCMD](/sql/tools/sqlcmd-utility), [Visual C++ 2017 Redistributable](/cpp/windows/latest-supported-vc-redist?preserve-view=true&view=msvc-170), and [Microsoft ODBC Driver 17 for SQL Server](/sql/connect/odbc/download-odbc-driver-for-sql-server#version-17) on the DPM server separately.<br>
         - When you use Remote SQL Server 2022, you must install SQLCMD version 16 on the DPM server. If SQLCMD version 16 isn't available to download, install SQLCMD version 15, rename the folder, and then copy the folder of `SQLCMD` version 16 (`C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\170\Tools\Binn`) from SQL server 2022 to DPM 2022 server before DPM 2022 installation. After the installation, delete version 16 and rename version 15 as needed.

::: moniker-end

::: moniker range=">=sc-dpm-2019"

[!INCLUDE [validation-dpm.md](../includes/validation-dpm.md)]

::: moniker-end

## <a name="BKMK_Install"></a>Install DPM

>[!IMPORTANT]
> When installing DPM, use NetBIOS names for the domain name and SQL machine name. Do not use fully qualified domain names (FQDNs).

::: moniker range="<=sc-dpm-2022"
1. If required, extract the DPM 2016.exe (for DPM 2016)/DPM 2019.exe (for DPM 2019) file onto the machine on which you want to run DPM. To do this, run the exe file, and on the **Welcome** screen, select **Next**. In **Select Destination Location**, specify where you want to extract the installation files to. In **Ready to Extract**, select **Extract**. After the extraction finishes, go to the specified location and run **Setup.exe**.
::: moniker-end

::: moniker range="sc-dpm-2025"
1. Extract the SCDPM_2025.exe file onto the machine on which you want to run DPM. To do this, run the exe file, and on the **Welcome** screen, select **Next**. In **Select Destination Location**, specify where you want to extract the installation files to. In **Ready to Extract**, select **Extract**. After the extraction finishes, go to the specified location and run **Setup.exe**.
::: moniker-end

2. On the **Welcome** page of DPM Setup, select **Next**. On the **License Terms** page, accept the agreement > **OK**.

3. On the **Prerequisites Check** page, wait for the check and resolve any issues before proceeding.

4. On the **Product Registration** page, select **Next**. On the **Microsoft Update Opt-In** page, choose whether you want to include DPM in your Microsoft Updates.

5. On the **Summary of Settings** page, check the settings and select **Install**. After the installation is completed, select **Close**. It will automatically launch a Windows update to check for changes.

## <a name="BKMK_Unattend"></a>Run an unattended install

Run an unattended install as follows:

1. Ensure that you have the prerequisites installed before you start.

::: moniker range="<=sc-dpm-2022"
2. On the remote SQL Server, ensure that .NET Framework 3.5 (for SQL 2016), 4.0, or 4.5 (SQL 2017) is installed on the Windows server before installing SQL.

3. Use the following code to ensure that the firewall is opened:

   ```
   netsh advfirewall firewall add rule name=DPM_SqlServr.exe dir=in action=allow program=\"%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe\" profile=Domain  
   netsh advfirewall firewall add rule name=DPM_UDP_Port_1434 dir=in action=allow protocol=UDP localport=1434 profile=Domain
   ```

4. Install SQL Server on the local or remote server.

5. Copy the following text into Notepad (or another text editor) and save the script on the DPM server as DPMSetup.ini. You use the same script whether the SQL Server Instance is installed on the DPM server or a remote server.

   >[!IMPORTANT]
   > When installing DPM, use NetBIOS names for the domain name and SQL machine name. Do not use fully qualified domain names (FQDNs).

   When creating DPMSetup.ini, replace the text inside <> with values from your environment. Lines beginning with the hash (#) are commented out, and the DPM setup uses the default values. To specify your values, type the values within the <> and delete the hash (#).

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
   # ---For using a remote SQL Server Instance ---
   # SQLMachineName = <Name of the SQL Server computer> OR <SQL Cluster Name>
   # SQLInstanceName = <Name of the instance of SQL Server that Setup must use>
   # SQLMachineUserName = <Username that Setup must user>
   # SQLMachinePassword = <Password for the username Setup must use>
   # SQLMachineDomainName = <Domain to which the SQL Server computer is attached>
   # ---For using a reporting SQL Server Instance in case of DPMDB in SQL Cluster ---
   # ReportingMachineName = <Name of the SQL Server computer>
   # ReportingInstanceName = <Name of the instance of SQL Server that Setup must use, SSRS in case of SQL 2017>
   # ReportingMachineUserName = <Username that Setup must user>
   # ReportingMachinePassword = <Password for the username Setup must use>
   # ReportingMachineDomainName = <Domain to which the SQL Server computer is attached>
   ```

6. After saving the file, at an elevated command prompt on the installation server, type: `start /wait [media location]\setup.exe /i /f <path>\DPMSetup.ini /l <path>\dpmlog.txt`.
   - `[media location]` indicates where you'll run setup.exe from.
   - `<path>` is the location of the .ini file.

::: moniker-end

::: moniker range="sc-dpm-2025"

2. Use the following code to ensure that the firewall is opened:

   ```
   netsh advfirewall firewall add rule name=DPM_SqlServr.exe dir=in action=allow program=\"%PROGRAMFILES%\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe\" profile=Domain   

   netsh advfirewall firewall add rule name=DPM_UDP_Port_1434 dir=in action=allow protocol=UDP localport=1434 profile=Domain 
   ```

3. Install SQL Server on the local or remote server.

4. Copy the following text into Notepad (or another text editor) and save the script on the DPM server as DPMSetup.ini. You use the same script whether the SQL Server Instance is installed on the DPM server or a remote server.

   >[!IMPORTANT]
   > When installing DPM, use NetBIOS names for the domain name and SQL machine name. Do not use fully qualified domain names (FQDNs).

   When creating DPMSetup.ini, replace the text inside <> with values from your environment. Lines beginning with the hash (#) are commented out, and the DPM setup uses the default values. To specify your values, type the values within the <> and delete the hash (#).

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
   # ---For using a remote SQL Server Instance --- 
   # SQLMachineName = <Name of the SQL Server computer> OR <SQL Cluster Name> 
   # SQLInstanceName = <Name of the instance of SQL Server that Setup must use> 
   # SQLMachineUserName = <Username that Setup must user> 
   # SQLMachinePassword = <Password for the username Setup must use> 
   # SQLMachineDomainName = <Domain to which the SQL Server computer is attached> 
   # ---For using a reporting SQL Server Instance in case of DPMDB in SQL Cluster --- 
   # ReportingMachineName = <Name of the SQL Server computer> 
   # ReportingInstanceName = SSRS 
   # ReportingMachineUserName = <Username that Setup must user> 
   # ReportingMachinePassword = <Password for the username Setup must use> 
   # ReportingMachineDomainName = <Domain to which the SQL Server computer is attached> 
   ```

5. After saving the file, at an elevated command prompt on the installation server, type: `start /wait [media location]\setup.exe /i /f <path>\DPMSetup.ini /l <path>\dpmlog.txt`.
   - `[media location]` indicates where you'll run setup.exe from.
   - `<path>` is the location of the .ini file.

::: moniker-end

## <a name="BKMK_DC"></a>Install DPM on a domain controller

If you want to set up DPM on an RODC, you'll need to do a couple of steps before you set up the SQL Server and install DPM.

1. Create the security groups and accounts needed for DPM. To do this, select **Start** > **Administrative Tools** > **Active Directory Users and Computers** > **Domain/Builtin** and create these security groups. For each group, use the default setting for Scope (Global) and Group type (Security):

    - DPMDBReaders$<*Computer Name*>;
    - MSDPMTrustedMachines$<*Computer Name*>;
    - DPMRADCOMTrustedMachines$<*Computer Name*>;
    - DPMRADmTrustedMachines$<*Computer Name*>;
    - DPMDBAdministrators$<*Computer Name*>;
    - MSDPMTrustedUsers$<*Computer Name*>;
    - DPMSCOM$<*Computer Name*>;
    - DPMRATrustedDPMRAs$<*Computer Name*>, where <*Computer Name*> is the name of the domain controller.

2. Add the local machine account for the domain controller (<*Computer Name*>) to the `MSDPMTrustedMachines$<*Computer Name*>` group. Then on the primary domain controller, create a domain user account with the lowest possible credentials. Assign it a strong password that doesn't expire and add it to the local administrators' group.

    > [!NOTE]
    > Make a note of this account because you need to configure the SQL Server Services during the installation of the SQL Server. You can name this user account anything you want. However, to easily identify the account's purpose, you might want to give it a significant name, such as *DPMSQLSvcsAcct*. For these procedures, this account is referred to as the *DPMSQLSvcsAcct* account.

3. On the primary domain controller, create another domain user account with the lowest possible credentials and name the account *DPMR$MACHINENAME*, assign it a strong password that doesn't expire, and then add this account to the `DPMDBReaders$<*Computer Name*>` group.

4. Then create the security groups and user accounts needed for the SQL Server database with scope: global and Group type: security. The group or account should be in this format <*grouporaccountnameComputerName*>.

    - SQLServerSQL2005BrowserUser$<*Computer Name*>

    - SQLServerMSSQLServerADHelperUser$<*Computer Name*>

    - SQLServerReportServerUser$<*Instance ID*><*Instance Name*>

    - SQLServerMSASUser$<*Computer Name*><*Instance Name*>

    - SQLServerDTSUser$<*Computer Name*>

    - SQLServerFDHostUser<*Computer Name*><*Instance Name*>

    - where <*Computer Name*> is the computer name of the domain controller on which SQL Server 2008 will be installed.
         - <*Instance Name*> is the name of the instance of SQL Server that you plan to create on the domain controller. The instance name can be any name other than the default DPM instance name (MSDPM2010).
         - <*Instance ID*> by default is assigned by SQL Server Setup and indicates that the group applies to Reporting Services (MSRS) for the major version of the instance (10) of SQL Server. For this release, this value is MSRS1A0_50.

5. On the primary domain controller, add the domain user account that you created earlier (the DPMSQLSvcsAcct account) to the following groups:
    SQLServerReportServerUser$<*ComputerName*>$MSRS10.<*InstanceID*>
    SQLServerMSASUser$<*ComputerName*>$<*InstanceID*>

6. After you've completed these steps, you can install the SQL Server:

    - Sign-in to the domain controller on which you want to install DPM using the domain user account that you created earlier. Let's refer to this account as DPMSQLSvcsAcct.

    - Start installing the SQL Server. On the **Server Configuration - Service Accounts** page of Setup, specify the sign-in account for the SQL Server Services (SQL Server Agent, SQL Server Database Engine, SQL Server Reporting Services) to run under the user account DPMSQLSvcsAcct.

    - After the SQL Server is installed, open **SQL Server Configuration Manager** > **SQL Server Network Configuration** > **Protocols**, right-click **Named Pipes** > **Enable**. You'll need to stop and restart the SQL Server Services.

7. Then you can install DPM:

    - On the **SQL Server Settings** page, type the name of the instance of SQL Server that you installed in the procedure as localhost\\&lt;Instance Name&gt;, and then type the credentials for the first domain user account you created (the DPMSQLSvcsAcct account).  This account must be a member of the local Administrators group on the domain controller where the remote instance is installed. After the setup is complete, you can remove the user account from the local Administrators group.

    - On the **Security Settings** page, you'll need to enter the same password that you used when you created the DPMR$MACHINENAME user account earlier.

    - Open SQL Server Management Studio and connect to the instance of SQL Server that DPM is configured to use. Select **New Query**, copy the text below to the right pane, and then press F5 to run the query.

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

::: moniker range="<=sc-dpm-2022"

## Upgrade SQL 2016 to SQL 2017

You can upgrade SQL Server 2016, or SQL Server 2016 SP1 Enterprise or Standard, to SQL 2017. The following procedure lists the steps to upgrade SQL 2016 to SQL 2017.

>[!NOTE]
> With DPM 2019, SQL 2017 is supported as a DPM database in both new installation and upgrade scenarios of DPM.

1. On the SQL Server, back up the Reporting database.
2. Back up the Encryption Keys.
3. Clean up the reporting folders on the local machine.
4. Install the Reporting Service.
5. On the DPM server, change the following DPM registry key to the new reporting instance name.

   - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\DB\<*ReportingInstanceName*>

6. Change the Reporting Service virtual directory name to ReportServer_SSRS.
7. Configure the Reporting Service, and restore the database and encryption keys.

::: moniker-end

::: moniker range="sc-dpm-2025"

## Upgrade to SQL 2022

The following procedure lists the steps to upgrade SQL 2022.

>[!NOTE]
> With DPM 2025 only SQL 2022 is supported as a DPM database in both new installation and upgrade scenarios of DPM.

Before upgrading from a version older than SQL 2017 to SQL 2022, ensure to

1. Back up the Reporting database on the SQL Server.
2. Back up the Encryption Keys.
3. Clean up the reporting folders on the local machine.
4. Install the Reporting Service.
5. On the DPM server, change the following DPM registry key to the new reporting instance name.

   - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\DB\<*ReportingInstanceName*>

6. Change the Reporting Service virtual directory name to ReportServer_SSRS.
7. Configure the Reporting Service, and restore the database and encryption keys.

::: moniker-end

## Next steps

- See [release notes](dpm-release-notes.md) for new hotfixes and URs that are applicable.
