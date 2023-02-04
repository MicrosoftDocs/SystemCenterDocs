---
ms.assetid: 
title: Create an instance of Azure Monitor SCOM Managed Instance Preview
description: This article describes how to create an SCOM managed instance to monitor workloads by using System Center Operations Manager functionality on Azure.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 01/27/2023
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Create an instance of Azure Monitor SCOM Managed Instance Preview

Azure Monitor SCOM Managed Instance Preview provides System Center Operations Manager functionality on Azure and helps you monitor all your workloads, whether they're on-premises, in Azure, or in any other cloud services.

This article describes how to create an instance of the service (a SCOM managed instance) with System Center Operations Manager functionality on Azure.

> [!VIDEO https://www.youtube.com/embed/urxiQBkObkU]

>[!Note]  
>In this preview, you can create an instance only in the *West Europe* and *West US* regions.

## Prerequisites

Before you create a SCOM managed instance, use all three of the following tabs to create the necessary prerequisites.

# [General pointers](#tab/pointers-general)

- Ensure that you have at least four virtual cores (one virtual machine) of type Standard DSv2 in your Azure subscription to deploy an instance.
- Ensure that you allow port 1433 (private port) from Azure Monitor SCOM Managed Instance to Azure SQL Managed Instance.
- If you enable public endpoint on Azure SQL Managed Instance, ensure that you allow 3342.
- To ensure reliability and support easy scaling, Azure Monitor SCOM Managed Instance creates a standard load balancer and a uniform virtual machine scale set. For more information, see [Azure Load Balancer](/azure/load-balancer/load-balancer-overview) and [Azure Virtual Machine Scale Sets](/azure/virtual-machine-scale-sets/overview).

# [In your Active Directory domain](#tab/prereqs-active)

>[!Note]
>- To perform Active Directory operations, install the install the **RSAT: Active Directory Domain Services and Lightweight Directory Tools** feature. Then install the **Active Directory Users and Computers** tool. You can install this tool on any machine that has domain connectivity. You must sign in to this tool with some admin permissions to perform all Active Directory operations.
>- To perform operations on DNS server, you need to sign in to the DNS server and run the **DNS Manager** tool.

## Establish direct connectivity (line of sight) between your domain controller and the Azure network

Ensure that there's direct network connectivity (line of sight) between the network that has your domain controller and the network in which you'll deploy a SCOM managed instance. This is required so that all your resources (domain controller, agents, System Center Operations Manager components such as the Ops console, and Azure Monitor SCOM Managed Instance components such as management servers) can communicate with each other over the network.

If your domain controller or any other component is on-premises, you can establish the line of sight through Azure ExpressRoute or VPN. For more information, see  [ExpressRoute documentation](/azure/expressroute/) and [VPN Gateway documentation](/azure/vpn-gateway/).

If your domain controller and all other components are in Azure (a conventional domain controller and not Azure Active Directory) with no presence on-premises, a virtual network will work. (ExpressRoute isn't required.) If you're using one virtual network to host all your components, you'll already have a line of sight between all your components. If you have multiple virtual networks, you'll need to do virtual network peering between all the virtual networks that are in your network. For more information, see  [Virtual network peering in Azure](/azure/virtual-network/virtual-network-peering-overview).

Allow communication on ports 5723, 5724, and 443 between Azure Monitor SCOM Managed Instance and the virtual machine being monitored, and vice versa.

The Active Directory web service must run on domain controllers. The firewall rule and network security group (NSG) must allow communication on port 9389 between the Azure Monitor SCOM Managed Instance virtual network and the domain controller.

We recommend a NAT gateway for outbound internet access from subnets. Edit the subnet to add a NAT gateway. In Azure, add a NAT gateway to the virtual network or subnet where the SCOM managed instance will be created. A NAT gateway is needed for outbound internet access from subnets. For more information, see [What is Virtual Network NAT?](/azure/virtual-network/nat-gateway/nat-overview).

To create a NAT gateway, follow these steps:

1. Create NAT gateway in the same region where the virtual network is present.
1. Create NAT gateway in the same subscription you use for Azure Monitor SCOM Managed Instance.
1. Create a public IP.

   :::image type="NAT gateway" source="media/create-operations-manager-managed-instance/nat-gateway.png" alt-text="Screenshot of public IP information for a NAT gateway.":::

1. Select a virtual network and subnet for Azure Monitor SCOM Managed Instance.

## Configure a domain account in Active Directory

Create a domain account in your Active Directory instance. The domain account is a typical Active Directory account. (It can be a non-admin account.) This account will be used to add the System Center Operations Manager management servers to your existing domain.

:::image type="Active directory users" source="media/create-operations-manager-managed-instance/active-directory-users.png" alt-text="Screenshot of Active Directory users.":::

Ensure that this account has the [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain) to join other servers to your domain. You can use an existing domain account if it has these permissions.

You'll use the configured domain account in later steps for creating a SCOM managed instance.

## Create and configure a computer group

Create a computer group in your Active Directory instance. For more information, see [Create a group account in Active Directory](/windows/security/threat-protection/windows-firewall/create-a-group-account-in-active-directory). All the management servers that you create will be a part of this group so that all the members of the group can retrieve group managed service account (gMSA) credentials (created in subsequent steps). This group can't contain spaces and must have alphanumeric characters only.

:::image type="Active directory computers" source="media/create-operations-manager-managed-instance/active-directory-computers.png" alt-text="Screenshot of Active directory computers.":::

To manage this computer group, provide permissions to the domain account that you created. Follow these steps to provide permissions:

1. Select the group properties, and then select **Managed By**.
1. For **Name**, enter the name of the domain account.
1. Select the **Manager can update membership list** checkbox.

:::image type="Server group properties" source="media/create-operations-manager-managed-instance/server-group-properties.png" alt-text="Screenshot of server group properties.":::

## Create a static IP and configure the DNS name

For all the System Center Operations Manager components to communicate with the load balancer that the Azure Monitor SCOM Managed Instance service will create, you need a static IP and DNS name for the load balancer's front-end configuration.

Ensure that the static IP is in the subnet that you created during virtual network creation. Create a DNS name (according to your organization's policy) for the static IP.

:::image type="DNS manager" source="media/create-operations-manager-managed-instance/dns-manager.png" alt-text="Screenshot of host information in DNS Manager.":::

## Create and configure a gMSA account

Create a gMSA to run the Management Server services and to authenticate the services. Use the following command to create a gMSA:

```powershell
New-ADServiceAccount ContosogMSA -DNSHostName "ContosoLB.aquiladom.com" -PrincipalsAllowedToRetrieveManagedPassword "ContosoServerGroup" -KerberosEncryptionType RC4, AES128, AES256 -ServicePrincipalNames MSOMHSvc/ContosoLB.aquiladom.com, MSOMHSvc/ContosoLB, MSOMSdkSvc/ContosoLB.aquiladom.com, MSOMSdkSvc/ContosoLB 
```

In that command:
- `ContosogMSA` is the gMSA name. 
- `ContosoLB.aquiladom.com` is the DNS name for the load balancer (specified previously).
- `ContosoServerGroup` is the computer group in Active Directory (specified previously).
- `MSOMHSvc/ContosoLB.aquiladom.com`, MSOMHSvc/ContosoLB`, MSOMSdkSvc/ContosoLB.aquiladom.com`, and `MSOMSdkSvc/ContosoLB` are service principal names.

Use the following command if the root key isn't effective:

```powershell
Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10)) 
```

# [In Azure portal](#tab/prereqs-portal)

## Register the Azure Monitor SCOM Managed Instance resource provider

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Subscriptions**.
2. Select the subscription where you want to deploy Azure Monitor SCOM Managed Instance.
3. Under **Settings**, select **Resource providers**.
4. Search for **SCOM** and register **Microsoft.Scom**.
5. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **microsoft.insights**. If the **microsoft.insights** provider isn't registered, select the provider and then select **Register**.

    :::image type="Microsoft insights resource provider" source="media/create-operations-manager-managed-instance/resource-provider.png" alt-text="Screenshot of the Microsoft insights provider.":::

## Create a managed service identity

The managed service identity (MSI) provides an identity for applications to use when connecting to resources that support Azure Active Directory (Azure AD) authentication. For Azure Monitor SCOM Managed Instance, a managed identity will replace the traditional four System Center Operations Manager service accounts. It will be used to access the Azure SQL Managed Instance database. You can also use the MSI to access the key vault.

>[!Note]
>- Ensure you're a contributor in the subscription where you create the MSI.
>- The MSI must have admin permission on Azure SQL Managed Instance and read permission on the key vault that you use for domain account credentials.

1. Sign in to the [Azure portal](https://portal.azure.com). Search for and select **Managed Identities**.
   :::image type="Managed Identity in Azure portal" source="media/create-operations-manager-managed-instance/azure-portal-managed-identity.png" alt-text="Screenshot of the icon for managed identities in the Azure portal.":::
1. On the **Managed Identities** page, select **+ Create**. 
   :::image type="Managed Identity" source="media/create-operations-manager-managed-instance/managed-identities.png" alt-text="Screenshot of Managed Identity.":::

   The **Create User Assigned Managed Identity** pane opens.
1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to create the SCOM managed instance.
        1. **Resource group**: Select the resource group in which you want to create the SCOM managed instance.
    1. **Instance details**:
        1. **Region**: Select the region in which you want to create the SCOM managed instance.
        1. **Name**: Enter a name for the instance.

    :::image type="Create user assigned managed identity" source="media/create-operations-manager-managed-instance/create-user-assigned-managed-identity.png" alt-text="Screenshot of project and instance details for a user-assigned managed identity.":::
1. Select **Next : Tags >**.
1. Under **Tags**, enter the **Name** value, and the select the resource.

   Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups.
1. Select **Next : Review + Create >**.
1. Under **Review + create**, review all the information that you provided, and then select **Create**.
   :::image type="Managed identity review" source="media/create-operations-manager-managed-instance/managed-identity-review.png" alt-text="Screenshot of the tab for reviewing a managed identity before creation.":::

Your deployment is now created on Azure. You can access the resource and view its details.

## Create and configure a SQL managed instance

Before you create a SCOM managed instance, create a SQL managed instance. For more information, see [Create a SQL managed instance](/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql&preserve-view=true).

We recommend the following for creating a SQL managed instance:

- **Resource group**: Create a new resource group for Azure SQL Managed Instance. Azure best practices recommend that you create a new resource group for large Azure resources.
- **Managed instance name**: Choose a unique name. This name will be used while you create a SCOM managed instance to refer to this SQL managed instance that you're creating.
- **Region**: Choose the region close to you. There's no strict requirement on region for the instance, but we recommend the closest region for latency purposes.
- **Compute + storage**: General Purpose (Gen5) with eight cores is the default. This will suffice for the SCOM managed instance.
- **Authentication method**: Select **SQL Authentication**. Enter the credentials that you want to use for accessing the SQL managed instance. These credentials don't refer to any that you've created so far.
- **Virtual network**: This SQL managed instance needs to have direct connectivity (line of sight) to the SCOM managed instance that you create in the future. Choose a virtual network that you'll eventually use for your SCOM managed instance. If you choose a different virtual network, ensure that it has connectivity to the Azure Monitor SCOM Managed Instance virtual network.

   The subnet that you provide to Azure SQL Managed Instance has to be dedicated (delegated) to the SQL managed instance. The provided subnet can't be used to house any other resources. 

   By design, a managed instance needs a minimum of 32 IP addresses in a subnet. As a result, you can use a minimum subnet mask of /27 when defining your subnet IP ranges. For more information, see [Determine required subnet size and range for Azure SQL Managed Instance](/azure/azure-sql/managed-instance/vnet-subnet-determine-size?view=azuresql&preserve-view=true).
- **Connection type**: By default, the connection type is **Proxy**.
- **Public endpoint**: This can either be enabled or disabled. To use Power BI reporting, you need to enable the public endpoint.

  If the Azure SQL Managed Instance virtual network is different from the Azure Monitor SCOM Managed Instance virtual network:

  - If you choose to enable, create an inbound NSG rule on the Azure SQL Managed Instance subnet to allow traffic from the System Center Operations Manager virtual network or subnet to port 3342. For more information, see [Configure public endpoint in Azure SQL Managed Instance](/azure/azure-sql/managed-instance/public-endpoint-configure?view=azuresql&preserve-view=true).
  - If you choose to disable, be sure to peer your Azure SQL Managed Instance virtual network with the one in which System Center Operations Manager and Azure Monitor SCOM Managed Instance are present.

For the rest of the settings on the other tabs, you can leave them as default or change them according to your requirements.

>[!Note]
> Creation of a new SQL managed instance can take up to six hours.

After you create a SQL managed instance, you need to provide permission to the Azure Monitor SCOM Managed Instance resource provider to access this SQL managed instance.

To provide the permissions:

1. Open the SQL managed instance and select **Access control (IAM)**. On the top menu, select **+ Add** > **Add role assignment**.
   :::image type="Access control" source="media/create-operations-manager-managed-instance/access-control.png" alt-text="Screenshot that shows selections for starting the process of adding a role assignment for access control.":::
1. On the **Add role assignment** pane:
   - For **Role**, select **Reader** from the dropdown list.
   - For **Assign access to**, select **User, group, or service principal** from the dropdown list.
   - For **Select**, enter **Microsoft.SCOM**
   :::image type="Add role assignment" source="media/create-operations-manager-managed-instance/add-role-assignment.png" alt-text="Screenshot of selections for adding a role assignment.":::
1. Select **Save**.

### Set the Active Directory admin value in the SQL managed instance

To set the Active Directory admin value in the SQL managed instance, use the following steps.

>[!Note]
>You must have Global Administrator or Privileged Role Administrator permissions for the subscription.

1. Open the SQL managed instance. Under **Settings**, select **Active Directory admin**.
   :::image type="Active directory admin" source="media/create-operations-manager-managed-instance/active-directory-admin.png" alt-text="Screenshot of the pane for Active directory admin information.":::

2. Select **Set admin**, and search for your MSI. This is the same MSI that you provided during the Azure Monitor SCOM Managed Instance creation flow. You'll find the admin added to the SQL managed instance.
   :::image type="Azure Active directory admin" source="media/create-operations-manager-managed-instance/azure-active-directory.png" alt-text="Screenshot of MSI information for Azure Active Directory.":::

3. If you get an error after you add a managed identity account, it indicates that read permissions aren't yet provided to your identity. Be sure to provide the necessary permissions before you create your instance, or your instance creation will fail.
   :::image type="SQL Active directory admin" source="media/create-operations-manager-managed-instance/sql-active-directory-admin.png" alt-text="Screenshot that shows successful Active Directory authentication.":::

For more information about permissions, see [Directory Readers role in Azure Active Directory for Azure SQL](/azure/azure-sql/database/authentication-aad-directory-readers-role?view=azuresql&preserve-view=true).

## Create a key vault and add credentials as a secret  

For security, you can store the domain account (which you created previously in Active Directory) in a key vault.

Azure Key Vault is a cloud service that provides a secure store for keys, secrets, and certificates. For more information, see [About Azure Key Vault](/azure/key-vault/general/overview).

>[!Note]
> You must have Global Administrator or Privileged Role Administrator permissions for the tenant to do the following steps.

1. In the Azure portal, search for and select **Key vaults**. 
     :::image type="Key vaults in portal" source="media/create-operations-manager-managed-instance/azure-portal-key-vaults.png" alt-text="Screenshot of the icon for key vaults in the Azure portal.":::

   The **Key vaults** page opens.

1. Select **+ Create**.
     :::image type="Key vault" source="media/create-operations-manager-managed-instance/key-vaults.png" alt-text="Screenshot of the button for creating a key vault.":::

1. On the **Basics** tab, do the following:
    - **Project details**:
        - **Subscription**: Select the subscription.
        - **Resource group**: Select the desired resource group.
    - **Instance details**:
        - **Key vault name**: Enter the name of your key vault. There are no added restrictions, except for those that apply to names in other Azure services.
        - **Region**: Choose the region that you're going to select for your other resources.
        - **Pricing tier**: Select **Standard** or **Premium** as required.
    - **Recovery options**:
        - **Days to retain deleted vaults**: Enter a value from 7 to 90.
        - **Purge protection**: We recommend enabling this feature to have a mandatory retention period.

   :::image type="create a key vault" source="media/create-operations-manager-managed-instance/create-a-key-vault.png" alt-text="Screenshot of basic information for creating a key vault.":::
1. Select **Next**.
1. On the **Access Policy** tab, do the following:
    - **Access configuration**: Select **Vault access policy**.
    - **Resource access**: Don't select any of the options.
    - **Access policies**: Select **+ Create** to create a new access policy. 
      :::image type="Access policies" source="media/create-operations-manager-managed-instance/access-policies.png" alt-text="Screenshot of the button for creating an access policy.":::

      The **Create an access policy** pane opens.

      1. On the **Permissions** tab, under **Secret permissions**, select **Get** and **List**.
         :::image type="Create an Access policy" source="media/create-operations-manager-managed-instance/create-an-access-policy.png" alt-text="Screenshot of checkboxes for get and list permissions.":::
      1. Select **Next**.
      1. On the **Principal** tab, select the same MSI that is used in Azure SQL Managed Instance admin configuration.

      1. In **Review + create**, review the selections, and select **Create**.
1. Select the access policy created and then select **Next**.
     :::image type="Access policy" source="media/create-operations-manager-managed-instance/access-policy.png" alt-text="Screenshot of Access policy.":::
1. In **Networking**, do the following:
    - Select **Enable public access**.
    - In **Public Access**, select **All networks** for **Allow access from**.

   :::image type="Networking tab" source="media/create-operations-manager-managed-instance/networking-inline.png" alt-text="Screenshot of Networking tab." lightbox="media/create-operations-manager-managed-instance/networking-expanded.png":::
1. Select **Next**.
1. In **Tags**, select the tags if required and select **Next**.
1. In **Review + create**, review the selections, and select **Create** to create the key vault.
  
    :::image type="content" source="media/create-operations-manager-managed-instance/review-inline.png" alt-text="Screenshot of review tab." lightbox="media/create-operations-manager-managed-instance/review-expanded.png":::

1. On the left pane, under **Objects**, select **Secrets**.

    :::image type="content" source="./media/create-operations-manager-managed-instance/secrets-inline.png" alt-text="Screenshot of secrets." lightbox="./media/create-operations-manager-managed-instance/secrets-expanded.png":::

     >[!Note]
     > You must create two secrets to store the domain account credentials.
     > - Username
     > - Password

1. Select **+ Generate/Import**. 

1. Do the following in **Create a secret** page.
    - **Upload options**: Select **Manual**.
    - **Name**: Enter the name of secret. For example, you can use *Username* for username secret and *Password* for password secret.
    - **Secret value**: For username value (in the format, domain\username), it will be the domain account username, and for password, it will be the domain account password.
       For example, if the domain is *contoso.com*, then the username would be in the format *contoso\username*. Here are the sample screenshots.

       :::image type="Secrets" source="media/create-operations-manager-managed-instance/create-a-secret-username.png" alt-text="Screenshot of create a secret username.":::

       :::image type="Secrets" source="media/create-operations-manager-managed-instance/create-a-secret-password.png" alt-text="Screenshot of create a secret password.":::

    - Leave the **Content type (optional)**, **Set activation date**, **Set expiration date**, **Enabled**, and **Tags** as default and select **Create** to create the secret.

       :::image type="Secrets" source="media/create-operations-manager-managed-instance/create-a-secret-2.png" alt-text="Screenshot of create a secret.":::

---

## Create a SCOM managed instance

To create a SCOM managed instance, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com), and search for **SCOM Managed Instance**.
1. On the Overview page, you have three options:
    - **Pre-requisites**: Allows you to view the prerequisites.
    - **Create SCOM managed instance**: Allows you to create a SCOM managed instance.
    - **Manage your SCOM managed instance**: Allows you to view the list of instances created.

         :::image type="Azure Monitor SCOM Managed Instance Overview" source="media/create-operations-manager-managed-instance/scom-mi-overview.png" alt-text="Screenshot showing Azure Monitor SCOM Managed Instance Overview.":::

1. Select **Create SCOM managed instance**. 
1. **Prerequisites to create SCOM managed instance** page opens. Download the script and run in a domain-joined machine to validate the prerequisites.
    :::image type="Script download" source="media/create-operations-manager-managed-instance/script-download-inline.png" alt-text="Screenshot showing script download option." lightbox="media/create-operations-manager-managed-instance/script-download-expanded.png":::
1. Under **Basics**, do the following:
    1. **Project details**:
        1. **Subscription**: Select the Azure subscription in which you want to place the SCOM managed instance.
        1. **Resource group**: Select the resource group in which you want to place the SCOM managed instance. If you don't have a resource group, select **Create New** to create a new resource group, and then place the instance. We recommend you have a new resource group exclusively for Azure Monitor SCOM Managed Instance.

             :::image type="Project details" source="media/create-operations-manager-managed-instance/project-details.png" alt-text="Screenshot showing project details.":::

    1. **Instance details**:
        1. **SCOM managed instance name**: Enter the desired SCOM managed instance name.
            >[!Note]
            >- SCOM managed instance name can have only alphanumeric characters and be up to 10 characters.
            >- Azure Monitor SCOM Managed Instance is equivalent to System Center Operation Manager Management Group, so choose a name accordingly.
        1. **Region**: Select the region near to you geographically so that latency between your agents and the SCOM managed instance is as low as possible. This region must also contain the virtual network.

             :::image type="Instance details" source="media/create-operations-manager-managed-instance/instance-details.png" alt-text="Screenshot showing instance details.":::

    1. **Active directory details**: 
        1. **Domain name**: Enter the name of the domain that is being administered by the Domain Controller.
        1. **DNS Server IP**: Enter the IP address of the DNS Server that is providing the IP addresses to the resources in the domain mentioned above.
        1. **OU Path**: Enter the OU Path to where you want to join the servers. This isn't a necessary field, and if left blank, it will assume the default value. Ensure that the value you enter is in the DistinguishedName format. For example, **OU=testOU,DC=domain,DC=Domain,DC=com**.

             :::image type="Active directory details" source="media/create-operations-manager-managed-instance/active-directory-details.png" alt-text="Screenshot showing Active directory details.":::

    1. **Domain account details**:
        1. **Key vault**: Select the key vault that has the secret username and secret password of the domain account user credentials.
        1. **Username secret**: Enter the secret name for the user under the selected key vault.
        1. **Password secret**: Enter the secret name for password under the selected key vault.
            >[!Note]
            >Ensure that you provide the secret names created in the **selected Key vault**, and not the actual domain username and password.


          :::image type="content" source="./media/create-operations-manager-managed-instance/secret-password-mapping-inline.png" alt-text="Screenshot showing password mapping for create a secret." lightbox="./media/create-operations-manager-managed-instance/secret-password-mapping-expanded.png":::

    1. **Azure Hybrid Benefit**: By default, **No** is selected. Select **Yes** if you're using a Windows Server license for your existing servers. This license is only applicable for the Windows Servers that will be used while creating virtual machine for the SCOM managed instance, and it won't apply to the existing Windows Servers.
           :::image type="Azure hybrid benefit" source="media/create-operations-manager-managed-instance/azure-hybrid-benefit.png" alt-text="Screenshot showing Azure hybrid benefit.":::
1. Select **Next**.
1. Under **Networking**, do the following:
    1. **Virtual network**:
        1. **Virtual network**: Select the virtual network that has direct connectivity to the workloads you want to monitor and to your domain controller + DNS server.
        1. **Subnet**: Select a subnet that has at least 32 IP addresses to house all the Azure Monitor SCOM Managed Instance components. The minimum address space is 28. The subnet can have existing resources in it; however, don't choose the subnet that houses the SQL managed instance because it won't contain enough IP addresses to house the instance.
           >[!Note]
           >Ensure that you have a NAT Gateway associated with the subnet you choose.
    1. **SCOM managed instance interface**:
        1. **Static IP**: Enter the Static IP for the load balancer. This IP should be in the selected subnet range for Azure Monitor SCOM Managed Instance.
        1. **DNS name**: Enter the DNS name that you attached to the Static IP above.
    1. **gMSA details**: 
        1. **Computer group name**: Enter the name of the computer group that you created post creation of the gMSA.
        1. **gMSA account name**: Enter the gMSA name. It must end with **$**.
           :::image type="gMSA details" source="media/create-operations-manager-managed-instance/gmsa-details.png" alt-text="Screenshot showing gMSA details.":::
1. Select **Next**.
1. Under **Database**, do the following:
    1. **SQL managed instance**:
        1. **Resource Name**: Select the Azure SQL Managed Instance resource name for the instance that you would like to associate with this SCOM managed instance. Only the SQL managed instance, which has given permissions to the SCOM managed instance, should be used here. For more information, see SQL managed instance creation and permission.
    1. **User managed Identity**:
        1. **User managed identity account**: Select the Managed Identity that you created and provided Admin permissions to the SQL managed instance. Ensure the same MSI has read permissions on the key vault for domain account credentials.
1. Select **Next**.
1. Under **Tags**, enter the Name, value, and select the Resource.
     
     Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see [Tags](/azure/azure-resource-manager/management/tag-resources?wt.mc_id=azuremachinelearning_inproduct_portal_utilities-tags-tab&tabs=json).
1. Select **Next**.
1. Under **Review + Submit**, review all the inputs given so far and select **Create**. Your deployment will now be created on Azure, and it takes up to an hour for the creation of a SCOM managed instance. 

    >[!Note]
    >If the deployment fails, delete the instance and all the associated resources, and recreate the instance again. For more information, see [delete the instance and its resources](./operations-manager-managed-instance-common-questions.md#what-is-the-procedure-to-delete-an-instance).

1. After the deployment is completed, select **Go to resource**.
     On the instance page, you can view some of the essential details and instructions to post-deployment steps/raise bugs appear.

## Next steps

- [Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance](migrate-to-operations-manager-managed-instance.md).
- [Scale Azure Monitor SCOM Managed Instance](scale-scom-managed-instance.md).

To provide feedback on Azure Monitor SCOM Managed Instance, use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUMUlFOUY4N0RENktHWDhNNkgwMkhQV0lSQi4u).
