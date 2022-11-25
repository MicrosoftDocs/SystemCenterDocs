---
ms.assetid: 
title: Azure Monitor SCOM Managed Instance (preview) Agents
description: This article provides design guidance for agent deployment on Windows  with Azure Monitor SCOM Managed Instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/25/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Azure Monitor SCOM Managed Instance (preview) Agents

In Azure Monitor SCOM Managed Instance (preview), an agent is a service that is installed on a computer that looks for configuration data and proactively collects information for analysis and reporting, measures the health state of monitored objects like an SQL database or logical disk, and execute tasks on demand by an operator or in response to a condition. It allows SCOM Managed Instance (preview) to monitor Windows operating systems and the components of an IT service installed on them, like a web site or an Active Directory domain controller.  

## Windows agent

On a monitored Windows computer, the SCOM Managed Instance (preview) agent is listed as the Microsoft Monitoring Agent (MMA) service. The Microsoft Monitoring Agent service collects event and performance data, executes tasks, and other workflows defined in a management pack. Even when the service is unable to communicate with the managed instance, it reports to the service continues to run and queues the collected data and events on the disk of the monitored computer. When the connection is restored, the Microsoft Monitoring Agent service sends collected data and events to the managed instance.

### Communication between agents and management servers

The SCOM Managed Instance (preview) agent sends alert and discovery data to its assigned primary management server, which writes the data to the operational database. The agent also sends events, performance, and state data to the primary management server for that agent, which writes the data to the operational and data warehouse databases simultaneously.

The agent sends data according to the schedule parameters for each rule and monitor. For optimized collection rules, data is only transmitted if a sample of a counter differs from the previous sample by a specified tolerance, such as 10%. This helps reduce network traffic and the volume of data stored in the operational database.

Additionally, all agents send a packet of data, called a *heartbeat*, to the management server on a regular schedule, by default every 60 seconds. The purpose of the heartbeat is to validate the availability of the agent and communication between the agent and the management server. For more information on heartbeats, see [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).

For each agent, Operations Manager runs a *health service watcher*, which monitors the state of the remote Health Service from the perspective of the management server.  The agent communicates with a management server over TCP port 5723.

## Agent security

### Authentication with gateway server

Gateway servers are used to enable agent-management of computers that are outside the Kerberos trust boundary of a management group. Because the gateway server resides in a domain that isn't trusted by the domain that the management group is in, certificates must be used to establish each computer's identity, agent, gateway server, and management server. This arrangement satisfies the requirement of SCOM Managed Instance (preview) for mutual authentication.

This requires you to request certificates for each agent that will report to a gateway server and import those certificates into the target computer using the `MOMCertImport.exe` tool, which is located on the installation media SupportTools\ (amd64 or x86) directory.  You need to have access to a certification authority (CA) which can be a public CA such as VeriSign, or you can use Microsoft Certificate Services.  

## Agent deployment

SCOM Managed Instance (preview) Agents may be installed by using manual installation method. The setup is manually run on the agent or deployed through an existing software distribution tool. 

>[!NOTE]
>You cannot install MMA on a computer, where SCOM Managed Instance (preview), Operations Manager management server, gateway server, operations console, operational database, web console, System Center Essentials or System Center Service Manager is installed - as they have their built-in version of MMA already installed.
