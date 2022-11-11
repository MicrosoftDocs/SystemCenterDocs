---
ms.assetid: 
title: About Arc-enabled System Center Virtual Machine Manager
description: This article provides an overview of Azure Arc-enabled System Center Virtual Machine Manager (SCVMM).
author: v-pgaddala
ms.author: v-pgaddala
manager: jsuri
ms.date: 11/11/2022
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
ms.custom: intro-overview
---

# About Arc-enabled System Center Virtual Machine Manager

Azure Arc-enabled System Center Virtual Machine Manager (SCVMM) empowers System Center customers to connect their VMM environment to Azure and perform VM self-service operations from Azure portal. With Azure Arc-enabled SCVMM, you get consistent management experience across Azure. 

Azure Arc-enabled System Center Virtual Machine Manager allows you to manage your Hybrid environment and perform self-service VM operations through Azure portal. For Microsoft Azure Pack customers, this solution is intended as an alternative to perform VM self-service operations. 

Arc-enabled System Center VMM allows you to: 

- Perform various VM lifecycle operations such as start, stop, pause, delete VMs on VMM managed VMs directly from Azure. 

- Empower developers and application teams to self-serve VM operations on-demand using [Azure role-based access control (RBAC)](/azure/role-based-access-control/overview).

- Browse your VMM resources (VMs, templates, VM networks, and storage) in Azure, providing you with a single pane view for your infrastructure across both environments. 

- Discover and onboard existing SCVMM managed VMs to Azure. 

## Discover Arc-enabled SCVMM from SCVMM console

You can discover and learn about Arc-enabled SCVMM from the *Azure Arc* blade from within the SCVMM console as shown below: 

:::image type="Arc-enabled SCVMM blade" source="media/about-arc-enabled-system-center-virtual-machine-manager/arc-enabled-scvmm.png" alt-text="Screenshot showing Arc-enabled SCVMM blade.":::

This discovery page provides guidance around prerequisites and steps to Arc-enable the SCVMM deployment and navigation to the Azure Portal to get started. 

You can also navigate to your SCVMM inventory page on the Azure Arc portal from within the Azure Arc blade. 

You can use the buttons to navigate to the Azure Arc Portal from the default web browser. You need appropriate credentials on the Azure Portal with the necessary permissions to onboard or use Azure Arc-enabled SCVMM. 

## Next steps

- Get started with [Arc-enabled SCVMM](/azure/azure-arc/system-center-virtual-machine-manager/overview#how-does-it-work).   