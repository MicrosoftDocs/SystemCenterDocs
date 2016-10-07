---
title: Security Planning for Service Provider Foundation
description: This topic provides an overview of security considerations for planning your Service Provider Foundation implementation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2550115-4469-4956-863e-2994275941f5
ms.date: 10-12-2016
author: rayne-wiselman
manager: cfreeman
ms.author: raynew
---
# Security Planning for Service Provider Foundation

>Apples To: System Center 2016 - Service Provider Foundation

This topic provides an overview of Service Provider Foundation security features and describes the security considerations for your deployment. You should create any required accounts and groups and determine if you have any additional security requirements before you start your Service Provider Foundation installation.

## Security features
Service Provider Foundation provides a tightly coordinated implementation of Windows and Internet Information Services \(IIS\) security features. Note that credentials in a domain in the Active Directory must be used.

Service Provider Foundation relies on IIS to authenticate users. Starting with System Center 2012 R2, Service Provider Foundation accepts only the Secure Sockets Layer \(SSL\) requests protocol from its provider endpoints using the default port of 8090. Only HTTPS requests are accepted. Typically, the request should have the security context of the user who is logged on to the make the request.

When the setup wizard installs a web service, it creates a local security group on the computer that runs the web service. You can specify users or groups that have access to each web service. The wizard assigns those users or groups to a local security group. Service Provider Foundation checks that the user who sends the request belongs to the appropriate local security group.

In addition the wizard creates application domains pools in Internet Information Services \(IIS\) for each web service. You can specify the Network Service account or an account that also belongs to the security group.

The wizard creates the following security groups application pools as shown on the following table.

|Security Group Name|Application Pool Name|
|-----------------------|-------------------------|
|SPF\_Admin|Admin|
|SPF\_Provider|Provider|
|SPF\_VMM|VMM|
|SPF\_Usage|Usage|

After you install Service Provider Foundation, you must verify that the credentials for VMM and the other service providers are configured correctly.
