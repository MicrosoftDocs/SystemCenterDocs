---
title: Step 5 - Bundle and Import the Custom Management Pack to Service Manager
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8388927-d818-4dbf-8351-5a1034913604
---

# Step 5 - Bundle and Import the Custom Management Pack to Service Manager

>Applies To: System Center 2016 - Service Manager

In this of the Woodgrove Bank customization scenario, Ken needs to bundle the management pack file with all the necessary resource files and then import the bundled file into Service Manager. When Service Manager imports a management pack, it validates the XML code in the management pack file and then imports the management pack only if it is valid.  

### To bundle the management pack file with its associated resource files  

1.  Ensure that the Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml file and its associated resource files, such as the Woodgrovebank.jpg image file and the AddComputerToGroupFormAssembly.dll file, are in the same folder. For example, put all the files in the AuthoringSample folder.  

2.  Copy the folder that contains the files to the Service Manager management server.  

3.  Bundle the files using the Windows&nbsp;PowerShell cmdlet [New\-SCSMManagementPackBundle](http://go.microsoft.com/fwlink/p/?LinkID=225397). For example:  

    ```  
    New-SCSMManagementPackBundle -Name AddComputerToGroup.mpb -ManagementPack Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml   
    ```  

### To import the management pack into Service Manager  

1.  In the Service Manager console, click **Administration**.  

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.  

3.  In the **Tasks** pane, under **Management Packs**, click **Import Management Pack**.  

4.  In the **Select Management Packs to Import** dialog box, select **AddComputerToGroup.mpb**.  

5.  In the **Import Management Packs** dialog box, click **Add**, click **Import**, and then click **OK**.  
