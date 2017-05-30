---
title: Configure Service Level Management
description: Learn about configuring Service Level Management in Service Manager.
manager:  carmonm
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology:  service-manager
ms.assetid:  a8f84795-11fd-4c62-8f50-0929cedd3b20
---

# Configure Service Level Management

>Applies To: System Center 2016 - Service Manager

This article provides an overview of how to configure service level management in Service Manager. This section also contains procedures that cover service level management configuration scenarios.

Service level management is the process that you use to measure incident and service request timeliness. In Service Manager, you create a service level item that consist of queues that correspond to each service level, plus time metrics to measure and warn for. Separately, you can also send notifications to users that occur before and after service level breach. In the Service Manager console, you manage this process in the Administration workspace using the following nodes:

-   Calendar
-   Metric
-   Service Level Objectives

## Calendar

The Calendar node is used to define work days, work hours, and holidays as a calendar item in the Service Manager console. Each calendar item is a distinct work schedule that represents time available for analysts to resolve incidents and fulfill service requests. Calendar items correspond to at least one service level objective where it is measured by a time metric, such as resolution time.

## Metric

The Metric node is used to define time metrics against a calendar item, corresponding to a service level objective. A time metric is the measurement between start and end dates. There are two predefined metrics in Service Manager:

-   Resolution Time

-   Completion Time

The Resolution Time metric is used to measure the maximum length of time that incidents should take before they are resolved. By default, the two points in time that define Resolution Time are the start date as the date and time that each incident is created and the end date as the date and time that each incident is resolved.

The Completion Time metric is used to measure the maximum length of time that service requests should take before they are completed. By default, the two points in time that define Completion Time are the start date as the date and time that each service request is created and the end date as the date and time that each service request is completed.

## Service level objectives

The Service Level Objectives node is used to create relationships between a queue and a service level. It is also used to define the relationship between a calendar item and a time metric. Separately, you can also send notifications to users that occur before and after service level breach.

## Create or edit a calendar item

You create a calendar item to define work days, work hours, and holidays in Service Manager. After you create a calendar item, you will use it as part of a service level objective, where it is measured against a time metric.

#### To create a calendar item

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Service Level Management**, and then click **Calendar**.
3.  In the **Tasks** pane, under **Calendar**, click **Create Calendar**.
4.  In the **Create/Edit Calendar** dialog box, in the **Title** box, type a title for the calendar. For example, type **Normal Work Calendar**.
5.  In the **Time zone** list, select the time zone of your location.
6.  Under **Working days and hours**, select the work days of your organization and for each selected day, type the start and end time for each day.
7.  Under **Holidays**, click **Add** to define any holidays that your organization does not normally work. In the **Add Holiday** dialog box, type the name and select the date of the holiday and then click **OK** to close the dialog box.
8.  Click **OK** to close the **Create/Edit Calendar** dialog box.

### Edit a calendar item

You edit a calendar item in Service Manager to update work days, work hours, and holidays. After you edit a calendar item, you will use it as part of a service level objective, where it is measured against a time metric. If the calendar is already associated with a service level objective, it appears in the **Related SLA(s)** area.

> [!NOTE]
> When you update an existing calendar item, the update is effective for incidents and service requests created afterward; however, the updates do not affect existing incidents.

#### To edit a calendar item

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Service Level Management**, and then click **Calendar**.
3.  In the Calendar list, select an existing calendar, and then in the **Tasks** pane, under *CalendarName*, click **Properties**.
4.  In the **Create/Edit Calendar** dialog box, modify any of the following items, as needed:
    -   **Title**
    -   **Time zone**
    -   **Working days and hours**
    -   **Holidays**
5.  Click **OK** to close the **Create/Edit Calendar** dialog box.

## Create or edit SLA metrics

You can create a service level management metric, which is analogous to service level agreements (SLAs), as a time metric to measure the difference between start and end times for incidents and service requests. After you define a metric, you associate it with a service level objective. If the metric is already associated with a service level objective, it appears in the **Related SLA(s)** area.

#### To create a metric for incidents

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Service Level Management**, and then click **Metric**.
3.  In the **Create/Edit SLA Metric** dialog box, in the **Title** box, type a title for the metric. For example, type **Incident Metric**.
4.  In the **Description** box, type a description of the metric. For example, type **Time that incidents are resolved**.
5.  Under **Class**, click **Browse** to open the **Select a Class** dialog box, select **Incident**, and then click **OK** to close the dialog box.
6.  Click the list next to **Start date** and then select the item that you want to use to define the start date. For example, select **First assigned date**.
7.  Click the list next to **End date**, and then select the item that you want to use to define the end date. For example, select **Resolved date**.
8.  Click **OK** to close the **Create/Edit SLA Metric** dialog box.

