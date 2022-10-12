---
ms.assetid: 
title: About Operations Manager managed instance (preview)
description: This article describes about Operations Manager managed instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 10/11/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# About Operations Manager managed instance (preview)

This article provides you a quick service overview of Operations Manager managed instance (preview) in System Center.

With the integration of Operations Manager managed instance (preview), System Center Operations Manager functionality is now available on Azure. Operations Manager managed instance enables you to monitor all your workloads running on-premises, in Azure, or in any other cloud service.

You can now:

- Configure an E2E System Center Operations Manager setup (Operations Manager managed instance (preview)) on Azure.
- Manage (view, delete) your Operations Manager managed instance (preview) in Azure.
- Connect to your Operations Manager managed instance (preview) using the System Center Operations Manager Ops Console.
- Monitor workloads (wherever they're located) using the Ops and Web Console, and while using your existing management packs.
- Incur zero database maintenance (Ops database and Data warehouse database) because of the offloading of database management to SQL Managed Instance (SQL MI).

## Architecture

When you create an Operations Manager managed instance (preview) (which is equivalent to your System Center Operations Manager Management Group), you'll get one Management Server and one Web Console, running on the same VM in your Azure subscription. On the SQL MI instance, you'll get two databases (Ops database & DW database). The entire infrastructure will be located on Azure.

When you connect your existing agents to your Azure-based Operations Manager managed instance (preview), ensure that there's a direct network connectivity (line-of-sight) between your existing network and your network in Azure. If your existing agents are in an untrusted domain, then connect a gateway server.

## Next steps

> [!div class="nextstepaction"]
> [Create a Operations Manager managed instance (preview) on Azure](create-operations-manager-managed-instance.md)