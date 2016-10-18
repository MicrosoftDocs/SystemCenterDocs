---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  Post installation tasks for Service Management Automation
ms.technology:  service-management-automation
ms.assetid:  a12e845d-bdec-43d8-a321-0d5e767a967f
---

# Post-installation tasks for Service Management Automation

>Applies To: Windows Azure Pack for Windows Server, System Center 2016

After you install Service Management Automation, perform the following best practices.

## Replace untrusted Self-Signed Certificates with trusted certificates
Each Service Management Automation component is installed on an Internet Information Services (IIS) website that, by default, is configured with a self-signed certificate. Because these self-signed certificates are not issued by any of the trusted root certification authorities that your browser loads on startup, your browser displays a security warning when you attempt to connect to any of the sites. We recommend that you replace the self-signed certificates with certificates that are issued by a trusted root certification authority to avoid this experience.
