---
ms.assetid: ba58d433-17ea-4ddc-af8d-42748ad2d349
title: Encrypt SQL connection by using SSL
description: This article provides information about how to encrypt a connection by using SSL.
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  11/14/2018
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology: service-management-automation
---

# Encrypt a SMA web service connection using SSL

This article provides information about how to encrypt SMA Web Service to SQL connection by using Secure Socket Layer (SSL)

Use the following procedure:

1.	Open an elevated PowerShell console.
2.	Navigate to your .NET Framework home directory. e.g. C:\Windows\Microsoft.NET\Framework64\v4.0.30319 )
3.	Decrypt config file section using below command.
.\aspnet_regiis.exe -pdf "connectionStrings" 'C:\inetpub\Service Management Automation'
4.	Open web.config in Notepad from the path C:\inetpub\Service Management Automation and append the Connection String with “;encrypt=true;trustServerCertificate=true” as shown below.
5.	Encrypt the Config File section by running the following command
.\aspnet_regiis.exe -pef "connectionStrings" 'C:\inetpub\Service Management Automation'
6.	Restart the SMA App Pool from Computer Management -> Service and Applications -> Internet Information Service(IIS) Manager.



> [!NOTE]
> .


## Next steps

Learn about  []()  
