---
title: Text Logs
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3d2ce59-a94b-4dd0-8aeb-5f985c56a964
---
# Text Logs
A *text log* is a text file that an application uses to log event information. In order to use a text log data source in a management pack, each entry in the log must be on a single line. If the log file does not fit this requirement, then a [Script Monitors and Rules](../Topic/Script-Monitors-and-Rules.md) has to be created to read the log.

Applications that use log files frequently create a new file each day or when one file reaches a certain size. To support this functionality, monitors and rules specify a **Directory** and a **Pattern** for the text logs being monitored. Directory is the path of the directory where the text logs will be located. This must be an absolute path without wildcard characters. A $Target variable could also be used if the path to the log files is stored in a property of the target class.  Pattern is the name of the log file including wildcard characters as appropriate.

For example, an application might create a log file each day with the date included in the name as in **log20100316.txt**. A pattern for such a log might be **log\*.txt** which would apply to any log file following the application’s naming scheme.

A text log can be defined as either a *Generic Text Log* or *Generic CSV Text Log*. CSV refers to Comma Separated Values, although you can specify any character as the delimiter. The two kinds of files are also referred as a *Simple Text Log* and a *Delimited Text Log*. With a simple text log, each line is considered a single entry. With a delimited text log, a single character is used to separate different fields of data, and each field can be analyzed separately.

## Text Log Wizards
The table below lists the wizards that are available for both simple and delimited text files.

|Management Pack Object|Wizards Available|
|--------------------------|---------------------|
|Monitors|Simple Event Detection using each of the standard [Event Monitor Reset](../Topic/Event-Monitor-Reset.md) methods|
|Monitors|Repeated Event Detection using each of the standard [Event Monitor Reset](../Topic/Event-Monitor-Reset.md) methods|
|Rules|Alert Generating rule|
|Rules|Event collection rule|

## Text Log Wizard Options
When you run a text log wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### General
The **General** page includes general settings for the rule or wizard including its name, category, target, and the management pack file to store it in.

|Option|Description|
|----------|---------------|
|Name|The name used for the rule or monitor. For a rule, the name appears in the **Rules** view in the **Authoring** pane. When you create a view or report, you can select this name to use the data collected by it. For a monitor, the name appears in the Health Explorer of any target objects.|
|Description|Optional description of the rule or monitor.|
|Management Pack|Management pack to store the rule.<br /><br />For more information on management packs, see [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).|
|Rule Category \(Rules only\)|The category for the rule. For a collection rule, this should be **Event Collection**. For an alerting rule, this should be **Alert**.|
|Parent Monitor \(Monitors only\)|The aggregate monitor that the monitor will be positioned under in the Health Explorer. For more information, see [Aggregate Monitors](../Topic/Aggregate-Monitors.md).|
|Target|The class to use for the target of the rule or monitor. The rule or monitor will be run on any agent that has at least one instance of this class. For more information on targets, see [Understanding Classes and Objects](../Topic/Understanding-Classes-and-Objects.md).|
|Rule is enabled<br /><br />Monitor is enabled|Specifies whether the rule or monitor is enabled.|

### Application Log Data Source
There will be a single application log data source page for a collection or alerting rule and for a monitor using manual or timer reset. For a monitor using event reset, you will have to define the log for both the error condition and for the healthy condition. You will typically specify the same log for both conditions, but a different log could be used for each.

The following table lists the settings that must be provided for an application log data source:

|Property Name|Description|
|-----------------|---------------|
|Directory|Directory that the log file is located in. This must be a single directory with no wildcards|
|Pattern|Name of the log file. This can include wildcards if the name of the log file will change. Use the ? wildcard to represent a single character. Use the \* wildcard to represent multiple characters.|
|Separator \(Delimited Logs only\)|The character that is used to separate the|
|UTF8||

### <a name="Expression"></a>Event Expression
There will be a single expression page for a collection or alerting rule and for a monitor using manual or timer reset. For a monitor using event reset, you will have to define an expression for both the error condition and for the healthy condition.

The expression for a text log rule or monitor will include criteria that matches text in the log entry. For a Generic Text Log this includes a search of the whole log entry treated as a single line. For a delimited log file, this will include a search of one or more of the included fields. The contents of a text log are included in the parameters of the event. For a generic text log, this is referenced by the parameter **Params\/Param\[1\]**. A delimited log uses the same variable by using the index number of the required parameter. The first field would be referenced with **Params\/Param\[1\]**, the second field would be referenced with **Params\/Param\[2\]**, and so on.

