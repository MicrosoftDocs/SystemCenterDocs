---
title: Guidelines and Best Practices for Authoring Forms in the Authoring Tool
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
ms.assetid: 9140312b-4d0b-4f22-a466-85887485e066
---

# Guidelines and Best Practices for Authoring Forms in the Authoring Tool

>Applies To: System Center 2016 - Service Manager

Use the following guidelines when you are authoring forms in the Service Manager Authoring Tool. For more information about how Windows Presentation Foundation \(WPF\) forms work and WPF customization guidelines, see [Windows Presentation Foundation](http://go.microsoft.com/fwlink/p/?LinkID=194437) on MSDN.  

-   When you are customizing existing default forms by adding new controls, first create a new **Tab** control, and then add the new controls to the new **Tab** control.  

-   Store all customizations of a particular form in a single management pack.  

-   Group related controls in a **Panel** control so that you can better handle them as a group.  

-   You can drop controls only in containers, such as the **Panel** container control.  

-   Set one or more of the following control properties to **Auto** to allow for dynamic adjustment of placement: **Height**, **Width**, **Minimum Height**, **Minimum Width**, **Left**, **Top**, **Right**, and **Bottom**. Depending on the resulting behavior, adjust these settings.  
