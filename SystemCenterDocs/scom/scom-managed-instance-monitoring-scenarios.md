---
ms.assetid: 
title: Azure Monitor SCOM Managed Instance (preview) monitoring scenarios
description: This article provides a high-level overview of the supported monitoring scenarios with Azure Monitor SCOM Managed Instance (preview).
author: Farha-Bano
ms.author: v-farhabano
manager: jsuri
ms.date: 02/13/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Azure Monitor SCOM Managed Instance (preview) monitoring scenarios

Azure Monitor SCOM Managed Instance (preview) supports various methods to actively monitor different services and the components and devices that support them.

This article provides a high-level overview of the supported monitoring scenarios with Azure Monitor SCOM Managed Instance (preview).

## Monitor a workload on-premises

SCOM Managed Instance (preview) allows you to monitor your on-premises workloads. 

To monitor on-premises workload, follow these steps:

1. Connect your instance to the Operations console.
2. Import the management pack of the on-premises workload that you plan to monitor.
3. After successfully importing the management pack, begin monitoring your workload.

## Monitor a workload in Azure 

SCOM Managed Instance (preview) allows you to monitor the workloads that you've migrated to cloud VMs. 

To monitor a cloud workload, follow these steps:

1. Connect your instance to the Operations console.
2. Import the management pack of the cloud workload that you plan to monitor.
3. After successfully importing the management pack, begin monitoring your workload.

## Monitor workloads running on-premises and in Azure 

If you've some workloads running on-premises and some in Azure, you can use SCOM Managed Instance (preview) to monitor all of them simultaneously. 

To monitor your workloads (both on-premises and in Azure), follow these steps:

1. Connect your instance to the Operations console.
2. Import the management pack of the workload that you plan to monitor.
3. After successfully importing the management pack, begin monitoring your workload.

## Agentless monitoring 

In SCOM Managed Instance (preview), agents need to be installed manually. The Discovery wizard isn't supported. 

## Next steps

[Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview)](migrate-to-operations-manager-managed-instance.md).

**Feedback**

Provide your feedback on Azure Monitor SCOM Managed Instance (preview) [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
