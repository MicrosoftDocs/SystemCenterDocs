---
ms.assetid: 6805c8cf-d768-4680-9990-2b8c895f31ec
title: Add an Azure subscription in VMM
description: This article describes how to add an Azure subscription, so that you can manage basic actions for Azure instances
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Add an Azure subscription in VMM


You can add Microsoft Azure subscriptions to System Center - Virtual Machine Manager (VMM), and perform basic actions on Azure instances in the subscriptions.

- For each Azure subscription you add, you can use a console to see all role instances in all Deployment Groups in that subscription.
- If you already manage your on-premises virtual machines in VMM, you can use this feature to perform some very basic actions on Azure instances without leaving the VMM console. You can:
    - Add and remove Azure subscriptions in the VMM console.
    - Get a list view of information about role instances in deployment subscriptions. Instances can be manually refreshed. 
    - Perform basic actions on the instances, including start, stop, shutdown, and restart.
    - Connect via RDP
- This feature isn't designed to provide feature parity with the Azure portal. It provides a small subset of the features to simplify management. You can't manage the Azure subscription, deploy instances, manage Azure storage and networks, migrate on-premises VMs to Azure, or view the dashboard and performance monitoring summaries.
- Certificates and subscription setting information is stored in the registry under HKEY_CURRENT_USER. The information is log in-specific, and visible on a per-machine, per-login basis. If you log into VMM with a shared account (not recommended), any subscription added under that shared account will be exposed to all users.
- Because information is log in-specific, Azure subscriptions added by one admin user aren't automatically visible to all other VMM admins. You need to set up the subscription for each VMM admin that needs to access it.


## Before you start
Here's what you need to add an Azure subscription in VMM:

**Requirement**| **Details**
--- | ---
**Azure subscription** | You need at least one Azure subscription to add it to the VMM console.
**Internet connectivity** | The computer on which you install the feature must be able to connect to the Azure subscription.
**Service administrator** | You need to be at least a service administrator for the subscription. You need this for access to the management certificate information that's required.
**Management certificate** | The subscription must have a management certificate associated with it. so that VMM can use the service management API in Azure. [Learn more](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-certs-create/) about service certificates. Make note of the subscription ID and the certificate thumbprint.<br/><br/> Certificates must be x509 v3 compliant.<br/>br/> The management certificate must be located in the local certificate store on the computer on which you add the Azure subscription feature.<br/><br/> The certificate should also be located in the **Current User \ Personal** store of the computer running the VMM console.

## Set up the Add Azure Subscription feature

1. Make sure you've complied with requirements in the previous section, and ensure that the option to add a subscription appears in the VMM console > **VMs and Services** > **Azure** > **Add Subscription**.
2. If you want to check for a certificate, log into the Azure portal with your account, and click **Settings** > **Management Certificates**. Note the certificate thumbprint if you've haven't already.
3. In the VMM console, click **VMs and Services** > **Azure** > **Add Subscription**, and fill in the subscription details. In the Subscriptions node you can add and remove subscriptions, and refresh VM lists. You can also start, stop, shut down, and restart a VM, and connect to it over RDP.
