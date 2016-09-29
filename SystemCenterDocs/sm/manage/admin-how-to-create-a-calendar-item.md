---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  How to Create or Edit a Calendar Item
ms.technology:  service-manager
ms.assetid:  b06ad28d-a10f-475a-9bce-ade1197cd169
---

# How to Create or Edit a Calendar Item

>Applies To: System Center 2016 - Service Manager

You create a calendar item to define work days, work hours, and holidays in Service Manager. After you create a calendar item, you will use it as part of a service level objective, where it is measured against a time metric.

### To create a calendar item

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Service Level Management**, and then click **Calendar**.

3.  In the **Tasks** pane, under **Calendar**, click **Create Calendar**.

4.  In the **Create/Edit Calendar** dialog box, in the **Title** box, type a title for the calendar. For example, type **Normal Work Calendar**.

5.  In the **Time zone** list, select the time zone of your location.

6.  Under **Working days and hours**, select the work days of your organization and for each selected day, type the start and end time for each day.

7.  Under **Holidays**, click **Add** to define any holidays that your organization does not normally work. In the **Add Holiday** dialog box, type the name and select the date of the holiday and then click **OK** to close the dialog box.

8.  Click **OK** to close the **Create/Edit Calendar** dialog box.

## How to Edit a Calendar Item

You edit a calendar item in Service Manager to update work days, work hours, and holidays. After you edit a calendar item, you will use it as part of a service level objective, where it is measured against a time metric. If the calendar is already associated with a service level objective, it appears in the **Related SLA(s)** area.

> [!NOTE]
> When you update an existing calendar item, the update is effective for incidents and service requests created afterward; however, the updates do not affect existing incidents.

### To edit a calendar item

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Service Level Management**, and then click **Calendar**.

3.  In the Calendar list, select an existing calendar, and then in the **Tasks** pane, under *CalendarName*, click **Properties**.

4.  In the **Create/Edit Calendar** dialog box, modify any of the following items, as needed:

    -   **Title**

    -   **Time zone**

    -   **Working days and hours**

    -   **Holidays**

5.  Click **OK** to close the **Create/Edit Calendar** dialog box.
