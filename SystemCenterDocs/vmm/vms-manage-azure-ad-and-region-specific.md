---
ms.assetid: d4b3e835-cd9b-4993-bfe0-e491f5f18508
title: Manage Azure Resource Manager-based and region-specific VMs using System Center VMM.
description: This article provides information about how to manage VMs with Azure Resource Manager-based and region-specific Azure subscriptions, using VMM.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/28/2023
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
monikerRange: '>= sc-vmm-1801 <= sc-vmm-1807'
ms.custom: UpdateFrequency2, engagement-fy23
---

# Manage VMs using Azure AD-based authentication & authorization and region-specific Azure subscriptions

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end


This article provides information about how to manage the Azure Resource Manager-based and region-specific Azure subscriptions using System Center - Virtual Machine Manager (VMM).

You can add Microsoft Azure subscriptions to System Center 2016 - Virtual Machine Manager (VMM) and later, and perform the required actions. [Learn more](azure-subscription.md). The VMM Azure plugin allows the management of Azure subscriptions through certificate-based authentication and authorization and VMs in public Azure region.

VMM 1801 and later supports management of Azure subscriptions through Azure active directory and region-specific Azure subscriptions. (namely, Germany, China, US Government Azure regions).

Management of Azure subscriptions through certificate-based authentication and authorization requires Management certificate. [Learn More](/azure/azure-api-management-certs).

Management of VMs using Azure AD-based authentication and authorization requires Azure AD application.


## Before you start

Ensure the following prerequisites:

- **Azure AD application** - to manage VMs by using VMM through AD authentication and authorization, you need to create an Azure AD application and then provide the following details through VMM Azure plugin:

    -	Azure Subscription ID
    -   Azure Active Directory ID
    - 	Azure Active Directory - Application ID & Application Key

  [Learn more](/azure/azure-resource-manager/resource-group-create-service-principal-portal) on how to create an Azure AD App.  

- **A management certificate** - with the configuration as described in [this article](./azure-subscription.md).

  - The subscription must have a management certificate associated with it so that VMM can use the service management API in Azure.
  - Make note of the subscription ID and the certificate thumbprint.
  - Certificates must be x509 v3 compliant.
  - The management certificate must be located in the local certificate store on the computer on which you add the Azure subscription feature.  
  - The certificate should also be located in the Current User\Personal store of the computer running the VMM console.

	> [!NOTE]
    > The certificate is required only if you choose to use certificate-based authentication to manage your Azure subscription.

## Procedure - manage Azure AD-based authentication & authorization and region-specific Azure subscriptions

**Use the following steps**:

1.	Browse to **Azure subscription** and select **Add Subscription**.
![Screenshot of add subscription.](media/azure-arm-based/add-subscription.png)

2. Provide **Display Name**, **Azure cloud**, and **Subscription ID**.

    You can provide any friendly name as display name. Choose either public Azure or region-specific subscription as appropriate.

    ![Screenshot of add subscription id.](media/azure-arm-based/add-subscription-id.png)

3. Select **Management using Azure AD authentication** (to use certificate based management, go to step 5).

    ![Screenshot of select authentication.](media/azure-arm-based/azure-ad-authentication.png)

4. Provide **Directory ID**, **Application ID**, and **Key**, and select **Finish** (after this step, directly go to step 6).
![Screenshot of ad authentication details.](media/azure-arm-based/management-using-ad.png)

5. To use management certificate, select **Management using management certificate** (not required if already performed step 3 and 4).

    If you want to continue using certificate-based authentication, then instead of selecting Azure AD authentication, choose management certificate based authentication and provide the management certificate from **Current User\Personal** certificate store and select **Finish**.

    ![Screenshot of select management certificate.](media/azure-arm-based/management-using-certificate.png)

6. Verify the Azure subscription and the VMs hosted on Azure.
![Screenshot of verify subscription authentication.](media/azure-arm-based/verify-azure-subscription.png)


## Next steps

- [Create certificates](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates).
- [Create active directory](/azure/azure-resource-manager/resource-group-create-service-principal-portal).
