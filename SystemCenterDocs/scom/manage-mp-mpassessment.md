---
ms.assetid: 7cb61f4f-d184-407e-abc1-f2334de51810
title: Management Pack Assessment
description: This article describes how to use the updates and recommendations feature in  System Center Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: na
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Management pack assessment



::: moniker range="<=sc-om-2016 <sc-om-2019"

Operations Manager includes a new feature called Updates and Recommendations, to help you proactively identify new technologies or components (that is, workloads) deployed in your IT infrastructure that weren't monitored by Operations Manager or aren't monitored using the latest version of a management pack.

If there are Management Packs in the catalog that are designed to monitor those workloads, they'll be displayed on the Updates and Recommendations screen. You'll also find a list of any updates that are available for Management Packs that are installed in your management group.

::: moniker-end


::: moniker range=">=sc-om-2019"

Operations Manager includes support for [Linux and Unix](plan-supported-crossplat-os.md) workloads and operating systems. See the following sections for detailed information. Updates and Recommendations feature in Operations Manager 2019 also supports a new capability called **Machine Details**, which provides the computer details (name and operating system) on which a selected workload is running.

If there are management packs in the catalog that are designed to monitor those workloads, they'll be displayed on the *Updates and Recommendations* screen. You'll also find a list of any updates that are available for management packs that are installed in your management group.

::: moniker-end

When a new workload is deployed in your IT infrastructure that was never monitored by Operations Manager, it will be detected and highlighted under the Updates and Recommendations node.  The management packs required to monitor that workload will be presented with a status of **Not Installed**.  If the necessary management pack files for a particular workload aren't installed, for example, the library management pack file is installed but not the corresponding discovery and monitoring management pack files, the Updates and Recommendations feature will list that workload with a status of **Partially Installed**.  

::: moniker range=">=sc-om-2019"

Operations Manager *Updates and Recommendation* feature includes support for application servers running on Linux and Unix operating systems.

::: moniker-end

This feature includes the following capabilities:

|  **Option** |  **Description** |
|----------|-------------|
|  **Get MP**  | Installs the management packs for the selected workload
|  **Get All MPs**  |  Installs the management packs for all of the workloads displayed
|  **View Guide**  |  Downloads the management pack guide from the web browser, for the selected workload, to your computer
|  **View DLC Page**  | Open from the web browser, the page on the Microsoft Download Center, to download the management pack file
|  **Machine Details** (applicable only for Operations Manager 2019)  | Highlights the machine name and operating system for the selected workload.
|  **More information**  | Highlights all impacted agent-managed systems and management pack details of selected workload (depending on the status of the workload)

>[!NOTE]
>In order to use the options highlighted in the table above, the computer you are running the Operations console from requires an Internet connection and your firewall needs to allow access to the following URL - **https://www.microsoft.com/mpdownload/ManagementPackCatalogWebService.asmx?**

## Importing a Management Pack using Get MP
The following procedure describes how to use the Get MP option to download a management pack for a selected workload.  

1. Sign in to the computer with an account that's a member of the Operations Manager Administrators role.

2. In the Operations console, select **Administration**.

3. Select **Updates and Recommendations**  under **Management Packs**.

    >[!NOTE]
    >When accessing the Updates and Recommendations view, you may receive the following message, "An error occurred while displaying the Updates and Recommendations View. This might be because the database query has encountered an issue or the online catalog is down."  This can be caused by having a duplicate management pack with the same name.  To help troubleshoot the issue, run the following command in the Operations Manager  Shell and review the output file to identify the duplicate MP:
    >`Get-SCManagementPack | Sort -property Name | Format-Table Name,Version,Sealed -AutoSize | Out-File "c:\temp\mplist_name.txt"`
    >

4. If a management pack is recommended for either an update or a new installation, select it and select **Get MP** from the **Actions** pane.

5. The **Connecting to Management Pack Catalog Web Service** window appears and after it successfully connects and synchronizes, the **Import Management Packs** wizard opens.

6. On the **Select Management Packs** page, in the list of management packs will be the management packs identified in the **Import Type** column with the value of **Not installed** if missing but applicable, or **Update available** if the management pack file isn't the most recent version.

    The management pack language matches the default language of the currently installed management pack files. You can choose to import in another language by selecting the option **Languages**, and in the **Select Languages** dialog, select the appropriate language and select **OK**.  The **Select Management Packs** page will update the list of management pack files that include the selected languages.

7. On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection as follows:

   - A green check mark indicates that the management pack can be imported. When all management packs in the list display this icon, select **Install**.
   - A yellow information icon indicates that the management pack is dependent on one or more management packs that aren't in the **Import** list but are available in the catalog. To add the management pack dependencies to the **Import** list, select **Resolve** in the **Status** column. When the **Dependency Warning** dialog appears, select **Resolve**.
   - A red error icon indicates that the management pack is dependent on one or more management packs that aren't in the **Import** list and aren't available in the catalog. To view the missing management packs, select **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right-click the management pack, and select **Remove**.

     >[!NOTE]
     >When you select **Install**, any management packs in the Install list that display the **Information** or **Error** icon aren't imported.

8. The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there's a problem at any stage of the import process, select the management pack in the list to view the status details. Select **Close**.

## Importing a management pack using Get All MPs
The following procedure describes how to use the Get All MPs option to download management pack for a selected workload.  

1. Sign in to the computer with an account that is a member of the Operations Manager Administrators role.

2. In the Operations console, select **Administration**.

