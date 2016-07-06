---
title: How to Close a Change Request
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36dc09ae-117f-4fa2-bb0e-641685b3601b
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
# How to Close a Change Request
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you can use the following procedures to permanently close a successful change request or a failed change request and then validate the closure of the change request. You cannot reopen a closed change request.  
  
> [!NOTE]  
>  If an end user cancels a software request before the software is deployed to the end user’s computer, the associated change request might reflect the **In Progress** status indefinitely. If this occurs, cancel the request and then close it.  
  
### To close a successful change request  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Work Items**, expand **Change Management**, and then click **Change Requests: Completed**.  
  
3.  Select the change request.  
  
4.  In the **Tasks** pane, click **Close**.  
  
5.  In the **Comment** box, type a comment, and then click **OK**.  
  
### To close a failed change request  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, click **Change Management**, and then click **Change Requests: Failed**.  
  
3.  Select the change request.  
  
4.  In the **Tasks** pane, click **Close**.  
  
5.  In the **Comments** box, type a comment, and then click **OK**.  
  
### To validate the closure of a change request  
  
-   Click the **Change Requests: Closed** view to ensure that the closed change request appears in the list.  
  
## See Also  
 [Implementing and Closing a Change Request](../../../sm/manage/operate/Implementing-and-Closing-a-Change-Request.md)