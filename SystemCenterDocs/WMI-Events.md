---
title: WMI Events
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3474a6f4-bca9-4492-a653-4459e19b1d2a
---
# WMI Events
*WMI events* are created from WMI queries that detect particular actions in the operating system or in applications that create their own WMI events. These events can be used to detect such actions as a process ending, a file being created, or a registry key being modified. WMI events are not persisted. Therefore, any WMI events that are created when the agent service is not running are lost.

> [!NOTE]
> This guide assumes knowledge of how to build a WMI notification query. For a an overview of this topic and sample queries see [Unlocking the Mystery of WMI Events in MOM](http://go.microsoft.com/fwlink/?LinkID=187607).

## WMI Event Wizards
The table below lists the wizards that are available for WMI events.

|||
|-|-|
|Management Pack Object|Wizards Available|
|Monitors|Simple Event Detection using each of the standard [Event Monitor Reset](./Event-Monitor-Reset.md) methods|
|Monitors|Repeated Event Detection using each of the standard [Event Monitor Reset](./Event-Monitor-Reset.md) methods|
|Rules|Alert Generating WMI event rule|
|Rules|Event collection WMI event rule|

## WMI Event Wizard Options
When you run a WMI event rule or monitor wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### General
The **General** page includes general settings for the rule or monitor including its name, category, target, and the management pack file to store it in.

|Option|Description|
|----------|---------------|
|Name|The name used for the rule or monitor. For a rule, the name appears in the **Rules** view in the **Authoring** pane. When you create a view or report, you can select this name to use the data collected by it. For a monitor, the name appears in the Health Explorer of any target objects.|
|Description|Optional description of the rule or monitor.|
|Management Pack|Management pack file to store the rule or monitor.<br /><br />For more information on management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).|
|Rule Category \(Rules only\)|The category for the rule. For an event collection rule, this should be **Event Collection**. For an alerting rule, this should be **Alert**.|
|Parent Monitor \(Monitors only\)|The aggregate monitor that the monitor will be positioned under in the Health Explorer. For more information, see [Aggregate Monitors](./Aggregate-Monitors.md).|
|Target|The class to use for the target of the rule or monitor. The rule or monitor will be run on any agent that has at least one instance of this class. For more information on targets, see [Understanding Classes and Objects](./Understanding-Classes-and-Objects.md).|
|Rule is enabled<br /><br />Monitor is enabled|Specifies whether the rule or monitor is enabled.|

### WMI Configuration \/ WMI Event Provider
The **WMI Configuration** Page allows you to provide the WMI namespace, query, and poll interval. There will be a single **WMI Configuration** page for a collection or alerting rule and for a monitor using manual or timer reset. For a monitor using **WMI Event Reset**, there will be a **WMI Event Provider** page to define the query for both the error condition and for the healthy condition.

|Option|Description|
|----------|---------------|
|WMI Namespace|The namespace containing the class that is used in the WMI query.|
|Query|WMI notification query that looks for the occurrence of a particular WMI event.|
|Poll Interval|Specifies how frequently [!INCLUDE[om12short](./Token/om12short_md.md)] will poll WMI for the occurrence of the event. This value should be the same as the value used in the WITHIN clause of the notification query.|

**WMI matching poll intervals**

![](/Image/AuthGuide_04_WMIPollInterval.gif)

### Build Expression
The **Build Expression** page allows you to define a filter for the data coming from the WMI query. There will be a single **Build Expression** page for a WMI event monitor using manual or timer reset. For a monitor using **WMI Event Reset**, there is an expression for each health state.

Because criteria can be specified in the WHERE clause of the WMI query, an expression is frequently not required in a WMI event monitor. It is only required if the query is expected to return multiple records. WMI event rules rely on the criteria in the query itself and don’t allow an expression. The Operations console wizards though require that criteria be specified in WMI Event monitors. If no criteria is required, then dummy criteria must be specified in the wizard and then removed by viewing the properties of the monitor after it is created.

The properties available for a WMI event will vary, depending on the kind of event being monitored. The properties available will also vary, depending on the properties of the WMI class included in the query. The data will be in the form of a property bag that has a collection of properties for one or more WMI class instances. WMI events created by using a query that uses either \_\_InstanceCreationEvent or \_\_InstanceDeletionEvent will have a single collection called TargetInstance with the instance being either created or deleted. WMI events created by using \_\_InstanceModificationEvent will have an additional collection called PreviousInstance.

The syntax for properties from a WMI event is as follows:

```
Collection[@Name='TargetInstance']/Property[@Name='Caption']
```

For example, the following WMI query monitors for the change in a file that is named c:\\MyApp\\MyAppLog.txt.

```scr
SELECT * FROM __InstanceModificationEvent WITHIN 60 WHERE TargetInstance ISA 'CIM_DataFIle' AND TargetInstance.Name = 'C:\\MyApp\\MyAppLog.txt'
```

Assuming that data is added to the file changing the file size and triggering the query, examples of properties from this query are shown in the following table:

|Property|Syntax|
|------------|----------|
|Original file size|Collection\[@Name\=’PreviousInstance’\]\/Property\[@Name\='FileSize'\]|
|New file size|Collection\[@Name\=’TargetInstance’\]\/Property\[@Name\='FileSize'\]|

### Auto Reset Timer
The **Auto Reset Timer** page is only available for timer reset monitors. It allows you to set the time that must pass after the alert is created before the alert is automatically resolved.

