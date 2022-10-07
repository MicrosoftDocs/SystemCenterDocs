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

This article provides you a quick service overview of Aquila in System Center.

With the integration of Aquila, System Center Operations Manager functionality is now available on Azure that enables you to monitor all your workloads running in on-premises, in Azure, or in any other cloud service.

You can now:

- Configure an E2E System Center Operations Manager setup (Aquila instance) on Azure.
- Manage (view, delete) your Aquila instances in Azure.
- Connect to your Aquila instance using the System Center Operations Manager Ops Console.
- Monitor workloads (wherever they are located) using the Ops and Web Console, and while using your existing management packs.
- Incur zero database maintenance (Ops database and Data warehouse database) because of the offloading of database management to SQL Managed Instance (SQL MI).

## Architecture

When you create an Aquila instance (which is equivalent to your System Center Operations Manager Management Group), you'll get one Management Server and one Web Console, running on the same VM in your Azure subscription. On the SQL MI instance, you'll get two databases (Ops database & DW database). The entire infrastructure will be located on Azure.

When you connect your existing agents to your Azure-based Aquila instance, ensure that there is a direct network connectivity (line-of-sight) between your existing network and your network in Azure. If your existing agents are in an untrusted domain, then connect a gateway server.

## Next steps

> [!div class="nextstepaction"]
> [Create an Aquila instance on Azure](create-aquila-instance.md)