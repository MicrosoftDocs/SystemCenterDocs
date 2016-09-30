---
title: How to Deploy a Workflow to Service Manager
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
ms.assetid: 68e697fe-9f0b-4813-bdce-c59cc4019ff3
---

# How to Deploy a Workflow to Service Manager

>Applies To: System Center 2016 - Service Manager

Use these procedures to move workflows from the Service Manager Authoring Tool to the Service Manager console. First, you must physically move the workflow assembly file and the management pack file that contains the workflow information. Then, you must import the management pack into Service Manager.  

### To move the management pack and workflow files  

1.  On the computer that is running the Authoring Tool, browse to the folder where you saved the management pack, and then copy the management pack and workflow files. The workflow file is automatically created in the same folder as the management pack. For example, copy **AddComputerToADGroupMP.xml** and **AddComputerToADGroupWF.dll**.  

2.  On the computer that is running the Service Manager console, browse to the Service Manager installation folder, for example, C:\\Program Files\\Microsoft System Center\\Service Manager 2016.  

3.  Paste the copied management pack and workflow files into this folder. For example, paste **AddComputerToADGroupMP.xml** and **AddComputerToADGroupWF.dll**.  

    > [!NOTE]  
    >  You can move the management pack file to a different folder before you import it into the Service Manager console. However, you must place the workflow assembly file in the Service Manager installation folder.  

### To import the management pack into Service Manager  

1.  In the Service Manager console, click **Administration**.  

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.  

3.  In the **Tasks** pane, under **Management Packs**, click **Import Management Pack**.  

4.  In the **Select Management Packs to Import** dialog box, select the management pack file that is associated with the workflow, and then click **Open**. For example, select **AddComputerToADGroupMP.xml**.  

5.  In the **Import Management Packs** dialog box, click **Add** to add the management pack that you want to import.  

6.  Click **Import**, and then click **OK**.  
