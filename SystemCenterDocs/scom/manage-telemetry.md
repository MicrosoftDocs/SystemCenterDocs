---
ms.assetid: 8cfca640-efd9-450b-87cc-e1cda74cca7d
title: Manage telemetry settings in System Center Operations Manager
description: This article provides information about how to manage the telemetry settings in System Center Operations Manager
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic:  article
ms.service: system-center
ms.subservice: operations-manager
ms.custom: engagement-fy23, UpdateFrequency3, engagement-fy24
---

# Manage telemetry settings in Operations Manager

This article provides information about how to manage the telemetry (Diagnostics and utility data) settings in System Center - Operations Manager.

By default, Operations Manager sends diagnostic and connectivity data to Microsoft. Microsoft uses this data to provide and improve the quality, security, and integrity of Microsoft products and services.

Administrators can turn off this feature at any point of time. Learn more about [data collected by Operations Manager](#telemetry-data-collected).

## Turn on/off telemetry from console

1. In the Operations Manager console, select **Settings** in the Administration pane.

2. Under **Type: General**, double-click **Privacy**.

   ![Screenshot of console telemetry privacy.](./media/telemetry/telemetry-privacy.png)

   **Diagnostic and Usage Data Settings** options page appears.

   ![Screenshot of console telemetry options.](./media/telemetry/telemetry-options.png)

3. Select the diagnostic and usage data sharing preference from the options displayed, and select **OK**.

   > [!NOTE]
   > We recommend you to read the Privacy Statement before you select the option.
   > - To turn on telemetry, select **Yes, I am willing to send data to Microsoft**.
   > - To turn off telemetry, select **No, I prefer not to send data to Microsoft**.

## Telemetry data collected

The following table details the telemetry data that is collected by Operations Manager:  

| Data related To | Data collected |
| --- | --- |
| **Setup** | Version of installed System Center - Operations Manager <br /><br /> Version of the  installed System Center - Operations Manager update rollup on different System Center - Operations Manager core components<br /><br /> System Center - Operations Manager management group identifier (To weed out duplicates)<br /><br />  Unique machine identifier <br /><br />  Operating system on which different System Center - Operations Manager core components are launched <br /><br /> Language of the System Center - Operations Manager installation <br /><br /> CPU and memory values of different System Center - Operations Manager servers <br /><br /> Number of System Center - Operations Manager web servers installed <br /><br />  Is reporting server installed <br /><br />  Is ACS installed <br /><br />  Number of gateways in the System Center - Operations Manager environment <br /><br />  Number of management servers in the System Center - Operations Manager environment<br /><br />  Is Operational Insights account set up  
| **Device monitoring** |  Number of Unix/Linux computers monitored<br /><br /> Number of Windows computers monitored<br /><br /> Number of network devices monitored<br /><br /> Unix/Linux flavors monitored<br /><br /> Network devices being monitored - their type, model number, and certification status <br /><br /> Number of applications for which APM is active <br /><br /> Type of workloads for which APM is enabled<br /><br /> Number of distributed applications<br /><br /> Number of computers on which ACS is implemented<br /><br /> Maximum number of concurrent Web console sessions<br /><br /> Number of new SSRS reports present<br /><br /> Number of uncanned SSRS reports present<br /><br /> Frequency of canned reports use<br /><br /> Frequency of each PowerShell command use <br /><br />  Features used in the administration console <br /><br />  Complete Heatmap <br /><br /> Report Status |
| **Management packs** |	Number of management packs in the System Center - Operations Manager environment <br /><br /> Number of non-Microsoft signed packs <br /><br /> 	Management packs installed/version/manufacturer (Microsoft and Non-Microsoft) <br /><br /> 	Table names and row counts in the operational database <br /><br /> 	Table names and row counts in the data warehouse database <br /><br /> 	Details of partner products installed <br /><br />	Details of the Microsoft MP import failures and error involved <br /><br /> Details of the Top used management packs deployed with Operations Manager
| **SCOM Console** |  Time taken for the windows console to launch <br /><br /> 	Time taken for each of the monitoring screens to launch <br /><br /> 	Time taken for each of the administration screens to launch <br /><br /> 	Number of times network vicinity dashboard is launched <br /><br /> 	Number of times the data warehouse jobs are failing <br /><br /> 	Number of times the web console is being launched <br /><br /> 	Number of times the Maintenance mode task and SMM SDK calls are made for create and edit to determine adoption of new feature
| **Updates and recommendations** |	Number of times the Updates and Recommendations link clicked/refreshed<br /><br /> 	Number of times the online catalog was down while loading Updates and Recommendations view <br /><br />	Time taken to load the Updates and Recommendations view <br /><br /> 	Number of workloads in Updates and Recommendations view has Updates available status <br /><br /> 	Number of workloads in Updates and Recommendations view have Not installedstatus <br /><br /> 	Number of workloads in Updates and Recommendations view has Partially installed status <br /><br /> 	Number of workloads shown in Updates and Recommendation <br /><br />  Number of times  Get MP link is clicked in Updates and Recommendations view <br /><br /> 	Number of times Get All MPs link is clicked in Updates and Recommendations view <br /><br /> 	Number of times View Guide link is clicked in Updates and Recommendations view <br /><br /> 	Workload selected in Get MP call in Updates and Recommendations view <br /><br /> 	Workloads selected in Get All MPs call in Updates and Recommendations view <br /><br /> 	Workload install status in Get MP call in Updates and Recommendations view <br /><br /> 	Workloads install status in Get All MPs call in Updates and Recommendations view<br /><br /> 	Time taken to install workload in Get MP call in Updates and Recommendationsview <br /><br />	Time taken to install workloads in Get All MPs call in *Updates and Recommendations* view <br /><br /> Is the installation fresh or upgrade <br /><br /> 	TotalSetuptimeInMinutes <br /><br /> 	Is setup silent  <br /><br /> 	Is error reporting enabled <br /><br /> 	Is the Microsoft update true or false <br /><br /> 	Is the setup 64 bit <br /><br /> 	SetupDefaultInstallPath <br /><br /> 	Install result - success or failure
| **Database** | 	Whether the management server installation is fresh or upgrade<br /><br /> 	Whether the database (DB) installation is fresh or upgrade<br /><br /> 	Whether the data warehouse (DW) installation is fresh or upgrade <br /><br /> 	Default DB Name <br /><br /> 	DB Size in MB<br /><br /> 	DB Port <br /><br />	Is DB Local <br /><br /> 	DW Port <br /><br /> 	Is DW local <br /><br /> 	Is the SDK service using the local system account <br /><br /> 	Is the agent using the local system account <br /><br />
| **Console Settings** |	Web console default website<br /><br /> 	Web console authorization mode<br /><br /> 	Web console SSL enabled<br /><br /> 	Count of maintenance schedules <br /><br /> 	Count of active alerts<br /><br /> 	User role <br /><br /> 	Console version <br /><br /> 	If users are enabling daily health report <br /><br /> 	If users are enabling computer discovery <br /><br /> 	If users are discovering entire domain, or the selected one<br /><br /> 	If users are enabling Auto-Select for updates <br /><br />	Telemetry on/off notifications<br /><br /> 	Click count on Tune Management Pack View <br /><br />	Click count, total days, minimum alert count, and total result set <br /><br /> 	Click count, MP name, alert name, and alert count <br /><br /> 	Click count of View or edit the settings of this monitor <br /><br /> 	Click count of View or override sources <br /><br /> 	Click count, source MP name and override MP name <br /><br />  Nano servers count <br /><br /> 	Alert view click count <br /><br /> 	Health explorer click count on alert view action menu <br /><br /> 	Open command window click count on alert view action menu <br /><br /> 	Start maintenance mode click count on alert view action menu <br /><br /> 	End maintenance mode click count on alert view action menu <br /><br /> 	Edit maintenance mode click count on alert view action menu <br /><br /> 	Time spent on alert view <br /><br /> 	Total number of items displayed on alert view <br /><br /> 	Performance view click count <br /><br /> 	Time spent on performance view<br /><br />	State view click count <br /><br /> 	Time spent on state view <br /><br /> 	Total number of items displayed on state view <br /><br /> Overrides being used <br /><br /> If notification channels & subscriptions are set up <br /><br /> Type of notification channels configured

::: moniker range="sc-om-2016"

 In addition to the data in the above table, Operations Manager 2016 UR10 also collects the information about **the platform the setup is hosted on** as part of the data collected under **Setup**.

::: moniker-end

### Data collected through UTC

- SQL configuration of the System Center - Operations Manager environment (version/SP version/SQL Always ON/Cluster)
- Microsoft alerts that are marked as not useful and the reason
- Number of widgets, views, and dashboards created in *Monitoring* pane
- Number of dashboards in *My Workspace*
- Time taken to load the Scheduled Maintenance summary screen
- Average number of entities that are set to maintenance mode through Maintenance mode task and Scheduled Maintenance mode screen
- System Center ID the System Center - Operations Manager environment resides in
- Selected features

### HTML5 dashboards data collected through App Insights

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
- Instances of  *Add to MyWorkspace* action
- Count of alerts per widget
- Count of performance legends per widget
- Count of rows per state widget  
- Count of icons in topology widget
- Widget count in a dashboard

## Next steps

See [Plan agent deployment](plan-planning-agent-deployment.md)
