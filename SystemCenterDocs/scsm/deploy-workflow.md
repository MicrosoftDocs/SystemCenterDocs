---
title: Deploy a workflow to Service Manager
description: Describes how to deploy a workflow to Service Manager using the Service Manager Authoring Tool.
ms.custom: intro-deployment, UpdateFrequency3, engagement-fy23, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: install-set-up-deploy
ms.assetid: 68e697fe-9f0b-4813-bdce-c59cc4019ff3
---

# Deploy a workflow to Service Manager using the Service Manager Authoring Tool



Use these procedures to move workflows from the Service Manager Authoring Tool to the Service Manager console. First, you must physically move the workflow assembly file and the management pack file that contains the workflow information. Then, you must import the management pack into Service Manager.  

## Move the management pack and workflow files  

1. On the computer that is running the Authoring Tool, browse to the folder where you saved the management pack, and then copy the management pack and workflow files. The workflow file is automatically created in the same folder as the management pack. For example, copy **AddComputerToADGroupMP.xml** and **AddComputerToADGroupWF.dll**.  

2. On the computer that is running the Service Manager console, browse to the Service Manager installation folder, for example, C:\Program Files\Microsoft System Center\Service Manager.  

3. Paste the copied management pack and workflow files into this folder. For example, paste **AddComputerToADGroupMP.xml** and **AddComputerToADGroupWF.dll**.  

    > [!NOTE]  
    > You can move the management pack file to a different folder before you import it into the Service Manager console. However, you must place the workflow assembly file in the Service Manager installation folder.  

## Import the management pack into Service Manager  

1. In the Service Manager console, select **Administration**.  

2. In the **Administration** pane, expand **Administration**, and select **Management Packs**.  

3. In the **Tasks** pane, under **Management Packs**, select **Import Management Pack**.  

4. In the **Select Management Packs to Import** dialog, select the management pack file that is associated with the workflow, and select **Open**. For example, select **AddComputerToADGroupMP.xml**.  

5. In the **Import Management Packs** dialog, select **Add** to add the management pack that you want to import.  

6. Select **Import**, and select **OK**.  

## Next steps

[Configure the Activities Toolbox in the Authoring Tool](config-activities-toolbox.md).
