---
ms.assetid: 
title: Create an Azure Monitor SCOM Managed Instance (preview)
description: This article describes how to create an Azure Monitor SCOM Managed Instance (preview) to monitor workloads using System Center Operations Manager functionality on Azure.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 12/14/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Create an Azure Monitor SCOM Managed Instance (preview) on Azure

Azure Monitor SCOM Managed Instance (preview) provides System Center Operations Manager functionality on Azure and helps you monitor all your workloads, whether on-premises, in Azure, or in any other cloud services.

This article describes how to create a SCOM Managed Instance (preview) with System Center Operations Manager functionality on Azure.

>[!Note]  
>In this preview, you can create an instance only in **West Europe** and **West US**.

## Prerequisites

Before you create a SCOM Managed Instance (preview), ensure you select all the three tabs (General pointers, In your active directory domain, In Azure portal) and create necessary prerequisites.

# [General Pointers](#tab/pointers-general)
 
- Ensure that you've at least four virtual cores (one VM) of type Standard DSv2 in your Azure subscription to deploy an instance.
- Ensure you allow port 1433 (private port) from the SCOM Managed Instance (preview) to the SQL MI.
- If you enable public endpoint on SQL MI, ensure you allow 3342.
- To ensure reliability and support easy scaling, SCOM Managed Instance (preview) creates a Standard Load Balancer and a Uniform Virtual Machine Scale Set. For more information, see  [Azure Load Balancer](/azure/load-balancer/load-balancer-overview) and [Azure Virtual Machine Scale Sets](/azure/virtual-machine-scale-sets/overview). 

# [In your Active directory domain](#tab/prereqs-active)

>[!Note]   
>- To perform active directory operations, install **Active directory users and computers** tool. Before you install this tool, install **RSAT: Active Directory Domain Services and Lightweight Directory Tools** feature. This tool can be installed on any machine which has domain connectivity. You must login to this tool with some admin permissions to perform all active directory operations.
>- To perform operation on DNS server, you need to login to DNS server and run **DNS manager** tool.

## Establish direct connectivity (line-of-sight) between your Domain Controller and Azure network

