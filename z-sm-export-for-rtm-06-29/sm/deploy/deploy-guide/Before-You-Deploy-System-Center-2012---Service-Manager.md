---
title: Before You Deploy System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a7bfe29-aa96-434f-b17f-a07990ca5549
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
# Before You Deploy System Center 2012 - Service Manager
Before you start the deployment process, prepare your environment for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], as described in the [Planning Guide for Service Manager for System Center 2012](http://go.microsoft.com/fwlink/p/?LinkID=209672). The Planning Guide contains information about the various parts of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], the hardware and software requirements, the port assignments, and the information about the accounts you must use to deploy [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. The Planning Guide also contains information about the accounts that you need to create for use with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
 In addition, you have to install the Authorization Manager hotfix and the Microsoft Report Viewer Redistributable security update before you start [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] deployment.  
  
## Install the Authorization Manager Hotfix \(KB975332\)  
 If the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, data warehouse management server, or the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] lose connection to the SQL Server databases—even briefly—the connection is not automatically re\-established. The Windows team recently released a hotfix to address this issue. It is extremely import that this hotfix be installed on your computers that host a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, data warehouse management server, or the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)]. For more information, see [How to Download and Install the Authorization Manager Hotfix](../../../sm/deploy/deploy-guide/How-to-Download-and-Install-the-Authorization-Manager-Hotfix.md).  
  
> [!NOTE]  
>  The Authorization Manager hotfix was included with Windows Server 2008 R2 with Service Pack 1 \(SP1\). If you are installing [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] on a computer running Windows Server 2008 R2 with SP1, you already have the Authorization Manager hotfix installed.  
  
## Install the Microsoft Report Viewer Redistributable Security Update \(KB971119\)  
 During installation of a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server or [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], the prerequisite checker checks to see whether the security update for Microsoft Report Viewer 2008 Service Pack 1 Redistributable Package has been installed. If you have not installed this security update, you will have the opportunity to do so during the installation. As an alternative, you can deploy this security hotfix before starting the installation of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. For more information, see [How to Install the Microsoft Report Viewer Redistributable Security Update](../../../sm/deploy/deploy-guide/How-to-Install-the-Microsoft-Report-Viewer-Redistributable-Security-Update.md).  
  
## Before you deploy topics  
  
-   [How to Download and Install the Authorization Manager Hotfix](../../../sm/deploy/deploy-guide/How-to-Download-and-Install-the-Authorization-Manager-Hotfix.md)  
  
     Describes how to download and install the Authorization Manager hotfix.  
  
-   [How to Install the Microsoft Report Viewer Redistributable Security Update](../../../sm/deploy/deploy-guide/How-to-Install-the-Microsoft-Report-Viewer-Redistributable-Security-Update.md)  
  
     Describes how to install the Microsoft Report Viewer Redistributable Security Update.