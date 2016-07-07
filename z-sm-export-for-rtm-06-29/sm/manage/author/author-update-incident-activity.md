---
title: Update Incident Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cc0aa4e-ac8e-4693-a2ad-859ef8481075
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
# Update Incident Activity
This activity in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] saves property changes to one [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] incident.  
  
## Design\-Time Prerequisites  
 None.  
  
## Run\-Time Prerequisites  
 None.  
  
## Properties  
 The **Update Incident** activity uses the input properties that are described in the following table.  
  
|Display name|Internal name|Type|Required|Description|  
|------------------|-------------------|----------|--------------|-----------------|  
|Action Log Comment|ActionLogComment|String|No|Specifies a comment to include in the Incident object’s action log.|  
|Affected User Domain|AffectedUserDomain|String|No|Specifies the name of the Domain Name System \(DNS\) domain of the primary user who is affected by the incident.|  
|Affected User Name|AffectedUserName|String|No|Specifies the user name of the primary user who is affected by the incident.|  
|Category|Category|Integer|No|Specifies the type of incident, such as "Networking" or "Printing." The value is the ID of **enum**. \(Category –**enum** data type\)|  
|Continue On Error|ContinueOnError|Boolean|No. \(The default setting is true.\)|Determines whether the workflow should continue running if the activity fails.|  
|Impact|Impact|Integer|No|Specifies the impact of the incident on the affected user or users. The value is the ID of **enum**. \(Impact \-**enum** data type\)|  
|Source|Source|Integer|No|Specifies the source of information about the incident, such as "Phone" or "E\-mail." The value is the ID of **enum**. \(Source –**enum** data type\)|  
|Service Manager Incident|SMIncident|System.Workitem.Incident|No|The constructed incident class instance to be updated.|  
|Status|Status|Integer|No|Specifies the status of the incident that generated the activity. The value is the ID of **enum**. \(Status –**enum** data type\)|  
|Summary|Summary|String|No|Specifies the summary text that describes the incident.|  
|Urgency|Urgency|Integer|No|Specifies the urgency of resolving the incident. The value is the ID of **enum**. \(Urgency –**enum** data type field\)|  
  
 The **Update Incident** activity generates the output that is described in the following table.  
  
|Display name|Internal name|Type|Description|  
|------------------|-------------------|----------|-----------------|  
|SM Incident|SMIncident|System.WorkItem.Incident|Returns an update of the incident class instance. The input **SM Incident** and the output **SM Incident**are equal unless the activity failed to find the **SM Incident**. In that case, the output **SM Incident** is set to Null.|  
  
## Errors and Exceptions  
 None.  
  
## Remarks  
 None.  
  
## Example  
 None.  
  
## See Also  
 [DeleteService Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///c338d0ef-503c-40ac-be6b-3b0a1a2edebf)