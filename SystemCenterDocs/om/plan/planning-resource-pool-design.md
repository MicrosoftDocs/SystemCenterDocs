---
ms.assetid: f70d4861-d0ec-43df-ba9c-7acdd1238ffb
title: Resource Pool Design Considerations
description: This article provides an overview of the design decisions with resource pools  when planning a management group configuration for your Operations Manager 2016 deployment.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/16/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Resource pool design considerations

>Applies To: System Center 2016 - Operations Manager

A Resource Pool is a logical grouping of management servers and/or gateway servers used to distribute work among themselves and take over work from a failed member.  In other words, they provide high availability and scalability for workflows.  When designing a management group, considerations must be made for monitoring of network devices, Linux/UNIX systems, and other workloads that are designed to take advantage of a resource pool.  

## Overview

Resource pools ensure the continuity of monitoring by providing multiple *members*, which are management servers and/or gateway servers that can take over monitoring workflows if one of the members of the pool becomes unavailable. You can create resource pools for specific purposes. For example, you might create a resource pool of management servers in your primary data center to monitor network devices. 

Resource pools apply a logic similar to clustering “majority node set”, where (< number of nodes as members of the pool > /2) + 1.  At a minimum, there must be three members in the  pool to maintain quorum, which must be more than 50% of the quorum voting members in a pool to maintain availability of the pool.  If you only have two members of the pool, and one is unavailable, you have lost quorum.  

For every resource pool created in the Operations console, the Operations Manager database, which is referred to as the *default observer*, is always given a vote, even if you have an even number of members in the pool in order to allow quorum to be reached.  This also applies to the three resource pools created by default when you first create the management group, which is discussed later in this topic.  For all resource pools created using the PowerShell cmdlet **NewSCOM-ResourcePool**, it is set to disabled by default. Including the Operations Manager database as the *default observer* reduces complexity of your management group by only requiring you to deploy two management servers at a minimum to maintain high availability of your resource pools.   

Another role supporting a resource pool are *Observers*.  This is a management server or a Gateway server that does not participate in loading workflows for the pool; however they participate in quorum decisions.  This is never used under normal circumstances, and therefore should not be considered.  

There are two types of membership, automatic and manual.  When you create a resource pool, it's membership is set to manual and cannot be reconfigured to automatic.  When a System Center 2016 – Operations Manager management group is created, three resource pools are created by default with automatic membership.  The following table describes these three resource pools.

| Resource Pool Name | Description 
|----------|---------- 
| All Management Servers Resource Pool | Performs workflows for group calculation, availability, distributed monitor health rollup, and database grooming.
| Notifications Resource Pool | The Alert Subscription Service workflows are targeted to this Resource Pool to support alert notifications.
| AD Assignment Resource Pool | The AD Integration workflows are targeted to this Resource Pool to support automatic agent assignment to management servers.

Because membership of the All Management Servers Resource Pool is automatic, any management server that is commissioned is automatically made a member of this resource pool.  In certain architectures and design considerations, such as those incorporating geographically dispersed contingency operations, automatic assignment to the All Management Servers Resource Pool may not be desired.  In these situations, it is possible to change the membership assignment from automatic to manual.  As such, management servers must be added to the All Management Servers Resource Pool through manual assignment.

