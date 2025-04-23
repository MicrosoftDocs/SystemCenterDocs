---
title: Bundle Management Packs and Resource Files
description: Learn about bundling management packs and resource files for Service Manager authoring.
ms.custom: engagement-fy24, UpdateFrequency3
ms.service: system-center
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/23/2025
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9cb6eaf-d744-4f91-b1d4-3294812953df
---

# Bundle management packs and resource files

In this article, you'll learn about bundling management packs and resource files for Service Manager authoring.

A custom management pack might include references to resources, such as an image or a form assembly. To import such a management pack into Service Manager, you must first bundle the management pack file and its associated resources into a single .mpb management pack file.  

In Service Manager, to bundle a management pack file with its resources, use the Windows&nbsp;PowerShell cmdlet **New\-SCSMManagementPackBundle**. For more information about this cmdlet, see [New\-SCSMManagementPackBundle](/previous-versions/system-center/powershell/system-center-2012-r2/hh316263(v=sc.20)).  

When you bundle a management pack, any form .dll in the bundle is stored in the Service Manager database along with any other resources, such as images. The form is then automatically deployed to any Service Manager console computer that needs to render that form. When the form is loaded for the first time in the Service Manager console, it's retrieved from the Service Manager database and cached on the local computer. In subsequent uses, the form is retrieved from the local cache.  

To customize management packs that are bundled in an .mpb file, you must first unbundle the .mpb file and then individually customize each management pack and resource file. For more information about how to unbundle an .mpb management pack file, see [How to Unbundle a Bundled Management Pack](unbundle-mps.md).  

## Next steps

[Unbundle a bundled management pack for use with the Authoring Tool](unbundle-mps.md).