The following table lists the common properties available from text log monitors and rules:

|Property Name|Description|
|-----------------|---------------|
|Directory|Directory that the log file is located in.|
|Pattern|Name of the log file that the event was taken from.|
|Param\[1\]|Complete entry in a generic text log.|
|Param\[\#\]|Specific parameter in a generic CSV text log. \# represents the number of the field.|

For more information about expressions, see [Expressions](../Topic/Expressions.md).

### Auto Reset Timer
The **Auto Reset Timer** page is only available for timer reset monitors. It allows you to set the time that must pass after the alert is created before the alert is automatically resolved.

### Configure Health
The **Configure Health** page is only available for monitors. It allows you to specify the health state that will be set for each of the events. For a manual reset monitor, the **Manual Reset** condition will be **Healthy**, and you can specify whether the **Event Raised** condition will set the monitor to a **Warning** or a **Critical** state. For a **Timer Reset** or an **Event Reset**, you can specify the health state set by each event. The first event will typically set the monitor to **Warning** or **Critical** while the second event or the timer will set the monitor to **Healthy**.

### Configure Alerts
The **Configure Alerts** page is only available for monitors and alerting rules. Its options are explained in [Alerts](../Topic/Alerts.md).

## <a name="Procedures"></a>Creating Text Log Rules and Monitors
Use the following procedure to create a text log alerting rule in [!INCLUDE[om12short](../Token/om12short_md.md)] with the following details:

-   Runs on all agents with a particular service installed.

-   Looks for a comma delimited log file with the naming pattern MyApp\*.log in the c:\\logs directory.

-   Generates an alert if the word “error” appears in the log message.

-   Includes the error message in the alert description.

-   The format of each line of the text file is as follows: Date,Time,Message

#### To create a delimited text log alert rule

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](../Topic/Selecting-a-Management-Pack-File.md).

2.  Create a new target using the process in [To create a Windows Service template](../Topic/Windows-Service-Template.md#CreateWindowsServiceTemplate). You can use any service installed on a test agent for this template.

3.  In the Operations console, select the **Authoring** workspace, and then select **Rules**.

4.  Right\-click **Rules** and select **Create a new rule**.

5.  On the **Rule Type** page, do the following:

    1.  Expand **Alert Generating Rules**, expand **Event Based**, and then click **Generic CSV Text Log \(Alert\)**.

    2.  Select the management pack from step 1.

    3.  Click **Next**.

6.  On the **General** page, do the following:

    1.  In the **Rule Name** box, type **MyApplication Delimited Log Error**.

    2.  In the **Rule Category** box, select **Alert**.

    3.  Next to **Rule Target** click **Select** and then select the name of the target that you created in step 2.

    4.  Leave **Rule is enabled** selected.

    5.  Click **Next**.

7.  On the **Application Log Data Source** page, do the following:

    1.  In the **Directory** box, type **c:\\logs**.

    2.  In the **Pattern** box, type **MyApp\*.log**.

    3.  In the **Separator** box, type a COMMA.

    4.  Click **Next**.

8.  On the **Build Event Expression** page, do the following:

    1.  Click **Insert**.

    2.  In the **Parameter Name** box type **Params\/Param\[3\]**.

    3.  In the **Operator** box select **Contains**.

    4.  In the **Value** box type **error**.

    5.  Click **Next**.

9. On the **Configure Alerts** page, do the following:

    1.  In the **Alert name** box, type **Error found in MyApplication delimited text log.**.

    2.  Click the ellipse button to the right side of the **Alert description** box.

    3.  Clear the text in the **Value** box.

    4.  Select Data, then Params, then Param.

    5.  Replace the text **<<INT>>** with **1**.

    6.  Move to the end of the line and press the SPACE bar.

    7.  Select Data, then Params, then Param.

    8.  Replace the text **<<INT>>** with **2**.

    9. Move to the end of the line and press the ENTER key.

    10. Select Data, then Params, then Param.

    11. Replace the text **<<INT>>** with **3**.

    12. Click **OK**.

10. Click **Finish**.

## See Also
[Event Monitors and Rules](../Topic/Event-Monitors-and-Rules.md)
[Event Monitor Reset](../Topic/Event-Monitor-Reset.md)
[Repeating Events](../Topic/Repeating-Events.md)
[Alerts](../Topic/Alerts.md)

