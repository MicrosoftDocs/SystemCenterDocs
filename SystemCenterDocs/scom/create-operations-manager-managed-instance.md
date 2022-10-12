---
ms.assetid: 
title: Create an Operations Manager managed instance (preview)
description: This article describes how to create an Operations Manager managed instance (preview) to monitor workloads using System Center Operations Manager functionality on Azure.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 10/11/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Create an Operations Manager managed instance (preview) on Azure

This article describes how to create a managed instance (preview) that helps you monitor all your workloads, whether on-premises, in Azure, or in any other cloud services with System Center Operations Manager functionality on Azure.

## Prerequisites

The following are the prerequisites before you create an Operations Manager managed instance (preview):

# [General Prerequisites](#tab/prereqs-general)

- Ensure that you've at least four virtual cores (one VM) of type Standard DSv2 in your Azure subscription to deploy an instance.
- Ensure that you've downloaded System Center Operations Manager 2019 or later executable file for the agent, Ops Console, and the gateway server.
- As all the components are on a single machine, ensure that you open the following ports on the single VM:
    - On the management server, open the inbound ports 5723/5724.
    - On the web-console server, open the inbound ports 80/443.
    - For agent, open the ports 5723/135/138/445.
- Ensure you allow ports 1433 and 11000-11999 from the Operations Manager managed instance (preview).
- If you enable public endpoint on SQL MI, ensure that you allow 3342.
- Ensure to establish direct connectivity (line-of-sight) between your Domain Controller and your Azure network and configure one domain account in Active Directory. For more information, see \<link\>.
- Ensure to create a Managed Service Identity (MSI), configure Operations Manager managed instance (preview) role-based access control (RBAC) and create and configure an SQL MI Instance. For more information, see \<link\>.

# [In existing infrastructure](#tab/prereqs-infra)

## Establish direct connectivity (line-of-sight) between your DC and your Azure network

