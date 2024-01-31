---
ms.assetid: d837d304-20ff-4d2a-8071-f1c5664d93dd
title: Create an Attribute
description: This article provides information on how to use Create Attribute wizard.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 11/28/2023
ms.custom: UpdateFrequency3
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# How to create an attribute

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

Use the Create Attribute Wizard to create a new attribute for a management pack. For more information, see [Attributes](/previous-versions/system-center/system-center-2012-R2/hh457609(v=sc.12)) in the Authoring Guide.

> [!WARNING]
> For every new attribute that you create, you're actually creating a new class based on the existing class, with the new class inheriting the parent class attributes as well as the new attribute. Because of this, creating new attributes can result in an increased workload in distributing configurations to agents. Create new attributes judicially and sparingly.

## Next steps

- To understand the differences between classes and groups in Operations Manage and how workflows apply to each, see [Using Classes and Groups for Overrides in Operations Manager](manage-mp-overview-override-targets.md).  

- To learn how to create a custom writeable management pack to store your overrides, see [How to Create a Management Pack for Overrides](~/scom/manage-mp-create-unsealed-mp.md).
