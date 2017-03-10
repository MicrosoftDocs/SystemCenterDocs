---
title: Set file attachment limits
description: Describes how you can set file attachment limits in Service Manager.
manager: carmonm
ms.topic: article
author: bandersmsft
ms.author: banders
ms.prod: system-center-2016
keywords:  
ms.date: 10/12/2016
ms.technology: service-manager
ms.assetid: f6e881e6-9365-4d27-8221-89229a96c22d
---

# Set file attachment limits in Service Manager

>Applies To: System Center 2016 - Service Manager

Use the following procedure to limit the number and size of files that can be attached to an incident in Service Manager. In this example, set the maximum number of files to 5 and the maximum file size to 500 kilobytes (KB).

### To set file attachment limits

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.

3.  In the **Settings** pane, click **Incident Settings**.

4.  In the **Tasks** pane, under **Incident Settings**, click **Properties**.

5.  In the **Incident Settings** dialog box, click **General**.

6.  Set **Maximum number of attached files** to **5**.

7.  Set **Maximum size (KB)** to **500**, and then click **OK**.

### To validate file attachment limits

-   When you create a new incident or edit an existing one, no more than five files can be attached, and each file can be no larger than 500 KB.
