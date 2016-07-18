---
title: Set Activity Status to Completed Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1df179e-8d1c-4478-9811-8f52652d6135
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
# Set Activity Status to Completed Activity
This activity updates the status of an  automated activity in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
## Design\-Time Prerequisites  
 None.  
  
## Run\-Time Prerequisites  
 None.  
  
## Properties  
 The **Set Activity Status to Completed** activity uses the input properties that are described in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Activity ID|ActivityID|String|Yes|Specifies the identifier of a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] automated activity object.|  
  
## Errors and Exceptions  
 None.  
  
## Remarks  
 When you are using this activity in a workflow that is triggered by a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] automated activity, enter **$Data\/BaseManagedEntityId$** as the value of this property. This value applies to the **Set Activity Status to Completed** activity at the automated activity that triggered the workflow to run.  
  
## Example  
 None.  
  
## See Also  
 [DeleteService Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///c338d0ef-503c-40ac-be6b-3b0a1a2edebf)