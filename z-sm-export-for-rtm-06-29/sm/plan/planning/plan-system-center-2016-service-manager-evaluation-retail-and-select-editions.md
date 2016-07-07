---
title: System Center 2012 - Service Manager Evaluation, Retail, and Select Editions
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23d3104b-5733-42f2-8a92-be48b5924533
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
# System Center 2012 - Service Manager Evaluation, Retail, and Select Editions
[!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] is available as both a retail edition and a select edition. Both editions offer the same functionality. The retail edition is purchased separately, and it includes a product key that you enter during setup. The select edition is delivered as part of a Microsoft Volume Licensing plan, and a product key is not required.  
  
 During setup of the retail edition of [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you have the option of performing the installation without a product key and instead installing [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] as an evaluation edition. The evaluation edition times out 180 days after installation. If you start with an evaluation version of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and you rerun Setup and install the retail edition or select edition, and you decide to use the existing databases that you created originally, your installation will time out after the original expiration date.  
  
 The following table describes the interactions between the various editions of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
|If you started with …|And then rerun Setup to install …|Will the new installation time out?|  
|---------------------------|---------------------------------------|-----------------------------------------|  
|Evaluation Edition|Retail Edition|Yes|  
|Evaluation Edition|Select Edition|Yes|  
|Retail Edition|Evaluation Edition|No|  
|Retail Edition|Select Edition|No|  
|Select Edition|Retail Edition|No|