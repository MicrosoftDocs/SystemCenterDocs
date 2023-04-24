---
ms.assetid: 
title: About Arc-enabled System Center Virtual Machine Manager
description: This article provides an overview of Azure Arc-enabled System Center Virtual Machine Manager (SCVMM).
author: Farha-Bano
ms.author: v-farhabano
manager: jsuri
ms.date: 02/15/2023
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
ms.custom: intro-overview, UpdateFrequency0.5
---

# About Arc-enabled System Center Virtual Machine Manager

Azure Arc-enabled System Center Virtual Machine Manager (SCVMM) empowers System Center customers to connect their VMM environment to Azure and perform VM self-service operations from the Azure portal. With Azure Arc-enabled SCVMM, you get consistent management experience across Azure. 

Azure Arc-enabled System Center Virtual Machine Manager allows you to manage your Hybrid environment and perform self-service VM operations through Azure portal. For Microsoft Azure Pack customers, this solution is intended as an alternative to perform VM self-service operations. 

Arc-enabled System Center VMM allows you to:

- Perform various VM lifecycle operations such as start, stop, pause, and delete VMs on VMM managed VMs directly from Azure.

- Empower developers and application teams to self-serve VM operations on-demand using [Azure role-based access control (RBAC)](/azure/role-based-access-control/overview).

- Browse your VMM resources (VMs, templates, VM networks, and storage) in Azure, providing you with a single pane view for your infrastructure across both environments.

- Discover and onboard existing SCVMM managed VMs to Azure.

## Discover Arc-enabled SCVMM from SCVMM console

You can discover and learn about Arc-enabled SCVMM from the *Azure Arc* blade from within the SCVMM console.

Navigate to **Azure Arc** in **SCVMM Console** and you can do the following:
   - **Overview**: Read the overview of Arc-enabled SCVMM.
   - **Pre-requisites**: Review the prerequisites of Are-enabled SCVMM.
   - **Steps to deploy**: View steps to Arc enable SCVMM deployment.
   - **Deploy Arc Resource Bridge**: Deploy Arc resource bridge.
   - **View onboarded SCVMM in Azure**: Navigate to your SCVMM inventory page on the Azure Arc portal from the default web browser.

You need appropriate credentials on the Azure portal with the necessary permissions to onboard or use Azure Arc-enabled SCVMM.

:::image type="Arc-enabled SCVMM blade" source="media/about-arc-enabled-system-center-virtual-machine-manager/arc-enabled-system-center-virtual-machine-manager.png" alt-text="Screenshot showing Arc-enabled SCVMM blade.":::

## Next steps

- Get started with [Arc-enabled SCVMM](/azure/azure-arc/system-center-virtual-machine-manager/overview#how-does-it-work).
