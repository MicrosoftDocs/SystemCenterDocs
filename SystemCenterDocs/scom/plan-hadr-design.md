---
ms.assetid: ffcc04ad-91ac-40cc-bdfc-65e33de7c390
title: Designing for High Availability and Disaster Recovery
description: This article provides high availability and disaster recovery design guidance for an Operations Manager management group.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: engagement-fy23, UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.update-cycle: 365-days
---

# High Availability and Disaster Recovery



System Center – Operations Manager servers and features can potentially fail, affecting Operations Manager functionality.  The amount of data and functionality lost during a failure is different in each failure scenario. It depends on the role of the failing feature and the length of time it takes to recover the failing feature.

## High availability

High-availability needs are addressed by building redundancy into the management group for the Operations Manager operational and data warehouse databases, the gateway and management servers, and specific workloads. These workloads include network device monitoring, cross-platform monitoring, and management group-specific workloads that were previously managed by the Root Management Server.

The multiple servers, single management group configuration can make use of SQL Server Always On for providing high availability and service continuity of the Operations Manager databases.  Management server fault-tolerance is provided by having at least two management servers and by using the resource pools for monitoring UNIX servers, Linux servers, and network devices. Agent-based Windows servers can be configured with a primary and secondary management server to redirect agent communications should a management server fail.

The RMS Emulator can be moved to another management server as well should the management server hosting the RMS Emulator become unavailable.

Operations console connections can be made highly available by configuring high availability for the Data Access Services. This can be done by installing Microsoft Network Load Balancing (NLB) or using a hardware-based load balancers or DNS alias.  One or more management servers are added as members of the NLB pool and when opening either the console, you reference the virtual name registered in DNS, of the load-balanced management servers.  

> [!NOTE]  
> A Network Load Balancer isn't supported for the Operations Manager web console server.

Multiple gateway servers can be deployed across a trust boundary to provide redundant pathways for agents that lie across that trust boundary. Just as agents can fail over between a primary management server and one or more secondary management servers, they can also fail over between gateway servers. In addition, multiple gateway servers can be used to distribute the workload of managing agentless-managed computers and managed network devices.  

In addition to providing redundancy through agent-gateway failover, gateway servers can be configured to fail over between management servers in a management group if multiple management servers are available.  

While SQL Server Reporting Services supports a scale-out deployment model that allows you to run multiple report server instances that share a single report server database, it isn't supported with Operations Manager.  Operations Manager Reporting installs a custom security extension as part of the setup of the front-end components, which can't be replicated across the web farm.

## Disaster recovery

Disaster recovery relates to measures taken to ensure that operations can be resumed if a catastrophic failure (for example, loss of the entire data center that hosts the primary infrastructure). It's an important element that must be considered in any deployment and the decisions that are made in planning for disaster recovery affect how Operations Manager will be able to continue supporting proactive monitoring and reporting of the performance and availability of your critical IT services. This section will focus on the recommended strategy of disaster recovery and resiliency and what steps should be taken to ensure a smooth recovery.

While HA and DR solutions will provide protection from system failure or system loss, they shouldn't be relied on for protection from accidental, unintended, or malicious data loss or corruption. In these cases, back up copied or lagged replication copies might have to be used for restore operations. In many cases, a restore operation is the most appropriate form of DR. One example of this could be a low-priority reporting database or analysis data. In many cases, the cost to enable multisite DR at the system or application level far outweighs the value of the data. In cases in which the near-term value of the data is low and the need to access the data can be delayed without severe business impact if a failure or site DR excessive, consider using simple backup and restore processes for DR if the cost savings warrant it.

Understanding the impact and tolerance for downtime will help drive the decisions that need to be understood in order to properly design the architecture for Operations Manager and the level of complexity and cost required to support disaster recovery. Additionally, consider the extent of monitoring data loss the IT organization can tolerate without causing business consequences. This is best described in two terms: recovery time objective (RTO) and recovery point objective (RPO).  

The two most common disaster recovery design configurations for Operations Manager are:

- Creating a duplicate management group deployed to your secondary data center that duplicates  in scale and configuration the primary management group.
- Deploying additional servers in a secondary data center to support the Operational and Data Warehouse database, with management servers deployed in a cold-standby configuration, not participating in the management group until recovery actions need to be performed.

Deploying a duplicate management group is an option when there's no tolerance for downtime; however, it's the most complex option.  Configuration between both needs to be consistent so that when you cut over, there's no difference in what's monitored, alerted or reported, presented, and finally escalated. Integration with other monitoring platforms or ITSM platforms such as System Center - Service Manager, Remedy, or ServiceNow will need to exist as well, and possibly configured in an active/passive state to avoid duplication of incidents, configuration items, and so on. Agents will be multihomed between both management groups, so there will be duplication of data.

