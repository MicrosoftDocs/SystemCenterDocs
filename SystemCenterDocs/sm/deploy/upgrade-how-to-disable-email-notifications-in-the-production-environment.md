---
title: How to Disable Email Notifications in the Production Environment
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1317d2e6-b47b-41c0-826b-f7a4b3adf11b
---

# How to Disable Email Notifications in the Production Environment

>Applies To: System Center 2016 - Service Manager

Use the following procedure to disable incoming and outbound E\-mail notifications in the production environment.  

### To disable the outbound E\-mail notifications  

1.  In the Service Manager console, click **Administration**.  

2.  In the **Administration** pane, expand **Notifications**, and then click **Channels**.  

3.  In the **Channels** pane, click **E\-Mail Notification Channel**.  

4.  In the **Tasks** pane, under **E\-Mail Notification Channel**, click **Properties** to open the **Configure E\-Mail Notification Channel** dialog box.  

5.  Clear the **Enable e\-mail notifications** check box.  

### To disable incoming E\-mail notifications  

1.  In the Service Manager console, select **Administration**.  

2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.  

3.  In the **Settings** pane, double\-click **Incident Settings**.  

4.  In the Incident **Settings** dialog box, click **Incoming E\-mail**.  

5.  Clear **Turn on incoming e\-mails processing**, and then click **OK**.
