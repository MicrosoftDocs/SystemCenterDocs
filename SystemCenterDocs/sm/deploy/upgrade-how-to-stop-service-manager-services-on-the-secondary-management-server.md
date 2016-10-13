---
title: How to Stop Service Manager Services on the Secondary Management Server
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
ms.assetid: b4f30bdb-d45e-4390-b873-509d0b012398
---

# How to Stop Service Manager Services on the Secondary Management Server

>Applies To: System Center 2016 - Service Manager

Use the following procedure to stop the Service Manager services.  

### To stop the Service Manager services  

1.  In the **Run** dialog box, in the **Open** text field, type **services.msc**, and then click **OK**.  

2.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services and for each one, click **Stop**:  

    1.  System Center Data Access Service  

    2.  System Center Management  

    3.  System Center Management Configuration  

3.  Open Windows Explorer.  

4.  Locate the folder \\Program Files\\Microsoft System Center\\Service Manager.  

5.  Delete the **Health Service State** folder and all of its contents.
