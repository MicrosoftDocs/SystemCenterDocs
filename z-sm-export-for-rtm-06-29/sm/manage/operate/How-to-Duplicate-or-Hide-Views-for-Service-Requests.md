---
title: How to Duplicate or Hide Views for Service Requests
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4cb0ca1-f909-4c22-852f-f2cada96dae1
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
# How to Duplicate or Hide Views for Service Requests
You can use the following procedures to duplicate or hide a service request view in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)]. You can use the **Unhide** task if you want to show the hidden view. You can modify the title or other view criteria using the **Edit View** task.  
  
### To duplicate a service request view  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], expand **Work Items**, expand **Service Request Fulfillment**, and then select a subnode. For example, click **Assigned To Me**.  
  
2.  In the **Tasks** pane, click **Duplicate View**.  
  
3.  In the **Select management pack** dialog box, select a management pack to add the new view information to or create a new one, and then click **OK**.  
  
4.  Optionally, you can use the **Edit View** task to edit the new view, titled **\<View Name – Copy\>**, to change the view name or other criteria of the view.  
  
5.  In the **Work Items** pane, locate the new duplicate view that was created. For example, click **Assigned To Me – Copy**.  
  
6.  In the **Tasks** pane, click **Edit View**.  
  
7.  In the **Edit Assigned To Me –Copy** dialog box, click **Criteria**.  
  
8.  In the **Criteria** area, next to **Assigned To User ID**, in the text box after **equals**, type **\[me\]**, and then click **OK**.  
  
### To hide a service request view  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], expand **Work Items**, expand **Service Request Fulfillment**, and then select a subnode, such as **Closed Service Requests**.  
  
2.  In the **Tasks** pane, click **Hide View**.  
  
## See Also  
 [Managing Service Requests in System Center 2012 \- Service Manager](../../../sm/manage/operate/Managing-Service-Requests-in-System-Center-2012---Service-Manager.md)