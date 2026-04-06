---
title: Publish a Visio diagram to SharePoint Server
description: This article describes how to publish a Visio diagram created with the add-in to your SharePoint document library.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency3
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: 4c5bb8ee-725f-4ff2-ba85-21e689bcc1de
---

# Publish a Visio diagram to SharePoint Server



With the Visio Add-in installed on the client and the data provider installed on the SharePoint server, you can now publish diagrams that you've connected to Operations Manager data to a SharePoint document library to share them with others in your organization.  

## To publish a diagram to a SharePoint document library  

1.  From the **File** tab on the Visio ribbon, select **Save & Send**.  

2.  Select **Save to SharePoint**.  

3.  Select **Browse for a location** to specify where to save the diagram.  

4.  Under **File Types**, choose **Web Drawing (*.vdw)**.  

    If you don't choose this option, the drawing won't be visible through a browser, only the client.  

5.  Select **Save As**.  

6.  Specify the name and location for the file. To browse to a SharePoint server, enter the name of the SharePoint server in the address field, and select **Go To**.  

7.  Select **Save**.  

When the diagram is saved to a document library, you can browse to the document library in your browser and select the link to the document. The Visio diagram will open in your browser. With the data provider installed, the data will be refreshed directly from the management server.  

> [!NOTE]
> When viewing a published Visio diagram on SharePoint, when you select a linked shape it will open the Operations Manager Web console and direct you to the homepage rather than the Health Explorer. This is a known issue currently being investigated.
>

## Next steps

[Learn how to customize the way health state is represented in Visio](manage-visio-addin-change-healthstate-datagraphic.md)
