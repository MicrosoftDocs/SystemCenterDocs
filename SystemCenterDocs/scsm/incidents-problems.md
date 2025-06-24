---
title: Manage incidents and problems
description: Provides an overview and explains how to manage incidents and problems in Service Manager.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 7904413b-ace2-4e65-b609-d0804d99c764
---

# Manage incidents and problems in Service Manager



Service Manager helps your organization manage incidents and problems by implementing and automating help desk ticketing processes so that these processes comply with the best practices that are described in the Microsoft Operations Framework \(MOF\) and in the Information Technology Infrastructure Library \(ITIL\). For more information about MOF&nbsp;4.0, see [Microsoft Operations Framework](/previous-versions/tn-archive/cc936627(v=technet.10)).  

If you need to add or extend the functionality of Service Manager to implement custom processes for handling incidents and problems, you can use standard Microsoft development tools and the Service Manager SDK.  

The procedures in this section are organized according to common problem and incident management scenarios. Even though the sample scenarios refer to a fictitious organization, Woodgrove Bank, the scenarios and steps are based on real use and they describe how to use the problem and incident management features in Service Manager.  

At first, the difference between affected items and related items in problem and incident forms might not be obvious. However, the difference describes different relationships. An affected item is something that is directly affected by the problem or incident; for example, your computer. But a related item is something more loosely related but not directly affected. For example, a related item could be any other configuration item that isn't directly affected but connected to another configuration item as a reference.  

## Sample scenarios to manage incidents and problems in Service Manager

The following sample scenarios for Service Manager help you achieve your goal of managing incidents and problems by using multiple scenarios end to end. You can think of these sample scenarios as a case study that helps put the individual scenarios and procedures in context.  

### Manage incidents  

In the scenario that encompasses incident management, Phil uses incident management to restore regular operations as quickly and as cost\-effectively as possible. For example, by using the E\-mail Incident template to populate a new email\-related incident, he can quickly create an incident and ensure that the correct **Impact**, **Urgency**, **Assigned Analyst**, and **Support Tier** fields are configured. Carrying the example further, he creates a new incident for a user who is unable to view an email that was sent with restricted permissions. Phil creates an incident view so that he can easily work with all the incidents that are created for email problems. When changes are made to an incident, he edits the incident to reflect the changes.  

In another example, an end-user experiences a printer problem, and she sends an email message to the help desk. Upon receipt of the message, Service Manager automatically creates an incident from the message. Phil investigates the problem, in part, by viewing the service. After the underlying problem has been solved, he resolves and closes the incident.  

At Woodgrove Bank, connectors are configured in such a way that Service Manager imports configuration items and alerts from, so that some new incidents are created automatically. Phil reviews the automatically created incidents for accuracy.  

### Troubleshoot incidents  

In the scenario that encompasses troubleshooting incidents, Phil is conducting an initial investigation of the problem that Joe is experiencing. Phil suspects that the root cause of the problem is that an update for Microsoft Exchange Server needs to be applied to Joe's Exchange server. However, there are other Exchange servers at Woodgrove Bank that probably also need to be updated. Phil starts his investigation by viewing the service that Garret created for the Exchange service. When any incidents affect a service component, that component is marked with an orange icon resembling a square containing an exclamation point. When a change request affects a service component, the component is marked with a special blue icon resembling a square containing a right\-pointing arrow. Phil uses the map view on the **Service Components** tab to view configuration items and view incidents associated with them. Then, he opens other configuration items and adds them to the open incident.  

 To further troubleshoot, Phil wants to ping a remote computer that is exhibiting problems. He can use tasks that are part of the Service Manager console instead of having to use various other tools.  

### Manage problems  

In the scenario that encompasses problem management, Phil has created a change request asking the Exchange Administrators group to apply an update, which is expected to resolve the problem. When a root cause is found and mitigated or resolved, the change request is completed and Phil is notified. He then uses the prescribed procedures to resolve a problem and automatically resolve incidents associated with the problem.  

## Manage Service Manager incidents

Help desk analysts use incident management to restore regular operations as quickly and as cost\-effectively as possible by creating new incidents. They also work in partnership with Service Manager administrators to ensure that incidents that are created automatically or by end-users are correctly categorized and reassigned to appropriate personnel. Methods that analysts use to accomplish these duties include:  

