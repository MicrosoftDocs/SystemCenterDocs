---
title: Windows Events
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 836cd87d-c9fe-4b8e-86c4-f8bdd23cc995
author:markgalioto
---
# Windows Events
Many Windows\-based applications post information to events in a Windows event log. This could be a standard log such as **Application** or a log specific to the application being monitored. These events follow a standard format and frequently contain detailed information about the particular issue. If the application you are monitoring creates a Windows event in response to a particular issue, then this likely be the most effective way to detect the issue in an [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] management pack.  
  
When you create a rule or monitor that uses a Windows event, [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] continuously monitors the log and immediately responds when an event matching the specified criteria is detected. These events are persisted meaning that they are available after they are initially created. [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] will record the last position that it read in the log and continue from that position the next time it reads the log. If the health service on the agent is not running when a particular event is created, [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] will detect it the next time that the agent is started.  
  
## Windows Event Wizards  
The table below lists the wizards that are available for Windows events.  
  
**Monitors**  
  
|Wizards Available|  
|---------------------|  
|Simple Event Detection using each of the standard [Event Monitor Reset](../../om/manage/Event-Monitor-Reset.md) methods|  
|Repeated Event Detection using each of the standard [Event Monitor Reset](../../om/manage/Event-Monitor-Reset.md) methods|  
|Missing Event Detection using each of the standard [Event Monitor Reset](../../om/manage/Event-Monitor-Reset.md) methods|  
|Correlated Event Detection using each of the standard [Event Monitor Reset](../../om/manage/Event-Monitor-Reset.md) methods|  
|Correlated Missing Event Detection using each of the standard [Event Monitor Reset](../../om/manage/Event-Monitor-Reset.md) methods|  
  
**Rules**  
  
|Wizards Available|  
|---------------------|  
|Alert Generating Windows event rule|  
|Event collection Windows event rule|  
  
## Windows Event Wizard Options  
When you run a Windows event rule or monitor wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.  
  
### General  
The **General** page includes general settings for the rule or wizard including its name, category, target, and the management pack file to store it in.  
  
|Option|Description|  
|----------|---------------|  
|Name|The name used for the rule or monitor. For a rule, the name appears in the **Rules** view in the **Authoring** pane. When you create a view or report, you can select this name to use the data collected by it. For a monitor, the name appears in the Health Explorer of any target objects.|  
|Description|Optional description of the rule or monitor.|  
|Management Pack|Management pack file to store the rule or monitor.<br /><br />For more information on management packs, see [Selecting a Management Pack File](../../om/manage/Selecting-a-Management-Pack-File.md).|  
|Rule Category \(Rules only\)|The category for the rule. For an event collection rule, this should be **Event Collection**. For an alerting rule, this should be **Alert**.|  
|Parent Monitor \(Monitors only\)|The aggregate monitor that the monitor will be positioned under in the Health Explorer. For more information, see [Aggregate Monitors](../../om/manage/Aggregate-Monitors.md).|  
|Target|The class to use for the target of the rule or monitor. The rule or monitor will be run on any agent that has at least one instance of this class. For more information on targets, see [Understanding Classes and Objects](../../om/manage/Understanding-Classes-and-Objects.md).|  
|Rule is enabled<br /><br />Monitor is enabled|Specifies whether the rule or monitor is enabled.|  
  
### Event Log Type  
The **Event Log Type** page includes the name of the event log where you expect the event to be created. There will be a single **Event Log Type** page for a collection or alerting rule and for a monitor using manual or timer reset. For a monitor using **Windows Event Reset**, you will have to define the log for both the error condition and for the healthy condition. You will typically specify the same log for both conditions, but a different log could be used for each.  
  
You can type in the name of the event log in the **Log name** box, or you can click the ellipse button and select a log.  
  
### <a name="Criteria"></a>Event Expression  
In addition to the name of the log to retrieve events from, workflows using a Windows event must specify sufficient criteria to identify the particular events that relate to the issue being identified. Frequently, the **Event ID** and the **Event Source** will be sufficient for this purpose. This depends on the kind of information that the application provides in the particular event in addition to the target that is being used for the monitor. If the class being used as the target for the monitor is expected to have multiple instances on a particular agent, then these two properties are probably insufficient for uniqueness. Unless the criteria included a key property for the target class then the criteria would possibly apply to all instances.  
  
There will be a single **Event Log Type** page for each Event Log Type Page collection or alerting rule and for a monitor using manual or timer reset. For a monitor using **Windows Event Reset**, you will have to define the log for both the error condition and for the healthy condition. You will typically specify the same log for both conditions, but a different log could be used for each.  
  
The following table lists the properties available from Windows Events. These properties can be accessed for setting criteria in monitors and rules and can be included in alert descriptions.  
  
