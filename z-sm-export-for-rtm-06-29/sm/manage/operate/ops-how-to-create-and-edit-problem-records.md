---
title: How to Create and Edit Problem Records
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: adeb984b-aef3-419f-ba74-b4bc22312757
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
# How to Create and Edit Problem Records
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you can use the following procedures to create new problem records and then edit them by using the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]. You can create a new problem record from the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], from an incident view, or from an incident form.  
  
### To create a new problem record from the console  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Problem Management**, and then click **Active Problems**.  
  
3.  In the **Tasks** pane, click **Create Problem**.  
  
4.  In the **Title** box, type a title for the problem. For example, type **Outlook E\-Mail Restricted Permissions**.  
  
5.  In the **Description** box, type a description of the problem. For example, type **Users cannot view e\-mail messages sent with restricted permissions**.  
  
6.  If you want to assign the problem to an analyst, enter the name of the analyst in the **Assigned to** box.  
  
7.  In the **Source** list, select the source of the problem request.  
  
8.  Select the appropriate values in the **Category**, **Impact**, and **Urgency** boxes.  
  
9. Click **OK**.  
  
### To create a new problem record from an incident view  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Incident Management**, and then click **All Incidents**.  
  
3.  In the **All Incidents** list, search for incidents whose titles match the problem record that you want to create, and then click **Search**. For example, search for **restricted permission**.  
  
4.  In the search results, select the incidents for which you want to create a problem record. In the **Tasks** pane under **Selected Items**, click **Create Problem**.  
  
5.  In the **Title** box, type a title for the problem. For example, type **Outlook E\-Mail Restricted Permissions**. When you create a problem by using this method, the problem form inherits the title from the open incident if a single incident was selected. If multiple incidents were selected, the **Title** box is blank. You can change the title of the problem record.  
  
6.  In the **Description** box, type a description of the problem. For example, type **Users cannot view e\-mail messages sent with restricted permissions**.  
  
7.  If you want to assign the problem to an analyst, enter the name of the analyst in the **Assigned to** box.  
  
8.  In the **Source** list, select the source of the problem request.  
  
9. Select the appropriate values in the **Category**, **Impact**, and **Urgency** boxes.  
  
10. Click **OK**.  
  
### To create a new problem record from an incident form  
  
1.  Make sure that an incident is already open. Then, under **Tasks**, click **Create Problem**.  
  
2.  In the **Title** box, type a title for the problem. For example, type **Outlook E\-Mail Restricted Permissions**. When you create a problem using this method, the problem form inherits the title from the open incident. You can change the title of the problem record.  
  
3.  In the **Description** box, type a description of the problem. For example, type **Users cannot view e\-mail messages sent with restricted permissions**.  
  
4.  If you want to assign the problem to an analyst, enter the name of the analyst in the **Assigned to** box.  
  
5.  In the **Source** list, select the source of the problem request.  
  
6.  Select the appropriate values in the **Category**, **Impact**, and **Urgency** boxes.  
  
7.  Click **OK**.  
  
### To edit a problem record  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Problem Management**, and then click **Active Problems**.  
  
3.  In the **Active Problems** view, double\-click a problem. For example, double\-click the **Outlook E\-Mail Restricted Permissions** problem.  
  
4.  In the problem form, edit information that needs to be changed. For example, if a workaround is found for the problem, click the **Resolution** tab. Then, in the **Workarounds** field, type the workaround steps.  
  
5.  Click **OK**.  
  
### To validate the creation of a new problem record  
  
-   In the **Tasks** list, click **Refresh** to view the new problem record, or open the problem record to view the revised information.  
  
## See Also  
 [Managing Problems](../../../sm/manage/operate/Managing-Problems.md)