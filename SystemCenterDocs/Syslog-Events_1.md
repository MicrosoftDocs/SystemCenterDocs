---
title: Syslog Events_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ab4dc57-93db-4a66-97ff-684f5ddcfca6
---
# Syslog Events_1
Syslog events can be used to collect messages from Unix systems and other devices in [!INCLUDE[om12short](../Token/om12short_md.md)]. Syslog rules can be run on an agent that is the receiver of messages from one or more devices. When the rule is run, the agent will listen for messages on UDP port 514. This is the only port that can be used.

## Target
Rules and monitors run on the agent computer of each instance of the target class, and they usually access data on the local computer. SNMP rules and monitors typically work with information from a computer or device different from the one running the monitors or rules. For SNMP traps, the monitor or rule needs to be running on the agent that receives the trap. The device needs to be configured to deliver traps to this agent. For SNMP probes, the monitor or rule needs to be running on any agent that is authorized to access the device with SNMP. The device may need to be configured to allow communication from this agent.

Network devices that are discovered with the Discovery Wizard are managed by a resource pool that you specify during the discovery process. A resource pool contains one or more management servers. You can use the classes for these devices as targets, and the rule or monitor will run on each computer in the resource pool. In this case, the device will need to send SNMP traps to each of the computers in the pool and allow access to each computer in the pool for SNMP probes.

## Syslog Event Wizards
The table below lists the wizards that are available for both simple and delimited text files.

|Management Pack Object|Wizards Available|
|--------------------------|---------------------|
|Monitors|None|
|Rules|Alert Generating rule|
|Rules|Event collection rule|

## Syslog Event Wizard Options
When you run a Syslog event rule wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### General
The **General** page includes general settings for the rule including its name, category, target, and the management pack file to store it in.

|Option|Description|
|----------|---------------|
|Name|The name used for the rule. The name appears in the **Rules** view in the **Authoring** pane. When you create a view or report, you can select this name to use the data collected by it.|
|Description|Optional description of the rule.|
|Management Pack|Management pack file to store the rule or monitor.<br /><br />For more information on management packs, see [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).|
|Rule Category \(Rules only\)|The category for the rule. For an event collection rule, this should be **Event Collection**. For an alerting rule, this should be **Alert**.|
|Parent Monitor \(Monitors only\)|The aggregate monitor that the monitor will be positioned under in the Health Explorer. For more information, see [Aggregate Monitors](../Topic/Aggregate-Monitors.md).|
|Target|The class to use for the target of the rule. The rule will be run on any agent that has at least one instance of this class. For more information on targets, see [Understanding Classes and Objects](../Topic/Understanding-Classes-and-Objects.md).|
|Rule is enabled|Specifies whether the rule is enabled.|

## Build Event Expression
The **Build Event Expression** page allows you to filter for specific events to be collected or to generate an alert. The Syslog data properties are shown in the following table:

|Property Name|Description|
|-----------------|---------------|
|Facility|The facility of the event that uses one of the values from the table that follows.|
|Severity|Numeric value that indicates the severity of the event using one of the following values:<br /><br />-   0 \- Emergency<br />-   1 \- Alert<br />-   2 \- Critical<br />-   3 \- Error<br />-   4 \- Warning<br />-   5 \- Notice<br />-   6 \- Info<br />-   7 \- Debug|
|Priority|Numeric priority of the message.|
|PriorityName|Text description of the priority level.|
|TimeStamp|Time that the message was sent.|
|HostName|Name of the device sending the message.|
|Message|Text of the message|

> [!IMPORTANT]
> The event expression will almost always contain the Host Name in addition to one or more properties depending on the criteria that you require. Since a single management server may receive messages from multiple network devices, it must be able to determine which device sent a particular event. If the Host Name is not in the criteria, then a single event will most likely create a separate alert for each device.

### Facility Values
The value for the **facility** property defines the part of the system that the message originated from. It will have one of the values from the following table:

|Facility|Description|Value|
|------------|---------------|---------|
|0|Kernel|Kernel messages|
|1|User|User\-level messages|
|2|Mail|Mail System|
|3|Daemons|System daemons|
|4|Auth|Security and authorization|
|5|Syslog|Syslog internal messages|
|6|LPR|Line printer subsystem|
|7|News|Network news|
|8|UUCP|Unix\-to\-Unix copy program|
|9|Cron|Cron daemon|
|10|Auth2|Security and authorization|
|11|FTP|FTP daemon|
|12|NTP|Network time subsystem|
|13|LogAudit|Audit level|
|14|LogAlert|Message alert|
|15|Cron2|Cron daemon|
|16|Local0|Local use 0|
|17|Local1|Local use 1|
|18|Local2|Local use 2|
|19|Local3|Local use 3|
|20|Local4|Local use 4|
|21|Local5|Local use 5|
|22|Local6|Local use 6|
|23|Local7|Local use 7|

### Configure Alerts
The **Configure Alerts** page is only available for monitors and alerting rules. Its options are explained in [Alerts](../Topic/Alerts.md).

## Creating Syslog Event Rules
The following procedure shows how to create a Syslog event alerting rule in [!INCLUDE[om12short](../Token/om12short_md.md)] with the following details:

-   Runs on all network devices.

-   Generates an alert for any message with a severity of error or worse.

#### To create a Syslog event alerting rule

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).

2.  In the Operations console, select the **Authoring** workspace, and then select **Rules**.

3.  Right\-click **Rules** and select **Create a new rule**.

4.  On the **Rule Type** page, do the following:

    1.  Expand **Alert Generating Rules**, expand **Event Based**, and then click **Syslog \(Alert\)**.

    2.  Select the management pack from step 1.

    3.  Click **Next**.

5.  On the **General** page, do the following:

    1.  In the **Rule Name** box, type **Alert on syslog message**.

    2.  In the **Rule Category** box, select **Alert**.

    3.  Next to **Rule Target** click **Select**.

    4.  Select **View all targets**.

    5.  In the list of targets, select **Node** and then click **OK**.

    6.  Leave **Rule is enabled** selected.

    7.  Click **Next**.

6.  On the **Build Event Expression** page, do the following:

    1.  Click **Insert**.

    2.  In the **Parameter Name** box type **Severity**.

    3.  In the **Operator** box select **Less than or equal to**.

    4.  In the **Value** box type **3**.

    5.  Click **Insert**.

    6.  In the **Parameter Name** box type **HostName**.

    7.  In the **Operator** box select **Equals**.

    8.  Click the ellipse button next to **Value** and click **SNMP Agent Address**.

    9. Click **Next**.

7.  On the **Configure Alerts** page, do the following:

    1.  In the **Alert name** box, type **Syslog error message received**

    2.  In the **Alert description** box, type **$Data\/EventData\/DataItem\/Message$**.

    3.  Click **Create**.

## See Also
[Event Monitors and Rules](../Topic/Event-Monitors-and-Rules.md)
[Alerts](../Topic/Alerts.md)

