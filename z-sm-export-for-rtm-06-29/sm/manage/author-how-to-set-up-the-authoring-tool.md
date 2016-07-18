---
title: How to Set Up the Authoring Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f835014e-3e38-4b57-ba71-9149667f288a


















---
# How to Set Up the Authoring Tool
The SCSM2012\_AuthoringTool\_RTM.exe program file contains the System Center 2016 - Service Manager Authoring Tool .msi installation package and support files. This includes the files that are required for customizing default System Center 2012 - Service Manager forms. Ensure that the user who will be running the Authoring Tool has access to the local folder that you used to extract the files from the SCSM2012\_AuthoringTool\_RTM.exe program file.  
  
 If Windows Error Reporting is enabled on the computer that is running the Authoring Tool, errors are reported automatically.  
  
### To install the Authoring Tool  
  
1.  Verify that the computer on which you plan to install the Authoring Tool meets the requirements that are described in [Requirements for the Authoring Tool](../../../sm/manage/author/Requirements-for-the-Authoring-Tool.md).  
  
2.  Download the [SCSM2012\_AuthoringTool\_RTM.exe](http://go.microsoft.com/fwlink/p/?LinkId=245126) program file from the Microsoft Download Center to the local computer on which you want to install the Authoring Tool. Double\-click **SCSM2012\_AuthoringTool\_RTM.exe**.  
  
3.  In the **WinZip Self\-Extractor – SCSM2012\_AuthoringTool\_RTM.exe** dialog box, type a path to which to extract the files, and then click **Unzip**.  
  
4.  Browse to the folder where you extracted the files, expand the **CDImage** folder, and locate **Setup.exe**. Double\-click **Setup.exe** to start Setup.  
  
5.  In the Service Manager Authoring Tool Setup Wizard, click **Install the Service Manager Authoring Tool**.  
  
6.  Continue through the **Product registration** and the **Installation location** pages.  
  
7.  On the **Prerequisites** page, if any prerequisite test fails, you must update the server to ensure that each prerequisite is met. If Microsoft Visual Studio 2008 Shell is not installed, click **Install Microsoft Visual Studio Shell 2008** to install the application.  
  
     Click **Check prerequisites again**, and fix any other problems until all prerequisite tests pass.  
  
8.  Continue through the **Use Microsoft Update to help keep your computer secure and up\-to\-date** pages.  
  
9. On the **Installation summary** page, click **Install** and wait for the installation to finish.  
  
### To start the Authoring Tool  
  
1.  On your desktop, click **Start**.  
  
2.  Click **Programs**, click **Microsoft System Center**, and then click **Service Manager 2012 Authoring**.  
  
3.  Click **Service Manager Authoring Tool**, and wait for the Authoring Tool to open.  
  
4.  In the **Class Browser** pane, click **Refresh**. This populates the browser with all the classes that are defined in management packs from the \<Installation folder\>\/Library folder. When you opened the Authoring Tool for the first time, this pane was empty.  
  
## See Also  
 [Overview of the Authoring Tool for System Center 2012 – Service Manager](../Topic/Overview%20of%20the%20Authoring%20Tool%20for%20System%20Center%202012%20%E2%80%93%20Service%20Manager.md)
