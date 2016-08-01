---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  cfreemanwa
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-07-01
title:  Release Notes for System Center RTM
ms.assetid:  5fad5608-4cb7-48b0-aa31-35ca5cc2d560
---

# Release Notes for System Center RTM

>Applies To: System Center 2016 RTM

### The following set of notes lists known issues and steps to mitigate the issue. These notes only apply to System Center 2016 RTM.


## System Center RTM - Data Protection Manager Release Notes
### The following release notes apply to System Center RTM - Data Protection Manager.

### TBD


## System Center RTM - Operations Manager Release Notes
### The following release notes apply to System Center RTM - Operations Manager.

### SharePoint integration with Operations Manager has to be recreated
**Description:** While using SharePoint to view Operations Manager data, the existing Web Console Dashboard URLs provided will not work and these Web parts have to be recreated will the below steps..

**Workaround:** Follow the below steps to setup SharePoint to view Operations manager data:
1.	Create a new page on SharePoint in which you want to display the Dashboard.
2.	Open the page and click edit and insert a new Web Part.
3.	In Web Part, under categories select “Media and Content” and under that select “Page Viewer” and click add.
4.	Edit the Web Part and select Web Page and enter the URL of the SCOM Web Console dashboard.
5.	Append “&disabletree=true” at the end of the dashboard URL for disabling the tree view getting displayed on the SharePoint page
6.	Configure the appearance, layout, and Advance attribute of the SharePoint page.


### In Web Console, Windows Computer Tasks is not displayed sometimes
**Description:** In Web Console, when you go to Windows computers view and select a computer, the tasks pane may not display Windows computer tasks.
Likelihood of occurrence: Medium

**Workaround:** None.

### In Web Console, Navigation view is not displayed in the tasks pane for state views
Description:  In Web Console, when you go to State View and select an entity in the list, the tasks pane does not display the Navigation View section of the selected entity.

**Workaround:** None.

### In Web Console, functionality in My Workspace tab does not work .
**Description:** In Web Console, none of the links/views in My Workspace tab work.

**Workaround:** None.

### Web Console might not work due to IIS becoming corrupt
**Description:** Web Console might throw an error **“Could not load type ‘System.ServiceModel.Activation.HttpModule”**.

**Workaround:** Add “HTTP Activation” to the role services of the OS.  Then,
On Server 2008 R2 – run the following in an elevated CMD:  “C:\Windows\Microsoft.NET\Framework64\v4.0.30319>aspnet_regiis.exe -i -enable”.
On Server 2012 – run the following in an elevated CMD:  “C:\Windows\Microsoft.NET\Framework64\v4.0.30319>aspnet_regiis.exe -r”.

### Anomalies in handling tables and bullets in the Knowledge Articles
**Description:** If the tables are inserted in the knowledge article then while re-editing the knowledge article the borders are not applied to the table. Similarly, if bullets are added in the knowledge article it gets converted to numeric bullets while re-editing. And, if there is a single bullet in the article then the article doesn’t gets saved in the MP and console throws error.

**Workaround:** None.

### MSI based installation does not work for Nano agent
**Description:** MSI based installation not supported for Nano agent, agent can be installed from discovery wizard\PowerShell installer scripts.

**Workaround:** None.

### Issues with uninstallation of Nano agent
**Description:** Uninstalling an update to Nano agent is not possible.

**Workaround** Only option is to uninstall the Nano-agent, then install the RTM + desired update.

### Issues with updates of Nano agent
**Description:** Updates to Nano agent will not be pushed from WU. To update Nano-agent.
Will need to either download the available updates and install using the PowerShell update scripts; or can trigger repair from an updated Management server.

**Workaround:** None.


### Unable to override the path or folder for Nano agent installation
**Description:** Nano agent is always installed to the agent folder: ‘%SystemDrive%\Program Files\Microsoft Monitoring Agent’, the agent installation folder cannot be overridden.

