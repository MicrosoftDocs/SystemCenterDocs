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
---

# About Aquila

Welcome to the Aquila service! This article provides a quick service overview.

Aquila is a service that provides SCOM functionality on Azure and it can be used to monitor all your workloads, whether on-prem, in Azure, or in any other cloud service. Aquila is in very early stages of development and it is the first time it is being previewed with customers.

During the public preview, you can:

- Configure an E2E SCOM setup (Aquila instance) on Azure.
- Manage (view, delete) your Aquila instances in Azure.
- Connect to your Aquila instance using the SCOM Ops Console.
- Monitor workloads (wherever they are located) using the Ops and Web Console, and while using your existing management packs.
- Incur zero DB maintenance (Ops DB and Data warehouse DB) because of the offloading of database management to SQL Managed Instance (SQL MI).

For this Public Preview, the architecture of Aquila will be as follows:

:::image type="Architecture" source="media/aquila-overview/architecture.png" alt-text="Screenshot of architecture.":::

When you create an Aquila instance (which is equivalent to your SCOM Management Group), you will get 1 Management Server and 1 Web Console, all of them running on the same 1 VM that will be located in your Azure subscription. On the SQL MI instance, you will get 2 databases (Ops DB & DW DB). The entire infrastructure will be located on Azure.

Meanwhile, you will also have to connect your existing agents (if your agents are in an untrusted domain, then you will have to connect a gateway server too) to your Azure-based Aquila instance by ensuring that there is a direct network connectivity (line-of-sight) between your existing network and your network in Azure.

Pre-requisites
Before getting into the pre-requisites, look at the Pointers to note before trying the preview

If all of these words are frightening you, don't be! The entire journey is documented in this Github repository with each step explained in detail. So let's begin that journey and introduce you to the pre-requisites that you need to fulfill in order to create an Aquila instance. The numbers in the diagram below correspond to the steps you need to complete.

:::image type="Prerequisite steps" source="media/aquila-overview/prerequisite-steps.png" alt-text="Screenshot of prerequisite steps.":::

1. Establish direct connectivity (line-of-sight) between your DC and your Azure network
2. Configure 1 domain account in Active Directory
3. Create a Managed Service Identity (MSI)
4. Configure Aquila RBAC
5. Create and configure an SQL MI Instance

With the pre-requisites completed, you can

6. Begin creating an Aquila instance