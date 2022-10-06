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

# Quick Start - Set up Microsoft Azure for Managed service identity, Aquila RBAC and SQL MI instance

This article describes how to create a Managed Service Identity (MSI), configure Aquila RBAC and create and configure an SQL MI Instance.

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

With the roles created, go to the Azure portal, and search for 'subscriptions' in the search bar. You will be led to a screen that shows all the subscriptions you have created. Select the subscription that you are going to create the Aquila instance in, and navigate to the blade that gives details of all the resources in that subscription along with the costs incurred so far.

Select *Access Control (IAM)* > *+Add* on top and then select *Add custom role*.

In the custom role editor, you will be asked details of the custom role you want to create

For both the roles created above (aquilaContributor.json & aquilaReader.json), the process below needs to be followed:

In the Basics tab, give the role a name (Aquila Contributor/Aquila Reader)
Give a description of the roles
In *Baseline permissions*, choose the option *Start from JSON* and upload the json file (aquilaContributor.json & aquilaReader.json). Uploading the json file will auto-populate the rest of the fields
For the rest of the tabs, review the permissions, subscription, and other details
In the final *Review + Create* tab, select *Create* to create the role.
Select *Review + Create* to create two custom roles. Now, you need to assign users to these roles. Go back to the *Access Control (IAM)* page and select *+Add* and then select *+Add role assignment*.

In the *Role* field, select the role that you want to add users to: Aquila Contributor (Similar to System Center Operations Manager Administrator) or Aquila Reader (Similar to System Center Operations Manager Operator).
In the *Assign access to*, keep it as *User, group, or service principal*.
In the *User* field, search for the users by their name.
Save the role assignment and carry out the same steps for the second role.

## Create and configure an SQL MI instance

Before creating an Aquila instance, you will have to create an instance of SQL MI. A step-by-step guide detailing how to create an SQL MI instance can be found HERE

While you create an SQL MI instance, here are some pointers and recommendations:

Resource Group: Create a new resource group for SQL MI because Azure best practices recommend creating a new Resource Group for large Azure resources.

Managed Instance name: Choose a unique name here. This name will be used while creating an Aquila instance to refer to this SQL MI instance that you are creating

Region: Choose the region that is closest to you. There is no strict requirement on Region for the instance but the closest region is recommended for latency purposes. If you don't see the desired region in the list of regions, see.

Compute+Storage: The default number of cores is General Purpose (Gen5) eight cores. This will suffice for the Aquila instance.

Authentication Method: You can select 'SQL Authentication'. In the credentials section, you can put in the credentials you would like to access the SQL MI instance with. These credentials don't refer to any that you have created so far.

VNet: This SQL MI instance needs to have direct connectivity (line-of-sight) to the Aquila instance you will create in the future. Thus, choose a VNet that you will eventually use for your Aquila instance, or if choosing a different VNet, make sure it has connectivity to the Aquila instance VNet. In terms of Subnet selection, the subnet you provide to SQL MI has to be dedicated (delegated) to the SQL MI Instance. The provided subnet can't be used to house any other resources. By design, a managed instance needs a minimum of 32 IP addresses in a subnet. As a result, you can use a minimum subnet mask of /27 when defining your subnet IP ranges. For more information, see.

Connection Type: Connection Type will be Proxy (Default)

Public Endpoint: This can either be 'Enabled' or 'Disabled'. Enable it if you are not using a peered VNet. If you enable it, you will have to create an inbound NSG rule on the SQL MI subnet to allow traffic from the System Center Operations Manager Vnet/Subnet to port 3342. How to create an NSG can be found HERE. If you disable it, you will have to peer your SQL MI VNet with the one in which System Center Operations Manager and Aquila are present

For the rest of the settings in the other tabs, you can leave them as default or change something according to your requirements

Creation of a new SQL MI instance can take up to 6 hours.
Once the SQL MI instance is created, you will need to provide the Aquila Resource Provider with permissions to access this SQL MI instance. To do that, open the details of this SQL MI instance, and select *Access Control (IAM)*. In the top menu bar, select *+Add* and then select *Add role assignment*.

There will be a pane that opens up on the right. The values to be input are:

Role = Reader
Assign access to = User, group, or service principal
Select = Microsoft.SCOM


Save the role assignment.

As a final step, you will need to set the 'Active Directory Admin' value in the SQL MI Instance. More information about why this step is required can be found HERE. The directions to implement this step are given below.

You will need to be the Global Admin/Privileged Role Admin of the subscription to carry out the process below
Open the SQL MI Instance and from the ToC, select *Active Directory Admin*.

Select **Set Admin**, search for your MSI (the same MSI that you provided during the Aquila instance creation flow).

You will see the Admin added to the SQL MI Instance.

If you see the error after you add managed identity account, it indicates that read permissions are not yet provided to your identity. Ensure to provide the necessary permissions before you create your instance, otherwise your instance creation will fail.

## Next steps

> [!div class="nextstepaction"]
> [Create an Aquila instance](create-aquila-instance.md)