---
ms.assetid: 
title: Quick Start - Set up Microsoft Azure for Managed service identity, Aquila RBAC and SQL MI instance
description: This article describes how to create a  Managed Service Identity (MSI), configure Aquila RBAC and create and configure an SQL MI Instance.
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

# Quick Start: Set up Microsoft Azure for Managed service identity, Aquila RBAC and SQL MI instance

This quickstart describes how to create a Managed Service Identity (MSI), configure Aquila RBAC and create and configure an SQL MI Instance.

## Create a Managed Service Identity (MSI)

The Managed Service Identity provide an identity for applications to use when connecting to resources that support Azure Active Directory (Azure AD) authentication. For Aquila, a Managed Identity will replace the traditional four System Center Operations Manager service accounts and it will be used to access the SQL MI database.

>[!Note]
>Ensure you are a contributor in the subscription you create the MSI.

### Sign in to the  Azure portal

1. Sign in to the [Azure portal](https://portal.azure.com) and search for **Managed Identities**. Managed Identities page opens.
1. Select **+ Create**. **Create User Assigned Managed Identity** page opens.

### Basics

1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to create Aquila instance.
        1. **Resource group**: Select the resource group in which you want to create Aquila instance.
    1. **Instance details**:
        1. **Region**: Select the region in which you want to create Aquila instance.
        1. **Name**: Enter the desired name.
1. Select **Next : Tags >**

### Tags

1. Under **Tags**, enter the Name, value and select the Resource. Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see Tags.
1. Select **Next : Review + Create >**.

### Review + create

1. Under **Review + create**, review all the inputs given so far and select **Create**. Your deployment will now be created on Azure, you can access the resource and view its details.

## Configure Aquila RBAC

### Register the RP

>[!Note]
>Ensure you are either a subscription owner or global administrator. For more information, see Azure RBAC.

In order to create and operate an Aquila instance, create the below two custom RBAC roles in Azure:
 - **Aquila Contributor**: This role allows users to create, update, and delete an Aquila instance in Azure. Its scope of permissions doesn't extend beyond Aquila. The ideal user for this role would be someone who will be responsible for creating an Aquila instance, and deleting it when done.
 
 - **Aquila Reader**: This role allows users to read an Aquila instance in Azure, without the ability to modify anything in the instance. Its scope of permissions doesn't extend beyond Aquila. The ideal user for this role would be someone who will be responsible for accessing the Aquila instance once it is created and reading the parameters. 

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Cloud Shell** in the top menu. A Shell opens at the bottom of the page.
1. Enter the below commands to enable Aquila preview in your subscription:

    ```   
    az account set --subscription "<your subscription name>"
    az feature register --name AquilaPrivatePreview --namespace Microsoft.Scom
    az provider register --namespace Microsoft.Scom
    ```

Resource Provider of Aquila is successfully registered in your subscription. If you don't see the `Microsoft.SCOM` resource provider in the IAM or experience any problems in the steps above, check your permission level in Azure. You might need to change your permission level to complete all the steps above.

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

1. After you create the roles, go to Azure portal and search for *Subscriptions*. Select the subscription where you would create the Aquila instance in, and navigate to the blade that displays the details of all the resources in that subscription along with the costs incurred so far.
1. Select *Access Control (IAM)* > *+Add* on top and then select **Add custom role**. **Create a custom role* page opens.
1. For both the roles aquilaContributor.json and aquilaReader.json, do the following:
    1. Under **Basics**:
        1. **Custom role name**: Enter the role name (Aquila Contributor/Aquila Reader).
        1. **Description**: Enter description of the role.
        1. **Baseline permissions**: Select *Start from JSON* and upload the json file (aquilaContributor.json/aquilaReader.json). Ater you upload the json file, rest of the fields will auto-populate.
1. Review the permissions, subscription, and other details in rest of the tabs. 
1. Under **Review + Create**, select **Create** to create the role.
1. Select **Review + Create** to create two custom roles. Now, assign users to these roles. 
1. Navigate to **Access Control (IAM)** page, select **+Add** and then select **+Add role assignment**.
1. In the **Role**, select the desired role to add users: Aquila Contributor (Similar to System Center Operations Manager Administrator) or Aquila Reader (Similar to System Center Operations Manager Operator).
1. In the **Assign access to**, select **User, group, or service principal**.
1. In the **User**, search for the users by their name.
1. Save the role assignment and perform the same steps for the second role.

## Create and configure an SQL MI instance

Before you create an Aquila instance, you have to create an instance of SQL MI. For more information, see [Create an Azure SQL Managed Instance](/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql&preserve-view=true).

Below are the recommendations while you create an SQL MI instance:

1. **Resource Group**: Create a new resource group for SQL MI. Azure best practices recommend creating a new Resource Group for large Azure resources.

1. **Managed Instance name**: Choose a unique name. This name will be used while creating an Aquila instance to refer to this SQL MI instance that you are creating.
1. **Region**: Choose the region that is close to you. There is no strict requirement on Region for the instance but the closest region is recommended for latency purposes.
1. **Compute+Storage**: The default number of cores is General Purpose (Gen5) eight cores. This will suffice for the Aquila instance.
1. **Authentication Method**: You can select **SQL Authentication**. In the credentials, enter the credentials you would like to access the SQL MI instance with. These credentials don't refer to any that you have created so far.
1. **VNet**: This SQL MI instance needs to have direct connectivity (line-of-sight) to the Aquila instance you will create in the future. Thus, choose a VNet that you will eventually use for your Aquila instance, or if choosing a different VNet, make sure it has connectivity to the Aquila instance VNet. In terms of Subnet selection, the subnet you provide to SQL MI has to be dedicated (delegated) to the SQL MI Instance. The provided subnet can't be used to house any other resources. By design, a managed instance needs a minimum of 32 IP addresses in a subnet. As a result, you can use a minimum subnet mask of /27 when defining your subnet IP ranges. For more information, see [Determine required subnet size and range for Azure SQL Managed Instance](/azure/azure-sql/managed-instance/vnet-subnet-determine-size?msclkid=354f1ab4cd3211eca3a5aa9416f0afa1&view=azuresql&preserve-view=true).
1. **Connection Type**: By default, connection type is Proxy.
1. **Public Endpoint**: This can either be *Enabled* or *Disabled*. Enable it if you are not using a peered VNet. If you enable it, you will have to create an inbound NSG rule on the SQL MI subnet to allow traffic from the System Center Operations Manager Vnet/Subnet to port 3342. For more information, see [Configure public endpoint in Azure SQL Managed Instance](/azure/azure-sql/managed-instance/public-endpoint-configure?view=azuresql&preserve-view=true). If you disable it, you will have to peer your SQL MI VNet with the one in which System Center Operations Manager and Aquila are present.

For the rest of the settings in the other tabs, you can leave them as default or change something according to your requirements.

>[!Note]
>Creation of a new SQL MI instance can take up to 6 hours.

1. Once the SQL MI instance is created, you need to provide the Aquila Resource Provider with permissions to access this SQL MI instance. To do that, open the details of this SQL MI instance, and select *Access Control (IAM)*. In the top menu, select *+Add* and then select *Add role assignment*.

1. Enter the values as below and save the role assignment:

    Role = Reader
    Assign access to = User, group, or service principal
    Select = Microsoft.SCOM

### Set the Active Directory Admin value in the SQL MI Instance

To set the *Active Directory Admin* value in the SQL MI Instance follow the steps below:

For more information, see [Directory Readers role in Azure Active Directory for Azure SQL](/azure/azure-sql/database/authentication-aad-directory-readers-role?view=azuresql&preserve-view=true). 

You need to be the Global Admin/Privileged Role Admin of the subscription to perform the below process 

1. Open the SQL MI Instance and select **Active Directory Admin**.

1. Select **Set Admin**, search for your MSI (the same MSI that you provided during the Aquila instance creation flow). You will find the Admin added to the SQL MI Instance.

1. If you find the error after you add managed identity account, it indicates that read permissions are not yet provided to your identity. Ensure to provide the necessary permissions before you create your instance, otherwise your instance creation will fail.

## Next steps

> [!div class="nextstepaction"]
> [Create an Aquila instance](create-aquila-instance.md)