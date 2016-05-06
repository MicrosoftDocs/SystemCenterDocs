---
title: Alerts_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f8c6185-c55c-4e37-8e6e-8f49c5e45675
---
# Alerts_1
Alerts in [!INCLUDE[om12short]./Token/om12short_md.md)] can be generated from either monitors or rules. While the Operations console does not distinguish between each type, there are distinct differences between the two that you should understand when defining monitors and rules. The sections below provide the alert properties that you will need to define when you configure a monitor to generate an alert or if you create an alerting rule.

## <a name="Alerts"></a>Alerts from Monitors
An alert will only be generated from a monitor if each of the following is true:

-   The monitor is configured to generate an alert.

-   The health state of the monitor changed from a Healthy State to a Warning or Error state, depending on the possible health states of the monitor.

-   An open alert does not already exist for the same object created by the same monitor.

Alerts are only generated from a monitor when the health state of the monitor changes from a Healthy state. Even though the criteria for the error condition may occur multiple times, multiple alerts will not be generated once the health state of the monitor is set to Warning or Critical. Only after the health state of the monitor returns to Healthy and the error condition occurs again will a new alert be generated.

For example, consider a Windows Event monitor that is configured to set a Critical state when an event with number 101 is detected and reset the monitor when an event with number 100 is detected. When the first event 101 is created, the monitor is set to a Critical state and an alert is generated. Even though you may close the alert, if an additional event 101 is detected a new alert is not created because the monitor did not change its state. Only after the monitor is reset, either by detecting an event 100 or by you manually resetting it, and an event 101 is detected will an alert be generated.

### Alert Name
The name of the alert is a single line of static text and cannot include any variables.

### Priority and Severity
The Alert severity defines the alert as either Information, Warning, or Critical. This severity does not have to match the severity of the health state triggering the alert. The severity of the alert is identified by an icon in the Operations console and is used by views and notification subscriptions. The alert priority is inaccessible in the Operations console but is used primarily for notification subscriptions.

### Alert Description
The alert description may have several lines of text that includes a combination of static text and variables. The most common kind of variable in the alert description will be $Data variables to include different information from the monitor’s data source in the description of the alert. The properties that are available will depend on the kind of data source being used.

The table below provides syntax and examples of variables in alerts created from monitors.

