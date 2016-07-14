---
title: Load-Balancing the Self-Service Portal
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51331131-1af1-4ec7-9dab-68ea2602dc11
 

















---
# Load-Balancing the Self-Service Portal
This topic describes how to configure the Self-Service Portal in a load balancing environment. There are two computers in a Self-Service Portal deployment, the SharePoint computer and the web content server \(WCS\). The SharePoint computer provides two basic functions; it generates the framework of the web page you see in the Self-Service Portal and it delivers the Silverlight code required for the Self-Service Portal to function. The WCS computer reads and writes data to the Service Manager database and generates the content you see in the center pane of the Self-Service Portal.  
  
 Of the two computers in the Self-Service Portal, the WCS computer performs most of the work and we recommend that you first consider load balancing this computer.  
  
## Load Balancing the WCS Computer  
 To create a load balancing environment for the WCS, you deploy multiple computers running Internet Information Services \(IIS\) and install WCS on each computer. If you are using Secure Socket Layer \(SSL\), which is recommended, you deploy a certificate with the same name to each computer. When you deploy the SharePoint computer, instead of specifying the URL for the WCS, you specify the URL for the node that is responsible for load balancing. If you are deploying a load balancing environment to an existing Self-Service Portal installation, you will need to edit the web.config file on the SharePoint and WCS computer and specify the URL for the load balancing node there. See the topic [How to Configure the Self\-Service Portal for Web Content Server Load Balancing](../../../sm/deploy/deploy-guide/How-to-Configure-the-Self-Service-Portal-for-Web-Content-Server-Load-Balancing.md).  
  
## Load Balancing the SharePoint Computer  
 Information about how to load balance the SharePoint computers is available at [Multiple servers for a three\-tier farm \(SharePoint Server 2010\)](http://go.microsoft.com/fwlink/?LinkId=244297). Be sure that you edit the web.config file on the SharePoint servers to configure the URL for the either the web content server or the web content server load balancing node. See the procedure "To define the WCS load balancing URL on the SharePoint website server" in this guide.