- Using the E\-mail Incident template to create new incidents.  
- Reviewing automatically created incidents, such as those incidents that are automatically created from System Center Operations Manager using the Operations Manager Alert connector.  
- Reviewing and updating incidents that are created by end-users who have sent requests by email.  
- Combining incidents into parent\-child relationships when incidents are related.  

Using the E\-mail Incident template to populate a new email\-related incident, you can quickly create an incident and ensure that the correct **Impact**, **Urgency**, **Assigned Analyst**, and **Support Tier** fields are configured.  

If you configure connectors so that Service Manager imports configuration items and alerts from Operations Manager, some new incidents are automatically created. An analyst reviews the automatically created incidents for accuracy.  

In Service Manager, incidents are automatically created from email requests by users. If the user is recognized as a Service Manager end-user, the request that is sent to the help desk email address automatically creates a new incident.  

> [!NOTE]  
> Service Manager can automatically generate new incidents from email requests only after a Service Manager administrator enables inbound email processing. By default, the impact and urgency of every incident created by email submission is set to medium, and no category is assigned.  

Normally, you create incidents only for user accounts in your organization that have Active&nbsp;Directory Domain Services \(AD&nbsp;DS\) accounts that are synchronized with Service Manager. However, you might occasionally need to manually create incidents for users. For example, you might need to create an incident for a new user whose account isn't yet in AD&nbsp;DS or if an Active&nbsp;Directory account isn't yet synchronized with Service Manager. You can also manually create incidents to support external vendors who don't have Active&nbsp;Directory accounts. In another example, you might need to open an incident for an on\-site technician who doesn't have an Active&nbsp;Directory account but who needs to report an incident. Or, you might need to open an incident for an externally\-supported customer who doesn't have an Active&nbsp;Directory account. In all these examples, you must manually create a user in Service Manager. For more information, see [How to Add a Member to a User Role](user-roles.md).  

Depending on the needs of your organization, you might want to have a clear distinction between an incident's Assigned To user and the primary owner. Within Service Manager, neither use has any implied value. For example, although you can choose both of these two users in an incident form, you might want customers to deal with a single person who is your customer focal point. In this case, that person might be the primary owner who also owns other incidents. An Assigned To user might be one of many analysts who might work on an incident temporarily before the incident is assigned to another analyst before it's ultimately resolved and closed.  

IDs that are assigned to change requests and incidents aren't created in sequence. However, newer change requests and incidents are assigned IDs with a higher number than the IDs created previously.  

## Combine Service Manager incidents into parent-child groups

Incidents in System Center - Service Manager are short-lived while help desk analysts investigate and then restore operations. Often, incidents are related and it's useful to group incidents together. You can create a parent incident to group other existing incidents together, which can help provide visibility into them and their relationship to one another.  

A Service Manager administrator can define automatic incident resolution settings so that when a parent incident is resolved, all its child incidents resolve automatically, don't resolve automatically, or to let the analyst decide whether to resolve or not. Similarly, an administrator can also define automatic incident reactivation settings so that when a parent incident is reactivated, all its child incidents reactivate automatically, don't reactivate automatically, or to let the analyst decide whether to reactivate the child incidents. Both processes can help you verify that all child incidents are resolved or activated together as a group.  

### Create a parent incident from an incident form

In System Center - Service Manager, one way a help desk analyst can create a parent incident is when an existing incident is already opened. You can create a parent incident using the following steps. A parent incident serves as a container for several incidents.  

The following procedure is performed on an incident that is neither a parent incident nor a child incident. Afterward, a new parent incident is created and the existing incident is converted to a child incident.  

To create a parent incident from an incident form, do the following:

