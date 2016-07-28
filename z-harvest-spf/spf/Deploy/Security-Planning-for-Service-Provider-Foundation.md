---
title: Security Planning for Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2550115-4469-4956-863e-2994275941f5
author:bwren
manager:cfreemanwa
---
# Security Planning for Service Provider Foundation
This topic provides an overview of Service Provider Foundation security features and describes the security considerations for your deployment. You should create any required accounts and groups and determine if you have any additional security requirements before you start your Service Provider Foundation installation.  
  
## Security features  
Service Provider Foundation provides a tightly coordinated implementation of Windows and Internet Information Services \(IIS\) security features. Note that credentials in a domain in the Active Directory must be used.  
  
Service Provider Foundation relies on IIS to authenticate users. Starting with [!INCLUDE[sc2012r2_1](../../om/manage/includes/sc2012r2_1_md.md)], Service Provider Foundation accepts only the Secure Sockets Layer \(SSL\) requests protocol from its provider endpoints using the default port of 8090. Only HTTPS requests are accepted. Typically, the request should have the security context of the user who is logged on to the make the request.  
  
When the setup wizard installs a web service, it creates a local security group on the computer that runs the web service. You can specify users or groups that have access to each web service. The wizard assigns those users or groups to a local security group. Service Provider Foundation checks that the user who sends the request belongs to the appropriate local security group.  
  
In addition the wizard creates application domains pools in Internet Information Services \(IIS\) for each web service. You can specify the Network Service account or an account that also belongs to the security group.  
  
The wizard creates the following security groups application pools as shown on the following table.  
  
|Security Group Name|Application Pool Name|  
|-----------------------|-------------------------|  
|SPF\_Admin|Admin|  
|SPF\_Provider|Provider|  
|SPF\_VMM|VMM|  
|SPF\_Usage|Usage|  
  
After you install Service Provider Foundation, you must verify that the credentials for --- translation.priority.ht:    - cs-cz   - da-dk   - de-de   - el-gr   - es-es   - fi-fi   - fr-fr   - hu-hu   - it-it   - ja-jp   - ko-kr   - nb-no   - nl-nl   - pl-pl   - pt-br   - pt-pt   - ru-ru   - sv-se   - tr-tr   - zh-cn   - zh-hk   - zh-tw --- System&nbsp;Center&nbsp;2012&nbsp;- Virtual&nbsp;Machine&nbsp;Manager and the other service providers are configured correctly, as described in [Manage Web Services and Connections in Service Provider Foundation](../../spf/Deploy/Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md).  
  
## See Also  
[Capacity Planning for Service Provider Foundation](../../spf/Deploy/Capacity-Planning-for-Service-Provider-Foundation.md)  
[How to Install Service Provider Foundation for System Center 2012 SP1](../../spf/Deploy/How-to-Install-Service-Provider-Foundation-for-System-Center-2012-SP1.md)  
[Setup Command-Line Options for Service Provider Foundation](../../spf/Deploy/Setup-Command-Line-Options-for-Service-Provider-Foundation.md)  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Architecture Overview of Service Provider Foundation](../../spf/Deploy/Architecture-Overview-of-Service-Provider-Foundation.md)  
  
