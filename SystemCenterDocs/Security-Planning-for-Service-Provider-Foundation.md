---
title: Security Planning for Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2550115-4469-4956-863e-2994275941f5
---
# Security Planning for Service Provider Foundation
This topic provides an overview of [!INCLUDE[spflong](../Token/spflong_md.md)] security features and describes the security considerations for your deployment. You should create any required accounts and groups and determine if you have any additional security requirements before you start your [!INCLUDE[spfshort](../Token/spfshort_md.md)] installation.

## Security features
[!INCLUDE[spfshort](../Token/spfshort_md.md)] provides a tightly coordinated implementation of Windows and Internet Information Services \(IIS\) security features. Note that credentials in a domain in the Active Directory must be used.

[!INCLUDE[spfshort](../Token/spfshort_md.md)] relies on IIS to authenticate users. Starting with [!INCLUDE[sc2012r2_1](../Token/sc2012r2_1_md.md)], [!INCLUDE[spfshort](../Token/spfshort_md.md)] accepts only the Secure Sockets Layer \(SSL\) requests protocol from its provider endpoints using the default port of 8090. Only HTTPS requests are accepted. Typically, the request should have the security context of the user who is logged on to the make the request.

When the setup wizard installs a web service, it creates a local security group on the computer that runs the web service. You can specify users or groups that have access to each web service. The wizard assigns those users or groups to a local security group. [!INCLUDE[spfshort](../Token/spfshort_md.md)] checks that the user who sends the request belongs to the appropriate local security group.

In addition the wizard creates application domains pools in Internet Information Services \(IIS\) for each web service. You can specify the Network Service account or an account that also belongs to the security group.

The wizard creates the following security groups application pools as shown on the following table.

|Security Group Name|Application Pool Name|
|-----------------------|-------------------------|
|SPF\_Admin|Admin|
|SPF\_Provider|Provider|
|SPF\_VMM|VMM|
|SPF\_Usage|Usage|

After you install [!INCLUDE[spfshort](../Token/spfshort_md.md)], you must verify that the credentials for [!INCLUDE[vmm12med](../Token/vmm12med_md.md)] and the other service providers are configured correctly, as described in [Manage Web Services and Connections in Service Provider Foundation](../Topic/Manage-Web-Services-and-Connections-in-Service-Provider-Foundation.md).

## See Also
[Capacity Planning for Service Provider Foundation](../Topic/Capacity-Planning-for-Service-Provider-Foundation.md)
[How to Install Service Provider Foundation for System Center 2012 SP1](../Topic/How-to-Install-Service-Provider-Foundation-for-System-Center-2012-SP1.md)
[Setup Command-Line Options for Service Provider Foundation](../Topic/Setup-Command-Line-Options-for-Service-Provider-Foundation.md)
[Deploying Service Provider Foundation](../Topic/Deploying-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](../Topic/Administering-Service-Provider-Foundation.md)
[Architecture Overview of Service Provider Foundation](../Topic/Architecture-Overview-of-Service-Provider-Foundation.md)

