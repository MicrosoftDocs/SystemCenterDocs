---
ms.assetid: f70d4861-d0ec-43df-ba9c-7acdd1238ffb
title: Resource Pool Design Considerations
description: This article provides an overview of the design decisions with resource pools  when planning a management group configuration for your Operations Manager 2016 deployment.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/04/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Resource pool design considerations

>Applies To: System Center 2016 - Operations Manager

A Resource Pool is a logical grouping of management servers and/or gateway servers used to distribute work among themselves and take over work from a failed member.  In other words, they provide high availability and scalability for workflows.  When designing a management group, considerations must be made when monitoring of network devices, Linux/UNIX systems, and other workloads that are designed to take advantage of a resource pool.  

## Overview

Resource pools ensure the continuity of monitoring by providing multiple management servers  and/or gateway servers that can take on monitoring workflows if one of the members becomes unavailable. You can create resource pools for specific purposes. For example, you might create a resource pool of management servers that are located in the same geographic area to provide network device monitoring.

Resource pools apply a logic similar to clustering “majority node set”, where (< number of nodes as members of the pool > /2) + 1.  At a minimum, there must be three members in the resource pool to maintain quorum - two must be management servers, and the third is an observer (commonly referred to as the witness in clustering terminology).  The Operations Manager database is always the observer and given a vote, even if you have an even number of members in the pool, in order to allow quorum to be reached.  You can designate a management server or gateway server to be the observer if you do not wish to have the Operational database serve as the observer.

With the introduction of resource pools it is recommended that all members are connected by a low latency network (less than 10 ms). Resource pools should not be deployed across multiple data centers or in a hybrid-cloud environment like Microsoft Azure.

There are two types of membership, automatic and manual.  When you create a resource pool, it's membership is set to manual and cannot be reconfigured to automatic.  When a System Center 2016 – Operations Manager management group is created, three resource pools are created by default  with automatic membership.  The following table describes these three resource pools.

| Resource Pool Name | Description 
|----------|---------- 
| All Management Servers Resource Pool | Performs workflows for group calculation, availability, distributed monitor health rollup, and database grooming.
| Notifications Resource Pool | The Alert Subscription Service workflows are targeted to this Resource Pool to support alert notifications.
| AD Assignment Resource Pool | The AD Integration workflows are targeted to this Resource Pool to support automatic agent assignment to management servers.


Because membership of the All Management Servers Resource Pool is automatic, any management server that is commissioned is automatically made a member of this Resource Pool.  In certain architectures and design considerations, such as those incorporating geographically dispersed contingency operations, automatic assignment to the All Management Servers Resource Pool may not be desired.  In these situations, it is possible to change the membership assignment from automatic to manual.  As such, management servers must be added to the All Management Servers Resource Pool through manual assignment.

> [!NOTE] 
> The membership of the All Management Servers Resource Pool is read-only.  To change its membership  from automatic to manual, see [Modifying Pool Membership](../Manage/how-to-manage-resource-pools.md#modifying-resource-pool-membership)
   

## Monitoring scenarios supporting resource pools

The following workflows are hosted by resource pools in Operations Manager:

- Management of network devices
- Management of UNIX/Linux agents
- Monitoring web application URLs

> [!NOTE] 
> Windows agents do not report to resource pools.

Network monitoring in Operations Manager requires its own separate, dedicated resource pool.  This is because network monitoring workflows run on management servers (on the SNMP module) and not on agents.  This places a heavy load on the management servers once you include monitoring of network ports, especially if you select most of the active ports available on the device.  Therefore, for better performance, we recommend using dedicated management servers in dedicated resource pools for network monitoring.  Additionally, the management servers that are members of this pool should be removed from the All Management Servers, Notifications, and AD Assignment pools.  

Linux/UNIX monitoring in Operations Manager can be assigned to a dedicated resource pool if necessary to enable high-availability monitoring and agent management, but is not required.  Operations Manager uses certificates to authenticate access to the computers it is managing. When the Discovery Wizard deploys an agent, it retrieves the certificate from the agent, signs the certificate, deploys the certificate back to the agent, and then restarts the agent.  To support high availability, each management server in the resource pool must have all the root certificates that are used to sign the certificates that are deployed to the agents on the UNIX and Linux computers. Otherwise, if a management server becomes unavailable, the other management servers would not be able to trust the certificates that were signed by the server that failed. 


