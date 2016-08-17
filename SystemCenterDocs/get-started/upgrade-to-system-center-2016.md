---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  cfreemanwa
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-07-25
title:  Upgrade-to-System-Center-2016
ms.technology:  system-center-2016
ms.assetid:  4f8701a5-8d55-4ffd-afee-e6341ec6b7f4
---

# Upgrade to System Center 2016

>Applies To: System Center 2016


If you are already running System Center 2012 R2 you can upgrade your environment to System Center 2016 by following the procedures and guidance in this article. Microsoft only supports upgrading from System Center 2012 R2 from one of the supported update rollup installations listed in the supported upgrade paths sections.


## Common steps
You will follow  the same general steps for upgrading to System Center 2016 from System Center 2012 R2 for all System Center components. The general steps are:
1. Uninstall the 2012 R2 version of the component with "retain database" option if appropriate.
2. Upgrade the operating system to a version supported with System Center 2016.
3. Install any other software required by the component (see list below).
4. Install the new version of the component with the "Upgrade database" option if appropriate.

> [!IMPORTANT]
> Make sure you are upgrading to a supported platform by reviewing the [System Requirements topics](../system-requirements/system-requirements-for-system-center-technical-preview.md).

## Supported upgrade paths
Microsoft supports the following upgrade paths.

|Component|Previous Version|
|---------|----------------|
|Data Protection Manager|System Center 2012 R2 with UR9 or later|
|Operations Manager|System Center 2012 R2 with UR9 or later|
|Orchestrator|System Center 2012 R2 with UR9 or later|
|Service Manager|System Center 2012 R2 with UR9 or later|
|Service Provider Foundation|See the SPF section for details|
|Virtual Machine Manager|System Center 2012 R2 with UR9 or later

## Component Specific Notes

The following sections provide detailed considerations for each component.

### DPM Upgrade Notes

You can not upgrade DPM Remote Administration and the DPM Central Console when upgrading from System Center 2012 R2. If you plan on using Remote Administration or the Central Console you will need to complete a fresh install of System Center 2016 - DPM.

### OM Upgrade
[!NOTE]
If your Operations Manager 2012 R2 management group is integrated with Microsoft Operations Management Suite (OMS), its configuration will be retained and continue to function normally after the upgrade is complete.  

> [!WARNING]
> If you are upgrading two or more System Center components, you must follow the procedures that are documented in Upgrade Sequencing for System Center 2012 R2.
>  
> The order in which you perform component upgrades is important. Failure to follow the correct upgrade sequence might result in component failure for which no recovery options exist. The affected System Center components are:
  > 1. Configuration Manager
  > 2. Data Protection Manager
  > 3. Orchestrator
  > 4. Configuration Manager
  > 5. Virtual Machine Manager

Before you upgrade to System Center 2016 - Operations Manager, you must first determine whether all servers in your Operations Manager management group meet the minimum supported configurations. For more information, see System Requirements: System Center 2016 - Operations Manager.

There are several options for upgrade:

1. If you run upgrade on a single-server management group, you only need to run upgrade one time since all features are installed on a single server. The Operations Manager Upgrade wizard performs system prerequisite checks and provides resolution steps for any issues. Installation will not continue until you resolve all issues.

2. If you are upgrading a distributed management group, you must upgrade certain features before others. For example, you upgrade the management servers first, followed by the gateways, operations consoles, and then agents. Next, you can upgrade any remaining features, such as the web console, reporting and Audit Collection Services (ACS). You must also perform a number of pre-upgrade and post-upgrade tasks.

3. If you want to maintain your Operations Manager 2012 R2 environment you can install System Center 2016 - Operations Manager in parallel and upgrade your agents and multi-home between both management groups.

### High Level Overview of System Center 2016 Operations Manager Upgrade Steps for a Distributed Management Group

The following steps outline the process for upgrading a distributed management group:

1. Accomplish Pre-Upgrade Tasks

2. Upgrade the initial management server and then additional management servers (each management server must be upgraded)

3. Upgrade ACS (because the ACS server must be on same machine as a management server, we recommend you perform this step along with the upgrade of the management server on which ACS resides.)

4. \*Upgrade Gateway(s)

5. Upgrade Console

6. Push Install to Agent(s) / Upgrading Manually Installed Agents

7. Upgrade Web Console

8. Upgrade Reporting Server

9. Perform Post-Upgrade Tasks

\*Steps 4 through 8 can be performed in parallel after all Management Servers have been upgrade.


### Orchestrator Upgrade Notes

### SM Upgrade Notes

- For Service Manager data warehouse database restoration, the Reporting database also needs to be restored **after** you install the data warehouse.
- Use the published information for the order of System Center components as well as Service Manager components.
- Do not mix Service Manager 2016 and Service Manager 2012 R2 with different Service Manager components - all should use the same version. For example, both the Self Service portal and the Service Manager management server  should use the same version.
- You can only use the Service Manager 2012 R2 old or new portal with Service Manager 2012 R2. You cannot use the Self Service portal in Service Manager 2016 with Service Manager 2012 R2.
- When upgrading from Service Manager 2012 R2 to Service Manager 2016 TP5, you should not enable or disable the Active Directory group expansion for any of the Active Directory connectors.

    In other words, if it is off, let it remain off and if it is on, let it remain on until the connector runs for the first time. See the screenshot below. This applies only to the first time that the Active Directory connector runs after you upgrade. You can change your preferences for Active Directory group expansion workflow after the first time that the Active Directory connector sync completes.

    ![Active Directory Connector wizard](../media/sm-adconnector01.png)



