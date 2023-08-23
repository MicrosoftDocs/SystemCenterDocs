---
ms.assetid: 
title: Create a SQL MI
description: This article describes how to create a SQL managed instance in a dedicated subnet of virtual network.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 08/23/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create a SQL MI

This article describes how to create a SQL managed instance in a dedicated subnet of virtual network. Peer SCOM Managed Instance subnet and SQL MI subnet.

## Create and configure a SQL managed instance

Before you create a SCOM managed instance, create a SQL managed instance. For more information, see [Create a SQL managed instance](/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql&preserve-view=true).

We recommend the following settings for creating a SQL managed instance:

- **Resource Group**: Create a new resource group for Azure SQL Managed Instance (preview). A best practice is to create a new resource group for large Azure resources.
- **Managed Instance name**: Choose a unique name. This name is used while you create a SCOM managed instance to refer to this SQL managed instance.
- **Region**: Choose the region close to you. There's no strict requirement on region for the instance, but we recommend the closest region for latency purposes.
- **Compute+Storage**: General Purpose (Gen5) with eight cores is the default. This configuration suffices for the SCOM managed instance.
- **Authentication Method**: Select **SQL Authentication**. Enter the credentials that you want to use for accessing the SQL managed instance. These credentials don't refer to any that you've created so far.
- **VNet**: This SQL managed instance needs to have direct connectivity (line of sight) to the SCOM managed instance that you create in the future. Choose a virtual network that you'll eventually use for your SCOM managed instance. If you choose a different virtual network, ensure that it has connectivity to the SCOM Managed Instance (preview) virtual network by peering both SCOM Managed Instance VNet and SQL Managed Instance VNet.

   The subnet that you provide to Azure SQL Managed Instance has to be dedicated (delegated) to the SQL managed instance. The provided subnet can't be used to house any other resources.

   By design, a managed instance needs a minimum of 32 IP addresses in a subnet. As a result, you can use a minimum subnet mask of /27 when defining your subnet IP ranges. For more information, see [Determine required subnet size and range for Azure SQL Managed Instance](/azure/azure-sql/managed-instance/vnet-subnet-determine-size?view=azuresql&preserve-view=true).
- **Connection Type**: By default, the connection type is **Proxy**.
- **Public Endpoint**: This setting can be either **Enabled** or **Disabled**. To use Power BI reporting, you need to enable the public endpoint.

  If the Azure SQL Managed Instance virtual network is different from the SCOM Managed Instance (preview) virtual network:

  - Create an inbound NSG rule on the Azure SQL Managed Instance subnet to allow traffic from the SCOM Managed Instance subnet to port 3342 on SQL Managed Instance subnet. For more information, see [Configure a public endpoint in Azure SQL Managed Instance](/azure/azure-sql/managed-instance/public-endpoint-configure?view=azuresql&preserve-view=true).
  - Peer your Azure SQL Managed Instance virtual network with the one in which SCOM Managed Instance (preview) is present.

For the rest of the settings on the other tabs, you can leave them as default or change them according to your requirements.

>[!Note]
> Creation of a new SQL managed instance can take up to six hours.

After you create a SQL managed instance, you need to provide permission to the SCOM Managed Instance (preview) resource provider to access this SQL managed instance.

To provide the permission, follow these steps:

1. Open the SQL managed instance and select **Access control (IAM)**. On the top menu, select **+Add** > **Add role assignment**.

   :::image type="Access control" source="media/create-sql-mi/access-control.png" alt-text="Screenshot that shows selections for starting the process of adding a role assignment for access control.":::
1. On the **Add role assignment** pane:
   - For **Role**, select **Reader** from the dropdown list.
   - For **Assign access to**, select **User, group, or service principal** from the dropdown list.
   - For **Select**, enter **Microsoft.SCOM Resource Provider**.

   :::image type="Add role assignment" source="media/create-sql-mi/add-role-assignment.png" alt-text="Screenshot of selections for adding a role assignment.":::
1. Select **Save**.

## Next steps

- [Create a Key vault ](create-key-vault.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
