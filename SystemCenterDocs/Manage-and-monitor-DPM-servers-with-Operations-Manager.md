---
title: Manage and monitor DPM servers with Operations Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97fd6656-af44-4e5c-bef8-dc57643b0181
---
# Manage and monitor DPM servers with Operations Manager
Central Console is a System Center Operations Manager console that you can deploy to manage and monitor multiple DPM servers from a single location. It provides:

-   Centralized monitoring of DPM servers from a single location—You can monitor different versions of DPM, and track the status and health of servers, tasks, protected resources, tape libraries, available storage and disk space, and backups.

-   View the state of all roles on DPM servers

-   Monitor, identify, action, and troubleshoot alerts that are generated when an SLA is broken. You can consolidate alerts to show: only one instance for repeated alerts; single alert for alerts with the same root cause, or if multiple backups fail for the same data source, and generate only one ticket if a ticketing system is used.

-   Remote corrective actions and remote recovery

-   Service\-level agreement \(SLA\)\-based alerting. Alerts are generated when an SLA is broken.

-   Monitor DPM server memory, CPU, disk resources, database, and performance trends.

-   Modify and manage settings, including disk allocation, recovery points, users, protect groups.

-   Recover data.

## Setting up Central Console
What you need:

-   A System Center Operations Manager server running 2012 R2. The Operations Manager Data Warehouse must be up and running.

-   View the state of all roles on DPM servers

-   To install the Management Packs the DPM server must be running at least DPM 2012 R2 with Update Rollup 5.

-   If you’re running a previous version of the Discover and Library Management Packs obtained from the DPM installation media you should remove them from the DPM server and install the new versions from the download page.

-   You can only run one language version of the Management Pack at one time. If you want to use the pack in a different language uninstall the pack in the existing language and then install it with the new language.

You deploy Central Console as follows:

1.  [Install the Operations Manager agent](#BKMK_OM)—Install the Operations Manager agent on each DPM server you want to manage and monitor.

2.  [Import the DPM discovery and library management packs](#BKMK_Import)—Downloads the packs and install them on the Operations Manager server.

3.  [Install Central Console](#BKMK_Central)—Install Central Console on the Operations Manager server.

4.  [Import the DPM reporting management pack](#BKMK_ImportReporting)—Downloads the pack and install it on the Operations Manager server.

### <a name="BKMK_OM"></a>Install the Operations Manager agent
Install the agent as follows:

1.  Install the agent on each DPM server you want to monitor.

2.  [Get](http://go.microsoft.com/fwlink/?LinkId=524729) the latest agent version.

### <a name="BKMK_Import"></a>Import the DPM discovery and library management packs
DPM provides the following management packs:

-   Reporting management pack \(Microsoft.SystemCenter.DataProtectionManager.2012.Reporting.mp\)—Collects and displays reporting data from all DPM servers, and exposes a set of Operations Manager warehouse views for DPM. You can query these views to generate custom reports.

-   Discovery and monitoring management pack \(Microsoft.SystemCenter.DataProtectionManager.2012.Discovery.mp\)

-   Library management pack—\(Microsoft.SystemCenter.DataProtectionManager.2012.Library\)

1.  On the Operations Manager server remove any existing DPM management packs.

2.  [Download](http://go.microsoft.com/fwlink/?LinkId=524726) the DPM management packs.

    By default, the download places the Discovery and Library Management Packs in the C:\\Program Files\\System Center Management Packs folder. The Reporting Management Pack is placed in a separate folder inside that folder.

3.  Log on to the Operations Manager server with an account that is a member of the Operations Manager Administrators role.

4.  Remember to remove any previous versions of the Library or Discover Management Packs running on the server.

5.  In the Operations console, click **Administration**. Right\-click **Management Packs** > **Import Management Packs**.

6.  Select **Microsoft.SystemCenter.DataProtectionManagerDiscovery.MP** > **Open** and then **Microsoft.SystemCenter.DataProtectionManagerLibrary.MP** > **Open**.

7.  Follow the instructions in the Import Management Packs wizard.

### <a name="BKMK_Central"></a>Install the Central Console

1.  Select **Install Central Console Server and Client side Components** if you want to monitor DPM servers that have the Operations Manager agent installed and run the DPM administrator console on the Operations Manager server.

2.  Select **Install Central Console Server side Components** if only want to monitor servers, without using the scoped DPM Administrator console.

Note that:

-   [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] adds firewall exceptions for port 6075 to enable scoped Administrator console. Open ports for SQL Server.exe and SQL browser.exe.

-   If you need to uninstall Operations Manager, see [How to Uninstall Operations Manager](http://go.microsoft.com/fwlink/p/?LinkId=245527).

### <a name="BKMK_ImportReporting"></a>Import the reporting management pack

1.  Log on to the Operations Manager server with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, click **Administration**. Right\-click **Management Packs** > **Import Management Packs**.

3.  Select **Microsoft.SystemCenter.DataProtectionManagerReporting.MP** > **Open**.

4.  Follow the instructions in the Import Management Packs wizard.

## Next steps
After you import the Management Packs they discover and monitor data without requiring any additional configuration. You can optionally tweak settings like monitors and rules for your environment. For example if you find that performance\-measuring rules that are enable degrade server performance with slow WAN links, you can disable them. When you have everything configured as needed you can generate DPM reports from Operations Manager

