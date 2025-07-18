---
title: View Network Devices and Data in Operations Manager
description: This article describes how to view the information about the network devices monitored by Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: f210ed66-1bed-4571-b506-868258f33329
---

# View network devices and data in Operations Manager


After System Center Operations Manager discovers your network devices, you can view information about the devices using the following procedures.

> [!IMPORTANT]
> You must open the Operations console as an Operations Manager administrator to view the dashboard views.

This article describes the following views:

- Network Summary Dashboard View

- Network Node Dashboard View

- Network Interface Dashboard View

- Network Vicinity Dashboard

## Network Summary Dashboard view

The Network Summary Dashboard view provides a view of important data for the nodes and interfaces of the network. A node can be any device connected to a network. Nodes can be switches, routers, firewalls, load balancers, or any other networked device. An interface is a physical entity with which network connections are made, such as a port.

Use the Network Summary Dashboard view to view the following information:

- Nodes with Slowest Response (ICMP ping)

- Nodes with Highest CPU Usage

- Interfaces with Highest Utilization

- Interfaces with Most Send Errors

- Interfaces with Most Receive Errors

- Nodes with the Most Alerts

- Interfaces with the Most Alerts

You can select a particular node or interface name in the Network Summary Dashboard view and then select the related tasks in the **Tasks** pane, such as starting the Network Node Dashboard view and the Network Interface Dashboard view.

### Open the Network Summary Dashboard view

1. Open the Operations console, and then select the **Monitoring** workspace.

2. Expand **Network Monitoring**.

3. Select **Network Summary Dashboard**.

## Network Node Dashboard view

A node can be any device connected to a network. Nodes can be switches, routers, firewalls, load balancers, or any other networked device. Use the Network Node Dashboard view to view the following information:

- Vicinity view of the node

- Availability statistics of the node over the last 24 hours, last 48 hours, past seven days, or past 30 days

    > [!NOTE]
    > Periods of time that were not monitored are counted as available in the availability statistics.

- Node properties

- Average response time of the node

- Processor usage of the node over the last 24 hours

- Current health of interfaces on the node

- Alerts generated by this node

- Alert details

### Open the Network Node Dashboard view

1. Open the Operations console, and then select the **Monitoring** workspace.

2. Expand **Network Monitoring**.

3. Select the view for the desired node, such as **Switches**.

4. Select a node.

5. In the **Tasks** pane, select **Network Node Dashboard**.

## Network Interface Dashboard view

An interface is a physical entity with which network connections are made, such as a port. By default, Operations Manager will only monitor ports that are connected to another device that's being monitored. Ports that aren't connected won't be monitored. Use the Network Interface Dashboard view to view the following information:

- Bytes sent and received over the past 24 hours

- Packets sent and received over the past 24 hours

- Interface properties

- Send and receive errors and discards over the past 24 hours

- Network interface usage percentage

- Alerts generated by this interface

- Alert details

### Open the Network Interface Dashboard view

1. Open the Operations console, and then select the **Monitoring** workspace.

2. Expand **Network Monitoring**.

3. Select the view for the desired node, such as **Switches**.

4. Select a node.

5. In the **Tasks** pane, select **Network Node Dashboard**.

6. In the **Health of Interfaces on this Node** section, select an interface, and then in the **Tasks** pane, select **Network Interface Dashboard**.

## Network Vicinity Dashboard

Use the Network Vicinity Dashboard to view a diagram of a node and all nodes and agent computers that are connected to that node. The Network Vicinity Dashboard view displays one "hop", or level of connection. However, you can configure the view to display up to five levels of connections. The diagram displays the health of the nodes and the health of the connections between nodes.

The vicinity view shows the relation between network devices and the Windows computers and other network devices that are connected to them. This logic is performed by relating the network adapter on the agent computer with the network device that it's connected to. Because of this, the network adapter must be discovered before this association can occur. You can view the discovered network adapters by either creating a new view or using the **Discovered Inventory** view to list instances of the **Computer Network Adapter** class.

> [!NOTE]
> Because devices that use OSI layer 1, such as hubs, don't have MAC addresses, layer 1 devices won't be connected to computers in the Network Vicinity Dashboard. The vicinity view will only show connections between layer 1 devices and layer 2 or 3 devices.

> [!NOTE]
> Network adapters using NIC teaming won't be identified as "teamed" in the Network Vicinity Dashboard.

> [!NOTE]
> Virtual machines are associated with the same network device as their host. This version of Operations Manager doesn't show a relationship between the two computers.

> [!NOTE]
> Operations Manager doesn't display UNIX- and Linux-based devices in the Network Vicinity Dashboard.

### Open Network Vicinity view

1. Open Operations console, and then select the **Monitoring** workspace.

2. Expand **Network Monitoring**.

3. Select a node state view, such as **Network Devices**.

4. In the **Tasks** pane, select  **Vicinity Dashboard**.

Things to try in the vicinity view:

- Select a node or connection to view details for that node or connection in the **Details** view.

- Change the levels of connection to be displayed in the diagram by selecting a new value for **Hops** in the toolbar.

- To include agent computers in the view in addition to network devices, select the **Show Computers** checkbox.

- Select a node in the vicinity view. In the **Tasks** pane, select the option to launch the Network Node dashboard.

- To change the central device of the view, select a device, and select **Vicinity View**.

## Next steps

- To understand how to configure what to monitor and alert with your network devices, see [How to configure monitoring of network devices](manage-monitor-networkdevice-configure-monitoring.md).  

- Operations Manager includes several reports that help analyze performance of monitored network devices. To learn more, see [Reports for network monitoring in Operations Manager](manage-monitor-networkdevice-reports.md).

- To understand how to stop monitoring a network device, see [How to Delete or Restore a Network Device in Operations Manager](manage-monitor-networkdevice-delete-restore.md).