1. In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incidents**.  
2. Select any Incident Management view that contains active incidents, and then select an incident.  
3. In the **Tasks** pane, select **Edit** to open the incident.  
4. In the **Tasks** pane, select **Link to New Parent Incident** to open the **Link to New Parent Incident** dialog.  
5. In the **Link to New Parent Incident** dialog, select a template to create the new parent incident with, and select **OK**. For example, select **Networking Issue Incident Template**, and select **OK**.  
6. In the **Title** box, enter a new description or modify the description that is inserted by the template. For example, enter **Network Outage in Bldg 773.**  
7. In the **Affected user** box, select the user who reported this incident. For example, select **Joe Andreshak**.  
8. In the **Alternate Contact Method** box, enter additional contact information for the affected user \(optional\).  
9. The **Child Incidents** tab appears in the form where you view the child incident that the new parent incident is grouped with and where you can add other child incidents.  
10. In the parent incident form, select **OK** to close it.  
11. In the original incident form, select **OK** to close it.  

### Link an open incident to a parent incident

The help desk analyst can link open incidents to a parent incident or remove links using the following procedures.  

To link open incidents to a parent incident, do the following:

1. In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
2. Select any incident view that contains one or more incidents that you want to link to a parent incident.  
3. Select one or more incidents, and in the **Tasks** pane, select **Link\/Unlink to Existing Parent Incident**, and then in the submenu, select **Link**.  
4. In the **Link to parent incident** dialog, select **Link**.  
5. In the **Select Parent Incident** dialog, select the parent incident that you want to link the open incident to, and select **OK** to create the link and close the **Select Parent Incident** dialog.  

#### Remove links between child incidents and the parent incident  

1. In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
2. Select any incident view that contains one or more incidents that you want to unlink from the parent incident.  
3. Select one or more incidents, and in the **Tasks** pane, select **Link\/Unlink to Existing Parent Incident**, and then in the submenu, select **Unlink**.  
4. In the **Unlink** confirmation dialog, select **Yes**.

### Resolve a parent incident

In Service Manager, the help desk analyst can resolve a parent incident, and then Service Manager will automatically resolve all its child incidents if the Service Manager administrator has configured Incident settings accordingly. This method of resolving incidents can help the analyst quickly close many child incidents. Use the following procedure to resolve a parent incident.  

To resolve a parent incident, do the following:

1. In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
2. Select the **All Open Parent Incidents** view, and then in the list of parent incidents, select the incident that you want to resolve.  
3. In the **Tasks** pane, select **Change Incident Status**, and then in the submenu, select **Resolve**.  
4. In the **Resolve** dialog, select a **Resolution Category**, and then in the **Comments** box, enter a description of the steps that you've taken to resolve the incident.  
5. If you want child incidents to resolve automatically and the option is available, ensure that the **Resolve child incidents when resolving this parent incident** option is selected, and select **OK** to resolve the incident-and child incidents, if selected, and then close the **Resolve** dialog.  

### Link an active incident to a resolved parent incident

While reviewing active incidents in Service Manager, help desk analysts might determine that an incident should have already been resolved because another analyst has already corrected the underlying cause. If there's a closed parent incident, the analyst can use the following procedure to link the incident to the resolved parent and then automatically resolve the active incident.  

#### Link an active incident to a resolved parent and automatically close the active incident  

1. In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
2. Select any incident view that contains the incident that you want to a resolved parent to.  
3. Select one or more incidents, and in the **Tasks** pane, select **Link\/Unlink to Existing Parent Incident**, and then in the submenu, select **Link**.  
4. In the **Select Parent Incident** dialog, select the resolved parent incident that you want to link the open incident to, and select **OK**.  
5. In the **Link to parent incident** dialog, select **Link to parent and resolve incident**.  
6. If you're linking multiple active incidents to a resolved parent, ensure that you select **Repeat this option for all conflicts** to automatically resolve all the incidents.

### Reactivate a resolved parent incident

In Service Manager, the help desk analyst can reactivate a parent incident, and then Service Manager will automatically activate all its child incidents if the Service Manager administrator has configured the Incident settings accordingly. This method of reactivating incidents can help the analyst quickly activate many child incidents. Use the following procedure to reactivate a parent incident.  

Depending on the parent incident settings in the Administration workspace, the behavior of automatic child incident resolution and reactivation varies.

#### Reactivate a parent incident  

1. In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
2. Select the **All Incidents** view, and then in the list of parent incidents, select the incident that you want to reactivate.  
3. In the **Tasks** pane, select **Change Incident Status**, and then in the submenu, select **Activate**.  
4. In the **Activate** dialog, in the **Comments** box, enter a description of the reason you're activating the incident.  
5. Select **OK** to activate the incident and child incidents, if they're available and selected, and to close the **Activate** dialog.

