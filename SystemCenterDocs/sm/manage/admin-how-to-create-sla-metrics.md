---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 10/12/2016
title:  How to Create or Edit SLA Metrics
ms.technology:  service-manager
ms.assetid:  6215e448-568f-4956-8d4c-60b685ce9d3e
---

# How to Create or Edit SLA Metrics

>Applies To: System Center 2016 - Service Manager

In Service Manager you create a service level management metric, which is analogous to service level agreements (SLAs), as a time metric to measure the difference between start and end times for incidents and service requests. After you define a metric, you associate it with a service level objective. If the metric is already associated with a service level objective, it appears in the **Related SLA(s)** area.

### To create a metric for incidents

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Service Level Management**, and then click **Metric**.

3.  In the **Create/Edit SLA Metric** dialog box, in the **Title** box, type a title for the metric. For example, type **Incident Metric**.

4.  In the **Description** box, type a description of the metric. For example, type **Time that incidents are resolved**.

5.  Under **Class**, click **Browse** to open the **Select a Class** dialog box, select **Incident**, and then click **OK** to close the dialog box.

6.  Click the list next to **Start date** and then select the item that you want to use to define the start date. For example, select **First assigned date**.

7.  Click the list next to **End date**, and then select the item that you want to use to define the end date. For example, select **Resolved date**.

8.  Click **OK** to close the **Create/Edit SLA Metric** dialog box.

### To create a metric for service requests

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Service Level Management**, and then click **Metric**.

3.  In the **Create/Edit SLA Metric** dialog box, in the **Title** box, type a title for the metric. For example, type **Service Request Metric**.

4.  In the **Description** box, type a description of the metric. For example, type **Time that service requests are completed**.

5.  Under **Class**, click **Browse** to open the **Select a Class** dialog box, select **Service Request**, and then click **OK** to close the dialog box.

6.  Click the list next to **Start date**, and then select the item that you want to use to define the start date. For example, select **First assigned date**.

7.  Click the list next to **End date**, and then select the item that you want to use to define the end date. For example, select **Completed date**.

8.  Click **OK** to close the **Create/Edit SLA Metric** dialog box.

## How to Edit SLA Metrics

In Service Manager, you edit a service level agreement (SLA) metric to update the title, start date, and end date. After you edit a metric, you associate it with a service level objective. If the metric is already associated with a service level objective, it appears in the **Related SLA(s)** area.

> [!NOTE]
> You should avoid making changes to an SLA metric that is in use because changing it might cause performance problems. If possible, edit in-use SLA metrics during a period of minimal system use, such during as a maintenance period.

### To edit an SLA metric

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Service Level Management**, and then click **Metric**.

3.  In the **Metric** list, select an existing metric, and then in the **Tasks** pane, under *MetricName*, click **Properties**.

4.  In the **Create/Edit Metric** dialog box, modify any of the following items, as needed:

    -   **Title**

    -   **Description**

    -   **Start date**

    -   **End date**

5.  Click **OK** to close the **Create/Edit Metric** dialog box.
