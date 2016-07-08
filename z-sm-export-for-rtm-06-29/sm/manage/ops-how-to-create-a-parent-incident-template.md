---
title: How to Create a Parent Incident Template
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1834b992-0abb-4898-93db-7638c799cb33


















---
# How to Create a Parent Incident Template
In System Center 2012 - Service Manager, a parent incident template is used to create new incidents. Incidents created from a template will include information for fields that you do not have to enter manually. By using a template for new incidents, new incidents are created faster than from scratch.  
  
 The template author creates a template for release records by using the following procedure.  
  
### To create a parent incident template  
  
1.  In the Service Manager console, open the Library workspace, and in the **Library** pane, select **Templates**.  
  
2.  In the **Tasks** list under **Template**, click **Create Template**.  
  
3.  In the **Create Template** dialog box, type a name for the incident template and a description of what the template applies.  
  
4.  Under **Class**, click **Browse**; in the **Select a Class** box, select **Incident**; and then click **OK** to close the **Select a Class** box.  
  
5.  Optionally, you can select the management pack where the template is saved.  
  
6.  Click **OK** to close the **Create Template** dialog box, and the new incident template form appears.  
  
7.  Enter information on the **General** tab, and then click the **Activities** tab.  
  
8.  Optionally, you can add, delete, or modify manual activities for the template.  
  
9. If you add an activity, the activity form opens. Enter necessary information, and then click **OK** to save the activity.  
  
10. When you have added all the activities you want, click **OK** to save the incident template and close it. The incident template then appears in **Templates** list.  
  
## See Also  
 [Combining Incidents into Parent\-Child Groups](../../../sm/manage/operate/Combining-Incidents-into-Parent-Child-Groups.md)