3. Select **Updates and Recommendations** under **Management Packs**.

4. If there are multiple management packs recommended for either an update or a new installation, you can download and import all of them by selecting **Get All MPs** from the **Actions** pane.

5. The **Connecting to Management Pack Catalog Web Service** window appears, and after it successfully connects and synchronizes, the **Import Management Packs** wizard opens.

6. On the **Select Management Packs** page, in the list of management packs will be the management packs identified in the **Import Type** column with the value of **Not installed** if missing but applicable, or **Update available** if the management pack file isn't the most recent version.

7. On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection, as follows:

   - A green check mark indicates that the management pack can be imported. When all management packs in the list display this icon, select **Install**.
   - A yellow information icon indicates that the management pack is dependent on one or more management packs that aren't in the **Import** list but are available in the catalog. To add the management pack dependencies to the **Import** list, select **Resolve** in the **Status** column. When the **Dependency Warning** dialog appears, select **Resolve**.
   - A red error icon indicates that the management pack is dependent on one or more management packs that aren't in the **Import** list and aren't available in the catalog. To view the missing management packs, select **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right-click the management pack, and select **Remove**.

     >[!NOTE]  
     >When you select **Install**, any management packs in the **Install** list that display the **Information** or **Error** icon aren't imported.

8. The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there's a problem at any stage of the import process, select the management pack in the list to view the status details. Select **Close**.

## Supported workloads

The following list includes the workloads that are supported by this feature.

- BizTalk 2006, 2009, 2010, server 2013 and 2013 R2
- Branch Cache 2016
- CRM 2011, 2013 and 2015
- Defender Technical Preview
- Distributed Transaction Coordinator 2012 R2 and 2016
- Dynamics AX 2009, 2012 and Retail 2012 R3
- Essentials Technical Preview
- Exchange Server 2013
- Host Integration Server 2010 and 2013
- NAV 2013 and 2013 R2
- Office SharePoint Foundation 2010
- SharePoint 2010 Products, Foundation Server 2013 and Server 2013
- SMA 2012 R2
- SPF 2012 R2
- SQL Server 2005, 2008, 2012, 2012 Analysis Services, 2012 Replication, 2012 Reporting Services (Native Mode), 2014, 2014 Analysis Services, 2014 Replication, 2014 Reporting Services (Native Mode), 2016, 2016 Analysis Services, 2016 Replication and 2016 Reporting Services (Native Mode)
- System Center 2012 App Controller, Configuration Manager and Orchestrator
- Windows Server Backup, Service Manager 2012 and TFS 2013

::: moniker range="sc-om-2019"

The following workloads are supported for the operating systems listed below.


|                **Feature**                | **Windows Server 2012 R2** | **Windows Server 2016** | **Windows Server 2019** |
|-------------------------------------------|----------------------------|-------------------------|-------------------------|
|   Active Directory Certificate Service    |             Y              |            Y            |                         |
|     Active Directory Domain Services      |             Y              |            Y            |            Y            |
|    Active Directory Federation Service    |             Y              |            Y            |            Y            |
| Active Directory Right Management Service |             Y              |            Y            |            Y            |
|                DHCP Server                |             Y              |            Y            |            Y            |
|                DNS Server                 |             Y              |            Y            |            Y            |
|           Fail Over Clustering            |             Y              |            Y            |            Y            |
|               File Services               |             Y              |            Y            |            Y            |
|                    IIS                    |             Y              |            Y            |            Y            |
|          Network Load Balancing           |             Y              |            Y            |            Y            |
|               Print Server                |             Y              |            Y            |            Y            |
|                Essentials                 |             Y              |            Y            |                         |
|                  Hyper-V                  |             Y              |            Y            |                         |
|                 Queueing                  |             Y              |            Y            |                         |
|               Remote access               |             Y              |                         |                         |
|          Remote Desktop Service           |             Y              |            Y            |                         |
|           Web application proxy           |             Y              |                         |                         |
|        Windows Deployment Services        |             Y              |                         |                         |
|          Windows Update Services          |             Y              |                         |                         |

::: moniker-end

::: moniker range="sc-om-2016"

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
::: moniker-end

::: moniker range="=sc-om-2019"

## Support for Linux and Unix platforms supported for application servers workload

- Oracle6 x64, Oracle7 x64
- Sles12 x64
- Rhel7 x64
- Debian8 x64, Debian9 x64
- Ubuntu16 x64, Ubuntu 18 x64
- Aix 7.x

## Supported application servers
- Apache Tomcat 7, Apache Tomcat 8, Apache Tomcat 9
- Red Hat JBoss 4, JBoss 5, JBoss 6, JBoss 7, Wildfly Application Server 8/9/10/11/12/13/14, Red Hat JBoss EAP 6,  Red Hat JBoss EAP 7
- IBM WebSphere 7.0, WebSphere 8.0, WebSphere 8.5, WebSphere 9.0
- Oracle WebLogic 10gR3, Oracle WebLogic 11, WebLogic 12cR1, WebLogic 12cR2


::: moniker-end

## Next steps

- To understand the approach to managing the lifecycle of management packs deployed in your management group, see [Management pack lifecycle](manage-mp-lifecycle.md).

- To understand what reports are available to help you explore the operational data and configuration information in your management group, review the [Operations Manager Reports library](manage-reports-installed-during-setup.md).

-  To create reports for your operational needs, follow the [How to create reports in Operations Manager](manage-reports-create-reports.md).
