---
title: Configure the Operations Manager Data Source in Visio 2010
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b286c07-c702-4ff9-8e4c-2865b34cf53d
---
# Configure the Operations Manager Data Source in Visio 2010
Before Visio 2010 can interact with [!INCLUDE[om12long](./Token/om12long_md.md)], you need to configure [!INCLUDE[om12short](./Token/om12short_md.md)] as a data source for your Visio document. You also need to configure the [!INCLUDE[om12short](./Token/om12short_md.md)] web console address to enable opening the Health Explorer or Alert view directly from Visio. You need to configure these items for each Visio document you create.

> [!NOTE]
> This latest version of the Visio 2010 Add\-in also functions with [!INCLUDE[om2007r2short](./Token/om2007r2short_md.md)]. If installing this version with [!INCLUDE[om2007r2short](./Token/om2007r2short_md.md)], ensure that credentials and access are configured to communicate with the root management server \(RMS\).

### To configure the Operations Manager data source and web console address in Visio

1.  Open a new drawing in Visio.

2.  Click **Operations Manager** in the ribbon, and then click **Configure**.

3.  In the **Name** field, type the name of the management server.

4.  In the **Address** field, type the address for the web console. This is the console that is used to launch the Health Explorer and Alert view from Visio.

    If you do not know the address, and you have [!INCLUDE[om12short](./Token/om12short_md.md)] administrator privileges, click **Look up web console address**. If you do not know the address, and you are not an [!INCLUDE[om12short](./Token/om12short_md.md)] administrator, contact the administrator for the address, and then type it in the **Address** field.

5.  If you want to receive regular updates of state information from the management server, select **Automatically refresh data**, and then specify a refresh interval in seconds.

6.  Click **OK**.


