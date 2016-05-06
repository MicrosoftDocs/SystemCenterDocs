---
title: SNMP Events
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6c5bcfa-32e6-400d-8256-c083042f18a4
---
# SNMP Events
SNMP monitors and rules in [!INCLUDE[om12short](./Token/om12short_md.md)] allow you to retrieve messages from computers and devices that support Simple Network Management Protocol \(SNMP\). You can create rules and monitors that either wait for an SNMP trap to be sent or that retrieve information on a periodic basis using an SNMP probe.

## Target
Rules and monitors run on the agent computer of each instance of the target class, and they usually access data on the local computer. SNMP rules and monitors typically work with information from a computer or device different from the one running the monitors or rules. For SNMP traps, the monitor or rule needs to be running on the agent that receives the trap. The device needs to be configured to deliver traps to this agent. For SNMP probes, the monitor or rule needs to be running on any agent that is authorized to access the device with SNMP. The device may need to be configured to allow communication from this agent.

Network devices that are discovered with the Discovery Wizard are managed by a resource pool that you specify during the discovery process. A resource pool contains one or more management servers. You can use the classes for these devices as targets, and the rule or monitor will run on each computer in the resource pool. In this case, the device will need to send SNMP traps to each of the computers in the pool and allow access to each computer in the pool for SNMP probes.

## SNMP Event Wizards
The table below lists the wizards that are available for both simple and delimited text files.

|Management Pack Object|Wizards Available|
|--------------------------|---------------------|
|Monitors|SNMP probe monitor with single event reset|
|Monitors|SNMP trap monitor with single event reset|
|Rules|Alert Generating SNMP trap rule|
|Rules|Event collection SNMP probe rule|
|Rules|Event collection SNMP trap rule|
|Rules|Performance collection SNMP probe rule|

## SNMP Event Wizard Options
When you run an SNMP monitor wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### General
The **General** page includes general settings for the rule or wizard including its name, category, target, and the management pack file to store it in.

|Option|Description|
|----------|---------------|
|Name|The name used for the rule or monitor. For a rule, the name appears in the **Rules** view in the **Authoring** pane. When you create a view or report, you can select this name to use the data collected by it. For a monitor, the name appears in the Health Explorer of any target objects.|
|Description|Optional description of the rule or monitor.|
|Management Pack|Management pack file to store the rule or monitor.<br /><br />For more information on management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).|
|Rule Category \(Rules only\)|The category for the rule. For an event collection rule, this should be **Event Collection**. For a performance collection rule, this should be **Performance Collection**. For an alerting rule, this should be **Alert**.|
|Parent Monitor \(Monitors only\)|The aggregate monitor that the monitor will be positioned under in the Health Explorer. For more information, see [Aggregate Monitors](./Aggregate-Monitors.md).|
|Target|The class to use for the target of the rule or monitor. The rule or monitor will be run on any agent that has at least one instance of this class. For more information on targets, see [Understanding Classes and Objects](./Understanding-Classes-and-Objects.md).<br /><br />If you are monitoring a network device discovered in the Discovery Wizard, then use the class for the device or one of its components, depending on what the monitor most applies to.|
|Rule is enabled<br /><br />Monitor is enabled|Specifies whether the rule or monitor is enabled.|

### SNMP Probe \/ SNMP Trap Provider
SNMP probe rules have an **SNMP Probe** page, while SNMP trap rules have an **SNMP Trap Provider** page. SNMP monitors will have two of the appropriate page, one to define the healthy state and the other to define the warning or critical state. The page defines the community string and OID of the SNMP probe or trap.

|Option|Description|
|----------|---------------|
|Frequency \(Probe only\)|The frequency that the probe is run. A frequency that is configured too low can result in excess overhead on the device being monitored. A frequency that is configured too high can result in the monitor not detecting a problem quickly. A frequency from 2 minutes to 15 minutes is a common range.|
|Community string|If **Use discovery community string** is selected, then the community of the target device is used. If **Use custom community string** is selected, then you can specify a community string.|
|Object Identifier|For a probe, one or more Object Identifiers \(OID\) to retrieve from the device. A value for each one will be collected and available for evaluation in the expression. Most rules and monitors will use a single OID, but multiple OIDs can be used.<br /><br />For a trap, one or more Object Identifiers \(OID\) to listen for from the device. Most rules and monitors will use a single OID, but multiple OIDs can be used.|
|All Traps \(Trap only\)|If select, the **Object Identifier** list is disabled, and all traps from the target object will be collected, regardless of the OID.|

