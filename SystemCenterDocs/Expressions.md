---
title: Expressions
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e4020ce-75c5-4c17-8719-baeeafd546a5
---
# Expressions
Wizards for creating monitors and rules will often require you to enter an expression that specifies criteria for the data being collected. The monitor or rule will only apply if the expression is true.

For example, you might have a rule that creates an alert for a particular event. You don’t want an alert for every single event that writes to the event log, so you specify the event number and event source in the expression. The rule will analyze all events that are written to the event log, but it will only generate an alert for those events with the specified source and number.

An expression may be simple with only a single criterion, or it may be a compound expression with multiple criteria and complex logic. Most expressions that you create will have only one or two criteria with very few using complex logic.

The syntax that you use for the expression will be different for different kinds of data sources. For some data source, you will be able to select criteria for a dialog box which keeps you from having to understand the underlying syntax. For other data sources, you will have to know the appropriate syntax and type it in. The following sections provide you with the details of the criteria for each data source.

## <a name="Syntax"></a>Criteria Syntax
A single piece of criteria is comprised of a *Parameter Name*, an *Operator*, and a *Value*. Each of these is described in detail in the following sections.

### Parameter Name
The *parameter name* specifies a parameter from the data source for the rule or monitor. The syntax of the parameter name will be different depending on the type of data being collected.  The syntax of the parameter name will be different depending on the type of data being collected.

The sections below provide the parameter name syntax for different kinds of data sources.

#### Windows Events
Windows events provide a prompt in the expression dialog box to select individual properties so you will typically not have to understand the actual syntax. The list of properties with their description is at [Windows Events](Windows-Events.md).

Event Description is not included in the dropdown list for property name. It can be used by typing in **EventDescription**. Before using Event Description though, you should verify whether the information that you are using in the description is available in parameters. Event descriptions are often made up of standard text with unique information included through parameters. Parameters are more efficient that the full description since they contain a specific piece of information.

#### Text Logs
Text Logs do not provide a prompt for the parameter name, so you need to type it in using the appropriate syntax. There are two types of text logs: Generic Text Logs where each line is processed as a single entry and Generic CSV Text Logs which use a delimiter to separate the fields of each entry.

For a Generic Text Log, the entire entry is referred to with a single parameter using the following syntax:

```
Params/Param[1]
```

For a Generic CSV Text Log, each field of the entry is referred to with a separate parameter for each field of the entry using the following syntax where \# refers to the number of the field starting with 1:

```
Params/Param[#]
```

