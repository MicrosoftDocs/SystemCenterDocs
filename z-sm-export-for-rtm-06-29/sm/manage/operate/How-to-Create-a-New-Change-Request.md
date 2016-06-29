---
title: How to Create a New Change Request
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c531d5f-915a-4c56-8bec-e70e839ab396
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
# How to Create a New Change Request
You can use the following procedures in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] to create a change request for servers that are part of a service and then validate the creation of the change request. First, you view items from the service dependency view. Then, you navigate to the configuration items and open a change request template. Lastly, you assess the priority, impact, and risk level of the request. Although you create the change request from a service dependency view, you can also create a new change request from other places in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
> [!NOTE]  
>  IDs that are assigned to change requests and incidents are not created in sequence. However, newer change requests and incidents are assigned IDs with a higher number than ones created previously.  
  
### To create a change request  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Configuration Items**.  
  
2.  In the **Configuration Items** pane, expand **Business Services**, and then click **All Business Services**.  
  
3.  In the **All Business Services** pane, double\-click the service. For example, double\-click **IT Messaging Service**.  
  
4.  In the dialog box that opens, click the **Service Dependents** tab.  
  
5.  In the **Expand to** list, click **Level 1**, and then view the items in the list. Notice the server names. For example, **Exchange01.woodgrove.com** and **Exchange02.woodgrove.com** appear in the list.  
  
6.  In the **Service Dependents** list, select a computer, and then click **Open**. For example, select and open **Exchange01.woodgrove.com**.  
  
7.  In the computer form, click **Create Related Change Request** under **Tasks**.  
  
8.  In the **Select Template** dialog box, click a template, and then click **OK**. For example, click **Changes to messaging infrastructure template**.  
  
9. In the **Title** box, type a name for the change request. For example, type **Apply Exchange Server 2010 Service Pack 1**. Notice that various values in the form are populated with information from the change request template.  
  
10. In the **Description** and **Reason** fields, type a description and the reason for the change request. For example, type **Apply Exchange Server 2010 Service Pack 1 to these servers** in the **Description** field, and type **The service pack fixes the problem that these servers have** in the **Reason** field.  
  
11. In the **Assigned To** field, enter the name of the person to whom you want to assign the change request. For example, type **Aaron Lee**.  
  
12. Specify the priority, impact, and risk. For example, In the **Priority** list, select **Medium**. In the **Impact** list, select **Standard**. In the **Risk** list, click **Medium**.  
  
13. In the **Config Items To Change** list, make sure that one server is listed, and then click **Add**.  
  
14. In the **Select Objects** dialog box, select another item to add to the change request, and then click **Add**. For example, select **Exchange02.woodgrove.com**, and then click **OK**.  
  
15. Click **OK** to close the change request form.  
  
### To validate the creation of a change request  
  
1.  Open the service that contains the items for which you created the change request, and then click the **Service Dependents** tab.  
  
2.  In the **Service Components** list, notice that the two servers you opened the change request for are marked with **YES** under the **Affected By Change** column.  
  
3.  Click **Cancel** to close the service.  
  
## See Also  
 [Initiating and Classifying a Change Request](../../../sm/manage/operate/Initiating-and-Classifying-a-Change-Request.md)