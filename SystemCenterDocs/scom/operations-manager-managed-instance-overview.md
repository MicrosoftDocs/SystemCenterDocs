---
ms.assetid: 
title: About Azure Monitor SCOM Managed Instance (preview)
description: This article describes about Azure Monitor SCOM Managed Instance (preview).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/29/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# About Azure Monitor SCOM Managed Instance (preview)

This article provides you a quick service overview of Azure Monitor SCOM Managed Instance (preview).

With the integration of SCOM Managed Instance (preview), System Center Operations Manager functionality is now available on Azure. 

SCOM Managed Instance (preview) is a cloud-based alternative for SCOM customers. SCOM Managed Instance (preview) provides you with continuous monitoring of your workloads with minimal infrastructure management, through migrations or after you enable Azure connectivity for your On-premises environments. 
 
## Key benefits

The key benefits of SCOM Managed Instance (preview) are:

- **Preserve investments in SCOM**: Allows you to preserve your existing SCOM investments. SCOM Managed Instance (preview) is compatible with all existing SCOM Management Packs and provide a means to migrate Management Pack configurations from the on-premises setup.  

- **Simplify SCOM-infrastructure management**: All the cloud connected SCOM components are managed by Microsoft, removes the responsibility of hardware/software updates and security patches.  

- **Monitor continuously through migration**: Won't cause disruptions in monitoring while you migrate infrastructure or workloads from on-premises to the cloud. As you migrate from one UR to the next, you can migrate from your existing SCOM setup.

- **Monitor workloads everywhere**:  SCOM Managed Instance (preview) is hosted in Azure with the capability of monitoring workloads running wherever they are (in Azure or on-premises) without the need to modification.     

## Features

SCOM Managed Instance (preview) functionality allows you to:

- Configure an E2E System Center Operations Manager setup (SCOM Managed Instance (preview)) on Azure.
- Manage (view, delete) your SCOM Managed Instance (preview) in Azure.
- Connect to your SCOM Managed Instance (preview) using the System Center Operations Manager Ops Console.
- Monitor workloads (wherever they're located) using the Ops and Web Console, and while using your existing management packs.
- Incur zero database maintenance (Ops database and Data warehouse database) because of the offloading of database management to SQL Managed Instance (SQL MI).
- Scale your instance immediately without the need to add/delete physical servers.
- View your SCOM Managed Instance (preview) reports in Power BI.
- Patch your instance in one-click with the latest bug fixes and features. 

## Architecture

:::image type="SCOM MI architecture" source="media/operations-manager-managed-instance-overview/architecture.png" alt-text="Screenshot showing architecture.":::

A SCOM Managed Instance (preview) consists of two parts: 
   - A Microsoft-managed part
   - A customer-managed part

### A Microsoft-managed part

A Microsoft-managed part consists of Management Servers and the [Azure SQL Managed Instance](/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview?view=azuresql&preserve-view=true) hosting an Operations database and Data Warehouse database. The Azure-hosted components can be managed directly from the Azure portal. At the back-end, the components interact continuously with ARM and the RP to carry out Azure-based operations. 


The databases hosted in the SQL MI allow formation and to view reports in Power BI. The Management Servers can be scaled up/down based on your requirements. When you create a new instance, you will get one management server. The number changes depending on how you decide to scale your instance. Furthermore, you can update your management servers at the click of a button.

### A customer-managed part

On the customer-managed part, there will be an Ops and Web Console that will be used to monitor and administer the instance. The agents to be monitored will be under the customer domain, and if they are in another domain, a gateway server will be needed to carry out the authentication. The customer-managed part will also host a DNS with a static IP that will be provided to the Management Servers hosted in Azure.  

## Next steps

> [!div class="nextstepaction"]
> [Create a SCOM Managed Instance (preview) on Azure](create-operations-manager-managed-instance.md)