- Ensure that there's direct network connectivity (line-of-sight) between the network, which has your Domain Controller, Ops Console, Agents, and the network in which you'll deploy an Operations Manager managed instance (preview). This is required so that all your resources (Domain Controller, System Center Operations Manager Components such as Ops Console, Operations Manager managed instance (preview) Components such as Management Servers) can talk to each other over the network.
- If your Domain Controller or any other component is on-premises, the line-of-sight can be established through *ExpressRoute* or *VPN*. For more information, see [ExpressRoute](/azure/expressroute/) and [VPN Gateway](/azure/vpn-gateway/)
- If your Domain Controller and all other components are in Azure with no presence on-premises, a VPN network will work (ExpressRoute isn't needed). If you are using one VPN to host all your components, you will already have a line-of-sight between all your components. If you have multiple VPNs, you will need to do VPN peering between all the VPNs that are in your network
- Allow Port 5723/5724/443 to communicate while talking from Operations Manager managed instance (preview) to the VMs being monitored and vice versa.

## Configure one domain account in Active Directory

- Create one domain account in your Active Directory. The domain account is a typical Active Directory account (it can be a non-admin account). This account will be used to join the Management Servers to your existing domain.
- Ensure that this account has the [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain) to join other servers to your domain.
- You can use an existing domain account if it has these [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain).

# [In Azure portal](#tab/prereqs-portal)

## Create a Managed Service Identity (MSI)

The Managed Service Identity provide an identity for applications to use when connecting to resources that support Azure Active Directory (Azure AD) authentication. For Operations Manager managed instance (preview), a Managed Identity will replace the traditional four System Center Operations Manager service accounts and it will be used to access the SQL MI database.

>[!Note]
>Ensure you are a contributor in the subscription you create the MSI.

1. Sign in to the [Azure portal](https://portal.azure.com) and search for **Managed Identities**. Managed Identities page opens.
1. Select **+ Create**. **Create User Assigned Managed Identity** page opens.
1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to create Operations Manager managed instance (preview).
        1. **Resource group**: Select the resource group in which you want to create Operations Manager managed instance (preview).
    1. **Instance details**:
        1. **Region**: Select the region in which you want to create Operations Manager managed instance (preview).
        1. **Name**: Enter the desired name.
1. Select **Next : Tags >**.
1. Under **Tags**, enter the Name, value, and select the Resource. Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see Tags.
1. Select **Next : Review + Create >**.
1. Under **Review + create**, review all the inputs given so far and select **Create**. Your deployment will now be created on Azure, you can access the resource and view its details.

## Configure Operations Manager managed instance (preview) role-based access control (RBAC)

### Register the RP

>[!Note]
>Ensure you are either a subscription owner or global administrator. For more information, see Azure RBAC.

In order to create and operate an Operations Manager managed instance (preview), create the below two custom RBAC roles in Azure:
 - **Aquila Contributor**: This role allows users to create, update, and delete an Operations Manager managed instance (preview) in Azure. Its scope of permissions doesn't extend beyond Operations Manager managed instance (preview). The ideal user for this role would be someone who will be responsible for creating an Operations Manager managed instance (preview), and deleting it when done.
 
 - **Aquila Reader**: This role allows users to read an Operations Manager managed instance (preview) in Azure, without the ability to modify anything in the instance. Its scope of permissions doesn't extend beyond Operations Manager managed instance (preview). The ideal user for this role would be someone who will be responsible for accessing the Operations Manager managed instance (preview) once it is created and reading the parameters. 

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Cloud Shell** in the top menu. A Shell opens at the bottom of the page.
1. Enter the below commands to enable Operations Manager managed instance (preview) in your subscription:

    ```   
    az account set --subscription "<your subscription name>"
    az feature register --name AquilaPrivatePreview --namespace Microsoft.Scom
    az provider register --namespace Microsoft.Scom
    ```

Resource Provider of Operations Manager managed instance (preview) is successfully registered in your subscription. If you don't see the `Microsoft.SCOM` resource provider in the IAM or experience any problems in the steps above, check your permission level in Azure. You might need to change your permission level to complete all the steps above.

### Add custom roles

#### Aquila Contributor

Copy and paste the below script in `.txt` file and name it as `aquilaContributor.json`. Change the `subscription1` value to the current subscription ID.

```
{ 
    "properties": { 
        "roleName": "Aquila Contributor", 
        "description": "Can onboard an Aquila Instance in Azure along with all the associated Azure resources.", 
        "assignableScopes": [ 
            "/subscriptions/<subscriptionID>" 
        ], 
        "permissions": [ 
            { 
                "actions": [ 
                    "Microsoft.Scom/managedInstances/*", 
                    "Microsoft.Scom/operations/read", 
                    "Microsoft.Scom/locations/operationStatuses/write", 
                    "Microsoft.Scom/locations/operationStatuses/read", 
                    "Microsoft.Resources/deployments/*", 
                    "Microsoft.Network/virtualNetworks/subnets/read", 
                    "Microsoft.Network/virtualNetworks/read", 
                    "Microsoft.Sql/managedInstances/read", 
                    "Microsoft.Sql/managedInstances/databases/read", 
                    "Microsoft.Resources/subscriptions/resourceGroups/read" 
                ], 
                "notActions": [], 
                "dataActions": [], 
                "notDataActions": [] 
            } 
        ] 
    } 
} 
```

#### Aquila Reader

Copy and paste the below script in `.txt` file and name it as `aquilaReader.json`. Change the `subscription1` value to the current subscription ID.

```
{ 
    "properties": { 
        "roleName": "Aquila Reader", 
        "description": "Can read aquila instances and deployments", 
        "assignableScopes": [ 
            "/subscriptions/<subscriptionID>" 
        ], 
        "permissions": [ 
            { 
                "actions": [ 
                    "Microsoft.Scom/managedInstances/*/read" 
                ], 
                "notActions": [], 
                "dataActions": [], 
                "notDataActions": [] 
            } 
        ] 
    } 
} 
```

1. After you create the roles, go to Azure portal and search for *Subscriptions*. Select the subscription where you would create the Operations Manager managed instance (preview) in and navigate to the blade that displays the details of all the resources in that subscription along with the costs incurred so far.
1. Select *Access Control (IAM)* > *+Add* on top and then select **Add custom role**. **Create a custom role** page opens.
1. For both the roles aquilaContributor.json and aquilaReader.json, follow the below steps:
    1. Under **Basics**:
        1. **Custom role name**: Enter the role name (Aquila Contributor/Aquila Reader).
        1. **Description**: Enter description of the role.
        1. **Baseline permissions**: Select *Start from JSON* and upload the json file (aquilaContributor.json/aquilaReader.json). After you upload the json file, rest of the fields will auto-populate.
1. Review the permissions, subscription, and other details in rest of the tabs. 
1. Under **Review + Create**, select **Create** to create the role.
1. Select **Review + Create** to create two custom roles. Now, assign users to these roles. 
1. Navigate to **Access Control (IAM)** page, select **+Add** and then select **+Add role assignment**.
1. In the **Role**, select the desired role to add users: Operations Manager managed instance (preview) Contributor (Similar to System Center Operations Manager Administrator) or Operations Manager managed instance (preview) Reader (Similar to System Center Operations Manager Operator).
1. In the **Assign access to**, select **User, group, or service principal**.
1. In the **User**, search for the users by their name.
1. Save the role assignment and perform the same steps for the second role.

## Create and configure an SQL MI instance

Before you create an Operations Manager managed instance (preview), you have to create an instance of SQL MI. For more information, see [Create an Azure SQL Managed Instance](/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql&preserve-view=true).

Below are the recommendations while you create an SQL MI instance:

- **Resource Group**: Create a new resource group for SQL MI. Azure best practices recommend creating a new Resource Group for large Azure resources.
- **Managed Instance name**: Choose a unique name. This name will be used while you create an Operations Manager managed instance (preview) to refer to this SQL MI instance that you are creating.
- **Region**: Choose the region that is close to you. There is no strict requirement on region for the instance but the closest region is recommended for latency purposes.
- **Compute+Storage**: The default number of cores is General Purpose (Gen5) eight cores. This will suffice for the Operations Manager managed instance (preview).
- **Authentication Method**: You can select **SQL Authentication**. In the credentials, enter the credentials you would like to access the SQL MI instance with. These credentials don't refer to any that you have created so far.
- **VNet**: This SQL MI instance needs to have direct connectivity (line-of-sight) to the Operations Manager managed instance (preview) you will create in the future. Thus, choose a VNet that you will eventually use for your Operations Manager managed instance (preview), or if you choose a different VNet, make sure it has connectivity to the Operations Manager managed instance (preview) VNet. In terms of Subnet selection, the subnet you provide to SQL MI has to be dedicated (delegated) to the SQL MI Instance. The provided subnet can't be used to house any other resources. By design, a managed instance needs a minimum of 32 IP addresses in a subnet. As a result, you can use a minimum subnet mask of /27 when defining your subnet IP ranges. For more information, see [Determine required subnet size and range for Azure SQL Managed Instance](/azure/azure-sql/managed-instance/vnet-subnet-determine-size?msclkid=354f1ab4cd3211eca3a5aa9416f0afa1&view=azuresql&preserve-view=true).
- **Connection Type**: By default, connection type is Proxy.
- **Public Endpoint**: This can either be *Enabled* or *Disabled*. Enable it if you are not using a peered VNet. If you enable it, you will have to create an inbound NSG rule on the SQL MI subnet to allow traffic from the System Center Operations Manager Vnet/Subnet to port 3342. For more information, see [Configure public endpoint in Azure SQL Managed Instance](/azure/azure-sql/managed-instance/public-endpoint-configure?view=azuresql&preserve-view=true). If you disable it, you will have to peer your SQL MI VNet with the one in which System Center Operations Manager and Operations Manager managed instance (preview) are present.

For the rest of the settings in the other tabs, you can leave them as default or change something according to your requirements.

>[!Note]
>Creation of a new SQL MI instance can take up to 6 hours.

1. Once the SQL MI instance is created, you need to provide the Operations Manager managed instance (preview) Resource Provider with permissions to access this SQL MI instance. To do that, open the details of this SQL MI instance, and select *Access Control (IAM)*. In the top menu, select *+Add* and then select *Add role assignment*.

1. Enter the values as below and save the role assignment:

    - Role = Reader
    - Assign access to = User, group, or service principal
    - Select = Microsoft.SCOM

### Set the Active Directory Admin value in the SQL MI Instance

To set the *Active Directory Admin* value in the SQL MI Instance, follow the steps below:

For more information, see [Directory Readers role in Azure Active Directory for Azure SQL](/azure/azure-sql/database/authentication-aad-directory-readers-role?view=azuresql&preserve-view=true). 

You need to be the Global Admin/Privileged Role Admin of the subscription to perform the below process 

1. Open the SQL MI Instance and select **Active Directory Admin**.

1. Select **Set Admin**, search for your MSI (the same MSI that you provided during the Operations Manager managed instance (preview) creation flow). You will find the admin added to the SQL MI Instance.

1. If you find the error after you add managed identity account, it indicates that read permissions are not yet provided to your identity. Ensure to provide the necessary permissions before you create your instance, otherwise your instance creation will fail.

---

>[!Note]
>- As Operations Manager managed instance (preview) can be created only in West Europe and West US regions, ensure that the VNet is in one of these regions.
>- Operations Manager managed instance (preview) will be deployed with one Management Server in Azure. We recommend monitoring a maximum of 500 servers during this preview to avoid latency.
>- You can multihome existing agents from your existing Management Groups to the Operations Manager managed instance (preview).

## Create an Operations Manager managed instance (preview)

To create an Operations Manager managed instance (preview), follow the below steps:

1. Sign in to the [Azure portal](https://portal.azure.com) and search for **Aquila**. Aquila Overview page opens.
1. On the Overview page, you have three options
    - Pre-requisites: Allows you to view the prerequisites
    - Aquila Instance: Allows you to create an Operations Manager managed instance (preview)
    - Manage your Aquila Instance: Allows you to view the list of instances created.
1. Select **Create Aquila Instance**.
1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to place the Operations Manager managed instance (preview).
        1. **Resource group**: Select the resource group in which you want to place the Operations Manager managed instance (preview). If you don't have a resource group in which you want to place the Operations Manager managed instance (preview), select **Create New** to create a new resource group and then place the instance. We recommend you have a new resource group exclusively for Operations Manager managed instance (preview).
    1. **Instance details**:
        1. **Aquila instance name**: Enter Operations Manager managed instance (preview) name as desired.
            >[!Note]
            >- Operations Manager managed instance (preview) name can have only alphanumeric  characters and up to 10 characters long.
            >- Operations Manager managed instance (preview) is equivalent to System Center Operation Manager Management Group so choose a name accordingly.
        1. **Region**: Select the region that is near to you geographically so that latency between your agents and the Operations Manager managed instance (preview) is as low as possible.
    1. **Azure Hybrid Benefit**: Select **Yes** if you are using a Windows Server license for your existing servers. This license is only applicable for the Windows Servers that will be used while creating VMs for the Operations Manager managed instance (preview) and it won't apply to existing Windows Servers.
1. Select **Next**.
1. Under **Networking**, do the following:
    1. **Configure virtual networks**:
        1. **Virtual network**: Select the virtual network that has direct connectivity to the workloads you want to monitor and to your domain controller + DNS server. If you have not created a VNet earlier, select **Create New** if you haven't already created a VNet before. For more information, see VNet creation process.
        1. **Subnet**: Select a subnet that has at least 10 IP addresses to house all the Operations Manager managed instance (preview) components. The minimum address space is 28. The subnet can have existing resources in it, however, don't choose the subnet that houses the SQL managed instance because it won't contain the sufficient number of IP addresses to house the instance.
    1. **Domain details**:
        1. **Domain Name**: Enter the name of the domain that is being administered by the Domain Controller.
        1. **DNS Server IP**: Enter the IP address of the DNS Server that is providing the IP addresses to the resources in the domain mentioned above.
    1. **Domain account**
        1. **Username**: Enter the username of the account you created in your active directory as part of the pre-requisites. Same account will be used to join the management servers (created as part of the Operations Manager managed instance (preview)) and SQL MI servers to your domain. For more information, see Domain Account.
        1. **Password**: Enter the password.
1. Select **Next**.
1. Under **Database inputs**, do the following:
    1. **SQL managed instance**:
        1. **Resource Name**: Select the SQL MI resource name for the instance that you would like to associate with this Operations Manager managed instance (preview). Only the SQL MI instance, which has given permissions to the Operations Manager managed instance (preview) should be used here. For more information, see SQL MI creation and permission.
    1. **User Managed Identity**:
        1. **User managed identity account**: Select the Managed Identity that you created and provided Admin permissions to in the SQL MI Instance. For more information, see MSI creation process.
1. Select **Next**.
1. Under **Tags**, enter the Name, value, and select the Resource. Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see Tags.
1. Select **Next**.
1. Under **Review + Submit**, review all the inputs given so far and select **Create**. Your deployment will now be created on Azure, and it takes up to an hour for the creation of an Operations Manager managed instance (preview). 

    >[!Note]
    >If the deployment fails, delete the instance and all associated resources, and recreate the instance again. For more information, see delete the instance and its resources.

1. After the deployment is completed, select **Go to resource**. On the created instance page, some of the essential details and instructions to view the post-deployment steps/raise bugs appear.
1. On the left pane, under **Manage**, select **SCOM infrastructure**. All the essential properties of your instance appear.

## Next steps

> [!div class="nextstepaction"]
> [Connect the Operations Manager managed instance (preview) to Ops console](connect-managed-instance-ops-console.md)