---
title:  Release Notes for System Center 2016 - Operations Manager
description: Release Notes for System Center 2016 - Operations Manager
manager:  cfcarmonm
ms.topic:  article
author:  mgoedtel
ms.author: magoedte
ms.prod:  system-center-2016
ms.technology: operations-manager
ms.topic: article
keywords:
ms.date: 05/23/2017
ms.assetid: e5b25d0f-9316-42d2-aeb9-4ba0b0afc6cf
---

# System Center 2016 - Operations Manager Release Notes
The following release notes apply to System Center 2016 - Operations Manager.

## SharePoint integration with Operations Manager has to be recreated
**Description:** While using SharePoint to view Operations Manager data, the existing Web Console Dashboard URLs provided will not work and these Web parts have to be recreated with the  steps below.

**Workaround:** Perform the following steps to setup SharePoint to view Operations manager data:
1.	Create a new page on SharePoint in which you want to display the Dashboard.
2.	Open the page and click edit and insert a new Web Part.
3.	In Web Part, under categories select “Media and Content” and under that select “Page Viewer” and click add.
4.	Edit the Web Part and select Web Page and enter the URL of the Operations Manager Web console dashboard.
5.	Append “&disabletree=true” at the end of the dashboard URL for disabling the tree view getting displayed on the SharePoint page
6.	Configure the appearance, layout, and Advance attribute of the SharePoint page.


## Web Console might not work due to IIS becoming corrupt
**Description:** Web Console might throw an error **“Could not load type ‘System.ServiceModel.Activation.HttpModule”**.

**Workaround:** Add “HTTP Activation” to the role services of the OS.  Then,
on Server 2012 – run the following in an elevated command prompt:  “C:\Windows\Microsoft.NET\Framework64\v4.0.30319>aspnet_regiis.exe -r”.

## Anomalies in handling tables and bullets in Knowledge Articles
**Description:** If tables are inserted in a knowledge article, when re-editing the knowledge article the borders are not applied to the table. Similarly, if bullets are added in the knowledge article it gets converted to numeric bullets while re-editing. And, if there is a single bullet in the article then the article doesn’t get saved in the MP and the console throws error.

**Workaround:** None.

## MSI based installation does not work for Nano agent
**Description:** MSI based installation is not supported for Nano agent. The agent can be installed from Discovery Wizard\PowerShell installer scripts.

**Workaround:** None.

## Issues with uninstalling an update for Nano agent
**Description:** Uninstalling an update to Nano agent is not possible.

**Workaround** Only option is to uninstall the Nano agent, then install the RTM version + desired update.

## Issues with updates of Nano agent
**Description:** Updates to Nano agent will not be pushed from Windows Update. To update Nano agent you Will need to either download the available update and install using the PowerShell update scripts; or trigger a repair from an updated Management server.

**Workaround:** None.

## Unable to override the path or folder for Nano agent installation
**Description:** Nano agent is always installed to the following path: ‘%SystemDrive%\Program Files\Microsoft Monitoring Agent’; the agent installation folder cannot be overridden.

**Workaround:** None.

## Inconsistencies in push install experience of Nano agent
**Description:** The Discover Wizard status dialog closes but agent stays in pending state in console for some time until the installation fails or completes successfully. Installation may fail, and you will need to refer to the setup log file for further information to troubleshoot.

**Workaround:** None.

## Inconsistencies in push uninstall experience of Nano agent
**Description:** When performing a Push uninstall from the Operations console, the status dialog (which shows progress status) shows the uninstall completed successfully, but the agent uninstall is still being performed. Uninstall may fail and refer to the setup log file for further information to troubleshoot.

**Workaround:** None.

## ACS is not working for Nano agent
**Description:** ACS is not working for Nano agent, in some cases. There are issues in certain scenarios.

**Workaround:** None.

## Client-side monitoring (CSM) alerts might stop flowing from the System Center Operations Manager management server
**Description:** The update sequence of System Center Operation Manager management server may cause an issue with the client-side monitoring alerts collection from the management server. System Center Operations Manager agents are not affected. Likelihood of occurrence: Medium.

**Workaround:** Restart the "Microsoft Monitoring Agent" service on System Center Operations Manager management server.

## After updating System Center Operations Manager server or agent, Application performance monitoring (APM) events, client-side monitoring (CSM) events, and APM alerts might stop flowing from the monitored hosts
**Description:** The update sequence of System Center Operations Manager agent may cause an issue with the following:

•	Client-side monitoring (CSM) events and alerts collected on the host.

•	Application Performance Monitoring (APM) events and alerts collected on the host.
System Center Operations Manager management server is not affected.


