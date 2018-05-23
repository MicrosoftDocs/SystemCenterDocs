---
ms.assetid: 8cfca640-efd9-450b-87cc-e1cda74cca7d
title: Manage telemetry settings in System Center Operations Manager
description: This article provides information about how to manage the telemetry settings in System Center Operations Manager
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  05/22/2018
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology: operations-manager
---

# Manage telemetry settings in Operations Manager

This article provides information about how to manage the telemetry (Diagnostics and utility data) settings in System Center - Operations Manager (SCOM).

By default, Operations Manager  sends diagnostic and connectivity data to Microsoft. Microsoft uses this data to provide and improve the quality, security, and integrity of Microsoft products and services.

Administrators can turn off this feature at any point of time. Learn more about [data collected by Operations Manager](#data-collected)

## Turn on/off telemetry from console

1. In the Operations Manager console, click **Settings** in the Administration pane.

2. Under **Type: General**, double-click **Privacy**.

  ![console telemetry privacy](./media/telemetry/telemetry-privacy.png)

  **Diagnostic and Usage Data Settings** options page appear.

  ![console telemetry options](./media/telemetry/telemetry-options.png)

3. Select the  diagnostic and usage data sharing preference from the options displayed, and click  **OK**.

  > ![NOTE]

  > We recommend you to read the Privacy Statement before you select the option.

  -  To turn on telemetry, select **Yes, I am willing to send data to Microsoft**.
  - 	To turn off telemetry, select **No, I prefer not to send data to Microsoft**.

## Telemetry data collected

**Data collected through UTC**

- Version of installed SCOM
- Version of the  installed SCOM update rollup on different SCOM core components
- SCOM management group identifier (To weed out duplicates)
- Unique machine identifier
- Operating system on which different SCOM core components are launched
- Language of the SCOM installation
- CPU and memory values of the different SCOM servers
- Number of SCOM web servers installed
- Is reporting server installed
- Is ACS installed
- Number of gateways in the SCOM environment
- Number of management servers in the SCOM environment
- Is Operational Insights account setup
- SQL configuration of the SCOM environment? (version/SP version/SQL Always ON/Cluster)
- Number of Unix/Linux machines monitored
- Number of Windows computers monitored
- Number of network devices monitored
- Unix/Linux favors monitored
- Network devices being monitored - their type, model number, and certification status.
- Number of applications for which APM is active
- Type of workloads for which APM is enabled
- Number of distributed applications
- Number of computers on which ACS is implemented
- Maximum number of concurrent Web console sessions
- Number of new SSRS reports present
- Number of Uncanned SSRS reports present
- How frequently are canned reports used
- Frequency of each PowerShell command use
- Features are used in the administration console. complete Heatmap
- Number of management packs in the SCOM environment
- Number of non-Microsoft signed packs
- Management packs installed/version/manufacturer (Microsoft and Non-Microsoft)
- Table names and row counts in the operational database
- Table names and row counts in the data warehouse database
- Which partner products are installed
- Time taken for the windows console to launch
-  Time taken for each of the monitoring screens to launch
- Time taken for each of the administration screens to launch
- Number of times network vicinity dashboard is launched
- Number of times the data warehouse jobs are failing
- Number of times the web console is being launched
- Number of times the Maintenance mode task and SMM SDK calls are made for create and edit to determine adoption of new feature
- Details of the Microsoft MP import failures and error involved
- Microsoft alerts that are marked as not useful and the reason
- Number of widgets, views, dashboards created in *Monitoring* pane
- Number of dashboards in *My Workspace*
- Time taken to load the Scheduled Maintenance summary screen
- Average number of entities that are set to maintenance mode through Maintenance mode task and Scheduled Maintenance mode screen
- Time taken for the setup to complete installation for the features chosen.  
- SQL configuration at setup time
- Errors observed by the users when they setup SCOM
- Are users entering a license key at the time of setup
- Number of customers  upgrading/ doing a full setup
- System Center ID the SCOM environment reside in
- Number of  times the *Updates and Recommendations* link clicked/refreshed
- Number of times the online catalog was down while loading *Updates and Recommendations* view
- Time taken to load the *Updates and Recommendations* view
- Number of workloads in *Updates and Recommendations* view has *Updates available* status
- Number of workloads in *Updates and Recommendations* view have *Not installed* status
- Number of workloads in *Updates and Recommendations* view has *Partially installed* status
- Number of workloads shown in *Updates and Recommendation*
- How many times *Get MP* link is clicked in *Updates and Recommendations* view
- Number of times *Get All MPs* link is clicked in *Updates and Recommendations* view
- Number of times *View Guide* link is clicked in *Updates and Recommendations* view
- Workload selected in *Get MP* call in *Updates and Recommendations* view
- Workloads selected in *Get All MPs* call in *Updates and Recommendations* view
- Workload install status in *Get MP* call in *Updates and Recommendations* view
- Workloads install status in *Get All MPs* call in *Updates and Recommendations* view
- Time taken to install workload in *Get MP* call in *Updates and Recommendations* view
- Time taken to install workloads in *Get All MPs* call in *Updates and Rec** view?
- Is the installation fresh or upgrade
- TotalSetuptimeInMinutes
- Is setup silent
- Is error reporting enabled
- Is the Microsoft update true or false
- Is the setup 64 bit
- SetupDefaultInstallPath
- Install result - success or failure
- Selected features
- Whether the management server installation is fresh or upgrade
- Whether the database (DB) installation is fresh or upgrade
- Whether the data warehouse (DW) installation is fresh or upgrade
- Default DB Name
- DB Size in MB
- DB Port
- Is DB Local
- Default DW Name
- DW Size in MB
- DW Port
- Is DW local
- Is the SDK service using the local system account
- Is the agent using the local system account
- Web console default website
- Web console authorization  mode
- Web console SSL enabled
- Count of maintenance schedules
- Count of active alerts
- User role
- Console version
- If users enabling daily health report
- If users are enabling computer discovery
- If users are discovering entire domain, or selected
- If users are enabling Auto-Select for updates
- Telemetry on/off notifications
- Click count on Tune Management Pack View
- Click count, total days, minimum alert count, and total result set
- Click count, MP name, alert name, and alert count
- Click count of *View or edit the settings of this monitor*
- Click count of *View or override sources*
- Click count, source MP name and override MP name
- Nano servers count
- Alert view click count
- Health explorer click count on alert view action menu
- Open command window click count on alert view action menu
- Start maintenance mode click count on alert view action menu
- End maintenance mode click count on alert view action menu
- Edit maintenance mode click count on alert view action menu
- Time spent on alert view
- Total number of items displayed on alert view
- Performance view click count
- Time spent on performance view
- State view click count
- Time spent on state view
- Total number of items displayed on state view

**HTML5 dashboards data collected through App Insights**

- All API exceptions
- User feedback
- Edited widget
- Authored widget
- launched widget
- Action clicked
- Personalized widget
- Instances when action *View in Full Screen* is clicked
- Dashboard edits
- Instances of drill-down page launch
- Instances of task pane launch
- Instances of *My Workspace*  launch
- Usage of *Windows Authentication*
- Usage of  *Alternate Credentials*
- When *Add to MyWorkspace* action is performed
- Count of alerts per widget
- Count of performance legends per widget
- Count of rows per state widget
- Count of icons in topology widget
- Widget count in a dashboard


## Next steps
[Plan agent deployment](plan-planning-agent-deployment.md)
