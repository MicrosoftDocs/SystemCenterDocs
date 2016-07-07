---
title: Step 4: Move the Assembly Files to the Service Manager Console
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 96894b7a-6317-4de3-bc0c-7f06280b6a90
translation.priority.mt: 
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
# Step 4: Move the Assembly Files to the Service Manager Console
In this step of the Woodgrove Bank customization scenario, in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] Ken must move the workflow assembly file and the form assembly file to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] program directory to use the workflow with the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
 For general information about deploying a workflow to [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], see [How to Deploy a Workflow to Service Manager](../../../sm/manage/author/How-to-Deploy-a-Workflow-to-Service-Manager.md).  
  
### To move the assembly files  
  
1.  In Windows Explorer, open the folder in which you saved the management pack, and copy the **AddComputerToADGroupWF.dll** and **AddComputerToGroupFormAssembly.dll** files.  
  
2.  Open the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation folder \(for example, C:\\Program Files\\Microsoft System Center\\Service Manager 2012\), and paste the copied files in that folder.  
  
## See Also  
 [Sample Scenario: The Woodgrove Bank Customization](../Topic/Sample%20Scenario:%20The%20Woodgrove%20Bank%20Customization.md)