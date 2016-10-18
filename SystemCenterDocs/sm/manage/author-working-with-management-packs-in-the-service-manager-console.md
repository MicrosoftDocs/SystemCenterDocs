---
title: Working with Management Packs in the Service Manager Console
manager: cfreeman
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
ms.assetid: 6bf81515-8883-471e-b1df-62c30ad9ae9e
---

# Working with Management Packs in the Service Manager Console

>Applies To: System Center 2016 - Service Manager

When you make customizations in the Service Manager console, you save them in a management pack file. Sometimes, you have to first create a new management pack file. Later, to implement the customizations of the management pack, you import it into the Service Manager console.  

 When you create a management pack in the Service Manager console, you provide the display name for the management pack. Service Manager generates a random ID that is used as the internal name for the management pack and that becomes the management pack's file name. If you need to further customize objects in that management pack by directly modifying its XML code, it might be difficult to locate the management pack file that you want to edit. In that case, we recommend that you modify the management pack internal file name to be a meaningful name, and use it as follows:  

-   Edit the management pack XML file itself; change the internal management pack name to the new name.  

-   Rename the management pack file on the hard drive to the new name.  
