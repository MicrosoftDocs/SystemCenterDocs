---
ms.assetid: 
title: About Aquila
description: This article describes about Aquila.
author: jyothisuri
ms.author: jsuri
manager: jsuri
ms.date: 10/04/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: 'sc-om-2022'
---

# About Aquila

Welcome to the Aquila service! This article provides a quick service overview.

Aquila is a service that provides System Center Operations Manager functionality on Azure to monitor all your workloads, whether on-premises, in Azure, or in any other cloud service.

During the public preview, you can:

- Configure an E2E System Center Operations Manager setup (Aquila instance) on Azure.
- Manage (view, delete) your Aquila instances in Azure.
- Connect to your Aquila instance using the System Center Operations Manager Ops Console.
- Monitor workloads (wherever they are located) using the Ops and Web Console, and while using your existing management packs.
- Incur zero DB maintenance (Ops DB and Data warehouse DB) because of the offloading of database management to SQL Managed Instance (SQL MI).

## Architecture

Below is the architecture for Aquila (Public preview):

:::image type="Architecture" source="media/aquila-overview/architecture.png" alt-text="Screenshot of architecture.":::

When you create an Aquila instance (which is equivalent to your System Center Operations Manager Management Group), you will get one Management Server and one Web Console, all of them running on the same VM that is located in your Azure subscription. On the SQL MI instance, you will get two databases (Ops DB & DW DB). The entire infrastructure will be located on Azure.

Meanwhile, connect your existing agents to your Azure-based Aquila instance by ensuring that there is a direct network connectivity (line-of-sight) between your existing network and your network in Azure. If your existing agents are in an untrusted domain, then connect a gateway server.

## Pre-requisites

1. Establish direct connectivity (line-of-sight) between your DC and your Azure network
2. Configure one domain account in Active Directory
3. Create a Managed Service Identity (MSI)
4. Configure Aquila RBAC
5. Create and configure an SQL MI Instance