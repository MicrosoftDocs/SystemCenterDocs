---
ms.assetid: 7cb61f4f-d184-407e-abc1-f2334de51810
title:  Management Pack Assessment
description: This article describes how to use the updates and recommendations feature in Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 02/22/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Management pack assessment

>Applies To: System Center 2016 - Operations Manager

Operations Manager includes a new feature called Updates and Recommendations, to help you proactively identify new technologies or components (i.e. workloads) deployed in your IT infrastructure that were not monitored by Operations Manager or are not monitored using the latest version of a management pack.

>[!NOTE]
>This feature only works with management packs released by Microsoft, it currently does not support third party management packs.  See [Supported workloads](#supported-workloads) below for the current list of workflows supported by this feature.  

If there are Management Packs in the catalog that are designed to monitor those workloads, they will be displayed on the Updates and Recommendations screen. You will also find a list of any updates that are available for Management Packs that are installed in your management group.

When a new workload is deployed in your IT infrastructure that was never monitored by Operations Manager, it will be detected and highlighted under the Updates and Recommendations node.  The management packs required to monitor that workload will be presented with a status of **Not Installed**.  If the necessary management pack files for a particular workload are not installed, for example the library management pack file is installed but not the corresponding discovery and monitoring management pack files, the Updates and Recommendations feature will list that workload with a status of **Partially Installed**.  

This feature includes the following capabilities:

|  Option |  Description | 
|----------|-------------|
|  **Get MP**  | Installs the management packs for the selected workload
|  **Get All MPs**  |  Installs the management packs for all of the workloads displayed
|  **View Guide**  |  Downloads the management pack guide from the web browser, for the selected workload, to your computer
|  **View DLC Page**  | Open from the web browser, the page on the Microsoft Download Center, to download the management pack file
|  **More information**  | Highlights all impacted agent-managed systems and management pack details of selected workload (depending on the status of the workload)

>[!NOTE]
>In order to use the options highlighted in the table above, the computer you are running the Operations console from requires an Internet connection.

>[!NOTE]
>Configuring the frequency and control the discovery of workloads cannot be performed directly from the Operations console.  If you wish to modify those settings of this feature, you can download a PowerShell script from the [Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Script-to-modify-settings-246c84af#content).

## Importing a Management Pack using Get MP
The following procedure describes how to use the Get MP option to download a management pack for a selected workload.  

1. Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2. In the Operations console, click **Administration**.

3. Click on **Updates and Recommendations**  under **Management Packs**.

    >[!NOTE]
    >When accessing the Updates and Recommendations view, you may receive the following message, "An error occurred while displaying the Updates and Recommendations View. This might be because the database query has encountered an issue or the online catalog is down."  This can be caused by having a duplicate management pack with the same name.  To help troubleshoot the issue, run the following command in the Operations Manager  Shell and review the output file to identify the duplicate MP:
    >`Get-SCManagementPack | Sort -property Name | Format-Table Name,Version,Sealed -AutoSize | Out-File "c:\temp\mplist_name.txt"`
    > 

4. If a management pack is recommended for either an update or a new installation, select it and click **Get MP** from the **Actions** pane.

5. The **Connecting to Management Pack Catalog Web Service** window appears and after it successfully connects and synchronizes, the **Import Management Packs** wizard opens.

6. On the **Select Management Packs** page, in the list of management packs will be the management packs identified in the **Import Type** column with the value of **Not installed** if missing but applicable, or **Update available** if the management pack file is not the most recent version.

    The management pack language matches the default language of the currently installed management pack files.   You can choose to import in another language by clicking on the option **Languages** and in the **Select Languages** dialog box select the appropriate language and then click **OK**.  The **Select Management Packs** page will update the list of management pack files which include the selected languages.

7. On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection, as follows:

 - A green check mark indicates that the management pack can be imported. When all management packs in the list display this icon, click **Install**.
 - A yellow information icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list but are available in the catalog. To add the management pack dependencies to the **Import** list, click **Resolve** in the **Status** column. When the **Dependency Warning** dialog box that appears, click **Resolve**.
 - A red error icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list and are not available in the catalog. To view the missing management packs, click **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right-click the management pack, and then click **Remove**.

    >[!NOTE]
    >When you click **Install**, any management packs in the Install list that display the **Information** or **Error** icon are not imported.

8. The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there is a problem at any stage of the import process, select the management pack in the list to view the status details. Click **Close**.

## Importing a management pack using Get All MPs
The following procedure describes how to use the Get All MPs option to download management pack for a selected workload.  

1. Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2. In the Operations console, click **Administration**.

3. Click on **Updates and Recommendations** under **Management Packs**.

4. If there are multiple management packs recommended for either an update or a new installation, you can download and import all of them by clicking **Get All MPs** from the **Actions** pane.

5. The **Connecting to Management Pack Catalog Web Service** window appears and after it successfully connects and synchronizes, the **Import Management Packs** wizard opens.

6. On the **Select Management Packs** page, in the list of management packs will be the management packs identified in the **Import Type** column with the value of **Not installed** if missing but applicable, or **Update available** if the management pack file is not the most recent version.

7. On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection, as follows:

 - A green check mark indicates that the management pack can be imported. When all management packs in the list display this icon, click **Install**.
 - A yellow information icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list but are available in the catalog. To add the management pack dependencies to the **Import** list, click **Resolve** in the **Status** column. When the **Dependency Warning** dialog box that appears, click **Resolve**.
 - A red error icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list and are not available in the catalog. To view the missing management packs, click **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right-click the management pack, and then click **Remove**.

    >[!NOTE]  
    >When you click **Install**, any management packs in the **Install** list that display the **Information** or **Error** icon are not imported.

8. The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there is a problem at any stage of the import process, select the management pack in the list to view the status details. Click **Close**.

## Supported workloads

The following list includes the workloads that are supported by this feature.

- BizTalk 2006
- BizTalk 2009
- BizTalk 2010
- Biztalk Server 2013
- Biztalk Server 2013R2
- Branch Cache 2016
- CRM 2011
- CRM 2013
- CRM 2015
- Defender Technical Preview
- Distributed Transaction Coordinator 2012 R2
- Distributed Transaction Coordinator 2016
- Dynamics AX 2009
- Dynamics AX 2012
- Dynamics AX Retail 2012 R3
- Essentials Technical Preview
- Exchange Server 2013
- Host Integration Server 2010
- Host Integration Server 2013
- NAV 2013
- NAV 2013 R2
- Office SharePoint Foundation 2010
- SharePoint 2010 Products
- Sharepoint Foundation Server 2013
- Sharepoint Server 2013
- SMA 2012 R2
- SPF 2012 R2
- SQL Server 2005
- SQL Server 2008
- SQL Server 2012
- SQL Server 2012 Analysis Services
- SQL Server 2012 Replication
- SQL Server 2012 Reporting Services (Native Mode)
- SQL Server 2014
- SQL Server 2014 Analysis Services
- SQL Server 2014 Replication
- SQL Server 2014 Reporting Services (Native Mode)
- SQL Server 2016
- SQL Server 2016 Analysis Services
- SQL Server 2016 Replication
- SQL Server 2016 Reporting Services (Native Mode)
- System Center 2012 App Controller
- System Center 2012 Configuration Manager
- System Center 2012 Orchestrator 
- Windows Server Backup
- Windows Service Manager 2012
- Windows TFS 2013

### Windows Server 2016

- Active Directory Certificate Service
- Active Directory Domain Services
- Active Directory Federation Service
- Active Directory Right Management Service
- DHCP Server
- DNS Server
- Fail Over Clustering
- File Services 
- IIS
- Network Load Balancing
- Print Server

### Windows Server 2012 R2 

- Active Directory Certificate Services
- Active Directory Domain Services
- Active Directory Federation Services
- Active Directory Light Weight Directory Services
- Active Directory Right Management Services
- Branch Cache
- Cluster
- DHCP
- DNS
- Essentials
- File Services
- Hyper-V
- NLB
- Print Services
- Queueing
- Remote access
- Remote Desktop Service
- Web application proxy
- Windows Deployment Services
- Windows Update Services

### Windows Server 2012 

- Active Directory Certificate Services
- Active Directory Domain Services
- Active Directory Federation Services
- AD Right Management Services
- Branch Cache
- Cluster
- DHCP
- DNS
- File Services
- Hyper-V
- IIS
- Message Queueing
- Network Load Balancing
- Print Services
- Remote Access
- Remote Desktop Services
- Windows Deployment Services
- Windows Server backup
- Windows Update Services

### Windows Server 2008 R2 version

- Active Directory Certificate Services
- Active Directory Domain Services
- Active Directory Federation Services
- Active Directory Lightweight Directory Services
- Active Directory Right Management Services
- Branch Cache
- DHCP
- DNS
- File Services
- Hyper-V
- IIS 2008 R2
- Message Queueing
- Network Load Balancing
- Print Services
- Remote Desktop Service
- Routing Remote Services

## Next steps

- To understand how to approach to managing the lifecycle of management packs deployed in your management group, see [Management pack lifecycle](Management-Pack-Lifecycle.md).

- Review the [Operations Manager Reports library](operations-manager-reports-library.md) to understand what reports are available to help you explore the operational data and configuration information in your management group and follow the [How to create reports in Operations Manager](how-to-create-reports-in-operations-manager.md) to create reports for your operational needs. 
