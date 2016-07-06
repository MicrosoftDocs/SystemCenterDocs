---
title: Managing Incidents Overview
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f8c2122-df9b-4903-ba19-caf01fd81990
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
# Managing Incidents Overview
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], help desk analysts use incident management to restore regular operations as quickly and as cost\-effectively as possible.  
  
 Using the E\-mail Incident template to populate a new email\-related incident, you can quickly create an incident and ensure that the correct **Impact**, **Urgency**, **Assigned Analyst**, and **Support Tier** fields are configured.  
  
 If you configure connectors so that [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] imports configuration items and alerts from [!INCLUDE[om12short](../../../sm/deploy/upgrade/includes/om12short_md.md)], some new incidents are automatically created. An analyst reviews the automatically created incidents for accuracy.  
  
 In [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], incidents are automatically created from email requests by users. If the user is recognized as a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] end user, the request that is sent to the help desk email address automatically creates a new incident.  
  
> [!NOTE]  
>  [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] can automatically generate new incidents from email requests only after a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] administrator enables inbound email processing. By default, the impact and urgency of every incident created by email submission is set to medium, and no category is assigned.  
  
 Normally, you create incidents only for user accounts in your organization that have Active Directory Domain Services \(AD DS\) accounts that are synchronized with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. However, you might occasionally need to manually create incidents for users. For example, you might need to create an incident for a new user whose account is not yet in AD DS or if an Active Directory account is not yet synchronized with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. You can also manually create incidents to support external vendors who do not have Active Directory accounts. In another example, you might need to open an incident for an on\-site technician who does not have an Active Directory account but who needs to report an incident. Or, you might need to open an incident for an externally\-supported customer who does not have an Active Directory account. In all these examples, you must manually create a user in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. [!INCLUDE[crdefault](../../../sm/manage/author/includes/crdefault_md.md)] “How to Add a Member to a User Role” in the [Administrator's Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkID=178233) in the topic.  
  
 Depending on the needs of your organization, you might want to have a clear distinction between an incident’s Assigned To user and the primary owner. Within [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], neither use has any implied value. For example, although you can choose both of these two users in an incident form, you might want customers to deal with a single person who is your customer focal point. In this case, that person might be the primary owner who also owns other incidents. An Assigned To user might be one of many analysts who might work on an incident temporarily before the incident is assigned to another analyst before it is ultimately resolved and closed.  
  
 IDs that are assigned to change requests and incidents are not created in sequence. However, newer change requests and incidents are assigned IDs with a higher number than the IDs created previously.  
  
## See Also  
 [Managing Incidents](../../../sm/manage/operate/Managing-Incidents.md)