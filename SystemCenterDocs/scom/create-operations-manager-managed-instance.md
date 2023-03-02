---
ms.assetid: 
title: Create an instance of Azure Monitor SCOM Managed Instance (preview)
description: This article describes how to create a SCOM managed instance to monitor workloads by using System Center Operations Manager functionality on Azure.
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 02/13/2023
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: 'sc-om-2022'
---

# Create an instance of Azure Monitor SCOM Managed Instance (preview)

Azure Monitor SCOM Managed Instance (preview) provides System Center Operations Manager functionality in Azure. It helps you monitor all your workloads, whether they're on-premises, in Azure, or in any other cloud services.

This article describes how to create an instance of the service (a SCOM managed instance) with System Center Operations Manager functionality in Azure.

For more information about deploying SCOM Managed Instance (preview), play the following video.

> [!VIDEO https://www.youtube.com/embed/urxiQBkObkU]

>[!Note]  
>In this preview of the service, you can create an instance only in the **West Europe** and **West US** regions.

## Prerequisites

Before you create a SCOM managed instance, use all three of the following tabs to meet the necessary prerequisites.

# [General pointers](#tab/pointers-general)

- Ensure that you have at least four virtual cores (one virtual machine) of type Standard DSv2 in your Azure subscription to deploy an instance.
- Ensure that you allow port 1433 (private port) from SCOM Managed Instance (preview) to Azure SQL Managed Instance.
- If you enable a public endpoint on Azure SQL Managed Instance, ensure that you allow port 3342.
- To help ensure reliability and support easy scaling, SCOM Managed Instance (preview) creates a standard load balancer and a uniform virtual machine scale set. For more information, see [Azure Load Balancer](/azure/load-balancer/load-balancer-overview) and [Azure Virtual Machine Scale Sets](/azure/virtual-machine-scale-sets/overview).

# [In your Active Directory domain](#tab/prereqs-active)

>[!Note]
>- To perform Active Directory operations, install the **RSAT: Active Directory Domain Services and Lightweight Directory Tools** feature. Then install the **Active Directory Users and Computers** tool. You can install this tool on any machine that has domain connectivity. You must sign in to this tool with admin permissions to perform all Active Directory operations.
>- To perform operations on the DNS server, you need to sign in to the DNS server and run the **DNS Manager** tool.

## Establish direct connectivity (line of sight) between your domain controller and the Azure network

Ensure that there's direct network connectivity (line of sight) between the network that has your domain controller and the network in which you'll deploy a SCOM managed instance. This is required so that all your resources (domain controller, agents, System Center Operations Manager components such as the Ops console, and SCOM Managed Instance (preview) components such as management servers) can communicate with each other over the network.

If your domain controller or any other component is on-premises, you can establish the line of sight through Azure ExpressRoute or VPN. For more information, see [ExpressRoute documentation](/azure/expressroute/) and [Azure VPN Gateway documentation](/azure/vpn-gateway/).

If your domain controller and all other components are in Azure (a conventional domain controller and not Azure Active Directory) with no presence on-premises, a virtual network will work. (ExpressRoute isn't required.) If you're using one virtual network to host all your components, you'll already have a line of sight between all your components. If you have multiple virtual networks, you'll need to do virtual network peering between all the virtual networks that are in your network. For more information, see  [Virtual network peering in Azure](/azure/virtual-network/virtual-network-peering-overview).

Allow communication on ports 5723, 5724, and 443 between SCOM Managed Instance (preview) and the virtual machine being monitored, and vice versa.

The Active Directory web service must run on domain controllers. The firewall rule and network security group (NSG) must allow communication on port 9389 between the SCOM Managed Instance (preview) virtual network and the domain controller.

To ensure the functioning of Active Directory commands on a SCOM managed instance, verify that the following ports are accessible from the virtual network or subnet:

- TCP port 389 for LDAP
- TCP port 636 for LDAP over SSL
- TCP port 3269 for global catalog over SSL
- TCP and UDP port 88 for Kerberos
- TCP and UDP port 53 for DNS

We recommend a NAT gateway for outbound internet access from subnets. Edit the subnet to add a NAT gateway. In Azure, add a NAT gateway to the virtual network or subnet where the SCOM managed instance will be created. A NAT gateway is needed for outbound internet access from subnets. For more information, see [What is Virtual Network NAT?](/azure/virtual-network/nat-gateway/nat-overview).

To create a NAT gateway, follow these steps:

1. Create a NAT gateway in the same region where the virtual network is present.
1. Create a NAT gateway in the same subscription that you use for SCOM Managed Instance (preview).
1. Create a public IP.

   :::image type="NAT gateway" source="media/create-operations-manager-managed-instance/nat-gateway.png" alt-text="Screenshot of public IP information for a NAT gateway.":::

1. Select a virtual network and subnet for SCOM Managed Instance (preview).

## Configure a domain account in Active Directory

Create a domain account in your Active Directory instance. The domain account is a typical Active Directory account. (It can be a non-admin account.) You'll use this account to add the System Center Operations Manager management servers to your existing domain.

:::image type="Active directory users" source="media/create-operations-manager-managed-instance/active-directory-users.png" alt-text="Screenshot of Active Directory users.":::

Ensure that this account has the [permissions](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain) to join other servers to your domain. You can use an existing domain account if it has these permissions.

You'll use the configured domain account in later steps for creating a SCOM managed instance.

## Create and configure a computer group

Create a computer group in your Active Directory instance. For more information, see [Create a group account in Active Directory](/windows/security/threat-protection/windows-firewall/create-a-group-account-in-active-directory). All the management servers that you create will be a part of this group so that all the members of the group can retrieve group managed service account (gMSA) credentials. (You'll create these credentials in later steps.) The group name can't contain spaces and must have alphabet characters only.

:::image type="Active directory computers" source="media/create-operations-manager-managed-instance/active-directory-computers.png" alt-text="Screenshot of Active Directory computers.":::

To manage this computer group, provide permissions to the domain account that you created. Follow these steps to provide permissions:

1. Select the group properties, and then select **Managed By**.
1. For **Name**, enter the name of the domain account.
1. Select the **Manager can update membership list** checkbox.

:::image type="Server group properties" source="media/create-operations-manager-managed-instance/server-group-properties.png" alt-text="Screenshot of server group properties.":::

## Create a static IP and configure the DNS name

For all the System Center Operations Manager components to communicate with the load balancer that the SCOM Managed Instance (preview) service will create, you need a static IP and DNS name for the load balancer's front-end configuration.

Ensure that the static IP is in the subnet that you created during virtual network creation. Create a DNS name (according to your organization's policy) for the static IP.

:::image type="DNS manager" source="media/create-operations-manager-managed-instance/dns-manager.png" alt-text="Screenshot of host information in DNS Manager.":::

## Create and configure a gMSA account

Create a gMSA to run the management server services and to authenticate the services. Use the following command to create a gMSA:

```powershell
New-ADServiceAccount ContosogMSA -DNSHostName "ContosoLB.aquiladom.com" -PrincipalsAllowedToRetrieveManagedPassword "ContosoServerGroup" -KerberosEncryptionType, AES128, AES256 -ServicePrincipalNames MSOMHSvc/ContosoLB.aquiladom.com, MSOMHSvc/ContosoLB, MSOMSdkSvc/ContosoLB.aquiladom.com, MSOMSdkSvc/ContosoLB 
```

In that command:
- `ContosogMSA` is the gMSA name. 
- `ContosoLB.aquiladom.com` is the DNS name for the load balancer (specified previously).
- `ContosoServerGroup` is the computer group in Active Directory (specified previously).
- `MSOMHSvc/ContosoLB.aquiladom.com`, `SMSOMHSvc/ContosoLB`, `MSOMSdkSvc/ContosoLB.aquiladom.com`, and `MSOMSdkSvc/ContosoLB` are service principal names.

Use the following command if the root key isn't effective:

```powershell
Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10)) 
```

Ensure that the created gMSA account is a local admin account. If there are any GPO policies on the local admins at the Active Directory level, ensure that they have the gMSA account as the local admin.

# [In the Azure portal](#tab/prereqs-portal)

## Register the SCOM Managed Instance (preview) resource provider

1. Sign in to the [Azure portal](https://portal.azure.com) and select **Subscriptions**.
2. Select the subscription where you want to deploy SCOM Managed Instance (preview).
3. Under **Settings**, select **Resource providers**.
4. Search for **SCOM** and register **Microsoft.Scom**.
5. On the **Subscription** page, under **Settings**, select **Resource providers** and search for **microsoft.insights**. If the **microsoft.insights** provider isn't registered, select the provider and then select **Register**.

    :::image type="Microsoft insights resource provider" source="media/create-operations-manager-managed-instance/resource-provider.png" alt-text="Screenshot of the Microsoft insights provider.":::

## Create a managed service identity

The managed service identity (MSI) provides an identity for applications to use when they're connecting to resources that support Azure Active Directory (Azure AD) authentication. For SCOM Managed Instance (preview), a managed identity will replace the traditional four System Center Operations Manager service accounts. It will be used to access the Azure SQL Managed Instance database. You can also use the MSI to access the key vault.

>[!Note]
>- Ensure that you're a contributor in the subscription where you create the MSI.
>- The MSI must have admin permission on Azure SQL Managed Instance and read permission on the key vault that you use for domain account credentials.

1. Sign in to the [Azure portal](https://portal.azure.com). Search for and select **Managed Identities**.

   :::image type="Managed Identity in Azure portal" source="media/create-operations-manager-managed-instance/azure-portal-managed-identity.png" alt-text="Screenshot of the icon for managed identities in the Azure portal.":::
1. On the **Managed Identities** page, select **+ Create**.

   :::image type="Managed Identity" source="media/create-operations-manager-managed-instance/managed-identities.png" alt-text="Screenshot of Managed Identity.":::

   The **Create User Assigned Managed Identity** pane opens.
1. Under **Basics**, do the following:
    - **Project details**:
        - **Subscription**: Select the Azure subscription in which you want to create the SCOM managed instance.
        - **Resource group**: Select the resource group in which you want to create the SCOM managed instance.
    - **Instance details**:
        - **Region**: Select the region in which you want to create the SCOM managed instance.
        - **Name**: Enter a name for the instance.

    :::image type="Create user assigned managed identity" source="media/create-operations-manager-managed-instance/create-user-assigned-managed-identity.png" alt-text="Screenshot of project and instance details for a user-assigned managed identity.":::
1. Select **Next : Tags >**.
1. Under **Tags**, enter the **Name** value, and then select the resource.

   Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see [Use tags to organize your Azure resources and management hierarchy](/azure/azure-resource-manager/management/tag-resources?wt.mc_id=azuremachinelearning_inproduct_portal_utilities-tags-tab&tabs=json).
1. Select **Next : Review + Create >**.
1. Under **Review + create**, review all the information that you provided, and then select **Create**.

   :::image type="Managed identity review" source="media/create-operations-manager-managed-instance/managed-identity-review.png" alt-text="Screenshot of the tab for reviewing a managed identity before creation.":::

Your deployment is now created on Azure. You can access the resource and view its details.

## Create and configure a SQL managed instance

Before you create a SCOM managed instance, create a SQL managed instance. For more information, see [Create a SQL managed instance](/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql&preserve-view=true).

We recommend the following settings for creating a SQL managed instance:

- **Resource Group**: Create a new resource group for Azure SQL Managed Instance (preview). A best practice is to create a new resource group for large Azure resources.
- **Managed Instance name**: Choose a unique name. This name will be used while you create a SCOM managed instance to refer to this SQL managed instance.
- **Region**: Choose the region close to you. There's no strict requirement on region for the instance, but we recommend the closest region for latency purposes.
- **Compute+Storage**: General Purpose (Gen5) with eight cores is the default. This configuration will suffice for the SCOM managed instance.
- **Authentication Method**: Select **SQL Authentication**. Enter the credentials that you want to use for accessing the SQL managed instance. These credentials don't refer to any that you've created so far.
- **VNet**: This SQL managed instance needs to have direct connectivity (line of sight) to the SCOM managed instance that you create in the future. Choose a virtual network that you'll eventually use for your SCOM managed instance. If you choose a different virtual network, ensure that it has connectivity to the SCOM Managed Instance (preview) virtual network.

   The subnet that you provide to Azure SQL Managed Instance has to be dedicated (delegated) to the SQL managed instance. The provided subnet can't be used to house any other resources. 

   By design, a managed instance needs a minimum of 32 IP addresses in a subnet. As a result, you can use a minimum subnet mask of /27 when defining your subnet IP ranges. For more information, see [Determine required subnet size and range for Azure SQL Managed Instance](/azure/azure-sql/managed-instance/vnet-subnet-determine-size?view=azuresql&preserve-view=true).
- **Connection Type**: By default, the connection type is **Proxy**.
- **Public Endpoint**: This setting can be either **Enabled** or **Disabled**. To use Power BI reporting, you need to enable the public endpoint.

  If the Azure SQL Managed Instance virtual network is different from the SCOM Managed Instance (preview) virtual network:

  - If you choose to enable, create an inbound NSG rule on the Azure SQL Managed Instance subnet to allow traffic from the System Center Operations Manager virtual network or subnet to port 3342. For more information, see [Configure a public endpoint in Azure SQL Managed Instance](/azure/azure-sql/managed-instance/public-endpoint-configure?view=azuresql&preserve-view=true).
  - If you choose to disable, be sure to peer your Azure SQL Managed Instance virtual network with the one in which System Center Operations Manager and SCOM Managed Instance (preview) are present.

For the rest of the settings on the other tabs, you can leave them as default or change them according to your requirements.

>[!Note]
> Creation of a new SQL managed instance can take up to six hours.

After you create a SQL managed instance, you need to provide permission to the SCOM Managed Instance (preview) resource provider to access this SQL managed instance.

To provide the permission, do the following:

1. Open the SQL managed instance and select **Access control (IAM)**. On the top menu, select **+Add** > **Add role assignment**.

   :::image type="Access control" source="media/create-operations-manager-managed-instance/access-control.png" alt-text="Screenshot that shows selections for starting the process of adding a role assignment for access control.":::
1. On the **Add role assignment** pane:
   - For **Role**, select **Reader** from the dropdown list.
   - For **Assign access to**, select **User, group, or service principal** from the dropdown list.
   - For **Select**, enter **Microsoft.SCOM Resource Provider**.

   :::image type="Add role assignment" source="media/create-operations-manager-managed-instance/add-role-assignment.png" alt-text="Screenshot of selections for adding a role assignment.":::
1. Select **Save**.

### Set the Active Directory admin value in the SQL managed instance

To set the Active Directory admin value in the SQL managed instance, use the following steps:

>[!Note]
>You must have Global Administrator or Privileged Role Administrator permissions for the subscription.

1. Open the SQL managed instance. Under **Settings**, select **Active Directory admin**.

   :::image type="Active directory admin" source="media/create-operations-manager-managed-instance/active-directory-admin.png" alt-text="Screenshot of the pane for Active Directory admin information.":::

2. Select **Set admin**, and search for your MSI. This is the same MSI that you provided during the SCOM Managed Instance (preview) creation flow. You'll find the admin added to the SQL managed instance.

   :::image type="Azure Active directory admin" source="media/create-operations-manager-managed-instance/azure-active-directory.png" alt-text="Screenshot of MSI information for Azure Active Directory.":::

3. If you get an error after you add a managed identity account, it indicates that read permissions aren't yet provided to your identity. Be sure to provide the necessary permissions before you create your instance, or your instance creation will fail.

   :::image type="SQL Active directory admin" source="media/create-operations-manager-managed-instance/sql-active-directory-admin.png" alt-text="Screenshot that shows successful Active Directory authentication.":::

For more information about permissions, see [Directory Readers role in Azure Active Directory for Azure SQL](/azure/azure-sql/database/authentication-aad-directory-readers-role?view=azuresql&preserve-view=true).

## Create a key vault and add credentials as a secret in the key vault  

For security, you can store the domain account (which you created previously in Active Directory) in a key vault.

Azure Key Vault is a cloud service that provides a secure store for keys, secrets, and certificates. For more information, see [About Azure Key Vault](/azure/key-vault/general/overview).

>[!Note]
> You must have Global Administrator or Privileged Role Administrator permissions for the tenant to do the following steps.

1. In the Azure portal, search for and select **Key vaults**.

     :::image type="Key vaults in portal" source="media/create-operations-manager-managed-instance/azure-portal-key-vaults.png" alt-text="Screenshot of the icon for key vaults in the Azure portal.":::

   The **Key vaults** page opens.

1. Select **+ Create**.

     :::image type="Key vault" source="media/create-operations-manager-managed-instance/key-vaults.png" alt-text="Screenshot of the button for creating a key vault.":::

1. For **Basics**, do the following:
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
1. For **Access Policy**, do the following:
    - **Access configuration**: Select **Vault access policy**.
    - **Resource access**: Don't select any of the options.
    - **Access policies**: Select **+ Create** to create a new access policy.

      :::image type="Access policies" source="media/create-operations-manager-managed-instance/access-policies.png" alt-text="Screenshot of the button for creating an access policy.":::

      The **Create an access policy** page opens on the right pane.

      1. For **Permissions**, under **Secret permissions**, select **Get** and **List**.

         :::image type="Create an Access policy" source="media/create-operations-manager-managed-instance/create-an-access-policy.png" alt-text="Screenshot of checkboxes for get and list permissions.":::
      1. Select **Next**.
      1. For **Principal**, select the same MSI that you used in Azure SQL Managed Instance admin configuration.

      1. For **Review + create**, review the selections, and then select **Create**.
1. Select the access policy that you created, and then select **Next**.

     :::image type="Access policy" source="media/create-operations-manager-managed-instance/access-policy.png" alt-text="Screenshot of a selected access policy.":::
1. For **Networking**, do the following:
    - Select **Enable public access**.
    - Under **Public Access**, for **Allow access from**, select **All networks**.

   :::image type="Networking tab" source="media/create-operations-manager-managed-instance/networking-inline.png" alt-text="Screenshot of selections for enabling public access on the Networking tab." lightbox="media/create-operations-manager-managed-instance/networking-expanded.png":::
1. Select **Next**.
1. For **Tags**, select the tags if required, and then select **Next**.
1. For **Review + create**, review the selections, and then select **Create** to create the key vault.
  
    :::image type="content" source="media/create-operations-manager-managed-instance/review-inline.png" alt-text="Screenshot of the tab for reviewing selections before creating a key vault." lightbox="media/create-operations-manager-managed-instance/review-expanded.png":::

1. On the left pane, under **Objects**, select **Secrets**.

    :::image type="content" source="./media/create-operations-manager-managed-instance/secrets-inline.png" alt-text="Screenshot of the pane for secrets." lightbox="./media/create-operations-manager-managed-instance/secrets-expanded.png":::

     >[!Note]
     > You must create two secrets to store the domain account credentials: 
     > - Username
     > - Password

1. Select **+ Generate/Import**.

1. On the **Create a secret** page, do the following:
    - **Upload options**: Select **Manual**.
    - **Name**: Enter the name of the secret. For example, you can use *Username* for the username secret and *Password* for the password secret.
    - **Secret value**: For the username value (in the format *domain\username*), enter the domain account username. For the password value, enter the domain account password. For example, if the domain is *contoso.com*, the username should be in the format *contoso\username*.

       :::image type="Secrets" source="media/create-operations-manager-managed-instance/create-a-secret-username.png" alt-text="Screenshot of entering a secret value for a username.":::

       :::image type="Secrets" source="media/create-operations-manager-managed-instance/create-a-secret-password.png" alt-text="Screenshot of entering a secret value for a password.":::

    - Leave the **Content type (optional)**, **Set activation date**, **Set expiration date**, **Enabled**, and **Tags** areas as default, and select **Create** to create the secret.

---

## Create a SCOM managed instance

To create a SCOM managed instance, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com). Search for and select **SCOM Managed Instance**.
1. On the **Overview** page, you have three options:
    - **Pre-requisites**: Allows you to view the prerequisites.
    - **SCOM managed instance**: Allows you to create a SCOM managed instance.
    - **Manage your SCOM managed instance**: Allows you to view the list of created instances.

    :::image type="SCOM Managed Instance (preview) overview" source="media/create-operations-manager-managed-instance/scom-mi-overview.png" alt-text="Screenshot that shows options on the overview page for SCOM Managed Instance (preview).":::

    Select **Create SCOM managed instance**.
1. The **Prerequisites to create SCOM managed instance** page opens. Download the script and run it on a domain-joined machine to validate the prerequisites.

    :::image type="Script download" source="media/create-operations-manager-managed-instance/script-download-inline.png" alt-text="Screenshot that shows the button for downloading a script." lightbox="media/create-operations-manager-managed-instance/script-download-expanded.png":::
1. Under **Basics**, do the following:
    - **Project details**:
        - **Subscription**: Select the Azure subscription in which you want to place the SCOM managed instance.
        - **Resource group**: Select the resource group in which you want to place the SCOM managed instance. If you don't have a resource group, select **Create new** to create a new resource group, and then place the instance. We recommend that you have a new resource group exclusively for SCOM Managed Instance (preview).

        :::image type="Project details" source="media/create-operations-manager-managed-instance/project-details.png" alt-text="Screenshot that shows project details for creating a SCOM managed instance.":::

    - **Instance details**:
        - **SCOM managed instance name**: Enter a name for your SCOM managed instance.
            >[!Note]
            >- The name of a SCOM managed instance can have only alphanumeric characters and be up to 10 characters.
            >- A SCOM managed instance is equivalent to a System Center Operations Manager management group, so choose a name accordingly.
        - **Region**: Select a region near to you geographically so that latency between your agents and the SCOM managed instance is as low as possible. This region must also contain the virtual network.

        :::image type="Instance details" source="media/create-operations-manager-managed-instance/instance-details.png" alt-text="Screenshot that shows instance details for creating a SCOM managed instance.":::

    - **Active directory details**:
        - **Domain name**: Enter the name of the domain that the domain controller is administering.
        - **DNS Server IP**: Enter the IP address of the DNS server that's providing the IP addresses to the resources in the domain from the previous step.
        - **OU Path**: Enter the organizational unit (OU) path to where you want to join the servers. This isn't a necessary field. If you leave it blank, it will assume the default value. Ensure that the value you enter is in the distinguished name format. For example: **OU=testOU,DC=domain,DC=Domain,DC=com**.

        :::image type="Active Directory details" source="media/create-operations-manager-managed-instance/active-directory-details.png" alt-text="Screenshot that shows Active Directory details for creating a SCOM managed instance.":::

    - **Domain account details**:
        - **Key vault**: Select the key vault that has the secret username and secret password of the domain account's user credentials.
        - **Username secret**: Enter the secret name for the user under the selected key vault.
        - **Password secret**: Enter the secret name for the password under the selected key vault.

        >[!Note]
        >Ensure that you provide the secret names created in the *selected key vault*, and not the actual domain username and password.

        :::image type="content" source="./media/create-operations-manager-managed-instance/secret-password-mapping-inline.png" alt-text="Screenshot that shows password mapping for creating a secret." lightbox="./media/create-operations-manager-managed-instance/secret-password-mapping-expanded.png":::

    - **Azure hybrid benefit**: By default, **No** is selected. Select **Yes** if you're using a Windows Server license for your existing servers. This license is applicable only for the Windows servers that will be used while you're creating virtual machine for the SCOM managed instance. It won't apply to the existing Windows servers.

        :::image type="Azure hybrid benefit" source="media/create-operations-manager-managed-instance/azure-hybrid-benefit.png" alt-text="Screenshot that shows options for Azure hybrid benefit.":::
1. Select **Next**.
1. Under **Networking**, do the following:
    - **Virtual network**:
        - **Virtual network**: Select the virtual network that has direct connectivity to the workloads that you want to monitor and to your domain controller and DNS server.
        - **Subnet**: Select a subnet that has at least 32 IP addresses to house the instance. The minimum address space is 28.

           The subnet can have existing resources in it. However, don't choose the subnet that houses the SQL managed instance because it won't contain enough IP addresses to house the SCOM Managed Instance (preview) components.

           >[!Note]
           >Ensure that you have a NAT gateway associated with the subnet that you choose.
    - **SCOM managed instance interface**:
        - **Static IP**: Enter the static IP for the load balancer. This IP should be in the selected subnet range for SCOM Managed Instance (preview).
        - **DNS name**: Enter the DNS name that you attached to the static IP from the preceding step.
    - **gMSA details**:
        - **Computer group name**: Enter the name of the computer group that you create after creation of the gMSA account.
        - **gMSA account name**: Enter the gMSA name. It must end with **$**.

        :::image type="gMSA details" source="media/create-operations-manager-managed-instance/gmsa-details.png" alt-text="Screenshot that shows gMSA details.":::
1. Select **Next**.
1. Under **Database**, do the following:
    - **SQL managed instance**: For **Resource Name**, select the Azure SQL Managed Instance resource name for the instance that you want to associate with this SCOM managed instance. Use only the SQL managed instance that has given permissions to the SCOM managed instance. For more information, see [SQL managed instance creation and permission](/system-center/scom/create-operations-manager-managed-instance?view=sc-om-2022&tabs=prereqs-portal#create-and-configure-a-sql-mi&preserve-view=true).
    - **User managed identity**: For **User managed identity account**, select the managed identity that you created and for which you provided admin permissions to the SQL managed instance. Ensure that the same MSI has read permissions on the key vault for domain account credentials.
1. Select **Next**.
1. Under **Tags**, enter the **Name, value** information, and then select the resource.
   
   Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see [Use tags to organize your Azure resources and management hierarchy](/azure/azure-resource-manager/management/tag-resources?wt.mc_id=azuremachinelearning_inproduct_portal_utilities-tags-tab&tabs=json).
1. Select **Next**.
1. Under **Review + Submit**, review all the inputs given so far, and then select **Create**. Your deployment will now be created on Azure. Creation of a SCOM managed instance takes up to an hour.

    >[!Note]
    >If the deployment fails, delete the instance and all the associated resources, and then create the instance again. For more information, see [How to delete an instance](./operations-manager-managed-instance-common-questions.md#what-is-the-procedure-to-delete-an-instance).

1. After the deployment is completed, select **Go to resource**.

   On the instance page, you can view some of the essential details and instructions for post-deployment steps and reporting bugs.

## Next steps

- [Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance (preview)](migrate-to-operations-manager-managed-instance.md)
- [Scale Azure Monitor SCOM Managed Instance (preview)](scale-scom-managed-instance.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