#### Upgrading the Self Service Portal from a standalone installation of the Service Manager 2012 R2 Silverlight-based Self Service portal
Use the following steps to upgrade your Self Service portal and Service Manager management servers where they are installed on different computers.

On the Service Manager 2012 R2 Silverlight Self Service Portal:
1. Uninstall the Silverlight-based Self Service portal. Support for Silverlight was removed with Service Manager 2016.
2. Install the new HTML5-based Self Service Portal, using the information at [Deploy the Self-Service Portal for Service Manager](../sm/deploy/Deploy-the-Self-Service-Portal-for-Service-Manager.md)

#### Upgrading the Self Service Portal from a standalone installation of the Manager 2012 R2 HTML5-based Self Service portal
Use the following step to upgrade your Self Service portal and Service Manger management servers where they are installed on different computers.

- Upgrade the Self Service portal directly from Service Manager 2012 R2 to Service Manager 2016.

#### Upgrading the Self Service Portal from Service Manager 2012 R2 installed on a secondary management server with a Silverlight-based Self Service Portal
1.  Uninstall Service Manager 2012 R2. This step uninstalls the management server role from the computer.
2.  Upgrade the primary Management Server from Service Manager 2012 R2 to Service Manager 2016.
3.  Install the secondary Management Server 2016 role on new computer.
4.  Install the Service Manager 2016 version of the Self Service Portal (HTML5) on same computer as the secondary management server.

#### Upgrading the Self Service Portal from Service Manager 2012 R2 installed on a secondary management server with a HTML-based Self Service Portal

1.  Decommission the computer - neither the Self Service portal nor Service Manager 2012 R2 can be uninstalled. Create backups of the Self Service portal configuration files - web.config (inside the website folder), custom.css (inside the website folder \Content\CSS) and sidebar.cshtml (inside the website folder \Views\Shared) because they are required later.
2.  Upgrade the primary Management Server from Service Manager 2012 R2 to Service Manager 2016.
3.  Install the secondary Management Server 2016 role on new computer.
4.  Install the Service Manager 2016 version of the Self Service Portal (HTML5) on the same computer as the secondary management server.
5.  Overwrite the current configuration files with those backed-up in step 1 to restore any customizations.

#### Upgrading the Self Service Portal from Service Manager 2012 R2 installed on a primary Management Server with the Self Service portal (Silverlight/HTML5):
*Installing the Self Service portal on the same computer as the primary management server is not recommended.* However, in the event that you are using this combination, then use the following steps to upgrade to Service Manager 2016. Enabling the upgrade is the first step to move the primary Management Server to a Secondary management server by using the following steps.

1. Add new the Service Manager 2012 R2 secondary management server to a management group.
2. Promote the secondary management server to a primary management server role, which will move the current primary management server to a secondary role.
3. Follow the steps mentioned in the *Upgrading the Self Service Portal from Service Manager 2012 R2 installed on a secondary management server with a Silverlight-based Self Service Portal* or in the *Upgrading the Self Service Portal from Service Manager 2012 R2 installed on a secondary management server with a HTML-based Self Service Portal* sections to upgrade your management server and Self Service portal to Service Manager 2016.

#### Upgrading the Self Service Portal from Service Manager 2016 TP5 Self Service portal (stand alone or with a management server)
  - You can upgrade the Self Service portal directly from Service Manager 2012 R2 to Service Manager 2016.

## SPF Upgrade Notes

- If you have integrated SPF with Windows Azure Pack, your version of Windows Azure Pack must be running Update Rollup 10 or later. Also, both System Center 2012 R2 - VMM and SPF must be running Update Rollup 9 or later.

## VMM Upgrade Notes

- For all upgrades to VMM 2016 you can either continue with the current version of SQL Server, or, you can upgrade to the supported version of SQL Server. Review [SQL Server Requirements](../system-requirements/SQL-server-version-compatibility-for-system-center-technical-preview.md) for the list of supported versions of SQL Server.
- You can upgrade both host and guest VMM agents from the VMM console.

### Upgrading a highly available VMM environment.

The following procedures describe the steps to take if you are upgrading a  VMM management server deployed on a highly available cluster.

1.	Backup and retain the VMM database
2.	Uninstall VMM 2012 R2 from the highly available passive node.
3.	Upgrade to Windows Server 2016 and to a supported version of SQL Server on the passive node.
4.	Upgrade to the Windows 10 version of the ADK.
5.  Install System Center 2016 – Virtual Machine Manager in the highly available environment and when prompted, upgrade the database.
6.  Failover to the passive node.
7.  Repeat steps 2 - 5 for the other nodes in your HAVMM environment.
8.	[Optional] Install the appropriate SQL Command line utilities.

Note: If the VMMM database is hosted on a SQL Server running in the "Always on" mode, and the VMM database is in the availability group, you must remove it from the availability group before upgrading the SQL Server to a later version.
