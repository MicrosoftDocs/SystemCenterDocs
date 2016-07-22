---
title: Add Links to Operations Manager to a New or Existing Visio 2010 Document
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5a4749c-e042-401c-86ae-f9830576fcf2
author:mgoedtel
manager:cfreemanwa
---
# Add Links to Operations Manager to a New or Existing Visio 2010 Document
The Visio 2010 Add\-in for [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] lets you create a new Microsoft Office Visio document that you can link to [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] objects. The Visio Add\-in also lets you add live health state information to an existing Visio document.  
  
To do this, you first specify the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] management server from which the Visio Add\-in will get information about the managed objects and their health state. Then, you add the links by using one of the following methods:  
  
-   Link a single shape to a managed object. You can quickly link a few shapes to any object managed by [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)].  
  
-   Add multiple links to the document and then associate these to Visio shapes later. This option works best for large documents that have many different types of managed object.  
  
-   Automatically link shapes in the document to computers and to network devices. This option uses a single wizard to automatically add health state information to large and complex network or topology diagrams.  
  
-   Insert a new shape that is linked to an [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] object and that uses the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] icons.  
  
> [!NOTE]  
> This latest version of the Visio 2010 Add\-in also functions with [!INCLUDE[om2007r2short](../../om/manage/includes/om2007r2short_md.md)]. If installing this version with [!INCLUDE[om2007r2short](../../om/manage/includes/om2007r2short_md.md)], ensure that credentials and access are configured to the RMS instead of the management server.  
  
### To link a single Visio shape to an object managed by Operations Manager  
  
1.  Click **Operations Manager** in the ribbon, and then click **Link Shape**.  
  
2.  Select the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] class of the object, such as **Windows Computer**, to display a filtered list of available [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] objects.  
  
3.  Select the object that you want to link to this shape, and then click **Link**.  
  
The shape in the diagram now includes a state indicator in the upper\-right corner of the image.  
  
### To add multiple links to objects managed by Operations Manager  
  
1.  Click **Operations Manager** in the ribbon, and then click **Add Data Links**.  
  
2.  Select the class for the shape, and then click **OK**.  
  
3.  Select the managed objects you want to link to this shape, and then click **Insert**.  
  
    This adds the selected managed objects to the dataset in the Visio diagram, which can be viewed in the External Data window.  
  
4.  In the External Data window, select the object that you want to connect to a shape in the diagram or image.  
  
    For example, if you want to add the management server for a geographic location to a map, select the management server.  
  
5.  Drag the object to the diagram or image and drop it onto the shape. This establishes the link between the shape and that managed object's record.  
  
### To automatically link multiple Visio shapes to Operations Manager managed computers and network devices  
  
1.  Open the Visio document.  
  
    Ensure that each shape has defined shape data, such as the network name or IP address, or shape text \(such as the IP address of the object\).  
  
    To view the shape data, right\-click the shape, click **Data**, and then click **Shape Data**. This opens the Shape Data window for the selected shape.  
  
2.  Select all the shapes in the document.  
  
3.  Click **Operations Manager** in the ribbon, and then click **Reconcile Shapes**.  
  
4.  In the Automatically Link wizard, select **Selected shapes** or **All shapes in the document**, and then click **Next**.  
  
5.  Match the Visio shape property to the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] property. For example, match the Visio network name to the [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] display name. The following [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] classes are matched automatically:  
  
    -   Windows Computer \(Microsoft.Windows.Computer\)  
  
    -   Unix Computer \(Microsoft.Unix.Computer\)  
  
    -   SNMP Network Device \(Microsoft.SystemCenter.NetworkDevice\)  
  
    Click **Next**.  
  
6.  Review the list of matches. Click to clear any objects you do not want to link, and then click **Next**.  
  
    If more than one match is found, click **Select** to choose the object you want to link to. If no matches are found, click **Browse** to search for the object.  
  
7.  Review the list of links to define, and then click **Finish**.  
  
The shapes are automatically connected to the managed objects they represent on the management server.  
  
### To insert a shape that is linked to an Operations Manager object  
  
1.  In your Visio diagram, click **Operations Manager** in the ribbon, and then click **Insert shape**.  
  
2.  Select the class of the object you want to insert. This filters the available objects to only those of the specified class. You can also search for a specific object.  
  
3.  Select the specific object, and then click **Insert**.  
  
The new shape is added to the diagram. The shape icon matches those of other [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] objects of the same class, and the shape data is populated with information from the management server.  
  