Further details on text log expressions are available at [Event Expression](Text-Logs.md#Expression).

#### WMI Events
WMI Events do not provide a prompt for the parameter name, so you need to type it in using the appropriate syntax.

The properties available for a WMI event will vary, depending on the kind of event being monitored. The data will be in the form of a property bag that has a collection of properties for one or more WMI class instances. WMI events created by using a query that uses either \_\_InstanceCreationEvent or \_\_InstanceDeletionEvent will have a single collection called TargetInstance with the instance being either created or deleted. WMI events created by using \_\_InstanceModificationEvent will have an additional collection called PreviousInstance.

The syntax for properties from a WMI event is as follows:

```
Collection[@Name='TargetInstance']/Property[@Name='Caption']
```

Further details on WMI Events are available at [WMI Events](WMI-Events.md).

#### Syslog Events
Syslog Events do not provide a prompt for the parameter name, so you need to type it in using the appropriate syntax. The syntax for the properties of a syslog event is simply the name of the property. These properties are listed in [Syslog Events](Syslog-Events.md).

#### SNMP Events
SNMP probes and traps do not provide a prompt for the parameter name, so you need to type it in using the appropriate syntax. The syntax for the properties in the header of an SNMP probe or trap is simply the name of the property.

When a single OID is used:

```
SnmpVarBinds/SnmpVarBind/ElementName
```

When you have multiple OIDs and want to refer to each by its numeric order. The first OID is 1, the second is 2, and so on:

```
SnmpVarBinds/SnmpVarBind[#]/ElementName
```

When you have multiple OIDs and want to refer to each by the specific OID:

```
SnmpVarBinds/SnmpVarBind[OID="OID"]/ElementName
```

Further details on SNMP events are listed in [SNMP Events](SNMP-Events.md).

#### Scripts
Scripts do not provide a prompt for the parameter name, so you need to type it in using the appropriate syntax. Monitoring scripts output information in the form of a property bag that includes one or more values. The parameter specifies the name of one of the values from the property bag using the following syntax:

```
Property[@Name="PropertyName"]
```

Further details on monitoring scripts are available at [Script Monitors and Rules](Script-Monitors-and-Rules.md).

### Operator
The *operator* specifies the comparison that will be performed between the value from the data property specified in **Parameter Name** and the value specified in **Value**. Possible values are shown in the following table.

|Operator|Description|
|------------|---------------|
|Equals|The string or number specified in the data is exactly equal to the string or number specified in Value. If this is a string value, the comparison is not case sensitive.|
|Does not equal|The string or number specified in the data is not exactly equal to the string or number specified in Value. If this is a string value, the comparison is not case sensitive.|
|Greater than|The value in the data is greater than the number specified in Value.|
|Greater than or equal to|The value in the data is greater than or equal to the number specified in Value.|
|Less than|The value in the data is less than the number specified in Value.|
|Less than or equal to|The value in the data is less than or equal to the number specified in Value.|
|Contains|The string specified in Value appears somewhere in the data.|
|Does not contain|The string specified in Value does not appear somewhere in the data.|
|Matches wildcard|The string specified in Value matches the string including wildcard. The wildcard character is \* and represents any number of characters.|
|Does not match wildcard|The string specified in Value does not match the string including wildcard. The wildcard character is \* and represents any number of characters.|
|Matches regular expression|The string in the data matches the regular expression specified in Value.|
|Does not match regular expression|The string in the data does not match the regular expression specified in Value.|

### Value
The value can be specific text or a number typed into the Value field. For example, a particular event might be defined by its source and number. These are both constant values that can be typed into the Value field.

A value can also come from a property on the target object. Any property on the target object or on any of the object’s parents can be used. You can view a list of the properties and their values for any object by viewing the object in the **Discovered Inventory** view.

Target properties have different values for different objects. For example, you might use **Logical Disk \(Server\)** as a target and require the total size of the disk in the criteria. Logical disks have a property called **Size \(Mbytes\)** that stores the total size of the disk. The value of this property will be different for different disks in the management group. When you use a target variable for the value, it will be evaluated separately for each object.

You can select a target property by clicking the ellipse button on the right of the criteria line. This will display a list of all available properties for the object that you selected for the target and that objects parents. If you select one of these properties, the appropriate target variable will be added to the criteria.

## Examples

### Windows Events
The following expression identifies a Windows event with a source of Contoso and an event number of 100.

|Parameter Name<br /><br />AND group \(all of these are true\)|Operator|Value|
|---------------------------------------------------------|------------|---------|
|Event ID|Equals|100|
|Event Source|Equals|Contoso|

The following expression identifies a Windows event with a source of Contoso, an event number of 100, and the word “Error” in parameter 1.

|Parameter Name<br /><br />AND group \(all of these are true\)|Operator|Value|
|---------------------------------------------------------|------------|---------|
|Event ID|Equals|100|
|Event Source|Equals|Contoso|
|Parameter 1|Equals|Error|

The following expression identifies a Windows event with a source of Contoso, an event number of 100, and the word “Error” anywhere in the description.

|Parameter Name<br /><br />AND group \(all of these are true\)|Operator|Value|
|---------------------------------------------------------|------------|---------|
|Event ID|Equals|100|
|Event Source|Equals|Contoso|
|EventDescription|Contains|Error|

### Text Logs
The following expression identifies an entry in a generic text log that contains the word “Error”.

|Parameter Name|Operator|Value|
|------------------|------------|---------|
|Params\/Param\[1\]|Contains|Error|

The following expression identifies an entry in a generic csv text log that contains the word “Error” in the third field.

|Parameter Name|Operator|Value|
|------------------|------------|---------|
|Params\/Param\[3\]|Equals|Error|

### Scripts
The following expression identifies a numeric value from a script called “PerfValue” that is between 10 and 20.

|Parameter Name<br /><br />AND group \(all of these are true\)|Operator|Value|
|---------------------------------------------------------|------------|---------|
|Property\[@Name\="PerfValue"\]|Greater than|10|
|Property\[@Name\="PerfValue"\]|Less than|20|