The following diagram is an example of this design scenario.<br>

:::image type="content" source="./media/plan-hadr-design/om2016-dr-redundant-mg-inline.png" alt-text="Diagram of Duplicate MGs." lightbox="./media/plan-hadr-design/om2016-dr-redundant-mg-expanded.png":::

If immediate recovery isn't necessary for your Operations Manager deployment and you want to avoid the complexity of a duplicate management group, you can alternatively deploy additional management group components in your secondary data center in order to retain the functionality of your management group. At a minimum, consider implementing a SQL Server 2014 or 2016 Always On Availability Group to provide recovery of the Operational and Data Warehouse databases between two or more datacenters, where a two-node failover cluster instance (FCI) is deployed in the primary data center, and a standalone SQL Server in the secondary datacenter as part of a single Windows Server Failover Cluster (WSFC). The secondary replica for the Always On Availability Group would be on the non-FCI standalone instance as shown in the following diagram.<br>

:::image type="content" source="./media/plan-hadr-design/om2016-dr-simple-config-inline.png" alt-text="Diagram of Simple DR Config." lightbox="./media/plan-hadr-design/om2016-dr-simple-config-expanded.png":::

In this example, you would be required to deploy one or more Windows Servers with the same hardware configuration and computer name, and reinstall the management server role using the **/Recover** parameter. Here's a sample:

```powershell

Setup.exe /silent /AcceptEndUserLicenseAgreement:1 /recover /InstallPath:<Install Directory> /ManagementGroupName:MGNAME /SqlServerInstance:SQLServerName.domain.com /DatabaseName:OperationsManager /DWSqlServerInstance:SQLServerName.domain.com /DWDatabaseName:OperationsManagerDW /ActionAccountUser:DOMAIN\omaa /ActionAccountPassword:password /DASAccountUser:DOMAIN\omdas /DASAccountPassword:password /DatareaderUser:DOMAIN\omdr /DatareaderPassword:password /DataWriterUser:DOMAIN\omdw /DataWriterPassword:password /EnableErrorReporting:Always /SendCEIPReports:1 /UseMicrosoftUpdate:0

```

For more information, see [installing Operations Manager from the command prompt](install-using-cmdline.md).

During this time, agents will queue the data collected (alerts, events, performance, and so on) until they can resume communication with a management server in the management group. This approach avoids installing new instances of SQL Server and restoring databases from your last known good backup. However, in this recovery scenario there's likely going to be a longer delay in returning to an operable state given you'll need to deploy the other roles necessary to resume minimum monitoring functionality. If this approach isn't acceptable, you can deploy management servers in your secondary data center for on-standby recovery. Remove them as members of the three primary resources pools - All Management Servers Resource Pool, Notifications, and AD Assignment. This also includes any custom resource pool, which may include management servers hosted in the primary data center and need to continue to function as part of the recovery plan.  The System Center Data Access, System Center Configuration Management, and Microsoft Monitoring Agent services should be stopped and set to manual or disable and only started in a disaster recovery scenario.

If a management server is supporting integration (via a connector hosted directly on the management server or from another System Center product such as VMM, Orchestrator, or Service Manager), this will need to be planned for with manual or automatic recovery steps depending on the integration configuration and sequence of recovery steps. This ensures any other dependency on the management server is captured and planned for when the disaster recovery plan needs to be implemented.<br>

:::image type="content" source="./media/plan-hadr-design/om2016-dr-complex-config-inline.png" alt-text="Illustration of the Complex DR Config." lightbox="./media/plan-hadr-design/om2016-dr-complex-config-expanded.png":::

If one site goes offline, the agent will fail over to the management server in another site, assuming that the agent’s failover configuration allows this. Reconfigure the Windows agents to cache only management servers in your primary data center that should manage them to prevent them from attempting to failover to a management server in the secondary data center, which would only delay recovery and reporting.  This can be accomplished if you manually deploy the agent in an automated manner with a script (for example, VBScript, or better yet, PowerShell) to pre-configure during installation, or post deployment if you push the agent from the console, again using a scripted method managed with your enterprise configuration management solution.

Operations Manager can be deployed on Azure virtual machines as an alternative disaster recovery option to maintain continuity of the management group. It will be necessary to also deploy SQL Server on a virtual machine in Azure and not in a hybrid configuration, as the latency between a management server and the SQL Server hosting the Operations Manager databases will negatively affect the performance of the management group.  

Consider the monitoring scope, network topology, and network connectivity to Microsoft Azure (that is, site-to-site VPN or ExpressRoute), integration points (that is, ITSM solutions, other System Center products, third-part add-ons, and so on), console access, regulatory or relevant laws or policies, and so on in order to properly architect this scenario within Azure IaaS or other public cloud providers.  