#### To create a metric for service requests

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Service Level Management**, and then click **Metric**.
3.  In the **Create/Edit SLA Metric** dialog box, in the **Title** box, type a title for the metric. For example, type **Service Request Metric**.
4.  In the **Description** box, type a description of the metric. For example, type **Time that service requests are completed**.
5.  Under **Class**, click **Browse** to open the **Select a Class** dialog box, select **Service Request**, and then click **OK** to close the dialog box.
6.  Click the list next to **Start date**, and then select the item that you want to use to define the start date. For example, select **First assigned date**.
7.  Click the list next to **End date**, and then select the item that you want to use to define the end date. For example, select **Completed date**.
8.  Click **OK** to close the **Create/Edit SLA Metric** dialog box.

### Edit SLA metrics

In Service Manager, you edit a service level agreement (SLA) metric to update the title, start date, and end date. After you edit a metric, you associate it with a service level objective. If the metric is already associated with a service level objective, it appears in the **Related SLA(s)** area.

> [!NOTE]
> You should avoid making changes to an SLA metric that is in use because changing it might cause performance problems. If possible, edit in-use SLA metrics during a period of minimal system use, such during as a maintenance period.

#### To edit an SLA metric

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Service Level Management**, and then click **Metric**.
3.  In the **Metric** list, select an existing metric, and then in the **Tasks** pane, under *MetricName*, click **Properties**.
4.  In the **Create/Edit Metric** dialog box, modify any of the following items, as needed:
    -   **Title**
    -   **Description**
    -   **Start date**
    -   **End date**
5.  Click **OK** to close the **Create/Edit Metric** dialog box.

## Modify an SLA metric view

You can use the following procedures to customize an SLA view.

Views let you group SLA metrics that share certain criteria. However, when you personalize changes to a view, those changes are not saved. For example, you can customize the **Metrics** view, but if you change column widths, column sorting, grouping, or if you remove columns, the next time you return to the view it displays information in the same manner as it did before you personalized it.

### To personalize an SLA metric view

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Service Level Management**, and then select **Metric**.
3.  Right-click any view column heading to resize columns, to remove items from the results, or to change column sorting and grouping. Repeat this step until you are satisfied with the results.
4.  You can also type in the **Filter** box to show results that are limited items that match what you typed.

## Create or edit a service level objective

You create a service level objective to create relationships between a queue and a service level, a calendar item and a time metric, and actions that occur before or after service level breaches. Afterward, when you view incidents or service requests and they approach their warning time, you will see a notification bar stating that the item is about to breach. You can also create periodic notifications if you want analysts to receive email for incidents or service requests that might breach their service level objective. For more information about sending notifications, see [How to Send SLA Notification Information to the Assigned-To User](send-sla-info.md).

In order to create a service level objective, it is easier if you have already created or defined a calendar item and an SLA metric. Additionally, the service level objective that you create is linked to a queue. The queue that you associate to a service level objective must target the same type of work item, based on its class; otherwise, the queue will not be available when you create the service level objective.

#### To create a service level objective

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Service Level Management**, and then click **Service Level Objective**.
3.  In the **Tasks** pane, under **Service Level Objectives**, click **Create Service Level Objective**.
4.  In the Create Service Level Objective Wizard, on the **Before You Begin** page, click **Next**.
5.  On the **General** page, in the **Title** box, type a name for the new service level objective.
6.  In the **Description** box, type a description of the service level objective.
7.  Next to **Class**, click **Browse** to Open the **Select a Class** dialog box and then select a class pertinent to the type of service level objective you are creating. Normally, you should choose either **Incident** or **Service Request**.
8.  Ensure that **Enabled** is selected, and then click **Next**.
9. On the **Service Level Criteria** page, select a calendar and a time metric, or you can create new ones.
10. Under **Target**, specify the amount of time in hours or minutes that the work item should be completed by.
11. Under **Warning threshold**, specify the amount of time in hours or minutes before the service level is beached, which causes a warning notification in the work item notification bar, and then click **Next**.
12. On the **Summary** page confirm the choices you made, and then click **Create**.
13. On the **Completion** page, click **Close**.

### Edit a service level objective

You can edit a service level objective to modify relationships between a queue and a service level, a calendar item and a time metric, and actions that occur before or after service level breaches. Afterward, when you view incidents or service requests and they approach their warning time, you will see a notification bar stating that the item is about to breach. You can also create periodic notifications if you want analysts to receive email for incidents or service requests that might breach their service level objective.

The service level objective that you edit is linked to a queue. If you want to modify the association of queue to a service level objective, the service level objective must target the same type of work item as the queue, based on its class; otherwise, the queue will not be available when you modify the service level objective.

#### To modify a service level objective

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Service Level Management**, and then click **Service Level Objective**.
3.  In the **Service Level Objectives** list, select an existing service level objective, and then in the **Tasks** pane, under *ServiceLevelObjectiveName*, click **Properties**.
4.  In the **Edit SLO** dialog box, modify any of the following items, as needed.
    -   **Title**
    -   **Queues**
    -   **Service Level Criteria**
5.  Click **OK** to close the **Edit SLO** dialog box.

## View SLA information in an incident form

As you are working with incidents, it is easy to tell when an incident's service level is about to or has been breached by viewing incidents in the **Assigned To Me** view and then looking for information in the **Service Level Target** column.

