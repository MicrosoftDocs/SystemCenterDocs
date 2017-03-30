---
title: Link to Operations Manager Objects in a New or Existing Visio Document
description: This article provides a walk-through on how to create a basic monitoring drawing in Visio and link to Operations Manager objects.   
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 12/13/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: f5a4749c-e042-401c-86ae-f9830576fcf2
---

# Link to Operations Manager objects in a new or existing Visio document

>Applies To: System Center 2016 - Operations Manager

The Visio Add-in for System Center 2016 - Operations Manager lets you link to Operations Manager objects to present health state information in a new or existing Microsoft Visio drawing.   
  
To do this, you first specify a Operations Manager management server from which the Visio Add-in will query to get information about the managed objects and their health state. Then, you add the links by using one of the following methods:  
  
-   Link a single shape to a managed object. You can quickly link a few shapes to any object managed by Operations Manager.  
  
-   Add multiple links to the document and then associate these to Visio shapes later. This option works best for large documents that have many different types of managed object.  
  
-   Automatically link shapes in the document to computers or network devices. This option uses a single wizard to automatically add health state information to large and complex network or topology diagrams.  
  
-   Insert a new shape that is linked to an Operations Manager object and that uses the Operations Manager icons.  
  
## Link a single Visio shape to an object managed by Operations Manager  
  
1.  Click **Operations Manager** in the ribbon, and then click **Link Shape**.  
  
2.  Select the Operations Manager class of the object, such as **Windows Computer**, to display a filtered list of available Operations Manager objects.  
  
3.  Select the object that you want to link to this shape, and then click **Link**.  
  
The shape in the diagram now includes a state indicator in the upper-right corner of the image.  
  
## Add multiple links to objects managed by Operations Manager  
  
1.  Click **Operations Manager** in the ribbon, and then click **Add Data Links**.  
  
2.  Select the class for the shape, and then click **OK**.  
  
3.  Select the managed objects you want to link to this shape, and then click **Insert**.  
  
    This adds the selected managed objects to the dataset in the Visio diagram, which can be viewed in the External Data window.  
  
4.  In the External Data window, select the object that you want to connect to a shape in the diagram or image.  
  
    For example, if you want to add the management server for a geographic location to a map, select the management server.  
  
5.  Drag the object to the diagram or image and drop it onto the shape. This establishes the link between the shape and that managed object's record.  
  
## Automatically link multiple Visio shapes to Operations Manager managed computers and network devices  
  
1.  Open the Visio document.  
  
    Ensure that each shape has defined shape data, such as the network name or IP address, or shape text (such as the IP address of the object).  
  
    To view the shape data, right-click the shape, click **Data**, and then click **Shape Data**. This opens the Shape Data window for the selected shape.  
  
2.  Select all the shapes in the document.  
  
3.  Click **Operations Manager** in the ribbon, and then click **Reconcile Shapes**.  
  
4.  In the Automatically Link wizard, select **Selected shapes** or **All shapes in the document**, and then click **Next**.  
  
5.  Match the Visio shape property to the Operations Manager object property. For example, match the Visio network name to the Operations Manager object display name. The following Operations Manager classes are matched automatically:  
  
    -   Windows Computer (Microsoft.Windows.Computer)  
  
    -   Unix Computer (Microsoft.Unix.Computer)  
  
    -   SNMP Network Device (Microsoft.SystemCenter.NetworkDevice)  
  
    Click **Next**.  
  
6.  Review the list of matches. Click to clear any objects you do not want to link, and then click **Next**.  
  
    If more than one match is found, click **Select** to choose the object you want to link to. If no matches are found, click **Browse** to search for the object.  
  
7.  Review the list of links to define, and then click **Finish**.  
  
The shapes are automatically connected to the managed objects they represent on the management server.  
  
## Insert a shape that is linked to an Operations Manager object  
  
1.  In your Visio diagram, click **Operations Manager** in the ribbon, and then click **Insert shape**.  
  
2.  Select the class of the object you want to insert. This filters the available objects to only those of the specified class. You can also search for a specific object.  
  
3.  Select the specific object, and then click **Insert**.  
  
The new shape is added to the diagram. The shape icon matches those of other Operations Manager objects of the same class, and the shape data is populated with information from the management group.  
  
