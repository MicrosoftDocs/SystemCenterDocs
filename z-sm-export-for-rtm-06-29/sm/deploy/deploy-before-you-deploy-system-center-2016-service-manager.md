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
---

# Before You Deploy System Center 2012 - Service Manager

Before you start the deployment process, prepare your environment for System Center 2012 - Service Manager, as described in the [Planning Guide for Service Manager for System Center 2012](http://go.microsoft.com/fwlink/p/?LinkID=209672). The Planning Guide contains information about the various parts of Service Manager, the hardware and software requirements, the port assignments, and the information about the accounts you must use to deploy Service Manager. The Planning Guide also contains information about the accounts that you need to create for use with Service Manager.  

 In addition, you have to install the Authorization Manager hotfix and the Microsoft Report Viewer Redistributable security update before you start Service Manager deployment.  

## Install the Authorization Manager Hotfix \(KB975332\)  
 If the Service Manager management server, data warehouse management server, or the Self-Service Portal lose connection to the SQL&nbsp;Server databases-even briefly-the connection is not automatically re\-established. The Windows team recently released a hotfix to address this issue. It is extremely import that this hotfix be installed on your computers that host a Service Manager management server, data warehouse management server, or the Self-Service Portal. For more information, see [How to Download and Install the Authorization Manager Hotfix](../../../sm/deploy/deploy-guide/How-to-Download-and-Install-the-Authorization-Manager-Hotfix.md).  

> [!NOTE]  
>  The Authorization Manager hotfix was included with Windows&nbsp;Server&nbsp;2008&nbsp;R2 with Service Pack&nbsp;1 \(SP1\). If you are installing Service Manager on a computer running Windows&nbsp;Server&nbsp;2008&nbsp;R2 with SP1, you already have the Authorization Manager hotfix installed.  

## Install the Microsoft Report Viewer Redistributable Security Update \(KB971119\)  
 During installation of a Service Manager management server or Service Manager console, the prerequisite checker checks to see whether the security update for Microsoft Report Viewer&nbsp;2008 Service Pack&nbsp;1 Redistributable Package has been installed. If you have not installed this security update, you will have the opportunity to do so during the installation. As an alternative, you can deploy this security hotfix before starting the installation of Service Manager. For more information, see [How to Install the Microsoft Report Viewer Redistributable Security Update](../../../sm/deploy/deploy-guide/How-to-Install-the-Microsoft-Report-Viewer-Redistributable-Security-Update.md).  

## Before you deploy topics  

-   [How to Download and Install the Authorization Manager Hotfix](../../../sm/deploy/deploy-guide/How-to-Download-and-Install-the-Authorization-Manager-Hotfix.md)  

     Describes how to download and install the Authorization Manager hotfix.  

-   [How to Install the Microsoft Report Viewer Redistributable Security Update](../../../sm/deploy/deploy-guide/How-to-Install-the-Microsoft-Report-Viewer-Redistributable-Security-Update.md)  

     Describes how to install the Microsoft Report Viewer Redistributable Security Update.
