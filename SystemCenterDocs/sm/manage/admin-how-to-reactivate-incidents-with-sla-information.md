---
title: Reactivate incidents with SLA information
description: Describes how you can reactivate incidents with SLA information in Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: 7e121252-1728-4297-b41f-0b4e1ba92c57
---

# Reactivate incidents with SLA information in Service Manager

>Applies To: System Center 2016 - Service Manager

In Service Manager, you can reactivate resolved incidents that have an associated service level objective. However, keep in mind that the original date and time that the incident was opened is preserved. Consequently, the time that elapsed while the incident was resolved continues to apply against the service level objective--possibly resulting in the service level objective being breached.

### To reactivate an incident with SLA information

1.  In the Service Manager console, click **Work Items**.

2.  In the **Work Items** pane, expand **Incident Management**, and then click **All** .

3.  In the **All Incidents** list, locate a resolved incident that you want to reactivate, and select it.

4.  In the **Tasks** list, under **&lt;IncidentID - IncidentTitle&gt;**, click **Change Incident Status**, and then select **Activate**.

5.  In the **Activate** box, type a comment describing why you are activating the incident, and then click **OK**.
