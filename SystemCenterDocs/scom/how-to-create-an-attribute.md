---
ms.assetid: d837d304-20ff-4d2a-8071-f1c5664d93dd
title: How to Create an Attribute
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/07/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to create an attribute

>Applies To: System Center 2016 - Operations Manager

Use the Create Attribute Wizard to create a new attribute for a management pack. For more information, see [Attributes](https://technet.microsoft.com/library/hh457609.aspx) in the Authoring Guide.

> [!WARNING]
> For every new attribute that you create, you are actually creating a new class based on the existing class, with the new class inheriting the parent class attributes as well as the new attribute. Because of this, creating new attributes can result in an increased workload in distributing configurations to agents. Create new attributes judicially and sparingly.

## Next steps

- To understand the differences between classes and groups in Operations Manage and how workflows apply to each, review [Using Classes and Groups for Overrides in Operations Manager](manage-mp-overview-override-targets.md).  

- To learn how to create a custom writeable management pack to store your overrides, see [How to Create a Management Pack for Overrides](~/scom/manage-mp-create-unsealed-mp.md).  
