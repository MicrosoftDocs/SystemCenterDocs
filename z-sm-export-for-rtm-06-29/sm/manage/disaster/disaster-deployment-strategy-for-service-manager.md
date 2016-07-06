---
title: Deployment Strategy for Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: debd28f1-c449-4190-99e2-81a4e731b97d
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
# Deployment Strategy for Service Manager
As a best practice, deploy your management servers and associated databases for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] on separate computers. Isolating the management servers and databases provides for a successful disaster recovery operation in the event of potential software and equipment failures.  
  
 You must have a functioning database to restore a failed management server. Recovery of a management server is impossible if the management server and the associated database are on the same physical computer and that computer fails. For more information, see "Installing Service Manager on Four Computers" in the [Deployment Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=209670).