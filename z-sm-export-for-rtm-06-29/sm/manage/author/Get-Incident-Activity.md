---
title: Get Incident Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c300cd0-9338-4d70-9669-bddfda60133b
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
# Get Incident Activity
This activity retrieves one or more  incidents in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
## Design\-Time Prerequisites  
 None.  
  
## Run\-Time Prerequisites  
 None.  
  
## Properties  
 The **Get Incident** activity uses the input properties that are listed in the following table.  
  
|Display name|Internal name|Type|Required|Comments|  
|------------------|-------------------|----------|--------------|--------------|  
|Affected User Domain|AffectedUserDomain|String|No|Specifies the name of the Domain Name System \(DNS\) domain of the primary user who is affected by the incident.|  
|Affected User Name|AffectedUserName|String|No|Specifies the user name of the primary user who is affected by the incident.|  
|Category|Category|Integer|No|Specifies the type of incident, such as "Networking" or "Printing." The value is the ID of **enum**. \(Category –**enum** data field\)|  
|Continue On Error|ContinueOnError|Boolean|No. \(The default is true.\)|Determines whether the workflow should continue running if the activity fails.|  
|Incident ID|IncidentID|String|No|Specifies the unique identifier that is generated for the incident object.|  
|Search Type|SearchType|Integer?|No|Specifies the title of the search type that is used with the activity.|  
|Status|Status|Integer|No|Specifies the status of incident. The value is the ID of **enum**. \(Status –**enum** data field\)|  
|Summary Text|SummaryText|String|No|Specifies the summary text that describes the incident.|  
  
 The **Get Incident** activity generates the output that is described in the following table.  
  
|Display name|Internal name|Type|Comments|  
|------------------|-------------------|----------|--------------|  
|SM Incidents|SMIncidents|Array of System.Workitem.Incident|Specifies an array of incident objects.|  
  
## Errors and Exceptions  
 None.  
  
## Remarks  
 The **Get Incident** activity has its own validator to perform error validation on input properties.  
  
## Example  
 None.  
  
## See Also  
 [DeleteService Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///c338d0ef-503c-40ac-be6b-3b0a1a2edebf)