---
title: Configure the Operations Manager Data Source in Visio 
description: This article describes how to configure Visio to communicate with Operations Manager so that you can include monitored object health state in a drawing.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 12/13/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 2b286c07-c702-4ff9-8e4c-2865b34cf53d
---
# Configure the Operations Manager data source in Visio 

>Applies To: System Center 2016 - Operations Manager

Before Visio can interact with System Center 2016 - Operations Manager, you need to configure Operations Manager as a data source for your Visio document. You also need to configure the Operations Manager Web console address to enable opening the Health Explorer or Alert view directly from Visio. You need to configure these items for each Visio document you create.  
  
## To configure the Operations Manager data source and web console address in Visio  
  
1.  Open a new drawing in Visio.  
  
2.  Click **Operations Manager** in the ribbon, and then click **Configure**.  
  
3.  In the **Name** field, type the computer name of a management server in the management group.  
  
4.  In the **Address** field, type the address for the web console. This is the console that is used to launch the Health Explorer and Alert view from Visio.  
  
    If you do not know the address, and you have Operations Manager administrator privileges, click **Look up web console address**. If you do not know the address, and you are not an Operations Manager administrator, contact the administrator for the address, and then type it in the **Address** field.  
  
5.  If you want to receive regular updates of state information from the management server, select **Automatically refresh data**, and then specify a refresh interval in seconds.  
  
6.  Click **OK**.  
  
