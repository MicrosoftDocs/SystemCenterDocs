---
ms.assetid: 
title: Verify Azure and internal GPO policies for Azure Monitor SCOM Managed Instance (preview)
description: This article describes how to verify Azure and internal GPO policies.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/01/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Verify Azure and internal GPO policies for Azure Monitor SCOM Managed Instance (preview)

This article describes how to verify Azure and internal Group Policy Object (GPO) policies.

> [!NOTE]
> To learn about the Azure Monitor SCOM Managed Instance (preview) architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

## Verify Azure policies

If any Azure policies are aimed at constraining the creation of managed resource groups, virtual machine scale sets, load balancers, managed identities, and metric alerts, make an exception for the subscription that's associated with the instance of Azure Monitor SCOM Managed Instance (preview). This exception is necessary because the SCOM managed instance creates all these resources within the managed resource group.

Follow these steps to view the policies that are applied on a subscription:

1. Go to the specific subscription, and on the left menu under **Subscription**, select the policies.
1. On the **Policies** page, select the policy assignments and find the policy that's causing the issue.
1. Open the specific assignment and select the exemption.

   :::image type="create exemption" source="media/verify-azure-and-internal-gpo-policies/create-exemption.png" alt-text="Screenshot that shows the Create exemption page.":::

## Verify internal GPO policies

As SCOM managed instances become part of the designated domain or organizational unit (OU), any GPO policies come into play at the OU or domain level and affect the local administrators group. Consider the exclusion of the SCOM managed instance from those GPO policies.

The following policies could potentially influence the local administrator groups. Customized policies might also be in effect.

   - Review any GPO policies that might alter the configuration of the local administrator group.
   - Examine whether there are any GPO policies intended to deactivate network authentication.
   - Assess whether any policies are obstructing remote logins to the local administrator group.

> [!IMPORTANT]
> To minimize the need for extensive communication with both your Active Directory admin and network admin, see [Self-verification](scom-managed-instance-self-verification-of-steps.md). The article outlines the procedures that the Active Directory admin and network admin use to validate their configuration changes and ensure their successful implementation. This process reduces unnecessary back-and-forth interactions from the Operations Manager admin to the Active Directory admin and the network admin. This configuration saves time for the admins.

## Next steps

- [SCOM Managed Instance self-verification of steps](scom-managed-instance-self-verification-of-steps.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