If you are already in an incident form and an incident is about to breach, a notification bar is displayed in the form while on the **General** tab stating that **One or more Service Level Objectives are about to breach.** You can view additional information about the service level status on the corresponding tab and see that the status shown is a warning.

When an incident has already been breached, no notification bar is displayed in the form while you are on the **General** tab. However, you will see breached status while you are on the **Service Level** tab if that incident's service level objective has breached.

### To view warning SLA information in an incident form

1.  In the Service Manager console, click **Work Items**.
2.  In the **Work Items** pane, expand **Incident Management**, and then click **Incidents with Service Level Warning**.
3.  In the **Incidents with Service Level Warning** list, select an incident, and then in the **Tasks** pane, under *IncidentID-IncidentName*, click **Edit**.
4.  In the *Incident IncidentID-IncidentName - Status* form, observe the **One or more Service Level Objectives are about to breach** warning.
5.  Click the **Service Level** tab, and observe the status of the incident as **Warning**. You can also see other information about the incident, most notably **Time Before SLA Breached**.
6.  Click **OK** to close the incident.

### To view breached SLA information in an incident form

1.  In the Service Manager console, click **Work Items**.
2.  In the **Work Items** pane, expand **Incident Management**, and then click **Incidents with Service Level Breached**.
3.  In the **Incidents with Service Level Breached** list, select an incident, and then in the **Tasks** pane, under *IncidentID-IncidentName*, click **Edit**.
4.  Click the **Service Level** tab, and observe the status of the incident as **Breached**.  
5.  Click **OK** to close the incident.  

## Review incidents with SLA information

You can use the following procedure to view incidents that have a service level objective associated with them.

### To review incidents with SLA information

1.  In the Service Manager console, click **Work Items**.
2.  In the **Work Items** pane, expand **Incident Management**, and then click **Incidents with Service Level Warning** or **Incidents with Service Level Breached**.
3.  In the list of incidents, notice the time that is displayed for **Service Level Target**.

## Send SLA notification information to the assigned-to user

You can send notifications to analysts who are responsible for incidents when each incident is within the warning period of its service level objective. Because periodic notifications require a large amount of system resources, the following example notifies the analyst once when the service level objective goes to a warning state.

### To send an SLA notification to the assigned-to user

1.  In the Service Manager console, click **Administration**.
2.  In the **Administration** pane, expand **Notifications**, and then click **Subscriptions**.
3.  In the **Tasks** pane, click **Create Subscription** to open the Create E-Mail Notification Subscription Wizard.
4.  On the **Before You Begin** page, read the instructions, and then click **Next**.
5.  On the **General** page, complete these steps:
    1.  In the **Notification subscription name** box, type a name for the subscription for the service level objective.
    2.  In the **Description** box, type a description of the subscription for the service level objective.
    3.  In the **When to notify** list, select **When an object of the selected class is updated**.
    4.  Next to **Targeted class** click **Browse** and then in then in the **Frequently used basic classes** list, select **All basic classes**. In the **Select a Class** dialog box, click **Service Level Instance Time Information**, and then click **OK** to close the dialog box.
    5.  Keep the default management pack information, and then click **Next**.
6.  On the **Group/Queue Selection** page, click **Next**.
7.  On the **Additional Criteria** page, complete these steps:
    1.  In the **Changed From** tab, set **[Service Level Instance Time Information] Status Does Not Equal Warning**.
    2.  On the **Changed To** tab, set **[Service Level Instance Time Information] Status Equals Warning**, and then click **Next**.
8.  On the **Template** page, select an email template or create a new one targeted at the Service Level Instance Time Information class. For more information about creating email notification templates, see [How to Create Notification Templates](create-notification-templates.md). Click **Next**.
9. On the **Recipient** page, click **Add** and select the groups and users to send the notification to, and then click **Next**.
10. On the **Related Recipient** page, click **Add**, select **[WorkItem]WorkItem has Service Level Instance Information** in the left box, and then select **Primary Owner** and **Assigned To User** in the right box, and then click **Next**.
11. On the **Summary** page, review the information, and then click **Create**.
12. On the **Completion** page, click **OK** to close the wizard.

## Reactivate incidents with SLA information

You can reactivate resolved incidents that have an associated service level objective. However, keep in mind that the original date and time that the incident was opened is preserved. Consequently, the time that elapsed while the incident was resolved continues to apply against the service level objective--possibly resulting in the service level objective being breached.

### To reactivate an incident with SLA information

1.  In the Service Manager console, click **Work Items**.
2.  In the **Work Items** pane, expand **Incident Management**, and then click **All** .
3.  In the **All Incidents** list, locate a resolved incident that you want to reactivate, and select it.
4.  In the **Tasks** list, under **&lt;IncidentID - IncidentTitle&gt;**, click **Change Incident Status**, and then select **Activate**.
5.  In the **Activate** box, type a comment describing why you are activating the incident, and then click **OK**.

## Next steps

- [Configure workflows](workflows.md) to create a sequence of activities that automate a business process.
