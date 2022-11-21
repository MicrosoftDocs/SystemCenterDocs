---
ms.assetid: 
title: Create an Azure Monitor SCOM Managed Instance (preview)
description: This article describes how to create an Azure Monitor SCOM Managed Instance (preview) to monitor workloads using System Center Operations Manager functionality on Azure.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/21/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Create an Azure Monitor SCOM Managed Instance (preview) on Azure

This article describes how to create an Azure Monitor SCOM Managed Instance (preview) that helps you monitor all your workloads, whether on-premises, in Azure, or in any other cloud services with System Center Operations Manager functionality on Azure.

## Prerequisites

The following are the prerequisites before you create a SCOM Managed Instance (preview):

# [General Pointers](#tab/pointers-general)

- In this preview, you can create an instance only in West Europe and West US. 
- Ensure that you've at least four virtual cores (one VM) of type Standard DSv2 in your Azure subscription to deploy an instance.
- Ensure you allow ports 1433 (private port) from the SCOM Managed Instance (preview) to the SQL MI instance.
- If you enable public endpoint on SQL MI, ensure that you allow 3342.

# [In your Active directory domain](#tab/prereqs-active)

## Establish direct connectivity (line-of-sight) between your Domain Controller and your Azure network

- Ensure that there's direct network connectivity (line-of-sight) between the network, which has your Domain Controller, Ops Console, Agents, and the network in which you'll deploy a SCOM Managed Instance (preview). This is required so that all your resources (Domain Controller, System Center Operations Manager Components such as Ops Console, SCOM Managed Instance (preview) Components such as Management Servers) can talk to each other over the network.
- If your Domain Controller or any other component is on-premises, the line-of-sight can be established through *ExpressRoute* or *VPN*. For more information, see [ExpressRoute](/azure/expressroute/) and [VPN Gateway](/azure/vpn-gateway/)
- If your Domain Controller and all other components are in Azure (a conventional Domain Controller and not Azure Active Directory) with no presence on-premises, a Virtual network (VNet) will work (ExpressRoute isn't needed). If you are using one VNet to host all your components, you will already have a line-of-sight between all your components. If you have multiple VNets, you will need to do VNet peering between all the VNets that are in your network. For more information, see VNet peering in Azure.
- Allow Port 5723/5724/443 to communicate while talking from SCOM Managed Instance (preview) to the VMs being monitored and vice versa.

## Configure one domain account in Active Directory

- Create one domain account in your Active Directory. The domain account is a typical Active Directory account (it can be a non-admin account). This account will be used to join the SCOM Management Servers to your existing domain.
     :::image type="Active directory users" source="media/create-operations-manager-managed-instance/active-directory-users.png" alt-text="Screenshot of Active directory users.":::
- Ensure that this account has the [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain) to join other servers to your domain.
- You can use an existing domain account if it has these [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain).

## Create and configure a computer group 

- Create a computer group in your active directory. For more information, see [Create a group account in active directory](/windows/security/threat-protection/windows-firewall/create-a-group-account-in-active-directory). All the management servers you create will be a part of this group so that all the members of the group can retrieve gMSA account credentials (created in future steps).  
     :::image type="Active directory computers" source="media/create-operations-manager-managed-instance/active-directory-computers.png" alt-text="Screenshot of Active directory computers.":::
- To manage this computer group, provide permissions to the domain account you created in the above step. Follow the below steps to provide permissions:
    1. Select the group properties and select **Managed By**.
        1. **Name**: Enter the name of the domain account.
        1. Select the checkbox **Manager can update membership list**. 
            :::image type="Server group properties" source="media/create-operations-manager-managed-instance/server-group-properties.png" alt-text="Screenshot of Server group properties.":::

## Create a static IP and configure the DNS name

- For all the SCOM components, to communicate with the load-balancer that will be created by the SCOM Managed Instance (preview) service, you need a static IP and DNS name for the load-balancer front-end configuration. For more information, see \<link\>. 
- Ensure that the static IP is in the subnet that was created during VNet creation and it will be used during the creation of an instance. 
- Create a DNS name (as per your organization policy) for the static IP.
     :::image type="DNS manager" source="media/create-operations-manager-managed-instance/dns-manager.png" alt-text="Screenshot of DNS manager.":::

## Create and configure a gMSA account 

- Create a gMSA (Group Managed Service Account) account to run the Management Server services and to authenticate the services. Use the below PowerShell command to create a gMSA account: 

    ```powershell
    New-ADServiceAccount VMSSLBContoso -DNSHostName "ContosoVMSSLB.aquiladomdns.comnet" -PrincipalsAllowedToRetrieveManagedPassword ‘ContosoServerGroupcomputerGroup’ -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames MSOMHSvc/ ContosoLB.aquiladom.comVMSSLB.dns.net, MSOMHSvc/ ContosoLBVMSSLB, MSOMSdkSvc/ ContosoLB.aquiladom.comVMSSLB.dns.net, MSOMSdkSvc/ VMSSLB ContosoLB 
    ```
    
    - ContosoVMSSLB = gMSA account name 
    - ContosoLB.aquiladom.comVMSSLB.dns.net = DNS name for LB (specified in the previous step) 
    - ContosoServerGroupcomputerGroup = Computer group in AD (specified previously)
    - MSOMHSvc/ ContosoLB.aquiladom.comVMSSLB.dns.net, MSOMHSvc/ VMSSLB	ContosoLB, MSOMSdkSvc/ ContosoLB.aquiladom.comVMSSLB.dns.net, MSOMSdkSvc/ ContosoLBVMSSLB = Service Principal names 


# [In Azure portal](#tab/prereqs-portal)

## Create a Managed Service Identity (MSI)

The Managed Service Identity provide an identity for applications to use when connecting to resources that support Azure Active Directory (Azure AD) authentication. For SCOM Managed Instance (preview), a Managed Identity will replace the traditional four System Center Operations Manager service accounts and it will be used to access the SQL MI database. MSI can also be used to access the key vault.

>[!Note]
>Ensure you are a contributor in the subscription you create the MSI.

1. Sign in to the [Azure portal](https://portal.azure.com) and search for **Managed Identities**. Managed Identities page opens.
     :::image type="Managed Identity in Azure Portal" source="media/create-operations-manager-managed-instance/azure-portal-managed-identity.png" alt-text="Screenshot of Managed Identity in Azure portal.":::
1. Select **+ Create**. **Create User Assigned Managed Identity** page opens.
     :::image type="Managed Identity" source="media/create-operations-manager-managed-instance/managed-identities.png" alt-text="Screenshot of Managed Identity.":::
1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to create SCOM Managed Instance (preview).
        1. **Resource group**: Select the resource group in which you want to create SCOM Managed Instance (preview).
    1. **Instance details**:
        1. **Region**: Select the region in which you want to create SCOM Managed Instance (preview).
        1. **Name**: Enter the desired name.
         :::image type="Create user assigned managed identity" source="media/create-operations-manager-managed-instance/create-user-assigned-managed-identity.png" alt-text="Screenshot of Create user assigned managed identity.":::
1. Select **Next : Tags >**.
1. Under **Tags**, enter the Name, value, and select the Resource. Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see Tags.
1. Select **Next : Review + Create >**.
1. Under **Review + create**, review all the inputs given so far and select **Create**. 
     :::image type="Managed identity review" source="media/create-operations-manager-managed-instance/managed-identity-review.png" alt-text="Screenshot of Managed identity review.":::
Your deployment will now be created on Azure, you can access the resource and view its details.
     :::image type="Managed identity overview" source="media/create-operations-manager-managed-instance/overview-managed-identity.png" alt-text="Screenshot of Managed identity overview.":::

## Create and configure an SQL MI instance

Before you create a SCOM Managed Instance (preview), create a SQL MI instance. For more information, see Create an Azure SQL Managed Instance.

Below are the recommendations while you create a SQL MI instance:

- **Resource Group**: Create a new resource group for SQL MI. Azure best practices recommends you to create a new Resource Group for large Azure resources.
- **Managed Instance name**: Choose a unique name. This name will be used while you create a SCOM Managed Instance (preview) to refer to this SQL MI instance that you are creating.
- **Region**: Choose the region close to you. There is no strict requirement on region for the instance but the closest region is recommended for latency purposes.
- **Compute+Storage**: General Purpose (Gen5) eight cores is the default number of cores. This will suffice for the SCOM managed instance (preview).
- **Authentication Method**: You can select **SQL Authentication**. In the credentials, enter the credentials you would like to access the SQL MI instance with. These credentials don't refer to any that you have created so far.
- **VNet**: This SQL MI instance needs to have direct connectivity (line-of-sight) to the SCOM Managed Instance (preview) that you create in future. Thus, choose a VNet that you will eventually use for your SCOM Managed Instance (preview), or if you choose a different VNet, ensure it has connectivity to the SCOM Managed Instance (preview) VNet. 

    In terms of Subnet selection, the subnet you provide to SQL MI has to be dedicated (delegated) to the SQL MI Instance. The provided subnet can't be used to house any other resources. By design, a managed instance needs a minimum of 32 IP addresses in a subnet. As a result, you can use a minimum subnet mask of /27 when defining your subnet IP ranges. For more information, see Determine required subnet size and range for Azure SQL Managed Instance.
- **Connection Type**: By default, connection type is Proxy.
- **Public Endpoint**: This can either be *Enabled* or *Disabled*. To leverage the Power BI reporting, you need to enable the Public Endpoint. 

     If the SQL MI VNet is different from the SCOM MI VNet, 
       - If you enable it, you have to create an inbound NSG rule on the SQL MI subnet to allow traffic from the System Center Operations Manager Vnet/Subnet to port 3342. For more information, see Configure public endpoint in Azure SQL Managed Instance. 
       - If you disable it, you have to peer your SQL MI VNet with the one in which System Center Operations Manager and SCOM managed instance (preview) are present.
	
For the rest of the settings in the other tabs, you can leave them as default or change as per your requirements.

>[!Note]
> Creation of a new SQL MI can take up to 6 hours.

After the creation of SQL MI, you need to provide permission to the SCOM Managed Instance (preview) Resource Provider to access this SQL MI instance. To provide the permissions, do the following:

1. Open SQL MI, and select **Access Control (IAM)**. In the top menu, select **+Add** > **Add role assignment** 
     :::image type="Access control" source="media/create-operations-manager-managed-instance/access-control.png" alt-text="Screenshot of access control.":::
1. In **Add role assignment** page, do the following:
    - **Role**: Select **Reader** from the dropdown.
    - **Assign access to**: Select **User, group, or service principal** from the dropdown.
    - **Select**: Enter **Microsoft.SCOM**
         :::image type="Add role assignment" source="media/create-operations-manager-managed-instance/add-role-assignment.png" alt-text="Screenshot of Add role assignment.":::
1. Select **Save**.

### Set the Active Directory Admin value in the SQL MI Instance

To set the Active Directory Admin value in the SQL MI Instance, follow these steps:

For more information, see Directory Readers role in Azure Active Directory for Azure SQL.

To perform the below steps, you need to be the Global Admin/Privileged Role Admin of the subscription:

1.	Open the SQL MI, under **Settings**, select **Active Directory admin**.
     :::image type="Active directory admin" source="media/create-operations-manager-managed-instance/active-directory-admin.png" alt-text="Screenshot of Active directory admin.":::

2.	Select **Set admin**, search for your MSI (the same MSI that you provided during the SCOM Managed Instance (preview) creation flow). You will find the admin added to the SQL MI.
     :::image type="Azure Active directory admin" source="media/create-operations-manager-managed-instance/azure-active-directory.png" alt-text="Screenshot of Azure Active directory admin.":::

3.	If you get error after you add managed identity account, it indicates that read permissions are not yet provided to your identity. Ensure to provide the necessary permissions before you create your instance, else your instance creation will fails.
     :::image type="SQL Active directory admin" source="media/create-operations-manager-managed-instance/sql-active-directory-admin.png" alt-text="Screenshot of SQL Active directory admin.":::

## Create a key vault and add credentials as a secret in the Key vault  

Store the domain account you create in Active Directory in a Key vault account for security. Azure Key Vault is a cloud service that provides a secure store for keys, secrets, and certificates. For more information, see [Azure Key Vault](/azure/key-vault/general/overview). 

>[!Note]
> Ensure you are a contributor in the subscription you create the MSI.

1.	Open Azure portal and search for **Key vaults**. Key vaults page opens.
     :::image type="Key vaults in portal" source="media/create-operations-manager-managed-instance/azure-portal-key-vaults.png" alt-text="Screenshot of Key vaults in portal.":::

2.	Select **+ Create**. 
     :::image type="Key vault" source="media/create-operations-manager-managed-instance/key-vaults.png" alt-text="Screenshot of Key vaults.":::
    
3. In the **Basics**, do the following:
    - Project details:
        - Subscription:
        - Resource group:
    - Instance details:
        -  Key vault name: The name of your key vault. No added restrictions except for those that apply to names in other Azure services
        - Region: Choose the region that you are going to select for your other resources
        - Pricing tier: Standard is good enough for our needs. Select premium if you need to
    - Recovery options:
        - Soft-delete:
        - Days to retain deleted vaults: Can be a value from 7 to 90. 
        - Purge protection: We recommend enabling this feature to have a mandatory retention period.
             :::image type="create a key vault" source="media/create-operations-manager-managed-instance/create-a-key-vault.png" alt-text="Screenshot of create a key vault.":::
4. Select **Next**.
5. In the **Access Policy**, do the following:
    - **Access configuration**: Select **Vault access policy**.
    - **Resource access**: Don't select any of the options.
    - **Access policies**: Select **+ Create** to create a new access policy. **Create an access policy** page opens on the right pane. 
         :::image type="Access policies" source="media/create-operations-manager-managed-instance/access-policies.png" alt-text="Screenshot of Access policies.":::
        1. In **Permissions** > **Secret permissions**, select **Get** and **List**. 
             :::image type="Create an Access policy" source="media/create-operations-manager-managed-instance/create-an-access-policy.png" alt-text="Screenshot of Create an Access policy.":::
        1. Select **Next**.
        1. In **Principal**, search for the MSI you created in the previous step and select.
             :::image type="Access policies principal" source="media/create-operations-manager-managed-instance/principal.png" alt-text="Screenshot of Access policies principal.":::
        1. In **Review + create**, review the selections and select **Create**. 
             :::image type="Access policy review" source="media/create-operations-manager-managed-instance/access-policy-review.png" alt-text="Screenshot of Access policy review.":::
1. Select the access policy created and then select **Next**.
     :::image type="Access policy" source="media/create-operations-manager-managed-instance/access-policy.png" alt-text="Screenshot of Access policy.":::
1. In **Networking**, do the following:
    - Select **Enable public access**.
    - **Public Access**
        - **Allow access from**: Select **All networks**.
             :::image type="Networking tab" source="media/create-operations-manager-managed-instance/Networking.png" alt-text="Screenshot of Networking tab.":::
1. Select **Next**.
1. In **Tags**, select tags if required and select **Next**.
1. In **Review + create**, review the selections and select **Create** to create the Key vault.
     :::image type="Review tab" source="media/create-operations-manager-managed-instance/review.png" alt-text="Screenshot of review tab.":::
1. On the left pane, under **Objects**, select **Secrets**. 
    
     >[!Note]
     > You must create two secrets.
     > - Username
     > - Password. 

1. Select **+ Generate/Import**. 
     :::image type="Secrets" source="media/create-operations-manager-managed-instance/secrets.png" alt-text="Screenshot of secrets.":::
1. Do the following in **Create a secret** page.
    - **Upload options**: Select **Manual**.
    - **Name**: Enter the name of secret. For example, you can use *Username* for username secret and *Password* for password secret.
    - **Secret value**: Secret value will be the credential values for the specific item. For username, it will be the the domain account username and for password, it will be the domain account password.
    - Leave the **Content type (optional)**, **Set activation date**, **Set expiration date**,**Enabled**, **Tags** as default and select **Create** to create the secret.
         :::image type="Create a secret" source="media/create-operations-manager-managed-instance/create-a-secret.png" alt-text="Screenshot of create a secret.":::

--- 

## Create a SCOM Managed Instance (preview)

To create a SCOM Managed Instance (preview), follow the below steps:

1. Sign in to the [Azure portal](https://portal.azure.com) and search for **SCOM** or **SCOM Managed Instance**. The Overview page opens.
1. On the Overview page, you have three options:
    - **Pre-requisites**: Allows you to view the prerequisites
    - **Create SCOM Managed Instance**: Allows you to create a SCOM Managed Instance (preview)
    - **Manage your SCOM Managed Instance**: Allows you to view the list of instances created.
1. Select **Create SCOM Managed Instance**.
1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to place the SCOM Managed Instance (preview).
        1. **Resource group**: Select the resource group in which you want to place the SCOM Managed Instance (preview). If you don't have a resource group in which you want to place the SCOM Managed Instance (preview), select **Create New** to create a new resource group and then place the instance. We recommend you have a new resource group exclusively for SCOM Managed Instance (preview).
    1. **Instance details**:
        1. **SCOM Managed Instance name**: Enter the desired SCOM Managed Instance (preview) name.
            >[!Note]
            >- SCOM Managed Instance (preview) name can have only alphanumeric  characters and up to 10 characters long.
            >- SCOM Managed Instance (preview) is equivalent to System Center Operation Manager Management Group so choose a name accordingly.
        1. **Region**: Select the region that is near to you geographically so that latency between your agents and the SCOM Managed Instance (preview) is as low as possible.
    1. **Active directory details**: 
        1. **Domain name**: Enter the name of the domain that is being administered by the Domain Controller.
        1. **DNS Server IP**: Enter the IP address of the DNS Server that is providing the IP addresses to the resources in the domain mentioned above.
        1. **OU Path**: Enter the OU Path where you want to join the servers to. This is not a necessary field and if left blank, it will assume the default value.
    1. **Domain account details**: 
        1. **Key vault**: Select the key vault which you created that has the secret username and secret password of the domain account user credentials.
        1. **Username secret**: Enter the username under the selected key vault.
        1. **Password secret**: Enter the password under the selected key vault.
    1. **Azure Hybrid Benefit**: Select **Yes** if you are using a Windows Server license for your existing servers. This license is only applicable for the Windows Servers that will be used while creating VMs for the SCOM Managed Instance (preview) and it won't apply to existing Windows Servers.
1. Select **Next**.
1. Under **Networking**, do the following:
    1. **Virtual network**:
        1. **Virtual network**: Select the virtual network that has direct connectivity to the workloads you want to monitor and to your domain controller + DNS server. 
        1. **Subnet**: Select a subnet that has at least 10 IP addresses to house all the SCOM Managed Instance (preview) components. The minimum address space is 28. The subnet can have existing resources in it, however, don't choose the subnet that houses the SQL managed instance because it won't contain the sufficient number of IP addresses to house the instance.
    1. **SCOM managed instance interface**:
        1. **Static IP**: Enter the Static IP that you specified for the load-balancer. 
        1. **DNS name**: Enter the DNS name that you attached to the Static IP above.
    1. **gMSA details**: 
        1. **Computer group name**: Enter the name of the computer group that you created post creation of the gMSA account.
        1. **gMSA account name**: Enter the gMSA account name.
1. Select **Next**.
1. Under **Database**, do the following:
    1. **SQL managed instance**:
        1. **Resource Name**: Select the SQL MI resource name for the instance that you would like to associate with this SCOM Managed Instance (preview). Only the SQL MI instance, which has given permissions to the SCOM Managed Instance (preview) should be used here. For more information, see SQL MI creation and permission.
    1. **User managed Identity**:
        1. **User managed identity account**: Select the Managed Identity that you created and provided Admin permissions to in the SQL MI Instance. For more information, see MSI creation process.
1. Select **Next**.
1. Under **Tags**, enter the Name, value, and select the Resource. Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see Tags.
1. Select **Next**.
1. Under **Review + Submit**, review all the inputs given so far and select **Create**. Your deployment will now be created on Azure, and it takes up to an hour for the creation of a SCOM Managed Instance (preview). 

    >[!Note]
    >If the deployment fails, delete the instance and all associated resources, and recreate the instance again. For more information, see delete the instance and its resources.

1. After the deployment is completed, select **Go to resource**. On the created instance page, some of the essential details and instructions to view the post-deployment steps/raise bugs appear.

## Next steps

> [!div class="nextstepaction"]
> [Connect SCOM Managed Instance (preview) to Ops console](connect-managed-instance-ops-console.md)