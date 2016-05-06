---
title: Attributes
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff46b3ca-8afc-4470-ab84-cd741f3791c5
---
# Attributes
*Attributes* in [!INCLUDE[om12short]./Token/om12short_md.md)] are properties of a class. Each instance of the class has the same set of attributes, but each instance can have its own value for each attribute. These values are populated when the object is discovered.

## Uses for Attributes
The following table lists different ways that attributes can be used.

|Management Pack Element|How attributes can be used|
|---------------------------|------------------------------|
|Views and Dashboards|A view or dashboard can include all objects with a particular value for an attribute.|
|Groups|A group can define criteria for dynamic membership that populates the group with all objects that have a particular value for an attribute.|
|Monitors and Rules|The value of an attribute can be used in the definition of the monitor or rule. For example, a monitor may run a script that requires information from the target object. An attribute could be used as a command line parameter sent to the script.|
|Alert Descriptions|An alert description created by a monitor or rule can include values from the data or from the attributes of the target object.|

## Custom Attributes
You may want to add custom attributes to existing classes so that you can collect additional information supporting views and groups in your environment. You can add attributes to any class and populate it with data retrieved from the registry or from a WMI query.

When you create a new attribute, a new class is created based on the existing class. The new class has the new attribute and inherits all of the attributes from the original class, so that it is interchangeable with the original class. In order to use the new attribute, you must select the new class. An instance of the new class will be discovered for each member of the original class and the new attribute populated only on those agents where the specified data is found.

> [!WARNING]
> When you create a new attribute in the Operations console, a new class is created for each custom attribute that you create. Even if you create multiple attributes on the same class, a new class will be created for each one. Too many classes can result in excessive overhead. If you create more than a few custom attributes for a class, you should use another tool such as the [!INCLUDE[om2007r2long]./Token/om2007r2long_md.md)] Authoring Console that will allow you to create a single class with multiple attributes.

## Wizard Options
When you run the **Create Attribute Wizard**, you will need to provide values for options in the following tables. Each table represents a single page in the wizard.

### General Properties
The **General Properties** page includes the name and description of the attribute.

|Option|Description|
|----------|---------------|
|Name|The name of the attribute that will be displayed in the Operations console.|
|Description|Optional description of the attribute.|

### Discovery Method
The **Discovery Method** page includes the method for populating the attribute and the class that it will target.

|Option|Description|
|----------|---------------|
|Discovery Type|Specifies if the value of the attribute will be populated from the registry or from a WMI query.|
|Target|The class to which to add the attribute.|
|Management Pack|Management pack to store the attribute.<br /><br />For more information on management packs, see [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).|

### Registry Probe Configuration
The **Registry Probe Configuration** page includes the details of the registry key or value used to populate the attribute. This page is only displayed if the **Discovery Type** is **Registry**.

|Option|Description|
|----------|---------------|
|Key Or Value Type|Specifies if a registry key or registry value will be used. The data in a registry value can be used for the attribute, while it can only return a true or false indicating if a registry key exists.|
|Path|The path to the registry key or value.|
|Attribute Type|The type of data stored in the registry value. **Check if exists** can be selected if you only want to determine if a registry key or registry value exists.|
|Frequency|Specifies how often the discovery of the attribute should run. This should typically be a value of an hour or higher since the values of attributes rarely change.|

### WMI Configuration
The **WMI Configuration** page includes the details of the WMI query used to populate the attribute. This page is only displayed if the **Discovery Type** is **WMI Query**.

|Option|Description|
|----------|---------------|
|WMI Namespace|The WMI namespace with the class used in the query.|
|Query|The WMI query to run.|
|Property Name|The name of the property from the WMI query with the value to populate the attribute.|
|Frequency|Specifies how often the discovery of the attribute should run. This should typically be a value of an hour or higher since the values of attributes rarely change.|

## Creating custom attributes
The following example procedure creates an attribute with the following details:

-   New attribute named **Location** on all instances of **Windows Computer**.

-   Value populated from a registry key at HKLM\\SOFTWARE\\Contoso\\Location.

#### To create a new attribute using the registry

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

2.  In the Operations console, select the **Authoring** workspace, and then expand **Management Pack Objects**.

3.  Right\-click Attributes and select **Create a new attribute**.

4.  On the **General** page, do the following:

    1.  In the **Name** box, type **Location**.

    2.  Click **Next**.

5.  On the **Discovery Method** page, do the following:

    1.  In the **Discovery Type** dropdown, select **Registry**.

    2.  Click **Browse** to select the target class.

    3.  Select **Windows Computer** and then click **OK**.

    4.  In the Management Pack box, select the management pack from step 1.

    5.  Click **Next**.

6.  On the **Registry Probe Configuration** page, do the following:

    1.  For **Key or Key Value Type** select **Value**.

    2.  In the **Path** box, type **SOFTWARE\\Contoso\\Location**.

    3.  In the **Attribute Type** dropdown, select **String**.

    4.  In the **Frequency** box, type **3600** seconds.

    5.  Click **Finish**.

The following example procedure creates an attribute with the following details:

-   New attribute named **Manufacturer** on all instances of **Windows Computer**.

-   Value populated from a WMI query using the **Win32\_ComputerSystem** class.

#### To create a new attribute using WMI

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

2.  In the Operations console, select the **Authoring** workspace, and then expand **Management Pack Objects**.

3.  Right\-click Attributes and select **Create a new attribute**.

4.  On the **General** page, do the following:

    1.  In the **Name** box, type **Location**.

    2.  Click **Next**.

5.  On the **Discovery Method** page, do the following:

    1.  In the **Discovery Type** dropdown, select **WMI Query**.

    2.  Click **Browse** to select the target class.

    3.  Select **Windows Computer** and then click **OK**.

    4.  In the Management Pack box, select the management pack from step 1.

    5.  Click **Next**.

6.  On the **WMI Configuration** page, do the following:

    1.  In the **WMI Namespace** box, type **root\\cimv2**.

    2.  In the **Query** dropdown, type **select \* from win32\_computersystem**.

    3.  In the **Property Name** box, type **Manufacturer**.

    4.  In the **Frequency** box, type **3600** seconds.

    5.  Click **Finish**.

## See Also
[Base Classes](./Understanding-Classes-and-Objects.md#BaseClasses)
[Script Monitors and Rules](./Script-Monitors-and-Rules.md)
[Alerts](./Alerts.md)