### Configure Health
The **Configure Health** page is only available for monitors. It allows you to specify the health state that will be set for each of the events. For a manual reset monitor, the **Manual Reset** condition will be **Healthy**, and you can specify whether the **Event Raised** condition will set the monitor to a **Warning** or a **Critical** state. For a **Timer Reset** or an **WMI Event Reset**, you can specify the health state set by each event. The first event will typically set the monitor to **Warning** or **Critical** while the second event or the timer will set the monitor to **Healthy**.

### Configure Alerts
The **Configure Alerts** page is only available for monitors and alerting rules. Its options are explained in [Alerts](./Alerts.md).

## Creating WMI event monitors and rules
The following procedure shows how to create a WMI event monitor in [!INCLUDE[om12short](./Token/om12short_md.md)] with the following details:

-   Runs on all agents with a particular service installed.

-   Sets the monitor to a **critical** state when Notepad is started on the agent computer.

-   Sets the monitor to a **healthy** state when Notepad is ended on the agent computer.

> [!NOTE]
> This example is not meant to illustrate a real world scenario since there would be minimal value in monitoring when Notepad is started. It does through represent a common scenario of monitoring two different WMI events in a monitor. Using Notepad provides a sample that is easy to test by starting and stopping Notepad on the agent computer.

#### To create a WMI event monitor

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

2.  Create a new target using the process in [To create a Windows Service template](./Windows-Service-Template.md#CreateWindowsServiceTemplate). You can use any service installed on a test agent for this template.

3.  In the Operations console, select the **Authoring** workspace.

4.  Right\-click **Monitors**, select **Create a Monitor**, and then select **Unit Monitor**.

5.  On the **Monitor Type** page, do the following:

    1.  Expand **WMI Events**, then **Simple Event Detection**, and then **WMI Event Reset**.

    2.  Select the management pack from step 1.

    3.  Click **Next**.

6.  On the **General** page, do the following:

    1.  In the **Name** box, type **MyApplication WMI Event Error**.

    2.  Click **Select** next to the **Monitor Target** box.

    3.  Next to **Monitor Target** click **Select** and then select the name of the target that you created in step 2.

    4.  In the **Parent Monitor** box, select **Availability**.

    5.  Leave the **Monitor is enabled** box checked , select and click **Next**.

7.  On the **First WMI Event Provider** page, do the following:

    1.  In the **WMI Namespace** box, type **root\\cimv2**.

    2.  In the **Query** box, type the following WMI query.

        ```wmimof
        Select * From __InstanceCreationEvent WITHIN 60 Where TargetInstance ISA 'Win32_Process' and TargetInstance.Name = 'notepad.exe'
        ```

    3.  In the **Poll Interval** box, type **60**.

    4.  Click **Next**.

8.  On the **Build First Expression** page, do the following:

    > [!NOTE]
    > In this example, criteria is included in the WMI query, so no expression is required in the monitor. Since the WMI event wizard in the Operations console requires an expression for each event, dummy expressions will be provided to complete the wizard and then deleted once the monitor is created.

    1.  Click **Insert**.

    2.  In the **Parameter Name** box type **Dummy**.

    3.  In the **Operator** box select **Equals**.

    4.  In the **Value** box type **Dummy**.

    5.  Click **Next**.

9. On the **Second WMI Event Provider** page, do the following:

    1.  In the **WMI Namespace** box, type **root\\cimv2**.

    2.  In the **Query** box, paste the following WMI query.

        ```wmimof
        Select * From __InstanceDeletionEvent WITHIN 60 Where TargetInstance ISA 'Win32_Process' and TargetInstance.Name = 'notepad.exe'
        ```

    3.  In the **Poll Interval** box, type **60**.

    4.  Click **Next**.

10. On the **Second Expression** page, do the following:

    1.  Click **Insert**.

    2.  In the **Parameter Name** box type **Dummy**.

    3.  In the **Operator** box select **Equals**.

    4.  In the **Value** box type **Dummy**.

    5.  Click **Next**.

11. On the **Configure Health** page, do the following:

    1.  Next to **FirstEventRaised**, change the **Health State** to **Critical**.

    2.  Click **Next**.

12. On the **Configure Alerts** page, do the following:

    1.  Check **Generate alerts for this monitor**

    2.  In the **Generate an alert when** box, select **The monitor is in a critical health state**.

    3.  Leave the box selected to automatically resolve the alert.

    4.  In the **Alert name** box, type **Notepad process detected**

    5.  Click the ellipse button next to **Alert description**.

    6.  Clear the contents of the **Value** box and then type **Path of executable:** .

    7.  Click **Data**, then **Collection**, then **Property**.

    8.  In the variable, replace **<<INT>>** with "TargetInstance" and **<<STRING>>** with **ExecutablePath**. The final text in the **Value** box should be **Path of executable: $Data\/Context\/Collection\["TargetInstance"\]\/Property\[@Name\="ExecutablePath"\]$**

    9. Click **OK**.

13. Click **Create**.

14. Right\-click **MyApplication WMI Event Error** and select **Properties**.

15. On the **First Expression** tab, click **Delete**.

16. On the **Second Expression** tab, click **Delete**.

17. Click **OK**.

## See Also
[Event Monitors and Rules](./Event-Monitors-and-Rules.md)
[Event Monitor Reset](./Event-Monitor-Reset.md)
[Repeating Events](./Repeating-Events.md)
[Alerts](./Alerts.md)


