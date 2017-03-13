---
title: Combine incidents into parent-child groups
description: Explains how to combine Service Manager incidents into parent-child groups.
manager: carmonm
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
ms.assetid: a32d0372-ac68-4ddc-b60c-9a4ff4d55387
---

# Combine Service Manager incidents into parent-child groups

>Applies To: System Center 2016 - Service Manager

Incidents in System Center 2016 - Service Manager are usually short\-lived while help desk analysts investigate and then restore operations. Often, incidents are related and it is useful to group incidents together. You can create a parent incident to group other existing incidents together, which can help provide visibility into them and their relationship to one another.  

A Service Manager administrator can define automatic incident resolution settings so that when a parent incident is resolved, all its child incidents resolve automatically, do not resolve automatically, or to let the analyst decide whether to resolve or not. Similarly, an administrator can also define automatic incident reactivation settings so that when a parent incident is reactivated, all its child incidents reactivate automatically, do not reactivate automatically, or to let the analyst decide whether to reactivate the child incidents. Both processes can help you verify that all child incidents are resolved or activated together as a group.  

## Create a parent incident from an incident form

In System Center 2016 - Service Manager, one way a help desk analyst can create a parent incident is when an existing incident is already opened. You can create a parent incident using the following steps. A parent incident serves as a container for several incidents.  

 The following procedure is performed on an incident that is neither a parent incident nor a child incident. Afterward, a new parent incident is created and the existing incident is converted to a child incident.  

### To create a parent incident from an incident form  

1.  In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incidents**.  

2.  Select any Incident Management view that contains active incidents, and then select an incident.  

3.  In the **Tasks** pane, click **Edit** to open the incident.  

4.  In the **Tasks** pane, click **Link to New Parent Incident** to open the **Link to New Parent Incident** dialog box.  

5.  In the **Link to New Parent Incident** dialog box, select a template to create the new parent incident with, and then click **OK**. For example, select **Networking Issue Incident Template**, and then click **OK**.  

6.  In the **Title** box, type a new description or modify the description that is inserted by the template. For example, type **Network Outage in Bldg 773.**  

7.  In the **Affected user** box, select the user who reported this incident. For example, select **Joe Andreshak**.  

8.  In the **Alternate Contact Method** box, enter additional contact information for the affected user \(optional\).  

9. The **Child Incidents** tab appears in the form where you view the child incident that the new parent incident is grouped with and where you can add other child incidents.  

10. In the parent incident form, click **OK** to close it.  

11. In the original incident form, click **OK** to close it.  

## Link an open incident to a parent incident

The help desk analyst can link open incidents to a parent incident or remove links using the following procedures.  

### To link open incidents to a parent incident  

1.  In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  

2.  Select any incident view that contains one or more incidents that you want to link to a parent incident.  

3.  Select one or more incidents, and in the **Tasks** pane, click **Link\/Unlink to Existing Parent Incident**, and then in the submenu, click **Link**.  

4.  In the **Link to parent incident** dialog box, click **Link**.  

5.  In the **Select Parent Incident** dialog box, select the parent incident that you want to link the open incident to, and then click **OK** to create the link and close the **Select Parent Incident** dialog box.  

### To remove links between child incidents and the parent incident  

1.  In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  

2.  Select any incident view that contains one or more incidents that you want to unlink from the parent incident.  

3.  Select one or more incidents, and in the **Tasks** pane, click **Link\/Unlink to Existing Parent Incident**, and then in the submenu, click **Unlink**.  

4.  In the **Unlink** confirmation dialog box, click **Yes**.   

## Resolve a parent incident

In Service Manager, the help desk analyst can resolve a parent incident, and then Service Manager will automatically resolve all its child incidents, if the Service Manager administrator has configured Incident settings accordingly. This method of resolving incidents can help the analyst quickly close many child incidents. Use the following procedure to resolve a parent incident.  

### To resolve a parent incident  

