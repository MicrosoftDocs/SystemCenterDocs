---
title: Enable connectors in the lab environment
description: You need to enable the connectors in the lab environment before you upgrade.
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
ms.assetid: 20ec2aaa-9fee-463b-a1d7-9cb272d8dd73
---

# Enable the connectors in the lab environment before you upgrade

>Applies To: System Center 2016 - Service Manager

Use the following procedure to enable the Service Manager connectors in the lab environment. In this procedure, you will not be enabling the Operations Manager connector.  

> [!WARNING]  
>  Do not enable or delete the Operations Manager alert connector in the lab environment. Doing so will cause the alert connector in the production environment to fail.  

### To enable a connector  

1.  In the Service Manager console, click **Administration**.  

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.  

3.  In the **Connectors** pane, select the connector that you want to enable.  

4.  In the **Tasks** pane, under the connector name, click **Enable**.
