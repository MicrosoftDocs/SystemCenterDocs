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

There is no strict requirement on the region of the VPN but the recommendation is to put the VPN in the same region as your other Azure resources so that latency is maintained.

### What Address Range does the VNet need?

The minimum address space it needs to have is /27 (which means /28 and above won't work while /27 and below will work).

### How many subnets does the VPN need to have?

- The VPN will need 2 subnets. One will be for the Aquila instance and one will be for the SQL MI instance.
- The subnet for the SQL MI instance will be a delegated (dedicated) subnet and won't be used by the Aquila instance. Name the subnets accordingly to avoid confusion in the future while creating the SQL MI/Aquila Instance.

### What Address Range do the 2 subnets need?

The minimum address space needs to be /27 for the SQL MI subnet and /28 for the Aquila subnet.

### Do the Subnets need to specify a NAT gateway or Service Endpoint?

No. Both the options can be left blank.

### Are there limitations on the security options in the Create VNet experience (BastionHost, DDoS, Firewall)?

No requirements from our side. You can disable all of them or enable any of them based on your organizations preferences.

### I have created seperate VNets in Azure. What steps do I need to take?

If you have multiple VNets created, you need to peer your VNets. The screenshot below shows where you can peer your VNets from. If you are peering any 2 networks, remember to do the peering from both networks to each other. Thus, if you are peering three networks, you will need to do 6 peerings.

### What options do I select while peering?

- You need to specify a peering name (in the field 'Peering link name').
- The first name is used to name the peer network from the current network to the other network. The second name is used to name the peer network from the other network to this network.
- In the section *Virtual Network*, specify the name of the VNet that you are peering too. If you can't find the VNet, you can search for it using the Resource ID. The rest of the options can be left to default ones.

:::image type="Add peering" source="media/aquila-common-question/add-peering.png" alt-text="Screenshot of add peering.":::

## SQL-MI

### I don't see my region in SQL MI. How do I solve that?

In case you don't see the region that you want to choose (for this preview, West US or West Europe) in the list of regions, select *Not seeing a region*, and then select *Request quota increase for your subscription*.

:::image type="Region error" source="media/aquila-common-question/region-error.png" alt-text="Screenshot of region error.":::

With the *Basics* tab complete, go to the *Details* tab and fill out the *Problem Details*.

:::image type="New support request" source="media/aquila-common-question/new-support-request.png" alt-text="Screenshot of new support request.":::

On the pane on the right, in *Region*, choose the region that you want and change the limits to what you want (10 subnets and 500 vCores should suffice for the preview). Select *Save* and *Review & Create* to raise the ticket. Once the ticket is raised, wait for it to get resolved before proceeding to create the SQL MI instance. Note that it might take 24 hours for the ticket to get resolved.

## Azure RBAC

### What is Azure RBAC?

Azure RBAC is the role-based access control system that Azure follows while granting permissions. An overview of the topic can be found here. Azure RBAC is divided between Azure roles and Azure AD roles. At a high level, Azure roles control permissions to manage Azure resources, while Azure AD roles control permissions to manage Azure Active Directory resources. The following table compares some of the differences.

:::image type="Comparision of azure roles and azure active directory roles" source="media/aquila-common-question/comparision-of-azure-roles-and-azure-active-directory-roles.png" alt-text="Screenshot of azure roles and azure active directory roles.":::

The following diagram is a high-level view of how the classic subscription administrator roles, Azure roles, and Azure AD roles are related.

:::image type="Azure active directory roles" source="media/aquila-common-question/azure-active-directory-roles.png" alt-text="Screenshot of Azure active directory roles.":::

### What is a Global Administrator Role?

For a Global Administrator Role, Users with this role have access to all administrative features in Azure Active Directory, as well as services that use Azure Active Directory identities like the Microsoft 365 Defender portal, the Microsoft 365 compliance center, Exchange Online, SharePoint Online, and Skype for Business Online.

## Other Queries

### What are the charges that will be incurred during preview? 

The charges that you will incur while running Aquila will be the charges of owning a subscription in Azure along with all the resources inside it (SQL MI instance, Azure VMs, etc.). Apart from the infrastructure charges, there will be no other IP-related charge. For using SCOM 2019, the evaluation version (available for 6 months) can be used to test Aquila

### What if there is an error during deployment? 

During the deployment phase, there can be several reasons why deploying an Aquila instance shows an error. It might be some backend error, or you might have given the wrong credentials for one of the accounts. In the scenario of an error during deployment, it is best to delete the instance and create one again.

### What if the correct procedure to delete an Instance? 

In order to delete the instance, you can either delete it from the instance view itself or from the *Resource Group* view. In the instance view, select the *Delete* option from the top menu bar and wait for the confirmation that the instance has been deleted. The other way is to go to your resource group view (search for Resource Group in the Azure search bar, and in the list of results, open your resource group). If you created a separate resource group for Aquila, delete the resource group. Otherwise, in the resource group, search for your instance and select *Delete*. Once the instance is deleted, you will also have to delete the 2 databases created in SQL MI. In the resource view, select the 2 databases (depending on what name you gave to your SQL MI instance) and select *Delete*. With the 2 databases deleted, you can recreate your Aquila Instance.

### If an Arc instance to connect to private cloud with some resources is there, will Aquila scale to those resources in the future? 

In the future yes. Customers will be able to deploy SCOM anywhere, and that capability will come through Arc. Arc-enabled on-prem deployment will have incremental features as compared to current on-prem SCOM. Today, independent of SCOM, customers can install an Arc agent on a VM running on-prem and start seeing the resource in the Azure portal. Once they start seeing the resource in the Azure portal, they can use the Azure services for that resource (and incur the appropriate costs).

### How will network monitoring be done on Aquila? 

Aquila and SCOM share the same feature set. If it can be done in SCOM today, it will be done in Aquila tomorrow.

### How is Aquila different from running SCOM in Azure VMs?

- Aquila will be native to Azure while running SCOM in Azure VMs is not a native solution. That means Aquila will integrate smoothly with Azure and all of Azure’s updates will be available to Aquila.
- In terms of ease of deployment, Aquila will be very easy to deploy while running VMs in Azure takes possibly months of effort (and requires a lot of technical knowledge).
- Aquila uses SQL MI as the backend for database management by default.
- Aquila will come with backup and disaster recovery built in.

### What does line-of-sight mean? 

Being in the same private network so that the IPs assigned to each component in the network can be a private IP.

### Can I view the Aquila resources and VMs in my subscription? 

Since this preview requires you to create the Aquila instance in your subscription, all the Aquila resources (including the VMs) will be visible to you. However, it is strongly recommended that the VMs and other resources not be touched while you are operating Aquila in order to avoid unforeseen complexities.