---
title: How to Link a New Incident to a Parent Incident
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: efb321e9-d07e-4cee-9d31-2f0bd163de52


















---
# How to Link a New Incident to a Parent Incident
When analysts create new incidents, System Center 2012 - Service Manager automatically notifies you if any parent incidents exist with the same classification category. The purpose of the notification is to help you combine incidents into parent child groups where a common underlying issue exists. Later, you can use the parent incident to manage the group of incidents as a whole and to serve as a single point of resolution.  
  
 Use the following procedure to manually create a new incident and then link it to a related parent.  
  
### To link a new incident to a parent incident  
  
1.  In the Service Manager console, select **Work Items**.  
  
2.  In the **Work Items** pane, expand **Incident Management**, and then click an incident view, such as **All Incidents**.  
  
3.  In the **Tasks** pane, under **Incident Management**, click **Create Incident**.  
  
4.  In the **Tasks** pane, click **Apply Template**.  
  
5.  Under **Templates** in the **Apply Template** dialog box, select an incident template, such as **Software Issue Incident Template**, and then click **OK**.  
  
6.  When the template applies a classification category or if you manually select a classification category that is in use by an active parent incident, a message appears in the incident form banner. You can optionally click the link to create a link from the new incident to the existing parent. If you are linking the new incident to a parent incident, perform one of the appropriate following substeps:  
  
    -   If the parent incident is resolved, in the **Link to parent incident** dialog box, click **Link to parent and resolve incident**.  
  
    -   Click the link to create the link between the new incident and the parent incident.  
  
7.  In the **Title** box, type a new description or modify the description that is inserted by the template.  
  
8.  In the **Affected user** box, select the user who reported this incident.  
  
9. In the **Alternate Contact Method** box, enter additional contact information for the affected user \(optional\).  
  
10. If necessary, click the **Related Items** tab.  
  
11. Optionally, in the **Attached Files** area, click **Add**.  
  
12. Optionally, in the **Open** dialog box, select the file that you want to attach to this incident, and then click **Open**. For example, select the screen shot of an error message that the affected user has received.  
  
13. Click **OK**.  
  
### To validate creation of a new incident  
  
1.  In the Service Manager console, click **Work Items**.  
  
2.  In the **Work Items** pane, expand **Incident Management**, and then click **All Incidents**. New incidents appear in the **All Incidents** view.  
  
## See Also  
 [Combining Incidents into Parent\-Child Groups](../../../sm/manage/operate/Combining-Incidents-into-Parent-Child-Groups.md)