### Create a parent incident template

In Service Manager, a parent incident template is used to create new incidents. Incidents created from a template will include information for fields that you don't have to enter manually. By using a template for new incidents, new incidents are created faster than from scratch.  

The template author creates a template for release records by using the following procedure:

1. In the Service Manager console, open the Library workspace, and in the **Library** pane, select **Templates**.  
2. In the **Tasks** list under **Template**, select **Create Template**.  
3. In the **Create Template** dialog, enter a name for the incident template and a description of what the template applies.  
4. Under **Class**, select **Browse**; in the **Select a Class** box, select **Incident**; and then select **OK** to close the **Select a Class** box.  
5. Optionally, you can select the management pack where the template is saved.  
6. Select **OK** to close the **Create Template** dialog, and the new incident template form appears.  
7. Enter information on the **General** tab, and select the **Activities** tab.  
8. Optionally, you can add, delete, or modify manual activities for the template.  
9. If you add an activity, the activity form opens. Enter the necessary information, and select **OK** to save the activity.  
10. When you've added all the activities you want, select **OK** to save the incident template and close it. The incident template then appears in the **Templates** list.  

### View a parent incident from a child incident

In Service Manager, the help desk analyst can use the following procedure to easily view parent incidents when a child incident is open. Reviewing parent incident information is often necessary to determine the status of its child incidents. Use the following procedure to view a parent incident from a child incident.  

To view a parent incident from a child incident, do the following:

1. In the Service Manager console, open the Work Items workspace, and in the **Work Items** pane, expand **Incident Management**.  
2. Select an incident view that contains a child incident that you want to open, and then select the incident.  
3. In the **Tasks** pane, select **Edit**.  
4. In the incident form banner, the parent incident ID and description appears next to **Parent incident**. Select the linked parent incident to open it.  
5. After reviewing the parent incident information, you can optionally update any information, such as comments, in the Action Log.  
6. If you make changes to the parent incident, select **OK**. Otherwise, select **Cancel**.  
7. If you make changes to the child incident, select **OK**. Otherwise, select **Cancel**.   

### Link a new incident to a parent incident

When analysts create new incidents, Service Manager automatically notifies you if any parent incidents exist with the same classification category. The purpose of the notification is to help you combine incidents into parent child groups where a common underlying issue exists. Later, you can use the parent incident to manage the group of incidents as a whole and to serve as a single point of resolution.  

Use the following procedure to manually create a new incident and then link it to a related parent:

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**, and select an incident view, such as **All Incidents**.  
3. In the **Tasks** pane, under **Incident Management**, select **Create Incident**.  
4. In the **Tasks** pane, select **Apply Template**.  
5. Under **Templates** in the **Apply Template** dialog, select an incident template, such as **Software Issue Incident Template**, and select **OK**.  
6. When the template applies a classification category or if you manually select a classification category that is in use by an active parent incident, a message appears in the incident form banner. You can optionally select the link to create a link from the new incident to the existing parent. If you're linking the new incident to a parent incident, perform one of the appropriate following substeps:  
    - If the parent incident is resolved, in the **Link to parent incident** dialog, select **Link to parent and resolve incident**.  
    - Select the link to create the link between the new incident and the parent incident.  
7. In the **Title** box, enter a new description or modify the description that is inserted by the template.  
8. In the **Affected user** box, select the user who reported this incident.  
9. In the **Alternate Contact Method** box, enter additional contact information for the affected user \(optional\).  
10. If necessary, select the **Related Items** tab.  
11. Optionally, in the **Attached Files** area, select **Add**.  
12. Optionally, in the **Open** dialog, select the file that you want to attach to this incident, and select **Open**. For example, select the screenshot of an error message that the affected user has received.  
13. Select **OK**.  

#### Validate the creation of a new incident  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**, and select **All Incidents**. New incidents appear in the **All Incidents** view.  

## Manually create a new incident in Service Manager

In Service Manager, incidents are automatically created from email requests by users. However, you can use the following procedures to manually create a new incident in the Service Manager console and then validate it. For example, you might want to manually create a new incident for a person who is experiencing an email\-related problem. You can link other affected items, such as various computers, to indicate that the issue affects more than one computer.  