> [!NOTE] 
> The membership of the All Management Servers Resource Pool is read-only.  To change its membership from automatic to manual, see [Modifying Pool Membership](../Manage/how-to-manage-resource-pools.md#modifying-resource-pool-membership).

With the introduction of resource pools it is recommended that all members are connected by a low latency network (less than 10 ms). Resource pools should not be deployed across multiple data centers or in a hybrid-cloud environment like Microsoft Azure.

### Resource Pool availability examples

The following examples demonstrate the concept of resource pool availability based on the following configurations, only with management servers or only with Gateway servers.  

#### Single management server

* The *default observer* is enabled by default and provides no benefit since there are only two members and quorum is not reached.
* There is no high availability, because the management server is a single point of failure.

#### Two management servers 

* The *default observer* is enabled by default.
* There is high availability for the pool, because there are three voting members - two management servers and the *default observer*.
* If you disable the *default observer*, you will lose high availability for the pool.

#### Three management servers

* The *default observer* is enabled by default.
* There is high availability for the pool, because there are four voting members - three management serves and the *default observer*.
* By default you can only have one management server unavailable in order to maintain quorum.  If two management servers are unavailable, you have exactly 50% of voting members and the resource pool no longer functions to manage the monitoring workloads.  
- The *default observer* does not increase the number of management servers that can be down, therefore it does not increase pool availability.
- You can consider removing the *default observer* in this scenario.

#### Four management servers

* The *default observer* is enabled by default.
* There is high availability for the pool, because there are five voting members - four management servers and the *default observer*. 
* By default you can only have two management server unavailable in order to maintain  quorum.  If three management servers are down, you have less than 50% of voting members and the resource pool no longer functions to manage the monitoring workloads.    
* The *default observer* in this scenario provides significant value, because it increases the number of management servers that can be down.  Without the *default observer*, you would only have four quorum members, which only allows for one member to be unavailable.

#### Five management servers

* The *default observer* is enabled by default.
* There is high availability for the pool, because there are six voting members - five management servers and the *default observer*.  
* By default you can only have two management servers unavailable to maintain quorum. If three management servers are unavailable, this is exactly 50% of voting members, and the resource pool no longer functions to manage the monitoring workloads.    
* The *default observer* does not increase the number of management servers that can be down, therefore it does not increase pool availability.
* You can consider removing the *default observer* in this scenario.

Once you reach three or more management servers in a resource pool, where you have an odd number of members in the pool, you can consider removing the *default observer* as a member.  If you reach five management servers, there is the potential for the Operational database to experience significant load which might generate enough latency to affect  resource pool calculations.  

With the way the *default observer* plays a role, each management server in the pool queries its own local SDK service, which allows it to query a table in the Operational database for the *default observer*. If the SDK service or database is under a load, you will experience latency that would otherwise not exist.   

#### Single Gateway server

* The *default observer* is enabled by default.
* There is no high availability because the Gateway server is a single point of failure.
* The *default observer* should not be used here because Gateway servers do not have a local SDK service and therefore cannot query the Operational database.

#### Two Gateway servers

* The *default observer* is enabled by default.
* There is no high availability because there are only two members of the pool and the *default observer* is not a participant because Gateway servers do not directly communicate with the Operational database.  Three Gateway servers are required to maintain pool quorum.  

#### Three Gateway servers

* The *default observer* is enabled by default.
* There is high availability for the pool, because there are three voting members - three Gateway servers.
* By default you can only have one Gateway server unavailable to maintain to maintain quorum. If two Gateway servers are down, this is less than 50% of voting members, and the resource pool no longer functions to manage the monitoring workloads.
* The *default observer* should not be used here because Gateway servers do not have a local SDK service and therefore cannot query the Operational database.

## Monitoring scenarios supporting resource pools

The following workflows are hosted by resource pools in Operations Manager:

- Management of network devices
- Management of UNIX/Linux agents
- Monitoring web application URLs

> [!NOTE] 
> Windows agents do not report to resource pools.

Network monitoring in Operations Manager requires its own separate, dedicated resource pool.  This is because network monitoring workflows run on management servers (on the SNMP module) and not on agents.  This places a heavy load on the management servers once you include monitoring of network ports, especially if you select most of the active ports available on the device.  Therefore, for better performance, we recommend using dedicated management servers in dedicated resource pools for network monitoring.  Additionally, the management servers that are members of this pool should be removed from the All Management Servers, Notifications, and AD Assignment pools.  

Linux/UNIX monitoring in Operations Manager can be assigned to a dedicated resource pool if necessary to enable high-availability monitoring and agent management, but is not required.  Operations Manager uses certificates to authenticate access to the computers it is managing. When the Discovery Wizard deploys an agent, it retrieves the certificate from the agent, signs the certificate, deploys the certificate back to the agent, and then restarts the agent.  To support high availability, each management server in the resource pool must have all the root certificates that are used to sign the certificates that are deployed to the agents on the UNIX and Linux computers. Otherwise, if a management server becomes unavailable, the other management servers would not be able to trust the certificates that were signed by the server that failed. 

## Next steps

To learn how to create and manage resource pools, see [How to manage resource pools](../manage/how-to-manage-resource-pools.md).
