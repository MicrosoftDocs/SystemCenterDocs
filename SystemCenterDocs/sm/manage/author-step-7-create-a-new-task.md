---
title: Step 7 - Create a New Task
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
ms.assetid: 648500e3-5142-45a8-ae33-c07daff2347a
---

# Step 7 - Create a New Task

>Applies To: System Center 2016 - Service Manager

When Ken works with a compliance change request, he needs to easily access the Active Directory Users and Computers administrative tool.  

 In this step of the Woodgrove Bank customization scenario, to make it easy to access the tool, Ken creates a new task, **Start Active Directory Users and Computers**. He saves this task to the **Woodgrove Automated Activity - Add Computer To Group** management pack. He can later use the new task to start the tool.  

 The following procedure provides only the high\-level steps for creating a new task in the Service Manager console. For the complete procedure for creating a new task, see [How to Create a Task](admin-using-service-manager-tasks-to-troubleshoot-computer-problems.md).  

### To create a new task  

1.  In the Service Manager console, specify the task name: **Start Active Directory Users and Computers**.  

2.  Specify the target class: **Change Request**.  

3.  Specify the management pack in which to save this customization: **Service Manager Change Management Configuration Library**.  

4.  Specify the display category for the task: **Change Management Folder Tasks**.  

5.  Specify the command: **%systemroot%\\system32\\mmc.exe**.  

6.  Clear the **Show output when this task is run** check box.  