- Ensure that there's direct network connectivity (line-of-sight) between the network, which has your Domain Controller, Ops console, Agents, and the network in which you'll deploy a SCOM Managed Instance (preview). This is required so that all your resources (Domain Controller, System Center Operations Manager Components such as Ops console, SCOM Managed Instance (preview) Components such as Management Servers) can communicate with each other over the network.
- If your Domain Controller or any other component is on-premises, the line-of-sight can be established through *ExpressRoute* or *VPN*. For more information, see  [ExpressRoute](/azure/expressroute/) and [VPN Gateway](/azure/vpn-gateway/).
- If your Domain Controller and all other components are in Azure (a conventional Domain Controller and not Azure Active Directory) with no presence on-premises, a Virtual network (VNet) will work (ExpressRoute isn't required). If you're using one VNet to host all your components, you'll already have a line-of-sight between all your components. If you've multiple VNets, you'll need to do VNet peering between all the VNets that are in your network. For more information, see  [VNet peering in Azure](/azure/virtual-network/virtual-network-peering-overview).
- Allow ports 5723/5724/443 to communicate while talking from SCOM Managed Instance (preview) to the VMs being monitored and vice versa.
- We recommend a NAT gateway for outbound internet access from subnets. Edit the subnet to add a NAT gateway. For more information, see  [What is Virtual Network NAT?](/azure/virtual-network/nat-gateway/nat-overview).
    - In Azure, Add  NAT gateway to Subnet (VNET/Subnet) where SCOM Managed Instance (preview) is going to be created. A NAT gateway is needed for outbound internet access from subnets. For more information, see  [Virtual Network NAT](/azure/virtual-network/nat-gateway/nat-overview).
        - To create a NAT gateway, follow these steps:
            - Create NAT gateway in same region where the VNet is present.
            - Create NAT gateway in same subscription used for SCOM Managed Instance (preview).
            - Create public IP.
                 :::image type="NAT gateway" source="media/create-operations-manager-managed-instance/nat-gateway.png" alt-text="Screenshot of NAT gateway.":::
            - Select VNet and subnet for SCOM Managed Instance (preview).


## Configure a domain account in Active Directory

- Create a domain account in your Active Directory. The domain account is a typical Active Directory account (it can be a non-admin account). This account will be used to add the System Center Operations Manager Management Servers to your existing domain.
      :::image type="Active directory users" source="media/create-operations-manager-managed-instance/active-directory-users.png" alt-text="Screenshot of Active directory users.":::
- Ensure that this account has the [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain) to join other servers to your domain.
- You can use an existing domain account if it has these [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain).
- Configured domain account must be used in SCOM Managed Instance (preview) creation at later steps.

## Create and configure a computer group

- Create a computer group in your active directory. For more information, see  [Create a group account in active directory](/windows/security/threat-protection/windows-firewall/create-a-group-account-in-active-directory). All the management servers you create will be a part of this group so that all the members of the group can retrieve gMSA account credentials (created in subsequent steps). This group can't contain spaces and must have alphabets only.
      :::image type="Active directory computers" source="media/create-operations-manager-managed-instance/active-directory-computers.png" alt-text="Screenshot of Active directory computers.":::
- To manage this computer group, provide permissions to the domain account that you created. Follow the steps below to provide permissions:
    1. Select the group properties and select **Managed By**.
        1. **Name**: Enter the name of the domain account.
        1. Select the checkbox **Manager can update membership list**. 
            :::image type="Server group properties" source="media/create-operations-manager-managed-instance/server-group-properties.png" alt-text="Screenshot of Server group properties.":::

## Create a static IP and configure the DNS name

- For all the System Center Operations Manager components, to communicate with the load-balancer that will be created by the SCOM Managed Instance (preview) service, you need a static IP and DNS name for the load-balancer front-end configuration.
- Ensure that the static IP is in the subnet that was created during VNet creation and it will be used during the creation of an instance. 
- Create a DNS name (as per your organization policy) for the static IP.
     :::image type="DNS manager" source="media/create-operations-manager-managed-instance/dns-manager.png" alt-text="Screenshot of DNS manager.":::

## Create and configure a gMSA account 

- Create a gMSA (Group Managed Service Account) account to run the Management Server services and to authenticate the services. Use the below command to create a gMSA account: 

    ```powershell
    New-ADServiceAccount ContosogMSA -DNSHostName "ContosoLB.aquiladom.com" -PrincipalsAllowedToRetrieveManagedPassword "ContosoServerGroup" -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames MSOMHSvc/ContosoLB.aquiladom.com, MSOMHSvc/ContosoLB, MSOMSdkSvc/ContosoLB.aquiladom.com, MSOMSdkSvc/ContosoLB 
    ```
    
    - ContosogMSA = gMSA account name 
    - ContosoLB.aquiladom.com = DNS name for LB (specified in the previous step) 
    - ContosoServerGroup = Computer group in AD (specified previously)
    - MSOMHSvc/ContosoLB.aquiladom.com, MSOMHSvc/ContosoLB, MSOMSdkSvc/ContosoLB.aquiladom.com, MSOMSdkSvc/ContosoLB = Service Principal names 

- Use the below command, if the root key isn't effective:
 
    ```powershell
    Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10)) 
    ```

# [In Azure portal](#tab/prereqs-portal)

## Register SCOM Managed Instance (preview) Resource provider

To register SCOM Managed Instance (preview) resource provider, do the following:

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Subscriptions**.
2. Select the subscription where you want to deploy SCOM Managed Instance (preview).
3. Under **Settings**, select **Resource providers**.
4. Search for SCOM and register **Microsoft.Scom**.

## Create a Managed Service Identity (MSI)

The Managed Service Identity provides an identity for applications to use when connecting to resources that support Azure Active Directory (Azure AD) authentication. For SCOM Managed Instance (preview), a Managed Identity will replace the traditional four System Center Operations Manager service accounts and it will be used to access the SQL MI database. MSI can also be used to access the key vault.

>[!Note]    
>- Ensure you're a contributor in the subscription you create the MSI.
>- This MSI must have admin permission on SQL MI and read permission on the Key vault used for domain account credentials.

1. Sign in to the [Azure portal](https://portal.azure.com) and search for **Managed Identities**.
     :::image type="Managed Identity in Azure portal" source="media/create-operations-manager-managed-instance/azure-portal-managed-identity.png" alt-text="Screenshot of Managed Identity in Azure portal.":::
1. In the **Managed Identities** page, select **+ Create**. The **Create User Assigned Managed Identity** page opens.
     :::image type="Managed Identity" source="media/create-operations-manager-managed-instance/managed-identities.png" alt-text="Screenshot of Managed Identity.":::
1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to create the SCOM Managed Instance (preview).
        1. **Resource group**: Select the resource group in which you want to create the SCOM Managed Instance (preview).
    1. **Instance details**:
        1. **Region**: Select the region in which you want to create SCOM Managed Instance (preview).
        1. **Name**: Enter the desired name.
         :::image type="Create user assigned managed identity" source="media/create-operations-manager-managed-instance/create-user-assigned-managed-identity.png" alt-text="Screenshot of Create user assigned managed identity.":::
1. Select **Next : Tags >**.
1. Under **Tags**, enter the Name, value, and select the Resource. 
     Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups.
1. Select **Next : Review + Create >**.
1. Under **Review + create**, review all the information that you provided and select **Create**. 
     :::image type="Managed identity review" source="media/create-operations-manager-managed-instance/managed-identity-review.png" alt-text="Screenshot of Managed identity review.":::
Your deployment will now be created on Azure and you can access the resource and view its details.

## Create and configure an SQL MI

Before you create a SCOM Managed Instance (preview), create an SQL MI. For more information, see  [Create an Azure SQL Managed Instance](/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql&preserve-view=true).

We recommend the following for creating an SQL MI:

- **Resource Group**: Create a new resource group for SQL MI. Azure best practices recommend you create a new Resource Group for large Azure resources.
- **Managed Instance name**: Choose a unique name. This name will be used while you create a SCOM Managed Instance (preview) to refer to this SQL MI that you're creating.
- **Region**: Choose the region close to you. There's no strict requirement on region for the instance, but the closest region is recommended for latency purposes.
- **Compute+Storage**: General Purpose (Gen5) eight cores is the default number of cores. This will suffice for the SCOM Managed Instance (preview).
- **Authentication Method**: Select **SQL Authentication**. Enter the credentials you would like to access the SQL MI with. These credentials don't refer to any that you've created so far.
- **VNet**: This SQL MI needs to have direct connectivity (line-of-sight) to the SCOM Managed Instance (preview) that you create in the future. Thus, choose a VNet that you'll eventually use for your SCOM Managed Instance (preview), or if you choose a different VNet, ensure it has connectivity to the SCOM Managed Instance (preview) VNet. 

    The subnet you provide to SQL MI has to be dedicated (delegated) to the SQL MI. The provided subnet can't be used to house any other resources. By design, a managed instance needs a minimum of 32 IP addresses in a subnet. As a result, you can use a minimum subnet mask of /27 when defining your subnet IP ranges. For more information, see [Determine required subnet size and range for Azure SQL Managed Instance](/azure/azure-sql/managed-instance/vnet-subnet-determine-size?view=azuresql&preserve-view=true).
- **Connection Type**: By default, connection type is **Proxy**.
- **Public Endpoint**: This can either be *Enabled* or *Disabled*. To use the Power BI reporting, you need to enable the Public Endpoint. 

     If the SQL MI VNet is different from the SCOM Managed Instance (preview) VNet:

    - If you enable, create an inbound NSG rule on the SQL MI subnet to allow traffic from the System Center Operations Manager VNet/Subnet to port 3342. For more information, see  [Configure public endpoint in Azure SQL Managed Instance](/azure/azure-sql/managed-instance/public-endpoint-configure?view=azuresql&preserve-view=true).
    - If you disable, ensure to peer your SQL MI VNet with the one in which System Center Operations Manager and SCOM Managed Instance (preview) are present.
	
For the rest of the settings in the other tabs, you can leave them as default or change as per your requirements.

>[!Note]    
> Creation of a new SQL MI can take up to 6 hours.

After the creation of SQL MI, you need to provide permission to the SCOM Managed Instance (preview) Resource Provider to access this SQL MI. 

To provide the permissions, do the following:

1. Open SQL MI and select **Access Control (IAM)**. In the top menu, select **+Add** > **Add role assignment**.
     :::image type="Access control" source="media/create-operations-manager-managed-instance/access-control.png" alt-text="Screenshot of access control.":::
1. In **Add role assignment** page, do the following:
    - **Role**: Select **Reader** from the dropdown.
    - **Assign access to**: Select **User, group, or service principal** from the dropdown.
    - **Select**: Enter **Microsoft.SCOM Resource Provider**
         :::image type="Add role assignment" source="media/create-operations-manager-managed-instance/add-role-assignment.png" alt-text="Screenshot of Add role assignment.":::
1. Select **Save**.

### Set the Active Directory Admin value in the SQL MI

To set the Active Directory Admin value in the SQL MI, follow these steps:

>[!Note]    
>You must have the Global Admin/Privileged Role Admin of the subscription.

For more information on Directory Readers role, see  [Directory Readers role in Azure Active Directory for Azure SQL](/azure/azure-sql/database/authentication-aad-directory-readers-role?view=azuresql&preserve-view=true).

1.	Open the SQL MI. Under **Settings**, select **Active Directory admin**.
     :::image type="Active directory admin" source="media/create-operations-manager-managed-instance/active-directory-admin.png" alt-text="Screenshot of Active directory admin.":::

2.	Select **Set admin**, search for your MSI (the same MSI that you provided during the SCOM Managed Instance (preview) creation flow). You will find the admin added to the SQL MI.
     :::image type="Azure Active directory admin" source="media/create-operations-manager-managed-instance/azure-active-directory.png" alt-text="Screenshot of Azure Active directory admin.":::

3.	If you get an error after you add a managed identity account, it indicates that read permissions aren't yet provided to your identity. Ensure to provide the necessary permissions before you create your instance, else your instance creation will fail.
     :::image type="SQL Active directory admin" source="media/create-operations-manager-managed-instance/sql-active-directory-admin.png" alt-text="Screenshot of SQL Active directory admin.":::

## Create a key vault and add credentials as a secret in the Key vault  

For security, you can Store the domain account (you created previously in Active Directory) in a Key vault.

Azure Key Vault is a cloud service that provides a secure store for keys, secrets, and certificates. For more information, see  [Azure Key Vault](/azure/key-vault/general/overview). 

>[!Note]    
> You must have Global Admin/Privileged Role Admin of the tenant, to do the below steps.

1.	Open Azure portal and search for **Key vaults**. The Key vaults page opens.
     :::image type="Key vaults in portal" source="media/create-operations-manager-managed-instance/azure-portal-key-vaults.png" alt-text="Screenshot of Key vaults in portal.":::

2.	Select **+ Create**. 
     :::image type="Key vault" source="media/create-operations-manager-managed-instance/key-vaults.png" alt-text="Screenshot of Key vaults.":::
    
3. In the **Basics**, do the following:
    - **Project details**:
        - **Subscription**: Select the subscription.
        - **Resource group**: Select the desired resource group.
    - **Instance details**:
        -  **Key vault name**: The name of your key vault. No added restrictions except for those that apply to names in other Azure services
        - **Region**: Choose the region that you're going to select for your other resources
        - **Pricing tier**: Select **Standard** or **Premium** as required.
    - **Recovery options**:
        - **Days to retain deleted vaults**: Can be a value from 7 to 90. 
        - **Purge protection**: We recommend enabling this feature to have a mandatory retention period.
             :::image type="create a key vault" source="media/create-operations-manager-managed-instance/create-a-key-vault.png" alt-text="Screenshot of create a key vault.":::
4. Select **Next**.
5. In **Access Policy**, do the following:
    - **Access configuration**: Select **Vault access policy**.
    - **Resource access**: Don't select any of the options.
    - **Access policies**: Select **+ Create** to create a new access policy. **Create an access policy** page opens on the right pane. 
         :::image type="Access policies" source="media/create-operations-manager-managed-instance/access-policies.png" alt-text="Screenshot of Access policies.":::
        1. In **Permissions** > **Secret permissions**, select **Get** and **List**. 
             :::image type="Create an Access policy" source="media/create-operations-manager-managed-instance/create-an-access-policy.png" alt-text="Screenshot of Create an Access policy.":::
        1. Select **Next**.
        1. In **Principal**, ensure to select the same MSI that is used in SQL MI admin configuration.

        1. In **Review + create**, review the selections, and select **Create**. 
1. Select the access policy created and then select **Next**.
     :::image type="Access policy" source="media/create-operations-manager-managed-instance/access-policy.png" alt-text="Screenshot of Access policy.":::
1. In **Networking**, do the following:
    - Select **Enable public access**.
    - In **Public Access**, select **All networks** for **Allow access from**.
             :::image type="Networking tab" source="media/create-operations-manager-managed-instance/networking-inline.png" alt-text="Screenshot of Networking tab." lightbox="media/create-operations-manager-managed-instance/networking-expanded.png":::
1. Select **Next**.
1. In **Tags**, select the tags if required and select **Next**.
1. In **Review + create**, review the selections, and select **Create** to create the Key vault.
     :::image type="Review tab" source="media/create-operations-manager-managed-instance/review.png" alt-text="Screenshot of review tab.":::
1. On the left pane, under **Objects**, select **Secrets**. 
    
     >[!Note]    
     > You must create two secrets to store the domain account credentials.
     > - Username
     > - Password

1. Select **+ Generate/Import**. 
     :::image type="Secrets" source="media/create-operations-manager-managed-instance/secrets.png" alt-text="Screenshot of secrets.":::
1. Do the following in **Create a secret** page.
    - **Upload options**: Select **Manual**.
    - **Name**: Enter the name of secret. For example, you can use *Username* for username secret and *Password* for password secret.
    - **Secret value**: For username value (in the format, domain\username), it will be the domain account username and for password, it will be the domain account password.
       For example, if the domain is *contoso.com*, then the username would be in the format *contoso\username*.
        
    - Leave the **Content type (optional)**, **Set activation date**, **Set expiration date**, **Enabled**, **Tags** as default and select **Create** to create the secret.
         :::image type="Create a secret" source="media/create-operations-manager-managed-instance/create-a-secret.png" alt-text="Screenshot of create a secret.":::

--- 

## Create a SCOM Managed Instance (preview)

To create a SCOM Managed Instance (preview), follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com) and search for **SCOM Managed Instance**.
1. On the Overview page, you've three options:
    - **Pre-requisites**: Allows you to view the prerequisites.
    - **Create SCOM managed instance**: Allows you to create a SCOM Managed Instance (preview).
    - **Manage your SCOM managed instance**: Allows you to view the list of instances created.
         :::image type="SCOM Managed Instance (preview) Overview" source="media/create-operations-manager-managed-instance/scom-mi-overview.png" alt-text="Screenshot showing SCOM Managed Instance (preview) Overview.":::
1. Select **Create SCOM Managed Instance**.
1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to place the SCOM Managed Instance (preview).
        1. **Resource group**: Select the resource group in which you want to place the SCOM Managed Instance (preview). If you don't have a resource group, select **Create New** to create a new resource group, and then place the instance. We recommend you've a new resource group exclusively for SCOM Managed Instance (preview).
             :::image type="Project details" source="media/create-operations-manager-managed-instance/project-details.png" alt-text="Screenshot showing project details.":::
    1. **Instance details**:
        1. **SCOM Managed Instance name**: Enter the desired SCOM Managed Instance (preview) name.
            >[!Note]    
            >- SCOM Managed Instance (preview) name can have only alphanumeric characters and be up to 10 characters.
            >- SCOM Managed Instance (preview) is equivalent to System Center Operation Manager Management Group, choose a name accordingly.
        1. **Region**: Select the region near to you geographically so latency between your agents and the SCOM Managed Instance (preview) is as low as possible. This region must also contain the VNet.
             :::image type="Instance details" source="media/create-operations-manager-managed-instance/instance-details.png" alt-text="Screenshot showing instance details.":::
    1. **Active directory details**: 
        1. **Domain name**: Enter the name of the domain that is being administered by the Domain Controller.
        1. **DNS Server IP**: Enter the IP address of the DNS Server that is providing the IP addresses to the resources in the domain mentioned above.
        1. **OU Path**: Enter the OU Path to where you want to join the servers. This isn't a necessary field and if left blank, will assume the default value. For example, **OU=testOU,DC=domain,DC=Domain,DC=com**.
             :::image type="Active directory details" source="media/create-operations-manager-managed-instance/active-directory-details.png" alt-text="Screenshot showing Active directory details.":::
    1. **Domain account details**: 
        1. **Key vault**: Select the key vault that has the secret username and secret password of the domain account user credentials.
        1. **Username secret**: Enter the secret name for the user under the selected key vault.
        1. **Password secret**: Enter the secret name for password under the selected key vault.
             :::image type="Domain account details" source="media/create-operations-manager-managed-instance/domain-account-details.png" alt-text="Screenshot showing Domain account details.":::
    1. **Azure Hybrid Benefit**: By default, **No** is selected. Select **Yes** if you're using a Windows Server license for your existing servers. This license is only applicable for the Windows Servers that will be used while creating VMs for the SCOM Managed Instance (preview) and it won't apply to existing Windows Servers.
           :::image type="Azure hybrid benefit" source="media/create-operations-manager-managed-instance/azure-hybrid-benefit.png" alt-text="Screenshot showing Azure hybrid benefit.":::
1. Select **Next**.
1. Under **Networking**, do the following:
    1. **Virtual network**:
        1. **Virtual network**: Select the virtual network that has direct connectivity to the workloads you want to monitor and to your domain controller + DNS server. 
        1. **Subnet**: Select a subnet that has at least 32 IP addresses to house all the SCOM Managed Instance (preview) components. The minimum address space is 28. The subnet can have existing resources in it, however, don't choose the subnet that houses the SQL managed instance because it won't contain enough IP addresses to house the instance.
           >[!Note]
           >Ensure that you have a NAT Gateway associated with the subnet you choose.
    1. **SCOM managed instance interface**:
        1. **Static IP**: Enter the Static IP for the load balancer. This IP should be in the selected subnet range for SCOM Managed Instance (preview).
        1. **DNS name**: Enter the DNS name that you attached to the Static IP above.
    1. **gMSA details**: 
        1. **Computer group name**: Enter the name of the computer group that you created post creation of the gMSA account.
        1. **gMSA account name**: Enter the gMSA account name. The gMSA account name must end with **$**.
           :::image type="gMSA details" source="media/create-operations-manager-managed-instance/gmsa-details.png" alt-text="Screenshot showing gMSA details.":::
1. Select **Next**.
1. Under **Database**, do the following:
    1. **SQL managed instance**:
        1. **Resource Name**: Select the SQL MI resource name for the instance that you would like to associate with this SCOM Managed Instance (preview). Only the SQL MI instance, which has given permissions to the SCOM Managed Instance (preview) should be used here. For more information, see SQL MI creation and permission.
    1. **User managed Identity**:
        1. **User managed identity account**: Select the Managed Identity that you created and provided Admin permissions to the SQL MI. Ensure the same MSI has read permissions on the keyvault for domain account credentials.
1. Select **Next**.
1. Under **Tags**, enter the Name, value, and select the Resource.
     
     Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see  [Tags](/azure/azure-resource-manager/management/tag-resources?wt.mc_id=azuremachinelearning_inproduct_portal_utilities-tags-tab&tabs=json).
1. Select **Next**.
1. Under **Review + Submit**, review all the inputs given so far and select **Create**. Your deployment will now be created on Azure, and it takes up to an hour for the creation of a SCOM Managed Instance (preview). 

    >[!Note]    
    >If the deployment fails, delete the instance and all associated resources, and recreate the instance again. For more information, see  [delete the instance and its resources](./operations-manager-managed-instance-common-questions.md#what-is-the-procedure-to-delete-an-instance).

1. After the deployment is completed, select **Go to resource**. 
     On the instance page, you can view some of the essential details and instructions to post-deployment steps/raise bugs appear.

## Next steps

- [Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview)](migrate-to-operations-manager-managed-instance.md)
- [Scale SCOM Managed Instance (preview)](scale-scom-managed-instance.md)
