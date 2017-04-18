---
title: View an Operations Manager Distributed Application Diagram in Visio 
description: This article describes how to export a distributed application diagram in Visio format for modification and presentation in a custom Visio dashboard.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 12/13/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 316d9611-b4a4-495f-8272-8273b6012efe
---

# View an Operations Manager distributed application diagram in Visio 

>Applies To: System Center 2016 - Operations Manager

When you export a distributed application from the System Center 2016 - Operations Manager  Operations console and then open it in Microsoft Visio with the Visio Add-in for Operations Manager, the diagram in the Visio document contains information about the health state of each object. This information is provided through a connection to Operations Manager.  

## Export distributed application diagram to Visio
  
1.  In the Operations console, open your diagram.  
  
2.  On the toolbar, click the **To Visio** icon.  
  
3.  Open the folder in which you want to save the diagram, type a file name, and then click **Save**.  
  
4.  In Visio, open the exported diagram.  
  
    Visio automatically contacts the management server.  
  
5.  If you are prompted, type the user credentials for the management server, and then click **OK**.  
  
    When the diagram opens, the External Data window appears in the lower pane of Visio. This window contains detailed information about the objects in the diagram, including the health state and the last time the object state was refreshed in the diagram.  
  
    You can drill into the status of any object by opening the Health Explorer in the Operations Manager Web console. To do this, right click the object and select **Health Explorer**. To see the alerts associated with this object, you can open the alerts view from within the Health Explorer. Before you can do this, make sure you have configured the address for the web console. See [Configure the Operations Manager Data Source in Visio](../../scom/manage-visio-addin-configure-datasource.md) for more information.  
  
    Now that you have the initial diagram in Visio, you can customize it by adding new shapes. You can add links to Operations Manager components by dragging an object from the External Data window to an image or drawing in the diagram. The data is automatically linked to the image.  
  
    You can also change the way that the health state data is displayed on an object. Select the object, and then click a data graphic on the right side of Visio.  
  
