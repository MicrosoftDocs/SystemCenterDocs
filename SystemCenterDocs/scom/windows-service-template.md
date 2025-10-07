---
ms.assetid: 504be106-2b97-4a06-be11-7edef683359a
title: Windows Service template in Operations Manager management pack
description: This article provides an overview of windows service template.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Windows Service template



The _Windows Service_ template lets you find and monitor instances of a particular service installed on a Windows-based computer. The template locates computers that are running the service and then applies monitors and rules to test its availability and collect performance data. The only information that you've to provide is the name of the service and the types of monitoring that you want to perform.

## Scenarios

Use the  **Windows Service**  template for any application that uses a service because the basic health of the service is critical to the health of the application. You can provide the name of the service and have it discovered and monitored on any computer where the application is installed.

## Monitoring performed by Windows Service template

Depending on your selections in the Windows Service Template wizard, the monitoring performed by the created monitors and rules can include any of the following settings.

| Type | Description | Enabled? |
| --- | --- | --- |
| Monitors | Running state of the service | Enabled. |
|| CPU utilization of the service | Enabled if  **CPU Usage**  monitoring is selected in the wizard. |
|| Memory usage of the service | Enabled if  **Memory Usage**  monitoring is selected in the wizard. |
| Collection Rules | Collection of events indicating a change in service's running states. | Enabled. |
|| Collection of CPU utilization for the service | Enabled if  **CPU Usage**  monitoring is selected in the wizard. |
|| Collection of memory usage for the service | Enabled if  **Memory Usage**  monitoring is selected in the wizard. |
|| Collection of Handle Count for the service | Disabled. Can be enabled with an override. |
|| Collection of Thread Count for the service | Disabled. Can be enabled with an override. |
||Collection of Working Set for the service | Disabled. Can be enabled with an override. |

## Wizard options

When you run the  **Windows Service**  template, you've to provide values for options in the following tables. Each table represents a single page in the wizard.

## General Options

The following options are available on the  **General Options**  page of the wizard.

| Option | Description |
| --- | --- |
| Name | The name used for the service. This name is displayed in the Operations console for the wizard. |
| Description | Optional description of the service. |
| Management Pack | Management pack to store the class and monitors that the template creates. If you create any additional monitors or rules that use the service as a target class, they have to be stored in the same management pack. For more information about management packs, see [Selecting a Management Pack File](select-management-pack-file.md). |

## Service Details

The following options are available on the  **Service Details**  page of the wizard.

| Option | Description |
| --- | --- |
| Service name | The name of the service. This name is searched on the agent-managed computer to determine whether it's installed. |
| Targeted group | The service is only discovered on computers that are included in the specified group. |
| Monitor only automatic service | If selected, only those services that are set to start automatically when Windows starts are monitored. Any services with their startup value set to manual or anything other than Automatic aren't monitored. |

## Performance Data

The following options are available on the  **Performance Data**  page of the wizard.

| Option | Description |
| --- | --- |
| Generate an alert if CPU usage exceeds the specified threshold | Specifies if CPU usage should be monitored. A monitor is created to set an error state on the object and generate an alert when the specified threshold is exceeded. A rule is created to collect CPU usage for analysis and reporting. |
| CPU Usage (percentage) | If CPU usage is monitored, this option sets the threshold. If the percentage of total CPU usage exceeds the threshold, the object is set to an error state and an alert is generated. |
| Generate an alert if memory usage exceeds the specified threshold | Specifies whether memory usage should be monitored. A monitor is created to set an error state on the object and generate an alert when the specified threshold is exceeded. A rule is created to collect CPU usage for analysis and reporting. |
| Memory Usage (MB) | If memory usage is monitored, this option sets the threshold. If the percentage of total CPU usage exceeds the threshold, the object is set to an error state and an alert is generated. |
| Number of samples | If CPU usage or memory is monitored, this option specifies the number of consecutive performance samples that must be exceeded before the object is set to an error state and an alert is generated. <br>Specifying a number greater than one for this option limits the noise from monitoring by ensuring that an alert isn't generated when the service only briefly exceeds the threshold. The larger the value that you set, the longer the period of time before you receive an alert. A typical value is 2 or 3.</br> |
| Sample Interval | If CPU usage or memory is monitored, this option specifies the length of time between performance samples. A smaller value for this option reduces the time for detecting a problem but increases overhead on the agent and the amount of data collected for reporting. A typical value is between 5 and 15 minutes. |

## Additional monitoring

In addition to performing the specified monitoring, the  **Windows Service**  template creates a class that you can use for additional monitors and workflows. Any monitor or rule that's using this class runs on any agent where the service is installed. If it creates Windows events that indicate an error, for example, you could create a monitor or rule that detects the particular event and uses the service class as a target.

## Creating and modifying Windows Service templates

### Create a Windows Service template

1. Determine the target group for the monitor by using the following logic:

    - If you want to discover the service on all Windows-based computers in the management group, you don't have to create a group. You can use the existing group **All Windows Computers**.

    - If you only want the service to be discovered on a certain group of computers, either ensure that an appropriate group exists or create a new group by using the procedure in [How to Create Groups in Operations Manager](/previous-versions/system-center/system-center-2012-R2/hh298605(v=sc.12)).

    - If the service you're monitoring is in a cluster, create a group with objects of the class **Virtual Server** representing the nodes of the cluster that contains the service.

2. Start the  **Add Monitoring**  wizard.
3. On the  **Select Monitoring Type**  page, select  **Windows Service** , and select  **Next**.
4. On the  **General Properties**  page, in the  **Name**  and  **Description**  boxes, enter a  **name** and description for this new monitor.
5. Select a management pack in which to save the monitor, or select  **New**  to create a new management pack. For more information, see [Selecting a Management Pack File](select-management-pack-file.md).
6. Select  **Next**.
7. In the  **Service Name**  box, enter the name of the specific service that you want to monitor, or select the ellipsis ( **…** ) button to browse for the service. You can select any computer that has the service installed.
8. Under **Targeted Group**, specify the group from step 1 of this procedure.
9. Clear the  **Monitor only automatic services**  option if you want the monitor to apply to services that aren't configured to start automatically. If the service that you're monitoring is in a cluster, clear this option.
10. Select  **Next**.
11. Select the performance counters and thresholds that you want to monitor. For more detailed information, see the Wizard Options section.
12. If you've selected performance counters, specify the monitoring interval.
13. Select **Next**.
14. Review the summary of the monitor, and select **Create**.

### Modify an existing Windows Service template

1. Open the Operations console with a user account that has Author credentials.
2. Open the  **Authoring** workspace.
3. In the  **Authoring**  navigation pane, expand  **Management Pack Templates** , and then select  **Windows Service**.
4. In the  **Windows Service**  pane, locate the monitor to change.
5. Right-click the monitor, and then select  **Properties**.
6. Enter the changes that you want, and select  **OK**.

## View Windows Service Monitors and Collected Data

### View all Windows Service monitors

1. Open the Operations console.
2. Open the  **Monitoring**  workspace.
3. In the  **Monitoring**  navigation pane, select  **Windows Service and Process Monitoring** , and select  **Windows Service State**.

### View the state of each monitor

1. In the  **Windows Service State**  pane, right-click an object. Select  **Open**, and select  **Health Explorer**.
2. Expand the  **Availability**  and  **Performance**  nodes to view the individual monitors.

#### To view the performance collected for a service

1. In the  **Windows Service State**  pane, right-click an object. Select  **Open**, and select  **Performance**.
2. In the  **Legend**  pane, select the counters that you want to view.
3. Use options in the  **Actions**  pane to modify the Performance view.