### Create a new incident from a configuration item view  

1. In the Service Manager console, select **Configuration Items**.  
2. In the **Configuration Items** pane, expand **Configuration Items**, expand **Computers**, and select **All Windows Computers**.  
3. In the **All Windows Computers** view, filter for the computer for which you want to create an incident, and then select the computer. For example, select **Exchange01.woodgrove.com**.  
4. In the **Tasks** pane, select **Create Related Incident**.  
5. In the **Tasks** pane, select **Apply Template**.  
6. Under **Templates** in the **Apply Template** dialog, select **Software Issue Incident Template**, and select **OK**.  
7. In the **Title** box, enter a new description or modify the description inserted by the template. For example, enter **User unable to open e\-mail that has restricted permissions.**  
8. In the **Affected user** box, select the user who reported this incident. For example, select **Joe Andreshak**.  
9. In the **Alternate Contact Method** box, enter additional contact information for the affected user \(optional\).  
10. Select the **Related Items** tab.  
11. In the **Attached Files** area, select **Add**.  
12. In the **Open** dialog, select the file that you want to attach to this incident, and select **Open**. For example, select the screenshot of an error message that the affected user has received.  
13. Select **OK**.  

### Create a new incident by email  

1. In an email program, create a new email message, and enter the help desk alias or email address in the **To** box. For example, enter **Helpdesk\@Helpdesk.Woodgrove.com** in the **To** box.  
2. In the **Subject** box, enter a subject. For example, enter **Unable to print checks**.  
3. In the message body, enter additional information that the help desk analyst can use to correct the problem. For example, enter **The check printer has a paper jam. I will use a backup printer until the jam is fixed**.  
4. Optionally, attach files that the help desk analyst can use to correct the problem.  

### Validate creation of a new incident  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**, and select **All Incidents**. New incidents appear in the **All Incidents** view.  

## Change an existing incident in Service Manager

In Service Manager, you can use the following procedures to change the urgency of an incident, edit an unassigned incident from Operations Manager, link a knowledge article to an incident, and validate the changes. Users create simplified incidents using the Self-Service Portal based on the Incident portal template. Because user\-created incidents are simplified, analysts often need to revise new incidents with additional information. Additionally, there's no functional difference between incidents created with the Self-Service Portal, using either the **Need help with a problem** or **Need repair or fix** options.  

> [!NOTE]  
> Incidents are automatically created by System Center - Service Manager when the Operations Manager Alert connector is enabled. You can edit the new incidents that are generated when an Operations Manager alert is raised and then assign the incidents to analysts.  

### Change the urgency of an incident  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**, and select **All Open E\-Mail Incidents**.  
3. In the **All Open E\-Mail Incidents** view, select the original incident. For example, select the **Unable to print checks** incident.  
4. In the **Tasks** pane, select **Edit**.  
5. In the **Incident** form, in the **Urgency** list, select **High**.  
6. Optionally, enter a comment in the **Action Log** box. If you don't want end-users to be able to read the comment, select the **Private** checkbox that is above the **Action Log** box. For example, in the **Action Log** box, enter **The user called to say that the backup printer is unavailable and that this issue is now urgent**. Then, select **Add**. The new comment appears as a log entry.  
7. Select **OK** to close the form and to save your changes.  

### Edit an unassigned incident from Operations Manager  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**, and select **All Open Operations Manager Incidents**.  
3. In the **All Open Operations Manager Incidents** view, select an incident that was created automatically from an Operations Manager alert.  
4. In the **Tasks** pane, select **Edit**.  
5. In the **Incident** form, under **Support Group**, select **Tier 1**.  
6. Under **Assigned to**, enter the name of the help desk analyst who will investigate the problem.  
7. Select **OK** to close the form and to save your changes.  

### Link a knowledge article to an incident  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**, and select **All Open Operations Manager Incidents**.  
3. In the **All Open Operations Manager Incidents** view, select the incident that was created automatically from an Operations Manager alert.  
4. In the **Tasks** list, select **Search for Knowledge Articles**.  
5. In the **Knowledge Search** dialog, enter a search term in the **Search for** box, and select **Go**. For example, enter **MICR Check Printer Article**.  
6. Select the article, select **Link to \<IncidentName\>**, select **OK** to close the informational dialog, and select **Close**.  

