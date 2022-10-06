---
ms.assetid: 
title: General questions about Aquila
description: This article summarizes frequently asked questions about Aquila.
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

# General questions about Aquila

This article summarizes frequently asked questions about Aquila.

## VPN

### What regions do the VPN need to be in?

There is no strict requirement on the region of the VPN but the recommendation is to put the VPN in the same region as your other Azure resources to maintain latency.

### What Address Range does the VNet need?

The minimum address space is /27 (which means /28 and above wouldn't work).

### How many subnets does the VPN need to have?

- VPN needs two subnets. 
    - For Aquila instance
    - For SQL MI instance
- The subnet for SQL MI instance will be a delegated (dedicated) subnet and won't be used by the Aquila instance. Name the subnets accordingly to avoid confusion in the future while you create the SQL MI/Aquila Instance.

### What Address Range do the two subnets need?

The minimum address space needs to be /27 for SQL MI subnet and /28 for the Aquila subnet.

### Do the Subnets need to specify a NAT gateway or Service Endpoint?

No, both the options can be left blank.

### Are there limitations on the security options in the Create VNet experience (BastionHost, DDoS, Firewall)?

No, you can disable all of them or enable any of them based on your organizations preferences.

### I created separate VNets in Azure. What steps do I need to take?

If you have multiple VNets created, you need to peer your VNets. If your'e peering any two networks, ensure to peer from both networks to each other. Thus, if you peer three networks, you will need to do six peerings.

### What options do I select while peering?

- You need to specify a peering name (in the field *Peering link name*).
- The first name is used to name the peer network from the current network to the other network. The second name is used to name the peer network from the other network to this network.
- In the section *Virtual Network*, specify the name of the VNet that you are peering too. If you can't find the VNet, you can search for it using the Resource ID. The rest of the options can be left default.

:::image type="Add peering" source="media/aquila-common-question/add-peering.png" alt-text="Screenshot of add peering.":::

## SQL-MI

### I don't see my region in SQL MI. How do I solve that?

In case you don't see the region that you want to choose (for this preview, West US or West Europe) in the list of regions, select **Not seeing a region**, and then select **Request quota increase for your subscription**.

:::image type="Region error" source="media/aquila-common-question/region-error.png" alt-text="Screenshot of region error.":::

Enter the required fields in **Basics** and go to **Details** to enter the **Problem details**.

:::image type="New support request" source="media/aquila-common-question/new-support-request.png" alt-text="Screenshot of new support request.":::

Select **Enter details**. **Quota details** page opens on the right pane. In *Region*, choose the desired region and change the limits as desired (10 subnets and 500 vCores should suffice for the preview). Select **Save and continue** and then select **Next: Review + create >>** to raise the ticket. It might take 24 hours for the ticket to get resolved. Wait for it to get resolved before proceeding to create the SQL MI instance.

## Azure RBAC

### What is Azure RBAC?

Azure RBAC is the role-based access control system that Azure follows while granting permissions. For more information, see [Azure role-based access control](/azure/role-based-access-control/overview). 

Azure RBAC is divided between Azure roles and Azure Active Directory roles. At a high level, Azure roles control permissions to manage Azure resources, while Azure Active Directory roles control permissions to manage Azure Active Directory resources. The following table compares some of the differences.

:::image type="Comparision of Azure roles and Azure active directory roles" source="media/aquila-common-question/comparision-of-azure-roles-and-azure-active-directory-roles.png" alt-text="Screenshot of Azure roles and Azure active directory roles.":::

Below is the high-level view of how the classic subscription administrator roles, Azure roles, and Azure AD roles are related.

:::image type="Azure active directory roles" source="media/aquila-common-question/azure-active-directory-roles.png" alt-text="Screenshot of Azure active directory roles.":::

### What is a Global Administrator Role?

For a Global Administrator role, users with this role have access to all administrative features in Azure Active Directory, and services that use Azure Active Directory identities such as
   - Microsoft 365 Defender portal
   - Microsoft 365 compliance center
   - Exchange Online
   - SharePoint Online
   - Skype for Business Online.

## Other Queries

### What are the charges that will be incurred during preview? 

The charges that incur while running Aquila will be the charges of owning a subscription in Azure along with all the resources inside it (SQL MI instance, Azure VMs, etc.). Apart from the infrastructure charges, there will be no other IP-related charge. For using System Center Operations Manager 2019, the evaluation version (available for six months) can be used to test Aquila.

### What if there is an error during deployment? 

During the deployment phase, there can be several reasons why deploying an Aquila instance shows an error. It might be some backend error, or you might have given the wrong credentials for one of the accounts. In the scenario of an error during deployment, it is best to delete the instance and create one again.

### What if the correct procedure to delete an Instance? 

In order to delete the instance, you can either delete it from the instance view itself or from the *Resource Group* view. 

In the instance view, select *Delete* from the top menu and wait for the confirmation that the instance has been deleted. 

The other way is to go to your resource group view (search for Resource Group in the Azure search bar, and in the list of results, open your resource group). If you created a separate resource group for Aquila, delete the resource group. Otherwise, in the resource group, search for your instance and select *Delete*. 

Once the instance is deleted, you will also have to delete the two databases created in SQL MI. In the resource view, select the two databases (depending on what name you gave to your SQL MI instance) and select *Delete*. With the two databases deleted, you can recreate your Aquila Instance.

### If an Arc instance to connect to private cloud with some resources is there, will Aquila scale to those resources in the future? 

In the future, Yes. Customers will be able to deploy System Center Operations Manager anywhere, and that capability will come through Arc. Arc-enabled on-premises deployment will have incremental features as compared to current on-premises System Center Operations Manager. Today, independent of System Center Operations Manager, customers can install an Arc agent on a VM running on-premises and start seeing the resource in the Azure portal. Once they start seeing the resource in the Azure portal, they can use the Azure services for that resource (and incur the appropriate costs).

### How will network monitoring be done on Aquila? 

Aquila and System Center Operations Manager share the same feature set. If it can be done in System Center Operations Manager today, it will be done in Aquila tomorrow.

### How is Aquila different from running System Center Operations Manager in Azure VMs?

- Aquila will be native to Azure while running System Center Operations Manager in Azure VMs is not a native solution. That means Aquila will integrate smoothly with Azure and all of Azure’s updates will be available to Aquila.
- In terms of ease of deployment, Aquila will be easy to deploy while running VMs in Azure takes possibly months of effort (and requires technical knowledge).
- Aquila uses SQL MI as the backend for database management by default.
- Aquila will come with backup and disaster recovery built in.

### What does line-of-sight mean? 

Being in the same private network so that the IPs assigned to each component in the network can be a private IP.

### Can I view the Aquila resources and VMs in my subscription? 

Since this preview requires you to create the Aquila instance in your subscription, all the Aquila resources (including the VMs) will be visible to you. However, we recommend not to touch the VMs and other resources while you are operating Aquila in order to avoid unforeseen complexities.