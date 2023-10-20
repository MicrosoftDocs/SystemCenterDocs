---
ms.assetid: 
title: Tutorial - Create an instance of Azure Monitor SCOM Managed Instance
description: This article describes how to create an Azure Monitor SCOM managed instance to monitor workloads by using System Center Operations Manager functionality on Azure.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 10/20/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Tutorial: Create an instance of Azure Monitor SCOM Managed Instance

Azure Monitor SCOM Managed Instance provides System Center Operations Manager functionality in Azure. It helps you monitor all your workloads, whether they're on-premises, in Azure, or in any other cloud services.

This tutorial describes how to create an instance of the service (a SCOM managed instance) with System Center Operations Manager functionality in Azure.

For more information about deploying SCOM Managed Instance, play the following video.

> [!VIDEO https://www.youtube.com/embed/urxiQBkObkU]

>[!NOTE]
>You can create an instance only in the **West Europe** and **West US** regions.

## Prerequisites

Before you create a SCOM managed instance, follow these steps:

- [Step 1. Register the SCOM Managed Instance resource provider](register-scom-managed-instance-resource-provider.md).
- [Step 2. Create separate subnet in a VNet](create-separate-subnet-in-vnet.md).
- [Step 3. Create a SQL Managed Instance](create-sql-managed-instance.md).
- [Step 4. Create a Key vault](create-key-vault.md).
- [Step 5. Create a user assigned identity](create-user-assigned-identity.md).
- [Step 6. Create a computer group and gMSA account](create-gmsa-account.md).
- [Step 7. Store domain credentials in Key vault](store-domain-credentials-in-key-vault.md).
- [Step 8. Create a static IP](create-static-ip.md).
- [Step 9. Configure the network firewall](configure-network-firewall.md).
- [Step 10. Verify Azure and internal GPO policies](verify-azure-and-internal-gpo-policies.md).
- [Step 11. SCOM Managed Instance self-verification of steps](scom-managed-instance-self-verification-of-steps.md).

## Create a SCOM managed instance

To create a SCOM managed instance, follow these steps:

1. Sign in to the [Azure portal](https://portal.azure.com). Search for and select **SCOM Managed Instance**.
1. On the **Overview** page, you have three options:
    - **Pre-requisites**: Allows you to view the prerequisites.
    - **SCOM managed instance**: Allows you to create a SCOM managed instance.
    - **Manage your SCOM managed instance**: Allows you to view the list of created instances.

    :::image type="SCOM Managed Instance overview" source="media/create-operations-manager-managed-instance/scom-managed-instance-overview-inline.png" alt-text="Screenshot that shows options on the Overview page for SCOM Managed Instance." lightbox="media/create-operations-manager-managed-instance/scom-managed-instance-overview-expanded.png":::

    Select **Create SCOM managed instance**.
1. The **Prerequisites to create SCOM managed instance** page opens. Download the script and run it on a domain-joined machine to validate the prerequisites.

    :::image type="Script download" source="media/create-operations-manager-managed-instance/script-download-inline.png" alt-text="Screenshot that shows the button for downloading a script." lightbox="media/create-operations-manager-managed-instance/script-download-expanded.png":::
1. Under **Basics**, do the following:
    - **Project details**:
        - **Subscription**: Select the Azure subscription in which you want to place the SCOM managed instance.
        - **Resource group**: Select the resource group in which you want to place the SCOM managed instance. We recommend that you have a new resource group exclusively for SCOM Managed Instance.

        :::image type="Project details" source="media/create-operations-manager-managed-instance/project-details-inline.png" alt-text="Screenshot that shows project details for creating a SCOM managed instance." lightbox="media/create-operations-manager-managed-instance/project-details-expanded.png":::

    - **Instance details**:
        - **SCOM managed instance name**: Enter a name for your SCOM managed instance.
            >[!NOTE]
            >- The name of a SCOM managed instance can have only alphanumeric characters and be up to 10 characters.
            >- A SCOM managed instance is equivalent to a System Center Operations Manager management group, so choose a name accordingly.
        - **Region**: Select a region near to you geographically so that latency between your agents and the SCOM managed instance is as low as possible. This region must also contain the virtual network.

        :::image type="Instance details" source="media/create-operations-manager-managed-instance/instance-details-inline.png" alt-text="Screenshot that shows instance details for creating a SCOM managed instance." lightbox="media/create-operations-manager-managed-instance/instance-details-expanded.png":::

    - **Active directory details**:
        - **Domain name**: Enter the name of the domain that the domain controller is administering.
        - **DNS server IP**: Enter the IP address of the Domain Name System (DNS) server that's providing the IP addresses to the resources in the domain from the previous step.
        - **OU Path**: Enter the organizational unit (OU) path to where you want to join the servers. This field isn't a necessary. If you leave it blank, it assumes the default value. Ensure that the value you enter is in the distinguished name format. For example: **OU=testOU,DC=domain,DC=Domain,DC=com**.

        :::image type="Active Directory details" source="media/create-operations-manager-managed-instance/active-directory-details-inline.png" alt-text="Screenshot that shows Active Directory details for creating a SCOM managed instance." lightbox="media/create-operations-manager-managed-instance/active-directory-details-expanded.png":::

    - **Domain account details**:
        - **Security key vault**: Select the key vault that has the secret username and secret password of the domain account's user credentials.
        - **Username secret**: Enter the secret name for the user under the selected key vault.
        - **Password secret**: Enter the secret name for the password under the selected key vault.

        >[!NOTE]
        >Ensure that you provide the secret names created in the *selected key vault* and not the actual domain username and password.

        :::image type="content" source="./media/create-operations-manager-managed-instance/secret-password-mapping-inline.png" alt-text="Screenshot that shows password mapping for creating a secret." lightbox="./media/create-operations-manager-managed-instance/secret-password-mapping-expanded.png":::

    - **Azure hybrid benefit**: By default, **No** is selected. Select **Yes** if you're using a Windows Server license for your existing servers. This license is applicable only for the Windows servers that are used while you create a virtual machine for the SCOM managed instance. It won't apply to the existing Windows servers.

        :::image type="Azure hybrid benefit" source="media/create-operations-manager-managed-instance/azure-hybrid-benefit.png" alt-text="Screenshot that shows options for Azure hybrid benefit.":::
1. Select **Next**.
1. Under **Networking**, do the following:
    - **Virtual network**:
        - **Virtual network**: Select the virtual network that has direct connectivity to the workloads that you want to monitor and to your domain controller and DNS server.
        - **Subnet**: Select a subnet that has at least 32 IP addresses to house the instance. The minimum address space is 28.

           The subnet can have existing resources in it. However, don't choose the subnet that houses the SQL managed instance because it won't contain enough IP addresses to house the SCOM Managed Instance components.

           >[!NOTE]
           >Make sure to associate a NAT gateway with a chosen subnet. The presence of a NAT gateway is necessary for SCOM Managed Instance to retrieve the components required for both installation and auto upgrade scenarios.
    - **SCOM managed instance interface**:
        - **Static IP**: Enter the static IP for the load balancer. This IP should be in the selected subnet range for SCOM Managed Instance. Ensure that the IP is in the IPv4 format, and create it in your routing table.
        - **DNS name**: Enter the DNS name that you attached to the static IP from the preceding step. The DNS name is mapped to the static IP that's previously defined.
    - **gMSA details**:
        - **Computer group name**: Enter the name of the computer group that you create after creation of the group managed service account (gMSA) account.
        - **gMSA account name**: Enter the gMSA name. It must end with **$**.

        :::image type="gMSA details" source="media/create-operations-manager-managed-instance/gmsa-details.png" alt-text="Screenshot that shows gMSA details.":::
1. Select **Next**.
1. Under **Database**, do the following:
    - **SQL managed instance**: For **Resource Name**, select the Azure SQL Managed Instance resource name for the instance that you want to associate with this SCOM managed instance. Use only the SQL managed instance that has given permissions to the SCOM managed instance. For more information, see [SQL managed instance creation and permission](/system-center/scom/create-operations-manager-managed-instance?view=sc-om-2022&tabs=prereqs-portal#create-and-configure-a-sql-mi&preserve-view=true).
    - **User managed identity**: For **User managed identity account**, provide a user managed identity with system admin privileges on the SQL managed instance and **Get** and **List** permissions on key vault secrets that were selected on the **Basics** tab. Ensure that the same MSI has read permissions on the key vault for domain account credentials.
1. Select **Next**.
1. Under **Validate**, all the prerequisites are validated. It takes 10 minutes to finish the validation.

     :::image type="Validate tab" source="media/create-operations-manager-managed-instance/validate-inline.png" alt-text="Screenshot that shows the Validate tab." lightbox="media/create-operations-manager-managed-instance/validate-expanded.png":::

     After the validation is finished, check the results and revalidate if needed.

     :::image type="Validation complete" source="media/create-operations-manager-managed-instance/validation-complete-inline.png" alt-text="Screenshot that shows Validation status: Completed." lightbox="media/create-operations-manager-managed-instance/validation-complete-expanded.png":::

1. Select **Next: Tags**.
1. Under **Tags**, enter the **Name** and **Value** information, and then select the resource.

   Tags help you categorize resources and view consolidated billing by applying the same tags to multiple resources and resource groups. For more information, see [Use tags to organize your Azure resources and management hierarchy](/azure/azure-resource-manager/management/tag-resources?wt.mc_id=azuremachinelearning_inproduct_portal_utilities-tags-tab&tabs=json).
1. Select **Next**.
1. Under **Review + create**, review all the inputs given so far, and then select **Create**. Your deployment is created on Azure. Creation of a SCOM managed instance takes up to an hour.

    >[!NOTE]
    >If the deployment fails, delete the instance and all the associated resources, and then create the instance again. For more information, see [Delete an instance](./operations-manager-managed-instance-common-questions.md#what-is-the-procedure-to-delete-an-instance).

1. After the deployment is finished, select **Go to resource**.

   On the instance page, you can view some of the essential details and instructions for post-deployment steps and reporting bugs.

## Next steps

- [Troubleshoot commonly encountered errors while validating input parameters](troubleshooting-input-parameters-scom-managed-instance.md)
- [Troubleshoot issues with Azure Monitor SCOM Managed Instance](troubleshoot-scom-managed-instance.md)
- [Azure Monitor SCOM Managed Instance frequently asked questions](operations-manager-managed-instance-common-questions.md)

To provide feedback on SCOM Managed Instance, use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
