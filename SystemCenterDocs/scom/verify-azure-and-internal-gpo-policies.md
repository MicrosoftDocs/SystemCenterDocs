---
ms.assetid: 
title: Verify Azure and internal GPO policies
description: This article describes how to verify Azure and internal GPO policies.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 08/23/2023
ms.custom: UpdateFrequency.5
ms.prod: system-center
ms.technology: operations-manager-managed-instance
ms.topic: article
monikerRange: '>=sc-om-2019'
---

# Verify Azure and internal GPO policies

This article describes how to verify Azure and internal GPO policies.

>[!Note]
> To know about the SCOM Managed Instance (preview) Architecture, see [Azure Monitor SCOM Managed Instance (preview)](operations-manager-managed-instance-overview.md).

## Verify Azure policies

If there exist any Azure policies that are aimed at constraining the creation of managed resource groups, virtual machine scale sets, load balancers, managed identities, and metric alerts, make an exception for the subscription that is associated with the SCOM Managed Instance. This exception is necessary as the SCOM Managed Instance creates all these resources within the managed resource group.

Follow these steps to view the policies applied on subscription:
1. Go to specific subscription, on the Subscription left hand menu, select the policies.
2. In the policies page, select the policy assignments and find the policy, which is causing the issue.
3. Open the specific assignment and select exemption.

:::image type="create exemption" source="media/verify-azure-and-internal-gpo-policies/create-exemption.png" alt-text="Screenshot of create exemption.":::

## Verify internal GPO policies

As SCOM Managed Instances become part of the designated domain or Organizational Unit (OU), any Group Policy Object (GPO) policies come into play at the OU or domain level, impacting the local administrators group; Consider the exclusion of the SCOM Managed Instance from those GPO policies.

Following are certain policies that could potentially influence the local administrator groups. However, customized policies might also be in effect.

   - Review any GPO policies that might alter the configuration of the local administrator group.
   - Examine whether there are any GPO policies intended to deactivate network authentication.
   - Assess whether any policies are obstructing remote logins to the local administrator group.

>[!Important]
>To minimize the need for extensive communication with both your Active Directory admin and Network Admin, review  [**Self-verification**](/system-center/scom/scom-mi-self-verification-of-steps?view=sc-om-2022). The outlines the procedures through which the AD admin and network admin validate their configuration changes and ensure their successful implementation; thus, reducing unnecessary back-and-forth interactions from Operations Manager admin to AD Admin and network admin. This saves time of AD admin, Network admin and System Center Operaions Manager admin.

## Next steps

- [SCOM Managed Instance self-verification of steps](scom-mi-self-verification-of-steps.md)

To provide feedback on SCOM Managed Instance (preview), use [this online form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR8_G7TnWWL9AgnUEG-odf9BUNkhBQ0s4NUIxVTY5UjBSUzhENUZVNlNVUS4u).
