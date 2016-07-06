---
title: How to Deploy a Workflow to Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68e697fe-9f0b-4813-bdce-c59cc4019ff3
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Deploy a Workflow to Service Manager
Use these procedures to move workflows from the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)] to the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]. First, you must physically move the workflow assembly file and the management pack file that contains the workflow information. Then, you must import the management pack into [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
### To move the management pack and workflow files  
  
1.  On the computer that is running the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], browse to the folder where you saved the management pack, and then copy the management pack and workflow files. The workflow file is automatically created in the same folder as the management pack. For example, copy **AddComputerToADGroupMP.xml** and **AddComputerToADGroupWF.dll**.  
  
2.  On the computer that is running the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], browse to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation folder, for example, C:\\Program Files\\Microsoft System Center\\Service Manager 2012.  
  
3.  Paste the copied management pack and workflow files into this folder. For example, paste **AddComputerToADGroupMP.xml** and **AddComputerToADGroupWF.dll**.  
  
    > [!NOTE]  
    >  You can move the management pack file to a different folder before you import it into the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]. However, you must place the workflow assembly file in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation folder.  
  
### To import the management pack into [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Administration**.  
  
2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.  
  
3.  In the **Tasks** pane, under **Management Packs**, click **Import Management Pack**.  
  
4.  In the **Select Management Packs to Import** dialog box, select the management pack file that is associated with the workflow, and then click **Open**. For example, select **AddComputerToADGroupMP.xml**.  
  
5.  In the **Import Management Packs** dialog box, click **Add** to add the management pack that you want to import.  
  
6.  Click **Import**, and then click **OK**.  
  
## See Also  
 [Workflows and Management Packs](../../../sm/manage/author/Workflows-and-Management-Packs.md)   
 [Workflows: Customizing and Authoring](../Topic/Workflows:%20Customizing%20and%20Authoring.md)