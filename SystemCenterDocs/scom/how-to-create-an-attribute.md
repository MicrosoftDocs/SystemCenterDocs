---
ms.assetid: d837d304-20ff-4d2a-8071-f1c5664d93dd
title: Create an Attribute
description: This article provides information on how to use Create Attribute wizard.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Create an attribute


Use the Create Attribute Wizard to create a new attribute for a management pack. For more information, see [Attributes](/previous-versions/system-center/system-center-2012-R2/hh457609(v=sc.12)) in the Authoring Guide.

> [!WARNING]
> For every new attribute that you create, you're actually creating a new class based on the existing class, with the new class inheriting the parent class attributes as well as the new attribute. Because of this, creating new attributes can result in an increased workload in distributing configurations to agents. Create new attributes judicially and sparingly.

## Next steps

- To understand the differences between classes and groups in Operations Manage and how workflows apply to each, see [Using Classes and Groups for Overrides in Operations Manager](manage-mp-overview-override-targets.md).  

- To learn how to create a custom writeable management pack to store your overrides, see [How to Create a Management Pack for Overrides](~/scom/manage-mp-create-unsealed-mp.md).