### Validate incident edits  

- Open the incident, and then verify that your changes appear. For example, verify that the comment you entered appears as a log entry.  

## Contact a user from an incident form

In Service Manager, you can contact a user by Skype for Business when an incident form is open. The presence indicator is shown in the form next to the affected user's name, and it displays their current status, if known. For the presence indicator to accurately reflect a user's status, the user must have an Active&nbsp;Directory account, and the user must be a member of the same domain in which the Service Manager management server has its computer account. Additionally, the computer running the Service Manager console must have Skype for Business installed.  

> [!NOTE]  
> If a user's account belongs to a domain other than the domain in which the Service Manager management server has its computer account, the presence indicator might not accurately display the user's status.  

### Contact a user by instant message  

1. In an open incident form, select the presence indicator next to the **Affected user** box, and select the triangle next to the box.  
2. Select **Send Instant Message**.  
3. Your instant message program opens. Compose the instant message, and then send it.  

## Create an incident view and personalize it in Service Manager

In Service Manager, you can use the following procedures to create and personalize an incident view and then validate it.  

Views let you group incidents that share certain criteria. For example, the following procedure helps you create a view that lists all the incidents in which the classification has been set to **E\-mail Problems** or to some other classification. When you create a new view, it's saved and becomes available for later use.  

You can also personalize a view. However, when you personalize changes to a view, those changes aren't saved. For example, you can personalize the **All Incidents** view, but if you change column widths, column sorting, or grouping or if you remove columns, the next time you return to the view it displays information in the same manner as it did before you personalized it.  

### Create an incident view  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**.  
3. In the **Tasks** pane, select **Create View**.  
4. In the **General** section of the **Create View** dialog, enter a name for the view in the **Name** box. For example, enter **E\-mail Incidents**.  
5. In the **Description** box, enter a description. For example, enter **All incidents in which the classification is E\-Mail Problem**.  
6. Select **Criteria**.  
7. Next to the **Search for objects of a specific class** list, select **Browse**.  
8. In the **Select a Class** list, under **View**, select **Combination classes**, select **Incident \(Typical\)**, and select **OK**.  
9. In the **Related classes** box, ensure that **Incident** is selected. In the **Available properties** list, select **Classification Category**, and select **Add**. You might need to scroll to see the **Add** button.  
10. At the end of the **Criteria** section, in the **Criteria** definition area, select **E\-mail problems**. When the criterion is complete, it resembles **\[Incident\] Classification Category equals E\-Mail Problems**.  
11. Select **Display**, and in the **Columns to display** list, select **Status**, **Classification Category**, and **Description**. Next, under **Assigned To User**, select **Display Name**. Then, select **OK**.  

### Personalize an incident view  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**, and then select an incident view. For example, select **All Incidents**.  
3. Right\-click any view column heading to resize the columns, to remove items from the results, or to change column sorting and grouping. Repeat this step until you're satisfied with the results.  

### Validate the incident view creation  

- In the **Work Items** pane, ensure that an **E\-Mail Incidents** view exists under **Incident Management**. Ensure that the view displays all the incidents in the **E\-Mail Problems** category.  

    > [!NOTE]  
    > It might take a few seconds for the new incident view to appear.  

## Resolve and close an incident in Service Manager

In Service Manager, you can use the following procedures to resolve and close an incident and then validate that the incident was resolved and closed.  

After you research a problem and resolve its source, you can resolve and close the incident. An incident is considered resolved when the required change has been made. When the affected user has confirmed that the problem that caused the incident has been eliminated, the incident can be closed.  

### Resolve and close an incident  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**, and select **E\-Mail Incidents**.  
3. In the **E\-Mail Incidents** view, select the incident you want to resolve and close.  
4. In the **Tasks** pane, select **Change Incident Status** and select **Resolve**.  
5. In the **Resolve** dialog, select the appropriate category for resolving this incident in the **Resolution Category** list. For example, select **Fixed by higher tier support**.  
6. In the **Comments** box, enter a comment that explains the resolution. For example, enter **Resolved by installing Service Pack 1 on the Exchange server**, and select **OK**.  
7. In the **Tasks** pane, select **Change Incident Status** and then **Close**.  
8. In the **Close** dialog, enter a comment about the closure of the incident, and select **OK**.  

