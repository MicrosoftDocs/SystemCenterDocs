---
title: Prerequisites for the Woodgrove Bank Customization Scenario
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 944ee559-992b-4232-9fb9-f93b82323edb
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
# Prerequisites for the Woodgrove Bank Customization Scenario
The Woodgrove Bank customization scenario has the following prerequisites:  
  
-   [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] must be installed in your environment.  
  
-   The [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)] must be installed in your environment.  
  
-   The Workflow Account in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] must be a member of the Domain Administrators group because this scenario involves creating a workflow that adds a computer to a group in Active Directory Domain Services \(AD DS\). You specify the Workflow Account in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Server Setup Wizard.  
  
 The [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)]’s installation folder includes a **Samples** subfolder that contains the following files, which are required for the Woodgrove Bank customization scenario.  
  
|File|Description|  
|----------|-----------------|  
|Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml|A management pack that contains class definitions that are used in the Woodgrove Bank customization sample scenario.|  
|AddComputerToGroupFormAssembly.dll|The implementation of an automated activity form that is used in the Woodgrove Bank customization sample scenario.|  
|Woodgrovebank.jpg|An image that is used for form customization in the Woodgrove Bank customization sample scenario.|  
|New\-mpbfile.ps1|A Windows PowerShell script that is used to bundle a management pack with its associated resource files into an .mpb file that can then be imported into [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. Resource files can include items such as images and forms.|  
  
## See Also  
 [Sample Scenario: The Woodgrove Bank Customization](../Topic/Sample%20Scenario:%20The%20Woodgrove%20Bank%20Customization.md)