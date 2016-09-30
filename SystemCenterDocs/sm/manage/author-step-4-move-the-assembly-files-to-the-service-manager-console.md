---
title: Step 4: Move the Assembly Files to the Service Manager Console
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 96894b7a-6317-4de3-bc0c-7f06280b6a90
---

# Step 4: Move the Assembly Files to the Service Manager Console

>Applies To: System Center 2016 - Service Manager

In this step of the Woodgrove Bank customization scenario, in System Center - Service Manager Ken must move the workflow assembly file and the form assembly file to the Service Manager program directory to use the workflow with the Service Manager console.  

 For general information about deploying a workflow to Service Manager, see [How to Deploy a Workflow to Service Manager](author-how-to-deploy-a-workflow-to-service-manager.md).  

### To move the assembly files  

1.  In Windows Explorer, open the folder in which you saved the management pack, and copy the **AddComputerToADGroupWF.dll** and **AddComputerToGroupFormAssembly.dll** files.  

2.  Open the Service Manager installation folder \(for example, C:\\Program Files\\Microsoft System Center\\Service Manager 2016\), and paste the copied files in that folder.  
