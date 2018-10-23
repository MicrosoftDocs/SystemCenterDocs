---
title: Install the Visio Add-in
description: This article describes how to install the Visio Add-in for Microsoft Visio.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 10/23/2018
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: ac69f3db-00ab-4ca3-a2fc-f87d4503f1ed
---

# Install the Visio Add-in

You can download the Visio Add-in from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=29268).  

>[!NOTE]
>While the page on the Download Center specifies System Center 2012, the add-in does support System Center 2016 - Operations Manager and version 1801. For version 1801, configuring the add-in to point to the HTLM5 web console is not supported and should continue referencing the System Center 2016 - Operations Manager Web console in order to support launching the Health Explorer and Alert view from Visio diagrams.   
>

The Visio Add-in for System Center Operations Manager has the following prerequisites:  
  
-   System Center 2016 - Operations Manager Operations console.  
  
-   Microsoft Office Visio 2010 or 2013 Professional or Premium.  
  
-   Microsoft .NET Framework 3.5 SP1.  For Windows 8, 8.1 and 10 see [Installing the .NET Framework 3.5 on Windows 8, Windows 8.1 and Windows 10](https://msdn.microsoft.com/library/hh506443%28v=vs.110%29.aspx). 
 
## To install the Visio Add-in
 
When you run the Setup program for the Visio Add-in, your system is checked against these requirements. If your system does not meet the requirements, a link is provided so that you can download the missing software.  
  
1.  In Windows Explorer, navigate to the directory where you downloaded the Add-in and then double-click **OpsMgrAddinSetup.msi**. This is the installation file for the client.  
  
2.  Click **Next** on the Welcome page of the installation wizard.  
  
3.  Read the license agreement, select **I Agree**, and then click **Next**.  
  
4.  Specify the installation location, and then click **Next**.  
  
5.  Click **Next** to start the installation.  
  
6.  Click **Close** when the installation is complete.  
  
The next time you start Visio, you are asked if you want to install the Visio Add-in. Click **Install**. When the installation is complete, the Operations Manager command is available in the Visio ribbon.  
  
