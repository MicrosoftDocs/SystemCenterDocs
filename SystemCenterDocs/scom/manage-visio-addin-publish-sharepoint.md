---
title: Publish a Visio diagram to SharePoint Server
description: This article describes how to publish a Visio diagram created with the add-in to your SharePoint document library.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 02/16/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 4c5bb8ee-725f-4ff2-ba85-21e689bcc1de
---

# Publish a Visio diagram to SharePoint Server

With the Visio Add-in installed on the client and the data provider installed on the SharePoint server, you can now publish diagrams that you have connected to Operations Manager data to a SharePoint document library to share them with others in your organization.  
  
### To publish a diagram to a SharePoint document library  
  
1.  From the **File** tab on the Visio ribbon, click **Save & Send**.  
  
2.  Click **Save to SharePoint**.  
  
3.  Click **Browse for a location** to specify where to save the diagram.  
  
4.  Under **File Types**, choose **Web Drawing (*.vdw)**.  
  
    If you do not choose this option, the drawing will not be visible through a browser, only the client.  
  
5.  Click **Save As**.  
  
6.  Specify the name and location for the file. To browse to a SharePoint server, type the name of the SharePoint server in the address field and click **Go To**.  
  
7.  Click **Save**.  
  
When the diagram is saved to a document library, you can simply browse to the document library in your browser and click the link to the document. The Visio diagram will open in your browser. With the data provider installed, the data will be refreshed directly from the management server.  
  
> [!NOTE]
> When viewing a published Visio diagram on SharePoint, when you select a linked shape it will open the Operations Manager Web console and direct you to the homepage rather than Health Explorer.  This is a known issue currently being investigated.         
> 

