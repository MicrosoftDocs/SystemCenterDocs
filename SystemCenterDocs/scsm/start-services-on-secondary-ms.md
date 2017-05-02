---
title: Start Service Manager services on the secondary management server
description: You need to start Service Manager services on the secondary management server before you upgrade.
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
ms.assetid: c6eecbd1-f867-4050-b66f-de9427410bb7
---

# Start Service Manager services on the secondary management server before you upgrade

>Applies To: System Center 2016 - Service Manager

Use the following procedure to start the Service Manager services.  

### To start Service Manager services  

1.  On the Windows desktop, click **Start**, and then click **Run**.  

2.  In the **Run** dialog box, in the **Open** field, type **services.msc**, and then click **OK**.  

3.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services and for each one, click **Start**:  

    -   System Center Data Access Service  

    -   System Center Management  

    -   System Center Management Configuration