**Workaround:** Restart the "Microsoft Monitoring Agent" service on the System Center Operations Manager agent-managed computer that is experiencing the issue.

## Application performance monitoring (APM) for Windows services is not supported in System Center - Operations Manager on computers where Application Insights Status Monitor is installed.
**Description:** Application performance monitoring (APM) workflow fails to process monitoring configuration for .NET Windows services on the computer if Application Insights Status Monitor and the System Center - Operations Manager agent are both installed.

**Workaround:** Uninstall Application Insights Status Monitor.

## Namespace values for performance tracking will be ignored
**Description:** Setting the Namespace value for performance tracking when tracking a custom namespace in .NET Applications Performance Monitoring (APM) will be ignored.

**Workaround:** Set both the exception tracking and performance tracking settings to include the same custom namespaces.

## Using sudo elevation with Solaris operating systems requires a configuration change if sudo executable is not in an expected path
**Description:** If you want to use sudo elevation on a computer running Solaris, and the sudo executable is not in the expected path, you will need to create a link to the correct path. Operations Manager will look for the sudo executable in the path /opt/sfw/bin, and then in the path /usr/bin. If sudo is not installed in one of these paths, a link is required.

**Workaround:** The UNIX and Linux agent installation script creates the symbolic link /etc/opt/Microsoft/scx/conf/sudodir to the folder expected to contain sudo. The agent uses this symbolic link to access sudo. The installation script automatically creates the symbolic link, so no action is needed for standard UNIX and Linux configurations. However if sudo is installed in a non-standard location, you should change the symbolic link to point to the folder where sudo is installed. If you change the symbolic link, its value is maintained for uninstall, re-installation, and upgrade operations with the agent.

## Operations Manager Console will stop responding if you attempt to resolve a dependency while importing a management pack
**Description:** When you click **Import Management Packs** from the Administration workspace of the Operations Manager Operations console, the console will display the **Resolve** button if the Management Pack is dependent on another Management Pack. If you click **Resolve** you will see the **Dependency Warning**. If you click the **Resolve** button in the **Dependency Warning** dialog, the Operations console will stop responding.

**Workaround:** Install the Update for System Center 2016 - Operations Manager. See the Knowledge Base article [3117586](https://support.microsoft.com/en-us/kb/3117586) for specific instructions.

## Telemetry data may be erroneously sent when the "Usage and Connectivity Data" setting is set to "False"
**Description:**If two operators have Operations Manager consoles open and one sets the Usage and Connectivity Data setting to "Do not send data" data may continue to flow to Microsoft until the second user closes and reopens their instance of the Operations manager console.

**Workaround:** Restart all Operations Manager console sessions after making changes to the Usage and Connectivity setting.

**Description:**When a new component such as a management server or gateway server are added to an existing Operations Manager environment, usage information about the setup process is sent to Microsoft even though the Usage and Connectivity Data setting is set to "Do not send data". After the component is added, no further usage data will be sent to Microsoft from the component.

**Workaround:** None

## Namespace values for performance tracking will be ignored
**Description:** Setting the Namespace value for performance tracking when tracking a custom namespace in .NET Applications Performance Monitoring (APM) will be ignored.

**Workaround:** Set both the exception tracking and performance tracking settings to include the same custom namespaces.

## Operations Manager web console is not compatible with Microsoft Edge web browser
**Description:** When you open the Operations Manager web console from the Windows 10 Start Menu the console will open in the Microsoft Edge web browser. This will result in an error.

**Work around:** Open the Operations Manager web console with Internet Explorer. Internet Explorer is available from  Windows Accessories sub-menu.

## Launching the Operations Manager Web Console may result in a blank screen
**Description:** When you first open the Operations Manager web console you may encounter a blank screen.

**Work around:** To resolve the issue:

1. Click on "Configure" button.
2. When prompted to Run or Save SilverlightClientConfiguration.exe, click Save.
3. Run SilverlightClientConfiguration.exe.
4. Open the file properties of exe (right-click) and open the Digital Signatures tab.
5. Select the certificate with Digest Algorithm as sha256 and click on Details.
6. In the Digital Signature Details dialog box, Click on View Certificate.
7. In the dialog box which appears next, click on Install Certificate.
8. In the Certificate Import Wizard, Set store location as - Local Machine. Click Next.
9. Select the option - "Place all certificates in the following store" Browse to Trusted Publishers.
10. Click Next and then Finish.
11. Refresh the Browser

## Next steps
To learn about new features and capabilities, see [What's new in System Center 2016 - Operations Manager](what-is-new.md).