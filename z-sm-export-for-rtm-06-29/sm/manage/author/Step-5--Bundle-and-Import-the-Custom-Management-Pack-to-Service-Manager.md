---
title: Step 5: Bundle and Import the Custom Management Pack to Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8388927-d818-4dbf-8351-5a1034913604
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Step 5: Bundle and Import the Custom Management Pack to Service Manager
In this of the Woodgrove Bank customization scenario, Ken needs to bundle the management pack file with all the necessary resource files and then import the bundled file into [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)]. When [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] imports a management pack, it validates the XML code in the management pack file and then imports the management pack only if it is valid.  
  
### To bundle the management pack file with its associated resource files  
  
1.  Ensure that the Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml file and its associated resource files, such as the Woodgrovebank.jpg image file and the AddComputerToGroupFormAssembly.dll file, are in the same folder. For example, put all the files in the AuthoringSample folder.  
  
2.  Copy the folder that contains the files to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server.  
  
3.  Bundle the files using the Windows PowerShell cmdlet [New\-SCSMManagementPackBundle](http://go.microsoft.com/fwlink/p/?LinkID=225397). For example:  
  
    ```  
    New-SCSMManagementPackBundle –Name AddComputerToGroup.mpb -ManagementPack Woodgrove.AutomatedActivity.AddComputerToGroupMP.xml   
    ```  
  
### To import the management pack into [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Administration**.  
  
2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.  
  
3.  In the **Tasks** pane, under **Management Packs**, click **Import Management Pack**.  
  
4.  In the **Select Management Packs to Import** dialog box, select **AddComputerToGroup.mpb**.  
  
5.  In the **Import Management Packs** dialog box, click **Add**, click **Import**, and then click **OK**.  
  
## See Also  
 [Sample Scenario: The Woodgrove Bank Customization](../Topic/Sample%20Scenario:%20The%20Woodgrove%20Bank%20Customization.md)