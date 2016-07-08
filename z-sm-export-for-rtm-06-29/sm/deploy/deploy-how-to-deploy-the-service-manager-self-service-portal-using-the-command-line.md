---
title: How to Deploy the Service Manager Self-Service Portal Using the Command Line
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce5cb453-76bb-4004-911c-42ccf5fcfc8e


















---
# How to Deploy the Service Manager Self-Service Portal Using the Command Line
Use the following command\-line procedures to deploy the web content server and the SharePoint website for the Service ManagerSelf-Service Portal in System Center 2012 - Service Manager on separate computers.  
  
## Deploying the Web Content Server  
 Use the following procedure to deploy the web content server on a computer.  
  
#### To deploy the web content server  
  
1.  Log on to the computer where you want to install the Service Manager console using administrative credentials.  
  
2.  Open the command window.  
  
3.  At the command prompt, change directories to the location of the Service Manager installation media, and then type the following:  
  
    ```  
    Start /Wait   
    Setup.exe  
    /Install:Portal   
    /AcceptEula:[YES/NO]  
    /RegisteredOwner:[owner name]  
    /RegisteredOrganization:[company name]  
    /ProductKey:[25-character product key]  
    /PortalWebSiteName:[Self-service portal name]  
    /PortalWebSitePort:[Port number]  
    /PortalWebSiteCertificate:[SSL Certificate]  
    /PortalAccount:[domain\account name\password]  
    /UseExistingDatabase:[ComputerName:DB Name]  
    /CustomerExperienceImprovementProgram:[YES/NO]  
    /EnableErrorReporting:[YES/NO]   
    /Silent  
    ```  
  
## Deploying the SharePoint Website  
 Use the following procedure to deploy the SharePoint website on another computer.  
  
#### To deploy the SharePoint website  
  
1.  Log on to the computer where you want to install the Service Manager console using administrative credentials.  
  
2.  Open the command window.  
  
3.  At the command prompt, change directories to the location of the Service Manager installation media, and then type the following:  
  
    ```  
    Start /Wait   
    Setup.exe  
  
    /Install:Portal   
    /AcceptEula:[YES/NO]  
  
    /RegisteredOwner:[owner name]   
  
    /RegisteredOrganization:[company name]   
  
    /ProductKey:[25-character product key]   
  
    /SpPortalWebSiteName:[SharePoint Site Name]   
  
    /SpPortalWebSitePort:[Port number]   
  
    /SpPortalWebSiteCertificate:[SSL Certificate]  
  
    /CreateSpPortalDatabase:[YES/NO]  
  
    /SpPortalAppPoolAccount:[domain\account name\password]   
    /CustomerExperienceImprovementProgram:[YES/NO]  
  
    /EnableErrorReporting:[YES/NO]   
    /Silent  
  
    ```  
  
## Deploying the Web Content Server and the SharePoint Website on the Same Computer  
 Use the following command\-line procedure to deploy both Self-Service Portal elements—the web content server and the SharePoint website—on the same computer.  
  
#### Deploy the web content server and the SharePoint website on the same computer  
  
1.  Log on to the computer where you want to install the Service Manager console using administrative credentials.  
  
2.  Open the command window.  
  
3.  At the command prompt, change directories to the location of the Service Manager installation media, and then type the following:  
  
    ```  
    Start /Wait   
    Setup.exe  
  
    /Install:Portal   
    /AcceptEula:[YES/NO]  
  
    /RegisteredOwner:[owner name]   
  
    /RegisteredOrganization:[company name]   
  
    /ProductKey:[25-character product key]   
  
    /PortalWebSiteName:[Self-service portal name]  
  
    /PortalWebSitePort:[Port number]   
  
    /PortalWebSiteCertificate:[SSL Certificate]  
  
    /PortalAccount:[domain\account name\password]  
  
    /UseExistingDatabase:[ComputerName:DB Name]   
  
    /SpPortalWebSiteName:[SharePoint Site Name]   
  
    /SpPortalWebSitePort:[Port number]   
  
    /SpPortalWebSiteCertificate:[SSL Certificate]  
  
    /CreateSpPortalDatabase:[YES/NO]  
  
    /SpPortalAppPoolAccount:[domain\account name\password]   
    /CustomerExperienceImprovementProgram:[YES/NO]   
  
    /EnableErrorReporting:[YES/NO]   
    /Silent  
  
    ```  
  
## See Also  
 [Deploying Service Manager from a Command Line](assetId:///a918e488-349d-4955-b401-52f09e78bb9e)