**Workaround:** None.

### Inconsistencies in push install experience of Nano agent
**Description:** Push install: the status dialog (which shows that installation in progress etc.) closes but agent stays in pending state in console for some time till installation fails\passes. Installation may fail, and log file will need to be checked for the same.

**Workaround:** None.

### Inconsistencies in push uninstall experience of Nano agent
**Description:** Push uninstall: the status dialog (which shows that uninstallation in progress\completed) shows uninstall success for Nano-agent, but agent uninstalls only after sometime. Uninstallation may fail, and log file will need to checked for same.

**Workaround:** None.

### ACS is not working for Nano agent
**Description:** ACS is not working for Nano agent, in all the cases. There are issues in certain scenarios.

**Workaround:** None.

### Client-side monitoring (CSM) alerts might stop flowing from the System Center Operations Manager management server host
**Description:** The update sequence of System Center Operation Manager management server may cause an issue with the client-side monitoring alerts collection from the management server host. System Center Operations Manager agents are not affected. Likelihood of occurrence: Medium.

**Workaround:** Restart the "Microsoft Monitoring Agent" service on System Center Operations Manager management server host.

### After updating System Center Operations Manager server or agent, Application performance monitoring (APM) events, client-side monitoring (CSM) events, and APM alerts might stop flowing from the monitored hosts
**Description:** The update sequence of System Center Operations Manager agent may cause an issue with the following:

•	Client-side monitoring (CSM) events and alerts collected on the host.

•	Application Performance Monitoring (APM) events and alerts collected on the host.
System Center Operations Manager management server is not affected.


**Workaround:** Restart the "Microsoft Monitoring Agent" service on the System Center Operations Manager agent host that is experiencing the issue.

### Application performance monitoring (APM) for Windows services is not supported in System Center - Operations Manager on hosts where Application Insights Status Monitor is installed.
**Description:** Application performance monitoring (APM) workflow fails to process monitoring configuration for .NET Windows services on the hosts if Application Insights Status Monitor and the System Center - Operations Manager agent are both installed.

**Workaround:** Uninstall Application Insights Status Monitor.

### Namespace values for performance tracking will be ignored
**Description:** Setting the Namespace value for performance tracking when tracking a custom namespace in .NET Applications Performance Monitoring (APM) will be ignored.

**Workaround:** Set both the exception tracking and performance tracking settings to include the same custom namespaces.

### Using sudo elevation with Solaris operating systems requires a configuration change if sudo executable is not in an expected path
**Description:** If you want to use sudo elevation on a computer running Solaris, and the sudo executable is not in an expected path, you need to create a link to the correct path. Operations Manager will look for the sudo executable in the path /opt/sfw/bin, and then in the path /usr/bin. If sudo is not installed in one of these paths, a link is required.

**Workaround:** The UNIX and Linux agent installation script creates the symbolic link /etc/opt/Microsoft/scx/conf/sudodir to the folder expected to contain sudo. The agent uses this symbolic link to access sudo. The installation script automatically creates the symbolic link, so no action is needed for standard UNIX and Linux configurations. However if sudo is installed in a non-standard location, you should change the symbolic link to point to the folder where sudo is installed. If you change the symbolic link, its value is maintained for uninstall, re-installation, and upgrade operations with the agent.

## System Center RTM - Orchestrator and Service Management Automation Release Notes
### The following release notes apply to System Center RTM - Orchestrator and Service Management Automation .

### TBD
**Description:** TBD.

**Work around:** TBD

## System Center RTM - Service Manager Release Notes
### The following release notes apply to System Center RTM - Service Manager.

### TBD
**Description:** TBD.

**Workaround:** TBD.


## System Center 2016 - Virtual Machine Manager Release Notes
### The following release notes apply to System Center 2016 - Virtual Machine Manager.

### TBD
**Description:** TBD.

**Workaround:** TBD.