|Data Source|Syntax|Examples|
|---------------|----------|------------|
|Windows Event|$Data\/Context\/<Property Name>$|$Data\/Context\/EventDescription$|
|Windows Event|$Data\/Context\/Params\/Param\[\#\]$|$Data\/Context\/Params\/Param\[2\]$|
|Text Log|$Data\/Context\/<Property Name>$|$Data\/Context\/LogFileName$|
|Text Log|$Data\/Context\/Params\/Param\[1\]$|$Data\/Context\/Params\/Param\[1\]$|
|Delimited Text Log|$Data\/Context\/<Property Name>$|$Data\/Context\/LogFileName$|
|Delimited Text Log|$Data\/Context\/Params\/Param\[\#\]$|$Data\/Context\/Params\/Param\[2\]$|
|WMI Event|$Data\/Context\/Collection\[@Name\='<TargetInstance&#124;PreviousInstance>'\]\/Property\[@Name\='<PropertyName>'\]$|$Data\/Context\/Collection\[@Name\=’TargetInstance’\]\/Property\[@Name\='Name'\]$|
|Windows Performance|$Data\/Context\/<PropertyName>\]$|$Data\/Context\/Value$|
|WMI Performance|$Data\/Context\/<PropertyName>\]$|$Data\/Context\/Value$|
|Monitoring Script|$Data\/Context\/Property\[@Name\='<PropertyName>'\]$|$Data\/Context\/Property\[@Name\='Result'>'\]$|

### Automatic Alert Resolution
Monitors that create alerts can be configured to automatically resolve the alert when the monitor returns to a healthy state. This means that any unresolved alert for the monitor represents a problem that still exists. There is no configuration this requirement other than confirming the option that automatic resolution be performed.

> [!NOTE]
> Automatic alert resolution cannot be performed with rules because rules do not have any means of detecting that the problem has been corrected.

## <a name="Rules"></a>Alerts from Rules
An alert will only be generated from a rule under the following conditions:

-   The rule is configured to generate an alert.

-   The criteria defined in the rule is true.

-   An open alert does not already exist that matches the alert’s suppression configuration.

The table below discusses the ability of each type of rule to generate an alert.

|Rule Type|Alert Capabilities|
|-------------|----------------------|
|Event Rules|Alert rules can be created for each event data source. The criteria that is specified to determine when an alert should be created is the same as the criteria for a state change in the event monitors.|
|Performance Rules|You cannot create an alert rule based on a performance counter. A monitor should be used instead because a success condition is usually detectable from a performance counter and is usually related to some health state of the target class.|
|Scripting Rules|You cannot create an alert rule based on a script. A monitor should be used instead because a script will typically provide a return value for both and error and a healthy state in such a way that a success condition is usually detectable and related to some health state of the target class.|

### Alert Name
The name of the alert is a single line of static text and cannot include any variables.

### Priority and Severity
The Alert severity defines the alert as either Information, Warning, or Critical. This severity does not have to match the severity of the health state triggering the alert. The severity of the alert is identified by an icon in the Operations console and is used by views and notification subscriptions. The alert priority is inaccessible in the Operations console but is used primarily for notification subscriptions.

### Alert Description
The alert description may have several lines of text that includes static text or variables. The most common kind of variable in the alert description will be $Data variables to include different information from the rule’s data source in the description of the alert. The properties that are available will depend on the kind of data source being used. Each section of [Data Sources](./Data-Sources.md) includes a list of the properties available for different data sources.

The following table provides syntax and examples of variables in alerts created from rules:

|Data Source|Syntax|Examples|
|---------------|----------|------------|
|Windows Event|$Data\/<Property Name>$|$Data\/EventDescription$|
|Windows Event|$Data\/Params\/Param\[\#\]$|$Data\/Params\/Param\[2\]$|
|Text Log|$Data\/EventData\/DataItem\/<PropertyName>$|$Data\/EventData\/DataItem\/LogFileName$|
|Text Log|$Data\/EventData\/DataItem\/Params\/Param\[1\]$|$Data\/EventData\/DataItem\/Params\/Param\[1\]$|
|Delimited Text Log|$Data\/EventData\/DataItem\/<PropertyName>$|$Data\/EventData\/DataItem\/LogFileName$|
|Delimited Text Log|$Data\/EventData\/DataItem\/Params\/Param\[\#\]$|$Data\/EventData\/DataItem\/Params\/Param\[2\]$|
|WMI Event|$Data\/EventData\/DataItem\/Collection\[@Name\='<TargetInstance &#124; PreviousInstance>'\]\/Property\[@Name\='<PropertyName>'\]$|$Data\/EventData\/DataItem\/Collection\[@Name\='TargetInstance'\]\/Property\[@Name\='Name'\]$|
|Syslog Event|$Data\/EventData\/DataItem\/<PropertyName>$|$Data\/EventData\/DataItem\/Facility$|

### Alert Suppression
*Alert suppression* refers to logic that is defined on alert rules to suppress the creation of an alert when a corresponding alert is still open. This prevents alert storms where multiple alerts are created for the same issue. Because the issue has already been identified with an open alert, creation of additional alert creates unnecessary noise with minimal value. When the condition for an alerting rule is met but an existing alert is already open, instead of creating an additional alert suppression will increase the repeat count of the existing alert.

In order to define suppression on an alerting rule, the fields must be specified that identify a matching alert. Before an alerting rule creates a new alert, it will check whether an open alert exists with values for the fields that are defined for suppression that match the values in the same fields of the new alert. If an alert with matching values for each of these fields is open, then a new alert is not created.

The minimum number of fields that uniquely identify the alert should be specified for alert suppression. This will typically be the computer name in addition to the fields used for the criteria of the rule. For example, suppression on event rules can frequently be achieved by using the following fields:

-   Logging Computer

-   Event Source

-   Event Number

If the rule is targeted at a class that has multiple instances on an agent, however, then a parameter might be required to uniquely identify the event in the criteria of the rule. If this is the case, then the same parameter should be specified in the alert suppression.

> [!NOTE]
> Alert suppression is not available for monitors because it is not required. Monitors only generate alerts when their state changes from healthy to warning or critical. Even if the detected issue occurs again when the monitor is already in the negative state, then no alert is generated because the monitor state does not change. A new alert is only generated if the monitor returns to a healthy state before the problem occurs.