### Build Expression \(Monitors Only\)
SNMP monitors have a **Build Expression** page for each of the **SNMP Probe** or **SNMP Trap Provider** pages. The expression evaluates the SNMP data returned to determine the health state of the monitor.

For more information about expressions, [Expressions](./Expressions.md).

The **Parameter Name** in each expression requires a variable referring to a piece of data from the SNMP probe or trap. The data that is available includes header information and a data element for each OID specified. The header information is shown in the following table:

|Data Item|Description|
|-------------|---------------|
|Source|IP address of the device.|
|Destination|IP address of the agent receiving the event|
|CommunityString|Encrypted community string|
|ErrorCode|Error code returned by the request|
|Version|Version of SNMP used|

The information in each data element is shown in the following table:

|Data Item|Description|
|-------------|---------------|
|OID|OID of the data element|
|Syntax|Indicates the success or failure of the SNMP operation. If successful, the property is set to a value indicating the data type of the value. If unsuccessful, the property is set to a data type indicating the error. The specific values are listed in the documentation for the [SNMP Probe Module](http://go.microsoft.com/fwlink/?LinkID=230974).|
|Value|The value of the data element.|

To refer to the OID data elements, you can use the following syntax:

|Syntax|Example|Description|
|----------|-----------|---------------|
|SnmpVarBinds\/SnmpVarBind\/<ElementName>|SnmpVarBinds\/SnmpVarBind\/Value|Use this syntax when a single OID is used.|
|SnmpVarBinds\/SnmpVarBind\[\#\]\/<ElementName>|SnmpVarBinds\/SnmpVarBind\[2\]\/Value|Use this syntax when you have multiple OIDs and want to refer to each by its numeric order. The first OID is 1, the second is 2, and so on.|
|SnmpVarBinds\/SnmpVarBind\[OID\="<OID>"\]\/<ElementName>|SnmpVarBinds\/SnmpVarBind\[OID\="1.3.6.1.2.1.1.5.0"\]\/Value|Use this syntax when you have multiple OIDs and want to refer to each by the specific OID.|

### Configure Health
The **Configure Health** page is only available for monitors. It allows you to specify the health state that will be set for each of the events. The first event will typically set the monitor to **Warning** or **Critical** while the second event or the timer will set the monitor to **Healthy**.

### Configure Alerts
The **Configure Alerts** page is only available for monitors and alerting rules. Its options are explained in [Alerts](./Alerts.md).

## Creating SNMP Monitors and Rules

### Creating an SNMP Rule
Use the following procedure to create an SNMP performance collection rule in [!INCLUDE[om12short](./Token/om12short_md.md)] with the following details:

-   Runs on all network devices by using Node for the target.

-   Collects the number of open TCP connections \(OID 1.3.6.1.2.1.6.9.0\) every 10 minutes.

##### To create an SNMP Performance Collection Rule

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

2.  In the Operations console, select the **Authoring** workspace, and then select **Rules**.

3.  Right\-click **Rules** and select **Create a new rule**.

4.  On the **Rule Type** page, do the following:

    1.  Expand **Collection Rules**, expand **Performance Based**, and then click **SNMP Performance**.

    2.  Select the management pack from step 1.

    3.  Click **Next**.

5.  On the **General** page, do the following:

    1.  In the **Rule Name** box, type **Collect Open TCP Connections**.

    2.  In the **Rule Category** box, select **Performance Collection**.

    3.  Next to **Rule Target** click **Select** and then select **Node**.

    4.  Leave **Rule is enabled** selected.

    5.  Click **Next**.

6.  On the **SNMP Probe** page, do the following:

    1.  In the **Frequency** box, **10 minutes**.

    2.  In the **Object Identifier** box, type **1.3.6.1.2.1.6.9.0** and press ENTER.

    3.  Click **Create**.

### Creating an SNMP Monitor
Use the following procedure to create an SNMP trap monitor [!INCLUDE[om12short](./Token/om12short_md.md)] with the following details:

-   Runs on all network devices by using Node for the target.

-   Monitors for the status of a port. Link down is indicated with OID .1.3.6.1.6.3.1.1.5.3. Link up is indicated with OID .1.3.6.1.6.3.1.1.5.4.

-   Monitors port 16 only. This is indicated by Object Identifier .1.3.6.1.2.1.2.2.1.8.16 with a value of 2 for link down and Object Identifier .1.3.6.1.2.1.2.2.1.8.16 with a value of 1 for link up.

-   Includes the OID and value for the first four entries in the SNMP data.

##### To create an SNMP Trap monitor

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

2.  In the Operations console, select the **Authoring** workspace.

3.  Right\-click **Monitors**, select **Create a Monitor**, and then select **Unit Monitor**.

4.  On the **Monitor Type** page, do the following:

    1.  Expand **SNMP**, then **Trap Based Detection**, then **Simple Trap Detection**, and then **SNMP Trap Monitor**.

    2.  Select the management pack from step 1.

    3.  Click **Next**.

5.  On the **General** page, do the following:

    1.  In the **Name** box, type **Port active**.

    2.  Click **Select** next to the **Monitor Target** box.

    3.  Select **Node** and click **OK**.

    4.  In the **Parent Monitor** box, select **Availability**.

    5.  Leave the **Monitor is enabled** box checked, select and click **Next**.

6.  On the **First SnmpTrapProvider** page, do the following:

    1.  In the **Object Identifier** box, type **.1.3.6.1.6.3.1.1.5.3** and press ENTER.

    2.  Click **Create**.

7.  On the **Build First Expression** page, do the following:

    1.  Click **Insert**.

    2.  In the **Parameter Name** box type  **SnmpVarBinds\/SnmpVarBind\[OID\=".1.3.6.1.2.1.2.2.1.8.16"\]\/Value**.

    3.  In the **Operator** box select **Equals**.

    4.  In the **Value** box type **2**.

    5.  Click **Next**.

8.  On the **Second SnmpTrapProvider** page, do the following:

    1.  In the **Object Identifier** box, type **.1.3.6.1.6.3.1.1.5.4** and press ENTER.

    2.  Click **Create**.

9. On the **Build Second Expression** page, do the following:

    1.  Click **Insert**.

    2.  In the **Parameter Name** box type **SnmpVarBinds\/SnmpVarBind\[OID\=".1.3.6.1.2.1.2.2.1.8.16"\]\/Value**.

    3.  In the **Operator** box select **Equals**.

    4.  In the **Value** box type **1**.

    5.  Click **Next**.

10. On the **Configure Health** page, do the following:

    1.  Next to **FirstEventRaised**, change the **Health State** to **Critical**.

    2.  Click **Next**.

11. On the **Configure Alerts** page, do the following:

    1.  Check **Generate alerts for this monitor**

    2.  In the **Generate an alert when** box, select **The monitor is in a critical health state**.

    3.  Leave the box selected to automatically resolve the alert.

    4.  In the **Alert name** box, type **Port active**

    5.  Click the ellipse button next to the **Alert description** box.

    6.  Clear the contents of the **Value** box.

    7.  Click **Data** and then **Source**. Press ENTER.

    8.  Click **Data** and then **Destination**. Press ENTER.

    9. Click **Data**, then **SnmpVarBinds**, then **SnmpVarBind**, and then **OID**.

    10. In the variable, change **\[<<INT>>\]** to **\[1\]**.

    11. Type a space after the variable.

    12. Click **Data**, then **SnmpVarBinds**, then **SnmpVarBind**, and then **Value**.

    13. In the variable, change **\[<<INT>>\]** to **\[1\]**.

    14. Repeat the previous steps to add the OID and value for entries 2, 3, and 4.

    15. Click **OK**.

12. Click **Create**.

## See Also
[Monitoring Networks by Using Operations Manager](./Monitoring-Networks-by-Using-Operations-Manager.md)
[How to Discover Network Devices in Operations Manager](./How-to-Discover-Network-Devices-in-Operations-Manager.md)


