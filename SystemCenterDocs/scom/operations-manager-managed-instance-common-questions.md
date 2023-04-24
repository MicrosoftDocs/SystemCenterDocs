---
ms.assetid: 
title: Azure Monitor SCOM Managed Instance (preview) frequently asked questions
description: This article summarizes frequently asked questions about Azure Monitor SCOM Managed Instance (preview).
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

# Azure Monitor SCOM Managed Instance (preview) frequently asked questions

This article summarizes frequently asked questions about Azure Monitor SCOM Managed Instance (preview).

## Virtual Network (VNet)

### What regions do the VNet need to be in?

To maintain latency, we recommend you have the VNet in the same region as your other Azure resources.

### What address range does the VNet need?

The minimum address space is /27 (which means /28 and above wouldn't work).

### How many subnets does the VNet need to have?

- VNet needs two subnets. 
    - For SCOM Managed Instance (preview)
    - For SQL Managed Instance
- The subnet for SQL MI instance will be a delegated (dedicated) subnet and won't be used by the SCOM Managed Instance (preview). Name the subnets accordingly to avoid confusion in the future while you create the SQL MI/SCOM Managed Instance (preview).

### What address range do the two subnets need?

The minimum address space needs to be /27 for SQL MI subnet and /28 for the SCOM Managed Instance (preview) subnet.

### Do the subnets need to specify a NAT gateway or Service Endpoint?

No, both the options can be left blank.

### Are there limitations on the security options in the Create VNet experience (BastionHost, DDoS, Firewall)?

No, you can disable all of them or enable any of them based on your organization's preferences.

### I created separate VNets in Azure. What steps do I need to take?

If you have multiple VNets created, you need to peer your VNets. If you're peering any two networks, ensure to peer from both networks to each other. Thus, if you peer three networks, you'll need to do six peerings. For more information on peering, see [Azure Virtual Network peering](/azure/virtual-network/virtual-network-peering-overview).

### What options do I select while peering?

- You need to specify a peering name (in the field **Peering link name**).
- The first name is used to name the peer network from the current network to the other network. The second name is used to name the peer network from the other network to this network.
- In the section *Virtual Network*, specify the name of the VNet that you're peering. If you can't find the VNet, you can search for it using the *Resource ID*. Retain the rest of the options as default.

     :::image type="Add peering" source="media/operations-manager-managed-instance-common-questions/add-peering-inline.png" alt-text="Screenshot showing add peering screen." lightbox="media/operations-manager-managed-instance-common-questions/add-peering-expanded.png":::

## SQL managed instance

### I don't see my region in SQL MI. How do I solve that?

1. If you don't see the region that you want to choose (for this preview, West US or West Europe) in the list of regions, select **Not seeing a region**, and then select **Request quota increase for your subscription**.

    :::image type="Region error" source="media/operations-manager-managed-instance-common-questions/region-error.png" alt-text="Screenshot showing region error.":::

1. Enter the required fields in **Basics** and go to **Details** to enter the **Problem details**.

    :::image type="New support request" source="media/operations-manager-managed-instance-common-questions/new-support-request-inline.png" alt-text="Screenshot showing new support request." lightbox="media/operations-manager-managed-instance-common-questions/new-support-request-expanded.png":::

1. Select **Enter details**. **Quota details** page opens on the right pane. In *Region*, choose the desired region and change the limits as desired (10 subnets and 500 vCores should suffice for the preview). Select **Save and continue** and then select **Next: Review + create >>** to raise the ticket. It might take 24 hours for the ticket to get resolved. Wait for it to get resolved before proceeding to create the SQL MI instance.

## Azure role-based access control (RBAC)

### What is Azure RBAC?

Azure RBAC is the role-based access control system that Azure follows while granting permissions. For more information, see [Azure role-based access control](/azure/role-based-access-control/overview). 

Azure RBAC is divided into Azure roles and Azure Active Directory roles. At a high level, Azure roles control permissions to manage Azure resources, while Azure Active Directory roles control permissions to manage Azure Active Directory resources. The following table compares some of the differences.

:::image type="Comparision of Azure roles and Azure active directory roles" source="media/operations-manager-managed-instance-common-questions/comparision-of-azure-roles-and-azure-active-directory-roles.png" alt-text="Screenshot of Azure roles and Azure active directory roles.":::

Below is the high-level view of how the classic subscription administrator roles, Azure roles, and Azure AD roles are related.

:::image type="Azure active directory roles" source="media/operations-manager-managed-instance-common-questions/azure-active-directory-roles.png" alt-text="Screenshot of Azure active directory roles.":::

### What is a Global Administrator role?

Users with the Global administrator role have access to all administrative features in Azure Active Directory and services that use Azure Active Directory identities, such as:
   - Microsoft 365 Defender portal
   - Compliance portal
   - Exchange Online
   - SharePoint Online
   - Skype for Business Online

## Other queries

### What are the charges that will be incurred during preview? 

The charges that incur while running SCOM Managed Instance (preview) will be the charges of owning a subscription in Azure along with all the resources inside it (SQL MI instance, Azure VMs, and so on). Apart from the infrastructure charges, there will be no other IP-related charge.

### What if there's an error during the deployment? 

During the deployment phase, there can be several reasons why deploying a SCOM Managed Instance (preview) shows an error. It might be some backend error, or you might have given the wrong credentials for one of the accounts. In the scenario of an error during deployment, it's best to delete the instance and create one again. For more information, see [Troubleshoot issues with Azure Monitor SCOM Managed Instance (preview)](./troubleshoot-scom-managed-instance.md).

### What is the procedure to delete an instance? 

You can either delete the instance from the instance view itself or from the *Resource Group* view. 

In the instance view, select *Delete* from the top menu and wait for the confirmation that the instance has been deleted. 

:::image type="Delete option" source="media/operations-manager-managed-instance-common-questions/delete.png" alt-text="Screenshot showing delete option.":::

Alternatively, go to your resource group view (search for Resource Group in the Azure search bar, and in the list of results, open your resource group). If you created a separate resource group for SCOM Managed Instance (preview), delete the resource group. Otherwise, in the resource group, search for your instance and select *Delete*. 

Once the instance is deleted, you'll also have to delete the two databases created in SQL MI. In the resource view, select the two databases (depending on what name you gave to your SQL MI instance) and select **Delete**. With the two databases deleted, you can recreate your SCOM Managed Instance (preview).

### If an Arc instance to connect to private cloud with some resources is available, will SCOM Managed Instance (preview) scale to those resources? 

Currently not supported. Today, independent of System Center Operations Manager, customers can install an Arc agent on a VM running on-premises and start seeing the resource in the Azure portal. Once they start seeing the resource in the Azure portal, they can use the Azure services for that resource (and incur the appropriate costs).

### How will network monitoring be done on SCOM Managed Instance (preview)? 

SCOM Managed Instance (preview) and System Center Operations Manager share the same feature set. You can use the same Management packs that you use in on-premises to carry out network monitoring via SCOM Managed Instance (preview).

### How is SCOM Managed Instance (preview) different from running System Center Operations Manager in Azure VMs?

- SCOM Managed Instance (preview) is native to Azure, while running System Center Operations Manager in Azure VMs isn't a native solution. This means, SCOM Managed Instance (preview) will integrate smoothly with Azure and all of Azure’s updates will be available to SCOM Managed Instance (preview).
- In terms of ease of deployment, SCOM Managed Instance (preview) is easy to deploy, while running VMs in Azure takes possibly months of effort (and requires in-depth technical knowledge).
- SCOM Managed Instance (preview) uses SQL MI as the backend for database management by default.
- SCOM Managed Instance (preview) comes with built-in scaling, patching features, and integrated reports.

### What does line-of-sight mean? 

Being in the same private network so that the IPs assigned to each component in the network can be a private IP.

### Can I view the SCOM Managed Instance (preview) resources and VMs in my subscription? 

Since this preview requires you to create the SCOM Managed Instance (preview) in your subscription, all the SCOM Managed Instance (preview) resources (including the VMs) will be visible to you. However, we recommend not to do any actions on the VMs and other resources while you're operating SCOM Managed Instance (preview) to avoid unforeseen complexities.

## Next steps

[SCOM Managed Instance (preview) overview](operations-manager-managed-instance-overview.md)

**Feedback**

Provide your feedback on Azure Monitor SCOM Managed Instance (preview) [here](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
