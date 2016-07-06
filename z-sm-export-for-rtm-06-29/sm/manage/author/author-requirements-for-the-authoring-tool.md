---
title: Requirements for the Authoring Tool
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c351429b-70ff-496d-bacc-4627987f09a7
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
# Requirements for the Authoring Tool
Before you set up the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], ensure that the server on which you plan to install the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] meets all the following server and operating system requirements.  
  
## Server Requirements  
 You can install the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] on a server that hosts the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, or you can install it on a separate server.  
  
## Operating System Requirements  
  
-   Windows Vista \(any edition\) with the latest service pack  
  
-   Windows 7  
  
-   Windows Server 2008 with the latest service pack  
  
-   Windows Server 2008 R2  
  
## Additional Requirements  
  
-   [Microsoft .NET Framework 3.5](http://go.microsoft.com/fwlink/p/?LinkId=162791), which you can download from the Microsoft Download Center.  
  
-   Microsoft Visual Studio 2008 Shell, which must be in the same language as the display language of the operating system. You can install Visual Studio 2008 Shell from the **Prerequisites** page in the Service Manager Authoring Tool Setup Wizard.  
  
    > [!NOTE]  
    >  During Authoring Tool Setup, if an error appears stating that Microsoft Visual Studio Shell 2008 is not installed and you’ve verified that it is installed, then the Visual Studio 2008 Shell Isolated Mode Redistributable Package might not be installed completely. To install it, navigate to \<SystemDrive\>\\VS 2008 Shell Redist\\Isolated Mode\\ and run VS\_Shell\_isolated.enu.exe.  
  
## See Also  
 [Overview of the Authoring Tool for System Center 2012 – Service Manager](../Topic/Overview%20of%20the%20Authoring%20Tool%20for%20System%20Center%202012%20%E2%80%93%20Service%20Manager.md)