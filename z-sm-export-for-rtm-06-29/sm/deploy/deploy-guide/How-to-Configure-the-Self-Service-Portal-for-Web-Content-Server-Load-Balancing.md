---
title: How to Configure the Self-Service Portal for Web Content Server Load Balancing
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8778ebfd-01e0-4139-95f3-d8a2bbdf2550
translation.priority.ht: 
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
# How to Configure the Self-Service Portal for Web Content Server Load Balancing
When a user starts a browser and connects to the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], he or she is actually connecting to the SharePoint website server. The SharePoint website server delivers the framework for the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)], but it also delivers the URL for the web content server. In a web content server load\-balancing environment, you want the SharePoint website server to deliver the URL for the web content server load\-balancing node, not the URL for a specific web content server. If you are installing a new [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)], you can specify the web content server load\-balancing URL during setup. If you added web content server load\-balancing to an existing [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] installation, you can use the following procedure to reconfigure the URL for the web content server.  
  
 You will edit two files, one on the computer that hosts the SharePoint server and one on the computer that hosts the web content servers.  
  
### To define the web content server load\-balancing URL on the SharePoint website server  
  
1.  Log on to the computer that hosts the SharePoint website server with administrator privileges.  
  
2.  Using Windows Explorer, navigate to the folder location where you installed the SharePoint website server. The default location is \<drive\>:\\\\intetpub\\wwwroot\\wss\\VirtualDirectories\\Service Manager Portal.  
  
3.  Right\-click the Web.config file, and open it with the editor of your choice, for example, Notepad.  
  
4.  Scroll to the bottom of the Web.config file, locate the \<appSettings\> area, and then locate the \<add key\=…\> line.  
  
5.  Edit the URL in the value\= section to match the new URL that you want to use for the web content server load\-balancing node.  
  
6.  Close the editor, and save your changes.  
  
### To reconfigure the web content server URL on the web content servers  
  
1.  Log on to the computer that hosts each of the web content servers with administrator privileges.  
  
2.  Using Windows Explorer, navigate to the folder location where you installed the web content server. The default location is \<drive\>:\\\\inetpub\\wwwroot\\System Center Service Manager Portal\\ContentHost.  
  
3.  Right\-click the Web.config file, and then open it with the editor of your choice, for example, Notepad.  
  
4.  Scroll to the bottom of the Web.config file, locate the \<appSettings\> area, and then locate the \<add key\=…\> line.  
  
5.  Edit the URL in the value\= section to match the new URL that you want to use for the web.config load\-balancing node.  
  
6.  Close the editor, and save your changes.