---
title: Install the Visio Services Data Provider
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b1c21ab-529b-4c04-9384-717a503f3df7
author:mgoedtel
manager:cfreemanwa
---
# Install the Visio Services Data Provider
The Visio Services Data Provider for [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] leverages SharePoint 2010’s Visio Services to enable Visio diagrams to show live health state from [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] in SharePoint.  
  
The Visio Services Data Provider for [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] has the following prerequisites:  
  
-   System Center 2012 – Operations Manager, Operations or Authoring console  
  
-   SharePoint 2010 Enterprise  
  
-   [The Microsoft .NET Framework 3.5 SP1](http://go.microsoft.com/fwlink/?LinkID=131605)  
  
> [!NOTE]  
> You must install SharePoint Server 2010 in a farm environment versus standalone \(on a single server with a built\-in database by using the default settings\) so that Visio Services can be configured to run as a domain account with [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] access. For more information about installing SharePoint Server 2010 on a single server farm, see [Deploy a single server with SQL Server \(SharePoint Server 2010\)](http://go.microsoft.com/fwlink/?LinkID=102798). For more information about installing SharePoint Server 2010 on a multiple server farm, see [Multiple servers for a three\-tier farm \(SharePoint Server 2010\)](http://go.microsoft.com/fwlink/?LinkID=244297).  
  
### To install the Visio Services data provider  
  
1.  In Windows Explorer, navigate to the directory where you downloaded the Add\-in and then double\-click **the OpsMgrDataModuleSetup.msi**.  
  
2.  Read the license agreement, select **I Agree**, and then click **Next**.  
  
3.  Specify the installation location, and then click **Next**.  
  
    By default, files are extracted to the C:\\Program Files\\ directory. You can change this to any location.  
  
    > [!NOTE]  
    > The .msi program does not install or deploy the data provider to the SharePoint servers in the server farm. This program simply extracts the SharePoint deployment package to a location specified by the SharePoint administrator.  
  
4.  Open the SharePoint 2010 Management Shell as an administrator.  
  
5.  Run the following command:  
  
    ```  
    .\InstallOpsMgrDataModule.ps1  
    ```  
  
    > [!NOTE]  
    > The SharePoint 2010 Administration service must be running prior to running `.\InstallOpsMgrDataModule.ps1`  
  
    The `InstallOpsMgrDataModule` cmdlet installs the deployment package to the solution store for the server farm and then deploys the data module to each of the SharePoint servers in the server farm.  
  
6.  After the cmdlet has completed, you can verify that the package was successfully deployed by running the `get-spsolution` cmdlet. You should see “True” in the Deployed column next to the opsmgrdatamodule.wsp entry.  
  
7.  Start SharePoint Central Administration to verify that the data provider is listed as a Trusted Data Provider for Visio Services.  
  
