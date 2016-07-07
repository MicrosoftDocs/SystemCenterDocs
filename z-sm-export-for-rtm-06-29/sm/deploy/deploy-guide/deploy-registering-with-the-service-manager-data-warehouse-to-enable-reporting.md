---
title: Registering with the Service Manager Data Warehouse to Enable Reporting
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d5795bd5-7c01-47b9-909f-8147362b9cf4
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
# Registering with the Service Manager Data Warehouse to Enable Reporting
After you have deployed the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers and data warehouse management servers, for reporting to function you must run the Data Warehouse Registration Wizard. This wizard registers the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management group with the data warehouse management group. It also deploys management packs from the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server to the data warehouse management server.  
  
 The management pack deployment process can take several hours to complete. It is a best practice not to turn off any [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] computers or stop any [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] services during this time. During this registration process, you can continue to use the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] to perform any [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] functions that you want.  
  
 To ensure that reporting data will be available, use the procedures in the following topics to register the data warehouse and deploy the management packs.  
  
## Registering with the Service Manager Data Warehouse to Enable Reporting topics  
  
-   [How to Run the Data Warehouse Registration Wizard](../../../sm/deploy/deploy-guide/How-to-Run-the-Data-Warehouse-Registration-Wizard.md)  
  
     Describes how to run the data warehouse registration wizard.  
  
-   [How to Determine When Data Warehouse Registration Is Complete](../../../sm/deploy/deploy-guide/How-to-Determine-When-Data-Warehouse-Registration-Is-Complete.md)  
  
     You have to allow enough time for the management pack deployment process to complete. This topic describes how to determine when management pack deployment is complete.