|Expression|Description|  
|--------------|---------------|  
|Event Source|Source of the event. Generally used in the criteria of the monitor or rule.|  
|Logname\/Channel|Name of the event log such as Application or System.|  
|Logging Computer|Name of the computer logging the event.|  
|Event ID|Number of the event.|  
|Event Category|Category of the event.|  
|Event Level|Severity of the event that uses one of the following values.<br /><br />-   Success \(0\)<br />-   Error \(1\)<br />-   Warning \(2\)<br />-   Information \(4\)<br />-   Success Audit \(8\)<br />-   Failure Audit \(16\)|  
|User|Name of the user account that was used to create the event.|  
|EventDescription|Full event description.|  
|Parameter|Collection of event parameters.|  
  
### Auto Reset Timer  
The **Auto Reset Timer** page is only available for timer reset monitors. It allows you to set the time that must pass after the alert is created before the alert is automatically resolved.  
  
### Configure Health  
The **Configure Health** page is only available for monitors. It allows you to specify the health state that will be set for each of the events. For a manual reset monitor, the **Manual Reset** condition will be **Healthy**, and you can specify whether the **Event Raised** condition will set the monitor to a **Warning** or a **Critical** state. For a **Timer Reset** or a **Windows Event Reset**, you can specify the health state set by each event. The first event will typically set the monitor to **Warning** or **Critical** while the second event or the timer will set the monitor to **Healthy**.  
  
### Configure Alerts  
The **Configure Alerts** page is only available for monitors and alerting rules. Its options are explained in [Alerts](../../om/manage/Alerts.md).  
  
## <a name="Procedures"></a>Creating Windows Event Monitors  
  
### How to create a Windows event monitor  
Use the following procedure to create an event monitor in [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] with the following details:  
  
-   Runs on all agents with a particular service installed.  
  
-   Sets the monitor to a **critical** state when an event in the **Application** event log with an event source of **EventCreate**and an event number of **101** is detected.  
  
-   Sets the monitor to a **healthy** state when an event in the **Application** event log with an event source of **EventCreate**and an event number of **102** is detected.  
  
> [!NOTE]  
> **EventCreate** is used as the event source so that the EventCreate utility can be used to create a test event. This utility is available on any Windows Computer and creates test events with a source of **EventCreate**. If you have another method of creating test events, then you can use a different source.  
  
##### To create an event monitor  
  
1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](../../om/manage/Selecting-a-Management-Pack-File.md).  
  
2.  Create a new target using the process in [To create a Windows Service template](../../om/manage/Windows-Service-Template.md#CreateWindowsServiceTemplate). You can use any service installed on a test agent for this template.  
  
3.  In the Operations console, select the **Authoring** workspace.  
  
4.  Select **Management Pack Objects**.  
  
5.  Right\-click **Monitors**, select **Create and Monitor**, and then select **Unit Monitor**.  
  
6.  On the **Monitor Type** page, do the following:  
  
    1.  In the **Select the type of monitor to create** box, expand **Windows Events** and then **Simple Event Detection**.  
  
    2.  Select **Windows Event Reset**.  
  
    3.  In the **Management Pack** dropdown list, select the management pack for the application.  
  
    4.  Click **Next**.  
  
7.  On the **General** page, do the following:  
  
    1.  In the **Name** box, type **Error event 101** or another name for the monitor. This is the text that will appear in the Health Explorer.  
  
    2.  Click **Select**.  
  
    3.  In the **Select Items to Target** dialog box, select the name that you used for the Windows Service template in step 2.  
  
    4.  The **Parent monitor** box should show **Availability**. You can select a different parent monitor.  
  
    5.  Ensure that **Availability** is selected for the **Parent monitor**.  
  
    6.  The **Monitor is enabled** box should be checked so that the monitor is enabled.  
  
    7.  Click **Next**.  
  
8.  On the **Event Log \(Unhealthy Event\)** page, do the following:  
  
    1.  In the **Log Name** box, keep the default value of **Application**.  
  
    2.  Click **Next**.  
  
9. On the **Event Expression \(Unhealthy Event\)** page, do the following:  
  
    1.  For the **Event ID** value, type **101**  
  
    2.  For the **Event Source** value, type **EventCreate**  
  
    3.  Click **Next**.  
  
10. On the **Event Log \(Healthy Event\)** page, do the following:  
  
    1.  In the **Log Name** box, keep the default value of **Application**.  
  
    2.  Click **Next**.  
  
11. On the **Event Expression \(Healthy Event\)** page, do the following:  
  
    1.  For the **Event ID** value, type **102**  
  
    2.  For the **Event Source** value, type **EventCreate**  
  
    3.  Click **Next**.  
  
12. On the **Configure Health** page, do the following:  
  
    1.  For **FirstEventRaised**, change the **Health State** to **Critical**.  
  
    2.  For the **Event Source** value, type **EventCreate**  
  
    3.  Click **Next**.  
  
13. On the **Configure Alerts** page, do the following:  
  
    1.  Select **Generate alerts for this monitor**.  
  
    2.  Click **Create**.  
  
## See Also  
[Event Monitors and Rules](../../om/manage/Event-Monitors-and-Rules.md)  
[Event Monitor Logic](../../om/manage/Event-Monitor-Logic.md)  
[Event Monitor Reset](../../om/manage/Event-Monitor-Reset.md)  
[Alerts](../../om/manage/Alerts.md)  
  