1.  In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  

2.  Select the **All Open Parent Incidents** view, and then in the list of parent incidents, select the incident that you want to resolve.  

3.  In the **Tasks** pane, click **Change Incident Status**, and then in the submenu, click **Resolve**.  

4.  In the **Resolve** dialog box, select a **Resolution Category**, and then in the **Comments** box, type a description of the steps that you have taken to resolve the incident.  

5.  If you want child incidents to resolve automatically and the option is available, ensure that the **Resolve child incidents when resolving this parent incident** option is selected, and then click **OK** to resolve the incident-and child incidents, if selected, and then close the **Resolve** dialog box.  

## Link an active incident to a resolved parent incident

While reviewing active incidents in Service Manager, help desk analysts might determine that an incident should have already been resolved because another analyst has already corrected the underlying cause. If there is a closed parent incident, the analyst can use the following procedure to link the incident to the resolved parent and then automatically resolve the active incident.  

### To link an active incident to a resolved parent and automatically close the active incident  

1.  In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  

2.  Select any incident view that contains the incident that you want to a resolved parent to.  

3.  Select one or more incidents, and in the **Tasks** pane, click **Link\/Unlink to Existing Parent Incident**, and then in the submenu, click **Link**.  

4.  In the **Select Parent Incident** dialog box, select the resolved parent incident that you want to link the open incident to, and then click **OK**.  

5.  In the **Link to parent incident** dialog box, select **Link to parent and resolve incident**.  

6.  If you are linking multiple active incidents to a resolved parent, ensure that you select **Repeat this option for all conflicts** to automatically resolve all the incidents.

## Reactivate a resolved parent incident

In Service Manager, the help desk analyst can reactivate a parent incident, and then Service Manager will automatically activate all its child incidents, if the Service Manager administrator has configured Incident settings accordingly. This method of reactivating incidents can help the analyst quickly activate many child incidents. Use the following procedure to reactivate a parent incident.  

Depending on parent incident settings in the Administration workspace, behavior of automatic child incident resolution and reactivation varies.

### To reactivate a parent incident  

1.  In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  

2.  Select the **All Incidents** view, and then in the list of parent incidents, select the incident that you want to reactivate.  

3.  In the **Tasks** pane, click **Change Incident Status**, and then in the submenu, click **Activate**.  

4.  In the **Activate** dialog box, in the **Comments** box, type a description of the reason that you are activating the incident.  

5.  Click **OK** to activate the incident and child incidents, if they are available and selected, and to close the **Activate** dialog box.

## Create a parent incident template

In Service Manager, a parent incident template is used to create new incidents. Incidents created from a template will include information for fields that you do not have to enter manually. By using a template for new incidents, new incidents are created faster than from scratch.  

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

## View a parent incident from a child incident

In Service Manager, the help desk analyst can use the following procedure to easily view parent incidents when a child incident is open. Reviewing parent incident information is often necessary to determine the status of its child incidents. Use the following procedure to view a parent incident from a child incident.  

### To view a parent incident from a child incident  

1.  In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  

2.  Select an incident view that contains a child incident that you want to open, and then select the incident.  

3.  In the **Tasks** pane, click **Edit**.  

4.  In the incident form banner, the parent incident ID and description appears next to **Parent incident**. Click the linked parent incident to open it.  

5.  After reviewing the parent incident information, you can optionally update any information, such as comments, in the Action Log.  

6.  If you make changes to the parent incident, click **OK**. Otherwise, click **Cancel**.  

7.  If you make changes to the child incident, click **OK**. Otherwise, click **Cancel**.   

## Link a new incident to a parent incident

When analysts create new incidents, Service Manager automatically notifies you if any parent incidents exist with the same classification category. The purpose of the notification is to help you combine incidents into parent child groups where a common underlying issue exists. Later, you can use the parent incident to manage the group of incidents as a whole and to serve as a single point of resolution.  

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
