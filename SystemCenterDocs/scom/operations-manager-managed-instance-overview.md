---
ms.assetid: 
title: About Azure Monitor SCOM Managed Instance (preview)
description: This article describes about Azure Monitor SCOM Managed Instance (preview).
author: Farha-Bano
ms.author: v-farhabano
manager: jsuri
ms.date: 09/21/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# About Azure Monitor SCOM Managed Instance (preview)

This article provides you with a quick service overview of Azure Monitor SCOM Managed Instance (preview).

With the integration of SCOM Managed Instance (preview), System Center Operations Manager functionality is now available on Azure.

SCOM Managed Instance (preview) is a cloud-based alternative for System Center Operations Manager customers. SCOM Managed Instance (preview) provides you with continuous monitoring of your workloads with minimal infrastructure management through migrations or after you enable Azure connectivity for your on-premise environments. 

> [!VIDEO https://www.youtube.com/embed/lOlUq72wWag]

To know about the SCOM Managed Instance (preview) Architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

## Key benefits

The key benefits of SCOM Managed Instance (preview) are:

- **Preserves investments in SCOM**: Allows you to preserve your existing System Center Operations Manager investments. SCOM Managed Instance (preview) is compatible with all the existing System Center Operations Manager management packs and provides a means to migrate management pack configurations from the on-premises setup.  

- **Simplifies System Center Operations Manager infrastructure management**: All the cloud connected System Center Operations Manager components are managed by Microsoft; removes the responsibility of hardware/software updates and security patches.  

- **Continues monitoring through migration**: Won't cause disruptions in monitoring while you migrate infrastructure or workloads from on-premises to the cloud. As you migrate from one UR to the next, you can migrate from your existing System Center Operations Manager setup.

- **Monitors workloads everywhere**:  SCOM Managed Instance (preview) is hosted in Azure with the capability of monitoring workloads running wherever they are (in Azure or on-premises) without the need for modification.

## Features

> [!VIDEO https://www.youtube.com/embed/MG5kGoe1zj0]

SCOM Managed Instance (preview) functionality allows you to:

- Configure an E2E System Center Operations Manager setup (SCOM Managed Instance (preview)) on Azure.
- Manage (view, delete) your SCOM Managed Instance (preview) in Azure.
- Connect to your SCOM Managed Instance (preview) using the System Center Operations Manager Ops console.
- Monitor workloads (wherever they're located) using the Ops and Web console, and while using your existing management packs.
- Incur zero database maintenance (Ops database and Data warehouse database) because of the offloading of database management to SQL Managed Instance (SQL MI).
- Scale your instance immediately without the need to add/delete physical servers.
- View your SCOM Managed Instance (preview) reports in Power BI.
- Patch your instance in one click with the latest bug fixes and features. 

## Architecture

:::image type="SCOM Managed Instance (preview) architecture" source="media/operations-manager-managed-instance-overview/architecture.png" alt-text="Screenshot showing architecture.":::

A SCOM Managed Instance (preview) consists of two parts: 
   - A Microsoft-managed part
   - A customer-managed part

### A Microsoft-managed part

A Microsoft-managed part consists of Management Servers and the [Azure SQL Managed Instance](/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview?view=azuresql&preserve-view=true) hosting an Operations database and Data Warehouse database. The Azure-hosted components can be managed directly from the Azure portal. At the backend, the components interact continuously with ARM and the RP to carry out Azure-based operations.


The databases hosted in the SQL MI allow formation and to view reports in Power BI. The Management Servers can be scaled up/down based on your requirements. When you create a new instance, you get one management server. The number changes depending on how you decide to scale your instance. You can update your management servers at the click of a button.

### A customer-managed part

A customer-managed part consists of Ops and Web console that are used to monitor and administer the instance. The agents to be monitored are under the customer domain, and if they are in another domain, a gateway server is needed to carry out the authentication. The customer-managed part hosts a DNS with a static IP that is provided to the Management Servers hosted in Azure.

**Detailed Architecture of SCOM Managed Instance**

:::image type="Detailed architecture" source="media/operations-manager-managed-instance-overview/detailed-scom-managed-instance-architecture-inline.png" alt-text="Screenshot of SCOM Managed Instance detailed architecture."lightbox="media/operations-manager-managed-instance-overview/detailed-scom-managed-instance-architecture-expanded.png":::

SCOM Managed Instance deploys and manages Operations Manager in customer subscription. It establishes connectivity to the on-premises monitored agents through VPN/Express Route.

In customer subscription, SCOM Managed Instance, creates a Virtual Machine Scale Set in a managed resource group and deploys Operations Manager on the VMSS, which is front-loaded with Load Balancer for resiliency and elasticity. Operations Manager Management server connects to customer provided SQL MI for Database operations. Both SQL MI and VMSS are created in different VNets and are joined to establish line of sight.

Operations Manager Management server and monitored agents are connected through ER/VPN. Agents establish session with Operations Manager Management server using the Kerberos authentication, where Operations Manager VMSS VMs are joined to the AD domain of the monitored agents. 

## Next steps

  To create SCOM Managed Instance (preview), follow these steps:

   - [Step 1. Register the SCOM Managed Instance resource provider](register-scom-managed-instance-resource-provider.md).
   - [Step 2. Create separate subnet in a VNet](create-separate-subnet-in-vnet.md).
   - [Step 3. Create a SQL Managed Instance](create-sql-managed-instance.md).
   - [Step 4. Create a Key vault](create-key-vault.md).
   - [Step 5. Create a user assigned identity](create-user-assigned-identity.md).
   - [Step 6. Create a computer group and gMSA account](create-gmsa-account.md).
   - [Step 7. Store domain credentials in Key vault](store-domain-credentials-in-key-vault.md).
   - [Step 8. Create a static IP](create-static-ip.md).
   - [Step 9. Configure the network firewall](configure-network-firewall.md).
   - [Step 10. Verify Azure and internal GPO policies](verify-azure-and-internal-gpo-policies.md).
   - [Step 11. SCOM Managed Instance self-verification of steps](scom-managed-instance-self-verification-of-steps.md).
   - [Step 12. Create a SCOM Managed Instance (preview)](create-operations-manager-managed-instance.md).

[Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview)](migrate-to-operations-manager-managed-instance.md).

**Feedback**

Provide your feedback on Azure Monitor SCOM Managed Instance (preview) [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).