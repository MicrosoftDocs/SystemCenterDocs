---
title: Create Incident Activity
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4f476a8-1567-4414-861e-b51f6c9e4148


















---
# Create Incident Activity
This activity creates and populates an incident in System Center 2012 - Service Manager.  
  
## Design\-Time Prerequisites  
 None.  
  
## Run\-Time Prerequisites  
 None.  
  
## Properties  
 The **Create Incident** activity uses the input properties that are listed in the following table.  
  
|Display name|Internal name|Type|Required|Comments|  
|------------------|-------------------|----------|--------------|--------------|  
|Incident ID|IncidentID|String|Yes|Specifies the unique identifier who is generated for the **Incident** object.|  
|Action Log Comment|ActionLogComment|String|Yes|Specifies the comment to include in the **Incident** object's action log.|  
|Affected User Domain|AffectedUserDomain|String|Yes|Specifies the name of the Domain Name System \(DNS\) domain of the primary user who is affected by the incident.|  
|Affected User Name|AffectedUserName|String|Yes|Specifies the user name of the primary user who is affected by the incident.|  
|Category|Category|Integer|Yes|Specifies the type of incident, such as "Networking" or "Printing." The value is the ID of **enum**. \(Category -**enum** data field\)|  
|Continue On  Error|ContinueOnError|Boolean|No. \(The default setting is true.\)|Determines whether the workflow should continue running if the activity fails.|  
|Impact|Impact|Integer|Yes|Specifies the impact of the incident on the affected user or users. The value is the ID of **enum**. \(Impact \-**enum** data type\)|  
|Source|Source|Integer|No|Specifies the source of information about the incident, such as "Phone" or "E\-mail". The value is the ID of **enum**. \(Source -**enum** data type field\)|  
|Summary|Summary|String|Yes|Specifies the summary text that describes the incident.|  
|Urgency|Urgency|Integer|Yes|Specifies the urgency of resolving the incident. The value is the ID of **enum**. \(Urgency -**enum** data type field\)|  
  
 The **Create Incident** activity generates the output that is described in the following table.  
  
|Name|Type|Comments|  
|----------|----------|--------------|  
|SM Incident|System.WorkItem.Incident|Returns the constructed incident class instance.|  
  
## Errors and Exceptions  
 None.  
  
## Remarks  
 None.  
  
## Example  
 None.  
  
## See Also  
 [DeleteService Manager Activities &#91;SM2012\_AuthoringGuide&#93;](assetId:///c338d0ef-503c-40ac-be6b-3b0a1a2edebf)
