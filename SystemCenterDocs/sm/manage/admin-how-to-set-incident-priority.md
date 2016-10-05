---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  How to Set Incident Priority
ms.technology:  service-manager
ms.assetid:  ff64efdb-7923-451a-90a4-5e467bdbb17a
---

# How to Set Incident Priority

>Applies To: System Center 2016 - Service Manager

Use the following procedure in Service Manager to define a priority calculation table based on impact and urgency settings that are defined during the creation of an incident.

### To set incident priority

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.

3.  In the **Settings** pane, click **Incident Settings**.

4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.

5.  In the **Incident Settings** dialog box, select **Priority Calculation**.

6.  For each of the High, Medium, and Low settings for both impact and urgency, select an incident priority value from 1 through 9, and then click **OK**.

### To validate incident priority

-   When you create a new incident or edit an existing one, the resulting priority setting must match the value that is entered in the table for a specific High, Medium, and Low setting that is defined for impact and urgency.



