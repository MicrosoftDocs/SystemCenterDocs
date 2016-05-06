---
title: Windows Performance Collection Rules_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52cc8a38-7c82-487e-899b-7535a38b60f4
---
# Windows Performance Collection Rules_1
To define a collection rule in [!INCLUDE[om12short](./Token/om12short_md.md)] based on a Windows performance counter, the object name and counter name of the performance counter to sample must be defined with a frequency that specifies how frequently to sample the data. The instance name only has to be specified if the same counter will be collected for multiple objects on the same agent. If this is the case, a $Target variable will typically be used for the value in the instance name in order to differentiate between the performance values for different objects. The counter must be available on the agent computer that is running the rule or an error will be created in the Operations Manager event log on the agent.

## Windows Performance Collection Wizard Options
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

### Performance Counter
The **Performance Counter** page includes the definition of the performance counter to collect and the frequency it should be collected.

|Option|Description|
|----------|---------------|
|Object|Text for the Object name. This is required. You can type in the name of the object or select a property from the target.|
|Counter|Name of the performance counter.|
|Instance|Text for the Instance name. This only required if the performance counter has multiple instances. You can type in the name of the instance or select a property from the target.|
|Include all instances for the selected counter|If select, the **Instance** box is disabled and the value for each instance of the performance counter is collected.|
|Interval|Specifies the frequency to collect the performance counter.|

### Optimized Collection
The **Optimized Collection** page allows to you to enable and configure optimized collection for the counter. If you select optimization for a collection rule, a value is only collected if it differs from the previous sample by a specified tolerance, either an absolute value or a percentage. This helps reduce network traffic and the volume of data stored in the [!INCLUDE[om12short](./Token/om12short_md.md)] database. Optimization should be used for performance counters that are expected to only change gradually. For counters that are expected to very significantly from one value to the next, optimized collection should be disabled.

|Option|Description|
|----------|---------------|
|Use Optimization|Specifies whether optimization should be enabled for the counter. If it is disabled, then every sampled value will be collected.|
|Absolute number|Specifies a value that the number must vary between the current sample and the previous sample for the value to be collected. The value can change in either positive or negative direction.|
|Percentage|Specifies a percentage of the previous sample that the difference between the current value and the previous value must be for the value to be collected. The change can be in either positive or negative direction.|

## Creating Windows Performance Collection Rules
Use the following procedures to create a Windows performance collection rule in [!INCLUDE[om12short](./Token/om12short_md.md)] with the following details:

-   Runs on all agents with a particular service installed.

-   Collects the % Privileged Time for the selected service.

#### To create a Windows performance collection rule in [!INCLUDE[om12short](./Token/om12short_md.md)]

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

2.  Create a new target using the process in [To create a Windows Service template](./Windows-Service-Template.md#CreateWindowsServiceTemplate). You can use any service installed on a test agent for this template.

3.  In the Operations console, select the **Authoring** workspace, and then select **Rules**.

4.  Right\-click **Rules** and select **Create a new rule**.

5.  On the **Rule Type** page, do the following:

    1.  Expand **Collection Rules**, expand **Performance Based**, and then click **Windows Performance**.

    2.  Select the management pack from step 1.

    3.  Click **Next**.

6.  On the **General** page, do the following:

    1.  In the **Rule name** box, type **% Privileged Time**.

    2.  In the **Rule Category** box, select **Performance Collection**.

    3.  Next to **Rule Target** click **Select** and then select the name of the target that you created in step 2.

    4.  Leave **Rule is enabled** selected.

    5.  Click **Next**.

7.  On the **Performance Counter** page, do the following:

    1.  Click **Select**.

    2.  In the **Select Performance Counter** dialog box, type a computer name or browse to a **Computer**  that has the performance counter installed.

        > [!NOTE]
        > The name of the computer is not recorded in the rule. The computer is only used to retrieve the details of the performance counter.

    3.  In the **Object** dropdown, select **Process**.

    4.  In **Select counter from list**, select **% Privileged Time**.

    5.  Click **OK**.

    6.  Clear the text in the **Instance** box.

    7.  Click the arrow to the right of the **Instance** box and select **Service Name \(Windows Service\)**.

        > [!NOTE]
        > You can also select the name of the service process when you select the counter. The strategy used here is to use the $Target variable to use the Service Name property of the target class. This will resolve to the name of the service when the rule runs. This is to illustrate the use of $Target variables.

    8.  Leave the **Interval** at its default value of **15 minutes**.

    9. Click **Next**.

8.  On the **Optimized Performance Collection Settings** page, do one of the following:

    -   Leave the **Use Optimization** option unselected.

        > [!NOTE]
        > If you select optimization for a collection rule, a value is only collected if it differs from the previous sample by a specified tolerance, either an absolute value or a percentage. This helps reduce network traffic and the volume of data stored in the [!INCLUDE[om12short](./Token/om12short_md.md)] database. Optimization should be used for performance counters that are expected to only change gradually.  In this example, the privileged time of the process is expected to vary significantly between samples so it would not benefit from optimized collection.

    -   Click **Create**.

## See Also
[Performance Monitors and Rules](./Performance-Monitors-and-Rules.md)
[Performance Monitors](./Performance-Monitors.md)


