---
ms.assetid: 
title: Create an Aquila instance
description: This article describes how to create an Aquila instance to monitor workloads using System Center Operations Manager functionality on Azure.
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

# Create an Aquila instance on Azure

This article describes how to create an Aquila instance that helps you monitor all your workloads, whether on-premises, in Azure, or in any other cloud services System Center Operations Manager functionality on Azure.

## Prerequisites

- Ensure that you've at least four virtual cores (one VM) of type Standard DSv2 in your Azure subscription to deploy an instance.
- Ensure that you've downloaded System Center Operations Manager 2019 or later executable file for the agent, Ops Console, and the gateway server.
- As all the components are on a single machine, ensure that you open the following ports on the single VM:
    - On the management server, open the inbound ports 5723/5724.
    - On the web-console server, open the inbound ports 80/443.
    - For agent, open the ports 5723/135/138/445.
- Ensure you allow ports 1433 and 11000-11999 from the Aquila Instance.
- If you enable public endpoint on SQL MI, ensure that you allow 3342.
- Ensure to establish direct connectivity (line-of-sight) between your Domain Controller and your Azure network and configure one domain account in Active Directory. For more information, see \<link\>.
- Ensure to create a Managed Service Identity (MSI), configure Aquila role-based access control (RBAC) and create and configure an SQL MI Instance. For more information, see \<link\>.

>[!Note]
>- As Aquila instance can be created only in West Europe and West US regions, ensure that the VNet is in one of these regions.
>- Aquila will be deployed with one Management Server in Azure. We recommend monitoring a maximum of 500 servers during this preview to avoid latency.
>- You can multihome existing agents from your existing Management Groups to the Aquila Instance.

## Create an Aquila instance

To create an Aquila instance, follow the below steps:

### Sign in to the  Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com) and search for **Aquila**. Aquila Overview page opens.
1. On the Overview page, you have three options
    - Pre-requisites: Allows you to view the prerequisites
    - Aquila Instance: Allows you to create an Aquila instance
    - Manage your Aquila Instance: Allows you to view the list of instances created.
1. Select **Create Aquila Instance**.

### Basics

1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to place the Aquila instance.
        1. **Resource group**: Select the resource group in which you want to place the Aquila instance. If you don't have a resource group in which you want to place the Aquila instance, select **Create New** to create a new resource group and then place the instance. We recommend you have a new resource group exclusively for Aquila.
    1. **Instance details**:
        1. **Aquila instance name**: Enter Aquila instance name as desired.
            >[!Note]
            >- Aquila instance name can have only alphanumaric characters and up to 10 characters long.
            >- Aquila instance is equivalent to System Center Operation Manager Management Group so choose a name accordingly.
        1. **Region**: Select the region that is near to you geographically so that latency between your agents and the Aquila instance is as low as possible.
    1. **Azure Hybrid Benefit**: Select **Yes** if you are using a Windows Server license for your existing servers. This license is only applicable for the Windows Servers that will be used while creating VMs for the Aquila instance and it won't apply to existing Windows Servers.
1. Select **Next**.

### Networking

1. Under **Networking**, do the following:
    1. **Configure virtual networks**:
        1. **Virtual network**: Select the virtual network that has direct connectivity to the workloads you want to monitor and to your domain controller + DNS server. If you have not created a VNet earlier, select 'Create New' if you haven't already created a VNet before. For more information, see VNet creation process.
        1. **Subnet**: Select a subnet that has at least 10 IP addresses to house all the Aquila instance components. The minimum address space is 28. The subnet can have existing resources in it however, don't choose the subnet that houses the SQL managed instance because it won't contain the sufficient number of IP addresses to house the instance.
    1. **Domain details**:
        1. **Domain Name**: Enter the name of the domain that is being administered by the Domain Controller.
        1. **DNS Server IP**: Enter the IP address of the DNS Server that is providing the IP addresses to the resources in the domain mentioned above.
    1. **Domain account**
        1. **Username**: Enter the username of the account you created in your active directory as part of the pre-requisites. Same account will be used to join the management servers (created as part of the Aquila instance) and SQL MI servers to your domain. For more information, see Domain Account.
        1. **Password**: Enter the password.
1. Select **Next**.

### Database inputs

1. Under **Database inputs**, do the following:
    1. **SQL managed instance**:
        1. **Resource Name**: Select the SQL MI resource name for the instance that you would like to associate with this Aquila instance. Only the SQL MI instance, which has given permissions to the Aquila instance should be used here. For more information, see SQL MI creation and permission.
    1. **User Managed Identity**:
        1. **User managed identity account**: Select the Managed Identity that you created and provided Admin permissions to in the SQL MI Instance. For more information, see MSI creation process.
1. Select **Next**.

### Tags

1. Under **Tags**, enter the Name, value and select the Resource. Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see Tags.
1. Select **Next**.

### Review + Submit

1. Under **Review + Submit**, review all the inputs given so far and select **Create**. Your deployment will now be created on Azure, and it takes up to an hour for the creation of an Aquila instance. 

    >[!Note]
    >If your deployment fails, delete the instance and all associated resources, and recreate the instance again. For more information, see delete the instance and its resources.

1. After the deployment is completed, select **Go to resource**. Created instance page opens. You will find some of the essential details and instructions to view the post-deployment steps or raise bugs.
1. On the left navigation pane, under **Manage**, select **SCOM infrastructure**. It displays all the essential properties of your instance.

## Next steps

> [!div class="nextstepaction"]
> [Connect the Aquila instance to Ops console](connect-aquila-instance-to-ops-console.md)