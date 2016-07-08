---
title: How to Deploy a Service Manager Management Server Using the Command Line
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4822ed72-f9b0-46a5-afa3-5f94cb622cef


















---
# How to Deploy a Service Manager Management Server Using the Command Line
You can use the following command\-line procedures to deploy the Service Manager management server and the Service Manager database in System Center 2012 - Service Manager.  
  
### To deploy the Service Manager management server and database on one computer  
  
1.  Log on to the computer where you want to install the Service Manager console using administrative credentials.  
  
2.  Open the command window.  
  
3.  At the command prompt, change directories to the location of the Service Manager installation media, and then type the following:  
  
    ```  
    Start /Wait   
    Setup.exe   
    /Install:Server   
    /AcceptEula:[YES/NO]   
    /RegisteredOwner:[owner name]   
    /RegisteredOrganization:[company name]   
    /ProductKey:[25-character product key]   
    /CreateNewDatabase   
    /ManagementGroupName:[management group name]   
    /AdminRoleGroup:[domain\account name]   
    /ServiceRunUnderAccount:[domain\account name\password]   
    /WorkflowAccount:[domain\account name\password]   
    /CustomerExperienceImprovementProgram:[YES/NO]   
    /EnableErrorReporting:[YES/NO]   
  
    /Silent  
  
    ```  
  
## See Also  
 [Deploying Service Manager from a Command Line](assetId:///a918e488-349d-4955-b401-52f09e78bb9e)
