---
title: How to Select a Certificate for Web Content Server Use
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d97833d6-5e75-44bd-9bde-4f2afbd05118
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
# How to Select a Certificate for Web Content Server Use
In order for content from the web content server to display properly in the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)], the URL that is used to connect with the web content server must match the name on the web content server certificate. A potential solution to a certificate name mismatch problem is to change the certificate that is used by the web content server. Use the following procedure to select an alternative Secure Sockets Layer \(SSL\) certificate for use with the computer that is hosting the web content server.  
  
 In order to use the procedure, you must already have a certificate issued from a certification authority.  
  
### To select a certificate for web content server use  
  
1.  Log on to the computer that hosts the web content server with administrative privileges.  
  
2.  Click **Start**, point to **Administrative Tools**, and then click **Internet Information Services \(IIS\) Manager**.  
  
3.  In **Internet Information Services \(IIS\) Manager**, in the **Connections** pane, expand the computer name, expand **Sites**, and then click **SCSMWebContentServer**.  
  
    > [!NOTE]  
    >  **SCSMWebContentServer** is the default name used during setup of the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)].  
  
4.  In the **Actions** pane, under **Edit Site**, click **Bindings**.  
  
5.  In **Site Bindings**, select the port that you used for the SCSMWebContentServer then click **Edit**.  
  
6.  In **Edit Site Binding**, click the **SSL certificate** list, and then select the new certificate that you want to use.  
  
## See Also  
 [SSL Certificates for the Self\-Service Portal](../../../sm/deploy/deploy-guide/SSL-Certificates-for-the-Self-Service-Portal.md)