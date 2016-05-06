---
title: Post-installation tasks for Service Management Automation
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a12e845d-bdec-43d8-a321-0d5e767a967f
---
# Post-installation tasks for Service Management Automation
After you install [!INCLUDE[sma_1](../Token/sma_1_md.md)], perform the following best practices.

## Replace untrusted Self\-Signed Certificates with trusted certificates
Each [!INCLUDE[sma_1](../Token/sma_1_md.md)] component is installed on an Internet Information Services \(IIS\) website that, by default, is configured with a self\-signed certificate. Because these self\-signed certificates are not issued by any of the trusted root certification authorities that your browser loads on startup, your browser displays a security warning when you attempt to connect to any of the sites. We recommend that you replace the self\-signed certificates with certificates that are issued by a trusted root certification authority to avoid this experience.

