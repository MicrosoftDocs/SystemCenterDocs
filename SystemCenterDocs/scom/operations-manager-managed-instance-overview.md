---
ms.assetid: 
title: About Azure Monitor SCOM managed instance (preview)
description: This article describes about Azure Monitor SCOM managed instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 10/20/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# About Azure Monitor SCOM managed instance (preview)

This article provides you a quick service overview of Azure Monitor SCOM managed instance (preview).

With the integration of SCOM managed instance (preview), System Center Operations Manager functionality is now available on Azure. 
 
## Key benefits

Below are the key benefits of SCOM managed instance (preview)

- Get out of the stress of System Center Operations Manager infrastructure management. SCOM managed instance (preview) removes the burden of managing the management servers, web console, reporting server, and the databases.
- You can preserve and reuse all the investments made in System Center Operations Manager over the years.
- Monitor all your workloads running on-premises, Azure, or in any other cloud service.
- Have a consolidated administration and management experience for all your monitoring needs via the Azure portal.

## Features

SCOM managed instance (preview) functionality allows you to:

- Configure an E2E System Center Operations Manager setup (SCOM managed instance (preview)) on Azure.
- Manage (view, delete) your SCOM managed instance (preview) in Azure.
- Connect to your SCOM managed instance (preview) using the System Center Operations Manager Ops Console.
- Monitor workloads (wherever they're located) using the Ops and Web Console, and while using your existing management packs.
- Incur zero database maintenance (Ops database and Data warehouse database) because of the offloading of database management to SQL Managed Instance (SQL MI).
- Scale your instance immediately without the need to add/delete physical servers/VMs.
- View your reports in Power BI.
- Patch your instance immediately with the latest bug fixes and features. 

## Architecture

:::image type="SCOM MI architecture" source="media/operations-manager-managed-instance-overview/architecture.png" alt-text="Screenshot showing architecture.":::

When you create a SCOM managed instance (preview) (which is equivalent to your System Center Operations Manager Management Group), you’ll get a load-balancer behind which your management servers functions. When you create a new instance, the load-balancer will have one management server; Number changes depending on how you decide to scale your instance. Additionally, you’ll also get a web console running on the same management server VM. On the SQL MI instance, you'll get two databases (Ops database & DW database). The entire infrastructure will be located on Azure.

When you connect your existing agents to your Azure-based SCOM managed instance (preview), ensure that there's a direct network connectivity (line-of-sight) between your existing network and your network in Azure. If your existing agents are in an untrusted domain, then connect a gateway server.

## Next steps

> [!div class="nextstepaction"]
> [Create a SCOM managed instance (preview) on Azure](create-operations-manager-managed-instance.md)