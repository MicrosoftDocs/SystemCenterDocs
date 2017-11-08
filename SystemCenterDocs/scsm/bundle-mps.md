---
title: Bundle management packs and resource files
description: Learn about bundling management packs and resource files for Service Manager authoring.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9cb6eaf-d744-4f91-b1d4-3294812953df
---

# Bundle management packs and resource files

A custom management pack might include references to resources, such as an image or a form assembly. To import such a management pack into Service Manager, you must first bundle the management pack file and its associated resources into a single .mpb management pack file.  

 In Service Manager, to bundle a management pack file with its resources, use the Windows&nbsp;PowerShell cmdlet **New\-SCSMManagementPackBundle**. For more information about this cmdlet, see [New\-SCSMManagementPackBundle](https://go.microsoft.com/fwlink/p/?LinkID=225397).  

 When you bundle a management pack, any form .dll in the bundle is stored in the Service Manager database, along with any other resources, such as images. The form is then automatically deployed to any Service Manager console computer that needs to render that form. When the form is loaded for the first time in the Service Manager console, it is retrieved from the Service Manager database and cached on the local computer. In subsequent uses, the form is retrieved from the local cache.  

 To customize management packs that are bundled in an .mpb file, you must first unbundle the .mpb file and then individually customize each management pack and resource file. For more information about how to unbundle an .mpb management pack file, see [How to Unbundle a Bundled Management Pack](unbundle-mps.md).  

## Next steps

- [Unbundle a bundled management pack for use with the Authoring Tool](unbundle-mps.md).
