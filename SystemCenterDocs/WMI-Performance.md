---
title: WMI Performance
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c078fa8e-2644-4049-9efc-0ee1e589d5ab
---
# WMI Performance
WMI performance refers to numeric data that is retrieved from a WMI query. This lets performance data be retrieved that is not available from a performance counter and without using the complexity and overhead of a script. The monitor or rule runs the query on a specified schedule and maps the value of the specified numeric field into the value property of the performance data.

For example, a monitor might have to track the size of a particular file. This might be a log file that indicates a particular problem when it exceeds a particular size. The name and size of the file could be retrieved from a query similar to the following:

```wmimof
Select Name, FileSize from CIM_DataFile Where Name = 'C:\\MyApp\\MyAppLog.txt'
```

The monitor could run this query regularly by using the FileSize property for the value of the performance data and the Name property for the Instance property.

The WMI query returns a property bag with each property returned from the query. This set of properties will vary, depending on the class returned and the properties specified in the query.  For more information about property bags, see [Property Bags](./Script-Monitors-and-Rules.md#PropertyBags).

## Options
When you run the Windows performance collection wizard, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### General
The **General** page includes general settings for the rule including its name, category, target, and the management pack file to store it in.

|Option|Description|
|----------|---------------|
|Rule Name|The name used for the rule. This appears in the **Rules** view in the **Authoring** pane. When you create a view or report, you can select this name to use the data collected by it.|
|Description|Optional description of the rule.|
|Management Pack|Management pack to store the rule.<br /><br />For more information on management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).|
|Rule Category|The category for the rule. For a performance collection rule, this should be **Performance Collection**.|
|Rule target|The class to use for the target of the rule. The rule will be run on any agent that has at least one instance of this class. For more information on targets, see [Understanding Classes and Objects](./Understanding-Classes-and-Objects.md).|

### WMI Configuration
The **Performance Counter** page includes the definition of the performance counter to collect and the frequency it should be collected.

|Option|Description|
|----------|---------------|
|WMI Namespace|The namespace containing the class used by the query.|
|Query|Name of the performance counter.|
|Query Interval|The frequency in seconds to run the query and collect the|

### Performance Mapper
The **Performance Mapper** page is used to define values for the properties of the performance data being collected.

|Option|Description|
|----------|---------------|
|Object|Text for the Object name. This is required. You can type in the name of the object or select a property from the target or from the property bag.|
|Counter|Text for the Counter name. This is required. You can type in the name of the object or select a property from the target or from the property bag.|
|Instance|Text for the Instance name. This only required if the target of the rule has multiple instances. You can type in the name of the object or select a property from the target or from the property bag.|
|Value|Numeric for the value for the performance. This will usually be a $Data variable to use a value from the property bag.|

## Creating WMI Performance Collection Rules
Use the following procedure to create a WMI performance collection rule in [!INCLUDE[om12short](./Token/om12short_md.md)] with the following details:

-   Runs on all agents with a particular service installed.

-   Collects the size of a file called C:\\MyApp\\MyAppLog.txt.

#### To create a WMI performance collection rule

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

2.  Create a new target using the process in [To create a Windows Service template](./Windows-Service-Template.md#CreateWindowsServiceTemplate). You can use any service installed on a test agent for this template.

3.  In the Operations console, select the **Authoring** workspace, and then select **Rules**.

4.  Right\-click **Rules** and select **Create a new rule**.

5.  On the **Rule Type** page, do the following:

    1.  Expand **Collection Rules**, expand **Performance Based**, and then click **WMI Performance**.

    2.  Select the management pack from step 1.

    3.  Click **Next**.

6.  On the **General** page, do the following:

    1.  In the **Rule name** box, type **Collect File Size with WMI**.

    2.  In the **Rule Category** box, select **Performance Collection**.

    3.  Next to **Rule Target** click **Select** and then select the name of the target that you created in step 2.

    4.  Leave **Rule is enabled** selected.

    5.  Click **Next**.

7.  On the **WMI Configuration** page, do the following:

    1.  In the **WMI Namespace** box, type **root\\cimv2**.

    2.  In the **Query** box, paste the following WMI query.

        ```wmimof
        Select Name,FileSize From CIM_DataFile Where Name = 'C:\\Logs\\MyAppFile.txt'
        ```

    3.  In the **Query Interval** box, type **900**.

    4.  Click **Next**.

8.  On the **Performance Mapper** page, do the following:

    1.  In the **Object** box, type **MyApplication**.

    2.  In the **Counter** box, type **File Size**.

    3.  In the **Instance** box, type **$Data\/Property\[@Name\=’Name’\]$**.

    4.  In the **Value** box, type **$Data\/Property\[@Name\=’FileSize’\]$**.

    5.  Click **Finish**.

## See Also
[Performance Monitors and Rules](./Performance-Monitors-and-Rules.md)
[Performance Monitors](./Performance-Monitors.md)


