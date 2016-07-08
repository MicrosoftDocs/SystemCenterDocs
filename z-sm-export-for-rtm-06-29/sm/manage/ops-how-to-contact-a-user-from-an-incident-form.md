---
title: How to Contact a User from an Incident Form
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 063d010b-c955-4499-b690-561cfd7f9db5


















---
# How to Contact a User from an Incident Form
In System Center 2012 - Service Manager, you can contact a user by email or by instant message when an incident form is open. The presence indicator is shown in the form next to the affected user’s name, and it displays their current status, if known. For the presence indicator to accurately reflect a user’s status, the user must have an Active Directory account, and the user must be a member of the same domain in which the Service Manager management server has its computer account. Additionally, the computer running the Service Manager console must have Microsoft Office Lync 2010 installed.  
  
> [!NOTE]  
>  If a user’s account belongs to a domain other than the domain in which the Service Manager management server has its computer account, the presence indicator might not accurately display the user’s status.  
  
### To contact a user by email  
  
1.  In an open incident form, click the presence indicator next to the **Affected user** box, and then click the triangle icon next to the box.  
  
2.  Click **Send Mail**.  
  
3.  Your email client program opens and adds the user’s name to the **To** box. Compose the e\-mail message, and then send it.  
  
### To contact a user by instant message  
  
1.  In an open incident form, click the presence indicator next to the **Affected user** box, and then click the triangle next to the box.  
  
2.  Click **Send Instant Message**.  
  
3.  Your instant message program opens. Compose the instant message, and then send it.  
  
## See Also  
 [Managing Incidents](../../../sm/manage/operate/Managing-Incidents.md)