### Validate that an incident was resolved and closed  

- In the **All Incidents** pane, the status for the incident or incidents changes from **Active** to **Resolved** when you resolve an incident and from **Resolved** to **Closed** when you close the incident.  

    > [!NOTE]  
    > It might take a few seconds for the new status to appear. To immediately view the change, select **Refresh**.  

## Troubleshoot Service Manager incidents

You can use the following procedures to troubleshoot an incident in Service Manager using a service map. A service map is a visual representation of a service from the perspective of the business and user that shows critical dependencies, settings, and areas of responsibility. Because a service map can show the relationship between incidents and configuration items, it's especially useful when you troubleshoot issues that might affect multiple incidents and configuration items. For example, if an incident affects one configuration item, other configuration items that are part of the service might also be affected. If necessary, you can add additional configuration items as items that are affected by the same open incident.  

Additionally, when you use the **Service Components** tab to view the service map, you can easily determine whether there are active incidents or change requests open for a service component. When any incidents affect a service component, that component is marked with an orange icon resembling a square containing an exclamation point. When a change request affects a service component, the component is marked with a special blue icon resembling a square containing a right\-pointing arrow.  

### View incidents that affect service components  

1. In the Service Manager console, select **Configuration Items**.  
2. In the **Configuration Items** pane, expand **Business Services**, and select **All Business Services**.  
3. In the **All Business Services** list, double\-click a business service. For example, double\-click **Exchange Service**.  
4. In the dialog that opens, select the **Service Components** tab.  
    The list of service components includes configuration items. For example, the list might include computers running Microsoft Exchange&nbsp;Server. When a service component is marked with an icon, the icon indicates that an incident is associated with the service component.  
5. Select a configuration item that has a related work item. For example, select the **Exchange01.woodgrove.com** server.  
6. In the **Related work items for the selected item** list, select a work item to view, and select **Open**.  

### Add related service components to an open incident  

1. In the list of service components, select an item that has an active incident.  
2. Under **Related work items for the selected item**, select a work item, and select **Open** to open the incident.  
3. Under **Affected Items**, select **Add**.  
4. In the **Select objects** dialog, select the configuration item to add to the incident, select **Add**, and select **OK**.  
5. Select **OK** to update the incident, and then return to the **Service Components** tab for the service.  
6. Repeat the previous steps to add other service components to the open incident.  
7. Select **OK** to close the service item.  

### Validate that the service components were added to an incident  

- Open the business service to which you added the incident, and select the **Related Items** tab. Verify that the new incident appears under **Work items affecting this configuration item**.  

## Manage problems in Service Manager

The procedures in this section describe how to manage problems in Service Manager.  

In Service Manager, problems are records that are created to help prevent future problems and incidents from happening, to eliminate recurring incidents, and to minimize the impact of incidents that can't be prevented. Analysts can use the Service Manager console to create problem records and to associate incidents with problems.  

### Create and edit problem records

You can use the following procedures to create new problem records and then edit them by using the Service Manager console. You can create a new problem record from the Service Manager console, from an incident view, or from an incident form.  

#### Create a new problem record from the console  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Problem Management**, and select **Active Problems**.  
3. In the **Tasks** pane, select **Create Problem**.  
4. In the **Title** box, enter a title for the problem. For example, enter **Outlook E\-Mail Restricted Permissions**.  
5. In the **Description** box, enter a description of the problem. For example, enter **Users cannot view e\-mail messages sent with restricted permissions**.  
6. If you want to assign the problem to an analyst, enter the name of the analyst in the **Assigned to** box.  
7. In the **Source** list, select the source of the problem request.  
8. Select the appropriate values in the **Category**, **Impact**, and **Urgency** boxes.  
9. Select **OK**.  

