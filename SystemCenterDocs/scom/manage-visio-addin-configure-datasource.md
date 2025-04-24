---
title: Configure the Operations Manager Data Source in Visio
description: This article describes how to configure Visio to communicate with Operations Manager so that you can include monitored object health state in a drawing.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/24/2025
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: 2b286c07-c702-4ff9-8e4c-2865b34cf53d
---
# Configure the Operations Manager data source in Visio

This article describes how to configure Visio to communicate with Operations Manager so that you can include monitored object health state in a drawing.

Before Visio can interact with System Center - Operations Manager, you need to configure Operations Manager as a data source for your Visio document. You also need to configure the Operations Manager Web console address to enable opening the Health Explorer or Alert view directly from Visio. You need to configure these items for each Visio document you create.  

## Configure the Operations Manager data source and web console address in Visio  

To configure the Operations Manager data source and web console address in Visio, follow these steps:

1.  Open a new drawing in Visio.  

2.  Select **Operations Manager** in the ribbon, and select **Configure**.  

3.  In the **Name** field, enter the computer name of a management server in the management group.  

4.  In the **Address** field, enter the address for the web console. This is the console that is used to launch the Health Explorer and Alert view from Visio.  

    If you don't know the address, and you've Operations Manager administrator privileges, select **Look up web console address**. If you don't know the address, and you aren't an Operations Manager administrator, contact the administrator for the address, and then enter it in the **Address** field.  

5.  If you want to receive regular updates of state information from the management server, select **Automatically refresh data**, and then specify a refresh interval in seconds.  

6.  Select **OK**.  
