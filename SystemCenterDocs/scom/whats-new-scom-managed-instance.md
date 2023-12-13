---
ms.assetid: 
title: What’s new in Azure Monitor SCOM Managed Instance
description: This article provides details of what's new in each version of Azure Monitor SCOM Managed Instance.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 12/13/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: whats-new
monikerRange: '>=sc-om-2019'
---

# What’s new in Azure Monitor SCOM Managed Instance 

This article provides details of what's new in each version of Azure Monitor SCOM Managed Instance.

## Version 1.0.95

Enhance onboarding/pre-patching/pre-scaling validations to check the connectivity to required endpoints as described in [firewall requirements](configure-network-firewall.md#firewall-requirements).

## Version 1.0.94 

- Installation bug fix for domain joined machines.

- Fixed issue in scale down operation where incorrect management server was being assigned as RMS.

- Enhanced system resiliency by executing the SCOM managed gateway onboard and offboard commands exclusively on the present RMS.

- Bug fix in scale management server script to handle right reallocation of agents.

## Version 1.0.91

- **Implemented pre-patching validations**: Conducted essential checks before initiating the patching operation, ensuring optimal conditions for existing management servers, verifying SQL connectivity, confirming active directory accessibility, and validating the accuracy of domain account credentials.

- Bug fix to handle the concurrency in extension installation.

## Version 1.0.89

- The Log Analytics workspace feature is available for existing and new SCOM Managed Instances.

## Version 1.0.88

- Bug fixes for onboarding validation.

- Fixed issue where Static IP and LB association check fails with error **The property `IP4Address` cannot be found on this object**.

## Version 1.0.87

- Bug fixes for onboarding validation.

- Fixed issue where Domain Connectivity check fails with error **The property `TcpTestSucceeded` cannot be found on this object**.

## Version 1.0.86

- Introduced [Resource Health feature](/azure/service-health/resource-health-overview?WT.mc_id=Portal-Microsoft_Azure_Health) for SCOM Managed Instance.

- Introduced Log Analytics Integration feature for SCOM Managed Instance.

## Version 1.0.85

- Improved performance of extension for onboarding, scaling, and patching operations.

## Next steps

[Migrate from Operations Manager on-premises to Azure Monitor SCOM Managed Instance](migrate-to-operations-manager-managed-instance.md)