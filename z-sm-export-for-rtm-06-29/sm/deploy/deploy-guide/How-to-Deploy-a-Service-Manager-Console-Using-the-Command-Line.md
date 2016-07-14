---
title: How to Deploy a Service Manager Console Using the Command Line
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 53cf5f5f-f10d-42e6-8164-af8c0961a1e5
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
# How to Deploy a Service Manager Console Using the Command Line
Use the following command\-line procedure to deploy the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
### To deploy the Service Manager console  
  
1.  Log on to the computer where you want to install the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] using administrative credentials.  
  
2.  Open a command window.  
  
3.  At the command prompt, change directories to the location of the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation media, and then type the following:  
  
    ```  
    Start /Wait   
    Setup.exe   
    /Install:Console   
    /AcceptEula:[YES/NO]  
    /RegisteredOwner:[owner name]   
    /RegisteredOrganization:[company name]   
    /ProductKey:[25-character product key]   
    /Installpath:[drive name]\Program Files\Microsoft System Center\Service Manager 2012   
    /CustomerExperienceImprovementProgram:[YES/NO]   
    /EnableErrorReporting:[YES/NO]  
  
    /Silent  
    ```  
  
## See Also  
 [Deploying Service Manager from a Command Line](assetId:///a918e488-349d-4955-b401-52f09e78bb9e)