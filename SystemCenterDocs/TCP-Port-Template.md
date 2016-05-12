---
title: TCP Port Template
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a519703-61f9-4262-97d8-490a7807beef
---
# TCP Port Template
The **TCP Port** template lets you monitor the availability of an application that is accessible over TCP.

The application that is being tested can reside on any computer whether an agent for [!INCLUDE[om12short](Token/om12short_md.md)] installed or not. Each watcher node must have an [!INCLUDE[om12short](Token/om12short_md.md)] agent installed.

## Scenarios
Use the **TCP Port** template in scenarios where applications rely on a service accessible over TCP. You can define each client as a watcher node. The monitors created by the template attempt to connect to the application from each client at the defined interval. The monitors verify that each client can connect successfully. In addition to validating the availability of the application itself, any network connections and other required features between the watcher node and the application are also validated.

## Monitoring Performed by the TCP Port Template
The monitoring performed by the monitors and rules created by the TCP Port template can include any of the following settings.

**Monitors**

|Description|Enabled?|
|---------------|------------|
|Target host reachable|Enabled|
|Connection accepted|Enabled|
|Connection timeout|Enabled|
|DNS resolution|Enabled|

**Collection Rules**

|Description|Enabled?|
|---------------|------------|
|Connection time|Enabled|

## Viewing Monitoring Data
All data collected by the **TCP Port** template is available in the **TCP Port Checks State** view located in the **Synthetic Transaction** folder. In this view, an object represents each of the watcher nodes. The state of each object represents the worst state of the set of TCP Port monitors running on that node. If one or more of the nodes is shown with an error while at least one other node is healthy, it could indicate a problem with that particular node accessing the specified computer, for example, a network issue. If all of the nodes are unhealthy, it could indicate a problem with the application itself, either the computer being offline or the application not responding on the specified port.

You can view the state of the individual TCP Port monitors by opening the [!INCLUDE[om12short](Token/om12short_md.md)] Health Explorer for each object. You can view performance data by opening the Performance view for each of these objects.

## Wizard Options
When you run the **TCP Port** template, you have to provide values for options in the following tables. Each table represents a single page in the wizard.

### General Options
The following options are available on the **General Options** page of the wizard.

|Option|Description|
|----------|---------------|
|Name|The name used for the template. This name is displayed in the Operations console.|
|Description|Optional description of the service.|
|Management Pack|Management pack to store the class and monitors that the template created. If you create any additional monitors or rules by using the service as a target class, you must store them in the same management pack.<br /><br />For more information about management packs, see [Selecting a Management Pack File](Selecting-a-Management-Pack-File.md).|

### Target and Port
The following options are available on the **Target and Port** page of the wizard.

|Option|Description|
|----------|---------------|
|Computer or device name|The name of the computer or device to connect to. This can be a name or an IP address. It must be resolved by and accessible to each watcher node that you specify.|
|Port|The number of the port on which the application is listening.|

### Watcher Nodes
The following options are available on the **Watcher Nodes** page of the wizard.

|Option|Description|
|----------|---------------|
|Select one or more agent managed computers|Specify one or more computers to run the monitors and rules. For more information, see [Watcher Nodes](Watcher-Nodes.md).|
|Run this query every|The frequency to attempt the connection to the specified computer and port.|

### Creating and Modifying TCP Port Templates

##### To run the TCP Port data source wizard

1.  Start the Operations console with an account that has Author credentials in the management group.

2.  Open the **Authoring** workspace.

3.  In the **Authoring** navigation pane, right\-click **Management Pack Templates**, and then select **Add Monitoring Wizard**.

4.  On the **Select Monitoring Type** page, select **TCP Port**, and then click **Next**.

5.  On the **General Properties** page, in the **Name** and **Description** boxes, type a name and an optional description.

6.  Select a management pack in which to save the monitor, or click **New** to create a new management pack. For more information, see [Selecting a Management Pack File](Selecting-a-Management-Pack-File.md).

7.  Click **Next**.

8.  In the **Computer or device name** box, type the name or IP address of the computer or device to connect to.

9. In the **Port** box, type the port number on which the application is listening.

10. Click **Test** to perform a test connection by using the connection string and query that you just provided.

    > [!NOTE]
    > The test is performed on the workstation that you are using to run the template. If this workstation cannot access the computer or device, this test fails. When the template is completed, the test is run from the watcher nodes that you specify.

11. Click **Next** when you have validated your connection.

12. Select one or more [Watcher Nodes](Watcher-Nodes.md) to run the monitor.

13. Specify the frequency to run the monitor in the **Run this query** box. Click **Next**.

14. Review the summary of the monitor, and then click **Create**.

##### To modify an existing TPC Port template

1.  Open the Operations console with a user account that has Author credentials.

2.  Open the **Authoring** workspace.

3.  In the **Authoring** navigation pane, expand **Management Pack Templates**, and then select **TCP Port**.

4.  In the **TCP Port** pane, locate the template to change.

5.  Right\-click the monitor, and then select **Properties**.

6.  Enter the changes that you want, and then click **OK**.

### Viewing TCP Port Monitors and Collected Data

##### To view all TCP Port monitors

1.  Open the Operations console.

2.  Open the **Monitoring** workspace.

3.  In the **Monitoring** navigation pane, select **Synthetic Transaction**, and then click **TCP Port Checks State**.

##### To view the state of each monitor

1.  In the **TCP Port Checks State** pane, right\-click an object. Select **Open**, and then click **Health Explorer**.

2.  Expand the **Availability** and **Performance** nodes to view the individual monitors.

##### To view the performance collected for a monitor

1.  In the **TCP Port Checks State** pane, right\-click an object. Select **Open**, and then click **Performance**.

2.  In the **Legend** pane, select the counters you want to view.

3.  Use options in the **Actions** pane to modify the Performance view.

## See Also
[Creating Management Pack Templates](Creating-Management-Pack-Templates.md)
[Watcher Nodes](Watcher-Nodes.md)


