---
ms.assetid: 1bde753f-c0e9-43b9-9a73-a78a4233881b
title: TCP port template in Operations Manager management pack
description: This article provides an overview of TCP port template
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# TCP port template


The  **TCP Port**  template lets you monitor the availability of an application that's accessible over TCP.

The application that is being tested can reside on any computer whether an agent for Operations Manager installed or not. Each watcher node must have an Operations Manager agent installed.

## Scenarios

Use the  **TCP Port**  template in scenarios where applications rely on a service accessible over TCP. You can define each client as a watcher node. The monitors created by the template attempt to connect to the application from each client at the defined interval. The monitors verify that each client can connect successfully. In addition to validating the availability of the application itself, any network connections and other required features between the watcher node and the application are also validated.

## Monitoring performed by the TCP port template

The monitoring performed by the monitors and rules created by the TCP Port template can include any of the following settings.

| Type | Description | Enabled? |
| --- | --- | --- |
| Monitors | Target host reachable | Enabled |
|| Connection accepted | Enabled |
|| Connection timeout | Enabled |
|| DNS resolution | Enabled |
| Collection Rules | Connection time | Enabled |

## Viewing monitoring data

All data collected by the  **TCP Port**  template is available in the  **TCP Port Checks State**  view located in the  **Synthetic Transaction**  folder. In this view, an object represents each of the watcher nodes. The state of each object represents the worst state of the set of TCP Port monitors running on that node. If one or more of the nodes is shown with an error while at least one other node is healthy, it could indicate a problem with that particular node accessing the specified computer, for example, a network issue. If all the nodes are unhealthy, it could indicate a problem with the application itself, either the computer being offline or the application not responding on the specified port.

You can view the state of the individual TCP Port monitors by opening the Operations Manager Health Explorer for each object. You can view performance data by opening the Performance view for each of these objects.

## Wizard options

When you run the  **TCP Port**  template, you've to provide values for options in the following tables. Each table represents a single page in the wizard.

## General Options

The following options are available on the  **General Options**  page of the wizard.

| Option | Description |
| --- | --- |
| Name | The name used for the template. This name is displayed in the Operations console. |
| Description | Optional description of the service. |
| Management Pack | Management pack to store the class and monitors that the template created. If you create any additional monitors or rules by using the service as a target class, you must store them in the same management pack. For more information about management packs, see [Selecting a Management Pack File](select-management-pack-file.md). |

## Target and Port

The following options are available on the  **Target and Port**  page of the wizard.

| Option | Description |
| --- | --- |
| Computer or device name | The name of the computer or device to connect to. This can be a name or an IP address. It must be resolved by and accessible to each watcher node that you specify. |
| Port | The number of the port on which the application is listening. |

## Watcher Nodes

The following options are available on the  **Watcher Nodes**  page of the wizard.

| Option | Description |
| --- | --- |
| Select one or more agent managed computers | Specify one or more computers to run the monitors and rules. For more information, see [Watcher Nodes](/previous-versions/system-center/system-center-2012-R2/hh457584%28v%3dsc.12%29). |
| Run this query every | The frequency to attempt the connection to the specified computer and port. |

## Creating and modifying TCP port templates

### Run the TCP Port data source wizard

1. Start the Operations console with an account that has Author credentials in the management group.
2. Open the  **Authoring**  workspace.
3. In the  **Authoring**  navigation pane, right-click  **Management Pack Templates** , and then select  **Add Monitoring Wizard**.
4. On the  **Select Monitoring Type**  page, select  **TCP Port** , and select  **Next**.
5. On the  **General Properties**  page, in the  **Name**  and  **Description**  boxes, enter a name and an optional description.
6. Select a management pack in which to save the monitor, or select  **New**  to create a new management pack. For more information, see [Selecting a Management Pack File](select-management-pack-file.md).
7. Select  **Next**.
8. In the  **Computer or device name**  box, enter the name or IP address of the computer or device to connect to.
9. In the  **Port**  box, enter the port number on which the application is listening.
10. Select  **Test**  to perform a test connection by using the connection string and query that you just provided.

     > [!NOTE]
     > The test is performed on the workstation that you're using to run the template. If this workstation can't access the computer or device, this test fails. When the template is completed, the test is run from the watcher nodes that you specify.

11. Select  **Next**  when you've validated your connection.
12. Select one or more [Watcher Nodes](/previous-versions/system-center/system-center-2012-R2/hh457584%28v%3dsc.12%29) to run the monitor.
13. Specify the frequency to run the monitor in the  **Run this query**  box. Select  **Next**.
14. Review the summary of the monitor, and select  **Create**.

#### Modify an existing TPC Port template

1. Open the Operations console with a user account that has Author credentials.
2. Open the  **Authoring**  workspace.
3. In the  **Authoring**  navigation pane, expand  **Management Pack Templates** , and then select  **TCP Port**.
4. In the  **TCP Port**  pane, locate the template to change.
5. Right-click the monitor, and then select  **Properties**.
6. Enter the changes that you want, and select  **OK**.

## View TCP port monitors and collected data

### View all TCP port monitors

1. Open the Operations console.
2. Open the  **Monitoring**  workspace.
3. In the  **Monitoring**  navigation pane, select  **Synthetic Transaction** , and select  **TCP Port Checks State**.

### View the state of each monitor

1. In the  **TCP Port Checks State**  pane, right-click an object. Select  **Open** , and select  **Health Explorer**.
2. Expand the  **Availability**  and  **Performance**  nodes to view the individual monitors.

### View the performance collected for a monitor

1. In the  **TCP Port Checks State**  pane, right-click an object. Select  **Open** , and select  **Performance**.
2. In the  **Legend**  pane, select the counters you want to view.
3. Use options in the  **Actions**  pane to modify the Performance view.

## See also

- [Creating Management Pack Templates](create-management-pack-templates.md)
- [Watcher Nodes](/previous-versions/system-center/system-center-2012-R2/hh457584%28v%3dsc.12%29)
