---
title: Managing Problems
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62f1e2c8-2c78-41f6-a737-8d8fefd6079d
---

# Managing Problems

>Applies To: System Center 2016 - Service Manager

The procedures in this section describe how to manage problems in Service Manager.  

 In Service Manager, problems are records that are created to help prevent future problems and incidents from happening, to eliminate recurring incidents, and to minimize the impact of incidents that cannot be prevented. Analysts can use the Service Manager console to create problem records and to associate incidents with problems.  

## How to Create and Edit Problem Records

You can use the following procedures to create new problem records and then edit them by using the Service Manager console. You can create a new problem record from the Service Manager console, from an incident view, or from an incident form.  

### To create a new problem record from the console  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Problem Management**, and then click **Active Problems**.  

3.  In the **Tasks** pane, click **Create Problem**.  

4.  In the **Title** box, type a title for the problem. For example, type **Outlook E\-Mail Restricted Permissions**.  

5.  In the **Description** box, type a description of the problem. For example, type **Users cannot view e\-mail messages sent with restricted permissions**.  

6.  If you want to assign the problem to an analyst, enter the name of the analyst in the **Assigned to** box.  

7.  In the **Source** list, select the source of the problem request.  

8.  Select the appropriate values in the **Category**, **Impact**, and **Urgency** boxes.  

9. Click **OK**.  

### To create a new problem record from an incident view  

1.  In the Service Manager console, click **Work Items**.  

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

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Problem Management**, and then click **Active Problems**.  

3.  In the **Active Problems** view, double\-click a problem. For example, double\-click the **Outlook E\-Mail Restricted Permissions** problem.  

4.  In the problem form, edit information that needs to be changed. For example, if a workaround is found for the problem, click the **Resolution** tab. Then, in the **Workarounds** field, type the workaround steps.  

5.  Click **OK**.  

### To validate the creation of a new problem record  

-   In the **Tasks** list, click **Refresh** to view the new problem record, or open the problem record to view the revised information.

## How to Resolve Problem Records and Related Incidents Automatically

You can use the following procedures to resolve a problem record and the incidents that are associated with it and then validate the resolution.  

### To resolve a problem record and the incidents that are associated with it  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Problem Management**, and then click **Active Problems**.  

3.  In the **Active Problems** view, double\-click the problem record that you want to resolve. Then, in the **Tasks** pane, click **Resolve**.  

4.  Click the **Resolution** tab, and then click to select the **Auto\-resolve all incidents associated with this problem** check box.  

5.  In the **Resolution Category** box, select the appropriate category.  

6.  In the **Resolution Description** box, type a summary of the resolution for this problem record. For example, type **Application of Exchange Server 2010 SP1 fixed the restricted permission problem that affected users across forests**.  

7.  Click **OK**.  

### To validate problem and incident resolution  

-   Verify that the incidents associated with the problem record appear in the **All Incidents** view and that they have a status of **Resolved**.  

    > [!NOTE]  
    >  It might take a few minutes for the incident status to be updated to **Resolved**.  

## How to Link an Incident or Change Request to a Problem Record

You can use the following procedure to link an incident or change request to a problem record if you created a problem record without linking it to an existing incident or change request.  

### To link an incident or change request to a problem record  

1.  In the Service Manager console, click **Work Items**.  

2.  In the **Work Items** pane, expand **Problem Management**, and then click **Active Problems**.  

3.  In the **Active Problems** view, double\-click a problem record. For example, double\-click the **Outlook E\-mail Restricted Permissions** problem record.  

4.  In the problem form, click the **Related Items** tab.  

5.  Under **Work Items**, click **Add**.  

6.  In the **Select objects** dialog box, either select a work item or search for and select one or more work items to link to the problem record. Click **Add**, and then click **OK**.  

7.  Click **OK** to close the form.  

### To validate the link  

-   In the **Active Problems** view, open the problem record to which you linked a work item, click the **Related Items** tab, and then verify that the items you linked appear under **Work Items**.  
