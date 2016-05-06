---
title: How to Configure Microsoft SharePoint for Analytics
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1bc6fd91-6339-4bbf-9d7a-9c6098836542
robots: noindex,nofollow
---
# How to Configure Microsoft SharePoint for Analytics
Microsoft SharePoint 2010 not only stores Excel workbooks that contain [!INCLUDE[smshort](./Token/smshort_md.md)] Microsoft Online Analytical Processing \(OLAP\) data cubes in document libraries, but it is also used to render Excel workbooks with the use of a web browser. Using SharePoint makes it possible for [!INCLUDE[smshort](./Token/smshort_md.md)] users that do not have Excel to get access to the information they need. It also enables quick and easy access from mobile devices.

> [!NOTE]
> You must already have Microsoft SharePoint 2010 for Internet Sites Enterprise installed to perform this procedure.

### To enable Excel Services on SharePoint 2010

1.  Click **Start**, and then click **SharePoint 2010 Central Administration**.

2.  Under **System Settings**, click **Manage farm features**.

3.  Ensure that both the **Excel Services Application View Farm Feature** and **Excel Services Application Web Part Farm Feature** are set to **Active**. If they are not set to **Active**, click **Activate**.

## See Also
[Managing the Data Warehouse in System Center 2012 - Service Manager](./Managing-the-Data-Warehouse-in-System-Center-2012---Service-Manager.md)


