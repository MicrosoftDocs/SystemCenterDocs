---
ms.assetid: 
title: Azure Monitor SCOM Managed Instance (preview) Agents
description: This article provides design guidance for agent deployment on Windows  with Azure Monitor SCOM Managed Instance (preview).
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/01/2023
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Azure Monitor SCOM Managed Instance (preview) Agents

In Azure Monitor SCOM Managed Instance (preview), an agent is a service that is installed on a computer that looks for configuration data and proactively collects information for analysis and reporting, measures the health state of monitored objects like an SQL database or logical disk, and executes tasks on demand by an operator or in response to a condition. It allows SCOM Managed Instance (preview) to monitor Windows operating systems and the components of an IT service installed on them, like a website or an Active Directory domain controller.  

## Windows agent

On a monitored Windows computer, the SCOM Managed Instance (preview) agent is listed as the Microsoft Monitoring Agent (MMA) service. The Microsoft Monitoring Agent service collects events and performance data, executes tasks and other workflows defined in a management pack. Even when the service is unable to communicate with the managed instance, it reports to the service and continues to run and queues the collected data and events on the disk of the monitored computer. When the connection is restored, the Microsoft Monitoring Agent service sends collected data and events to the managed instance.

### Communication between agents and management servers

The SCOM Managed Instance (preview) agent sends alert and discovery data to its assigned primary management server, which writes the data to the operational database. The agent also sends events, performance, and state data to the primary management server for that agent, which writes the data to the operational and data warehouse databases simultaneously.

The agent sends the data according to the scheduled parameters for each rule and monitor. For optimized collection rules, data is only transmitted if a sample of a counter differs from the previous sample by a specified tolerance, such as 10%. This helps reduce network traffic and the volume of data stored in the operational database.

Additionally, all agents send a packet of data, called a *heartbeat*, to the management server on a regular schedule by default every 60 seconds. The purpose of the heartbeat is to validate the availability of the agent and communication between the agent and the management server. For more information on heartbeats, see [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).

For each agent, Operations Manager runs a *health service watcher*, which monitors the state of the remote Health Service from the perspective of the management server.  The agent communicates with a management server over TCP port 5723.

## Agent security

### Authentication with gateway server

Gateway servers are often used to enable agent-management of computers that are outside the Kerberos trust boundary of a management group. If the gateway server resides in a domain that isn't trusted by the domain that the System Center Operations Manager management group is in, certificates must be used to establish the computer's identity between gateway server and management server. This arrangement satisfies the requirement of SCOM Managed Instance (preview) for mutual authentication.

You need to request certificates for each gateway and management server involved and import those certificates into the target computer using the `MOMCertImport.exe` tool, which is located on the installation media SupportTools\amd64 directory. You need to have access to a certification authority (CA) to request the right type of certificates, which can be a public CA, or you can use Microsoft Certificate Services. For more information about how to obtain a certificate, see [Obtain a certificate for use with Windows Servers and System Center Operations Manager](obtain-certificate-windows-server-and-operations-manager.md).

## Agent deployment

SCOM Managed Instance (preview) agents can be installed by using manual installation method. The setup is manually run on the agent or deployed through an existing software distribution tool. 

>[!NOTE]
>You cannot install MMA on a computer where SCOM Managed Instance (preview) management server, Operations Manager management server, System Center Operations Manager gateway server, System Center Essentials, or System Center Service Manager is installed - as they have their built-in version of MMA installed.

## Next steps

[Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview)](migrate-to-operations-manager-managed-instance.md)

**Feedback**

Provide your feedback on Azure Monitor SCOM Managed Instance (preview) [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
