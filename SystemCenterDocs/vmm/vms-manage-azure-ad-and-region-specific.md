---
ms.assetid: d4b3e835-cd9b-4993-bfe0-e491f5f18508
title:  Manage arm-based and region-specific VMs using System Center VMM preview 1711.
description: This article provides information about how to manage arm-based and region-specific VMs using VMM 1711.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: riyazp
ms.date: 11/08/2017
ms.topic: article
ms.prod:  system-center-2016
ms.technology: virtual-machine-manager
monikerRange: 'sc-vmm-1711'
---

# Manage VMs using Azure AD-based authentication & authorization and region-specific Azure subscriptions (Technical Preview)

This article provides information about how to manage the ARM-based and region-specific Azure subscriptions using System Center Virtual Machine Manager Preview 1711 (VMM 1711).

You can add Microsoft Azure subscriptions to System Center 2016 - Virtual Machine Manager (VMM) and later and perform required actions. [Learn more](azure-subscription.md). Currently, the VMM Azure plugin  allows management of Azure subscriptions through certificate-based authentication and authorization, and VMs in public Azure region.

VMM 1711 supports management of Azure subscriptions through azure active directory and region-specific Azure subscriptions. (namely, Germany, China, US Government Azure regions).

Management of Azure subscriptions through certificate-based authentication and authorization requires Management certificate. [Learn More](https://docs.microsoft.com/en-us/azure/azure-api-management-certs).

Management of  VMs using Azure AD based authentication and authorization requires Azure AD application.


## Before you start

Ensure the following prerequisites:

- **Azure AD application** - to manage VMs by using VMM through AD authentication and authorization, you need to create an Azure AD application, and then provide the following details through VMM Azure plugin:

    -	Azure Subscription ID
    -   Azure Active Directory ID
    - 	Azure Active Directory - Application ID & Application Key

 [Learn more]((https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) on how to create an Azure AD App.  

- **A management certificate** - with the configuration as described in [this article](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-add-azure-subscription).

    - The subscription must have a management certificate associated with it so that VMM can use the service management API in Azure.
    - Make note of the subscription ID and the certificate thumbprint.
    - Certificates must be x509 v3 compliant.
    - The management certificate must be located in the local certificate store on the computer on which you add the Azure subscription feature.  
    - The certificate should also be located in the Current User\Personal store of the computer running the VMM console.

	> [!NOTE]

    > The certificate is required only if you choose to use certificate-based authentication to manage your Azure subscription.

## Procedure to manage

**Use the following steps**:

1.	Browse to **Azure subscription** and click **Add Subscription**.
![add subscription](media\azure-arm-based\add-subscription.png)

2. Provide **Display Name**, **Azure cloud** and **Subscription ID**.

    You can provide any friendly name as display name. Choose either public Azure or region-specific subscription as appropriate.

    ![add subscription id](media\azure-arm-based\add-subscription-id.png)

3. Select **Management using Azure AD authentication** (to use certificate based management, go to step 5)

    ![select authentication](media\azure-arm-based\azure-ad-authentication.png)

4. Provide **Directory ID**, **Application ID** and **Key**, and then click **Finish** (after this step, directly go to step 6).
![ad authentication details](media\azure-arm-based\management-using-ad.png)

5. To use management certificate, select **Management using management certificate**.  (not required if already performed step 3 and 4)

    If you want to continue using certificate based authentication, then instead of selecting Azure AD authentication choose management certificate based authentication and provide the management certificate from “Current User\Personal” certificate store and then click **Finish**.

    ![select authentication](media\azure-arm-based\management-using-certificate.png)

6. Verify the Azure subscription and the VMs hosted on Azure.
![verify subscription authentication](media\azure-arm-based\verify-azure-subscription.png)


## [Next steps]

- [Create Certificates](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [Create active directory](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)
