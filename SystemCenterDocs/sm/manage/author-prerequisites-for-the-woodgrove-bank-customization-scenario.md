---
title: Prerequisites for the Woodgrove Bank customization scenario
description: Describes prerequisites for the Woodgrove Bank customization scenario for the Service Manager Authoring Tool.
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
ms.assetid: 944ee559-992b-4232-9fb9-f93b82323edb
---

# Prerequisites for the Woodgrove Bank customization scenario for the Service Manager Authoring Tool

>Applies To: System Center 2016 - Service Manager

The Woodgrove Bank customization scenario has the following prerequisites:  

-   System Center 2016 - Service Manager must be installed in your environment.  

-   The System Center 2016 - Service Manager Authoring Tool must be installed in your environment.  

-   The Workflow Account in Service Manager must be a member of the Domain Administrators group because this scenario involves creating a workflow that adds a computer to a group in Active&nbsp;Directory Domain Services \(AD&nbsp;DS\). You specify the Workflow Account in the Service Manager Server Setup Wizard.  

 The Authoring Tool's installation folder includes a **Samples** subfolder that contains the following files, which are required for the Woodgrove Bank customization scenario.  

|File|Description|  
|----------|-----------------|  
|Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml|A management pack that contains class definitions that are used in the Woodgrove Bank customization sample scenario.|  
|AddComputerToGroupFormAssembly.dll|The implementation of an automated activity form that is used in the Woodgrove Bank customization sample scenario.|  
|Woodgrovebank.jpg|An image that is used for form customization in the Woodgrove Bank customization sample scenario.|  
|New\-mpbfile.ps1|A Windows PowerShell script that is used to bundle a management pack with its associated resource files into an .mpb file that can then be imported into Service Manager. Resource files can include items such as images and forms.|  
