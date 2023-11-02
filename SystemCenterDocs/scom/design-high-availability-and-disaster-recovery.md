---
ms.assetid: 
title: Design for High Availability and Disaster Recovery
description: This article describes about the Design for High availability and disaster recovery.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/02/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Design for High Availability and Disaster Recovery

## High Availability (HA)

In Azure Monitor SCOM Managed Instance, High Availability is defined as the amount of time for which the SCOM Managed Instance service is up and running. When you use SCOM Managed Instance, the service SLA is 99.9%. [Learn more](https://azure.microsoft.com/products/virtual-machines).

>[!NOTE]
>This service SLA is different from the Instance SLA (which is defined by various factors such as the network connectivity from the customer's end, AD availability in the customer's domain etc.).

An SLA of 99.9% implies a downtime of only 9 hours in an entire year.

## Customer-enabled Disaster Recovery for Region Redundancy

Disaster recovery relates to measures taken to ensure that operations can be resumed if a catastrophic failure occurs. In Azure, a disaster can occur if an Azure region becomes unavailable for some time. To protect against such disasters, customers can plan for disaster recovery of their instance by planning to deploy two SCOM managed instances in separate regions (for example, one in West US and the other in West Europe).

Given that the customer has deployed both the instances by themselves, they will have to ensure that both the setups have the same configuration and are constantly kept synchronised with each other.

### Key points

- Integration with other monitoring platforms or ITSM platforms such as Remedy or ServiceNow will need to exist in the secondary instance as well, and possibly configured in an active/passive state to avoid duplication of incidents.
- If management packs are installed, they must be configured in both the instances.
- Customers need to do multi-homing to ensure that agents send data to both the instances at the same time.

Following is an example architecture of the scenario explained earlier:
 
 
## SCOM Managed Instance Zone Redundancy

A SCOM Managed Instance by architecture is zone redundant. Zones are smaller subsets of individual regions with each region housing about two or three zones.

This means that if a zone in a region becomes unavailable, the SCOM Managed Instance will still be available. We achieve zone redundancy by deploying the SCOM Managed Instance service resources in a secondary region that is separate from the primary region chosen during instance creation.

For example, if you decide to create a SCOM managed instance in West Europe, we deploy a parallel set of SCOM Managed Instance service resources in another region such as North Europe. The resources in the secondary region will be same as the resources in the primary region, which helps the service to be highly available.

All these operations are carried out without any user involvement and ensure that the SCOM Managed Instance service is region redundant.

## Next steps

[Create a SCOM Managed Instance](create-operations-manager-managed-instance.md).