#### Create a new problem record from an incident view  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Incident Management**, and select **All Incidents**.  
3. In the **All Incidents** list, search for incidents whose titles match the problem record that you want to create, and select **Search**. For example, search for **restricted permission**.  
4. In the search results, select the incidents for which you want to create a problem record. In the **Tasks** pane under **Selected Items**, select **Create Problem**.  
5. In the **Title** box, enter a title for the problem. For example, enter **Outlook E\-Mail Restricted Permissions**. When you create a problem by using this method, the problem form inherits the title from the open incident if a single incident was selected. If multiple incidents were selected, the **Title** box is blank. You can change the title of the problem record.  
6. In the **Description** box, enter a description of the problem. For example, enter **Users cannot view e\-mail messages sent with restricted permissions**.  
7. If you want to assign the problem to an analyst, enter the name of the analyst in the **Assigned to** box.  
8. In the **Source** list, select the source of the problem request.  
9. Select the appropriate values in the **Category**, **Impact**, and **Urgency** boxes.  
10. Select **OK**.  

#### Create a new problem record from an incident form  

1. Ensure that an incident is already open. Then, under **Tasks**, select **Create Problem**.  
2. In the **Title** box, enter a title for the problem. For example, enter **Outlook E\-Mail Restricted Permissions**. When you create a problem using this method, the problem form inherits the title from the open incident. You can change the title of the problem record.  
3. In the **Description** box, enter a description of the problem. For example, enter **Users cannot view e\-mail messages sent with restricted permissions**.  
4. If you want to assign the problem to an analyst, enter the name of the analyst in the **Assigned to** box.  
5. In the **Source** list, select the source of the problem request.  
6. Select the appropriate values in the **Category**, **Impact**, and **Urgency** boxes.  
7. Select **OK**.  

#### Edit a problem record  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Problem Management**, and select **Active Problems**.  
3. In the **Active Problems** view, double\-click a problem. For example, double\-click the **Outlook E\-Mail Restricted Permissions** problem.  
4. In the problem form, edit information that needs to be changed. For example, if a workaround is found for the problem, select the **Resolution** tab. Then, in the **Workarounds** field, enter the workaround steps.  
5. Select **OK**.  

#### Validate the creation of a new problem record  

- In the **Tasks** list, select **Refresh** to view the new problem record, or open the problem record to view the revised information.

### Resolve problem records and related incidents automatically

You can use the following procedures to resolve a problem record and the incidents that are associated with it and then validate the resolution.  

#### Resolve a problem record and the incidents that are associated with it  

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Problem Management**, and select **Active Problems**.  
3. In the **Active Problems** view, double\-click the problem record that you want to resolve. Then, in the **Tasks** pane, select **Resolve**.  
4. Select the **Resolution** tab, and select to select the **Auto\-resolve all incidents associated with this problem** checkbox.  
5. In the **Resolution Category** box, select the appropriate category.  
6. In the **Resolution Description** box, enter a summary of the resolution for this problem record. For example, enter **Application of Exchange Server 2010 SP1 fixed the restricted permission problem that affected users across forests**.  
7. Select **OK**.  

#### Validate problem and incident resolution  

- Verify that the incidents associated with the problem record appear in the **All Incidents** view and that they have a status of **Resolved**.  

    > [!NOTE]  
    > It might take a few minutes for the incident status to be updated to **Resolved**.  

### Link an incident or change request to a problem record

You can use the following procedure to link an incident or change request to a problem record if you created a problem record without linking it to an existing incident or change request.  

To link an incident or change request to a problem record, do the following:

1. In the Service Manager console, select **Work Items**.  
2. In the **Work Items** pane, expand **Problem Management**, and select **Active Problems**.  
3. In the **Active Problems** view, double\-click a problem record. For example, double\-click the **Outlook E\-mail Restricted Permissions** problem record.  
4. In the problem form, select **Related Items** tab.  
5. Under **Work Items**, select **Add**.  
6. In the **Select objects** dialog, either select a work item or search for and select one or more work items to link to the problem record. Select **Add**, and select **OK**.  
7. Select **OK** to close the form.  

#### Validate the link  

- In the **Active Problems** view, open the problem record to which you linked a work item, select the **Related Items** tab, and then verify that the items you linked appear under **Work Items**.  

## Next steps

- [Manage changes and activities](changes-activities.md) by providing repeatable, predictable, and measured processes to implement change.
