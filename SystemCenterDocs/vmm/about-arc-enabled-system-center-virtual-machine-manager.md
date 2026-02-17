---
ms.assetid: 
title: About Arc-enabled System Center Virtual Machine Manager
description: This article provides an overview of Azure Arc-enabled System Center Virtual Machine Manager (SCVMM).
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/20/2025
ms.topic: concept-article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.update-cycle: 365-days
ms.custom: intro-overview, UpdateFrequency0.5, engagement-fy24
---

# About Arc-enabled System Center Virtual Machine Manager

Azure Arc-enabled System Center Virtual Machine Manager (SCVMM) empowers System Center customers to connect their VMM environment to Azure and perform VM self-service operations from Azure portal. Azure Arc-enabled SCVMM extends the Azure control plane to SCVMM-managed infrastructure, enabling the use of Azure security, governance, and management capabilities consistently across System Center-managed estate and Azure.

Azure Arc-enabled System Center Virtual Machine Manager also allows you to manage your hybrid environment consistently and perform self-service VM operations through Azure portal. For Windows Azure Pack customers, this solution is intended as an alternative to perform VM self-service operations.

Arc-enabled System Center Virtual Machine Manager allows you to:

- Perform various VM lifecycle operations such as start, stop, pause, and delete VMs on SCVMM-managed VMs directly from Azure.
- Empower developers and application teams to self-serve VM operations on demand using [Azure role-based access control (RBAC)](/azure/role-based-access-control/overview).
- Browse your VMM resources (VMs, templates, VM networks, and storage) in Azure, providing you with a single pane view for your infrastructure across both environments.
- Discover and onboard existing SCVMM-managed VMs to Azure.
- Install the Azure connected machine agents at scale on SCVMM VMs to [govern, protect, configure, and monitor](/azure/azure-arc/servers/overview#supported-cloud-operations) them.
- Procure Extended Security Updates (ESUs) for the WS 2012 and 2012 R2 VMs managed by SCVMM.
- Build automation and self-service pipelines using Python, Java, JavaScript, Go, and .NET SDKs; Terraform, ARM, and Bicep templates; Azure REST APIs, CLI, and PowerShell.

## Discover Arc-enabled SCVMM from SCVMM console

You can discover and learn about Arc-enabled SCVMM from the **Azure Arc** blade in the SCVMM console.

Navigate to **Azure Arc** in the administrator **SCVMM Console** and do the following:

   - **Overview**: Read the overview of Arc-enabled SCVMM.
   - **Pre-requisites**: Review the prerequisites of Arc-enabled SCVMM.
   - **Steps to deploy**: View steps to Arc-enable your SCVMM-managed estate.
   - **Install Arc agents at scale**: View steps to install Azure Connected Machine agents at scale to your SCVMM VMs from Azure.
   - **Azure Management Services**: Learn about the popular Azure management services to govern, protect, configure, and monitor your SCVMM VMs through Azure Arc.
   - **Deploy Arc Resource Bridge**: Deploy Arc resource bridge.
   - **View onboarded SCVMM in Azure**: Navigate to your SCVMM inventory page on the Azure Arc portal from the default web browser.

You need appropriate credentials on the Azure portal with the necessary permissions to onboard or use Azure Arc-enabled SCVMM.

:::image type="Arc-enabled SCVMM blade" source="media/about-arc-enabled-system-center-virtual-machine-manager/arc-enabled-system-center-virtual-machine-manager.png" alt-text="Screenshot showing Arc-enabled SCVMM blade." lightbox="media/about-arc-enabled-system-center-virtual-machine-manager/arc-enabled-system-center-virtual-machine-manager.png":::

## Next steps

Get started with [Arc-enabled SCVMM](/azure/azure-arc/system-center-virtual-machine-manager/overview#how-does-it-work).
