---
ms.assetid: d6e1034d-88be-49f0-a5d1-65da807a77f6
title: Configure Authentication with Reporting server
description: This article describes how to configure the Operations Manger reporting server to be compliant with Federal Information Processing Standards.
author: jyothisuri
ms.author: jsuri
ms.date: 08/07/2025
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Configure authentication for the Reporting server


In this article you learn how to configure the Operations Manager Reporting server component to use algorithms that are Federal Information Processing Standards (FIPS) compliant. Enabling FIPS compliance for System Center - Operations Manager requires that the underlying infrastructure used (Server OS, Active Directory, etc.) also be FIPS-compliant.  

## Enable FIPS on the Reporting server

To enable FIPS on the reporting server, change the configuration in the application-level Web.config file to specify that ASP.NET use the Triple Data Encryption Standard (3DES) algorithm. To do this, follow these steps:



1. In a text editor, such as Notepad, open the **Web.config** file in the **ReportManager** and **ReportServer** subfolders under the SQL Server Reporting Services installation root folder `C:\Program Files\Microsoft SQL Server\<InstanceName>\Reporting Services`.

2. In the **Web.config** file, locate the `<system.web>` section.

3. Add the following `<machineKey>` section to in the `<system.web>` section:
`<machineKey validationKey="AutoGenerate,IsolateApps" decryptionKey="AutoGenerate,IsolateApps" validation="3DES" decryption="3DES"/>`.

4. Save the **Web.config** file.

5. Restart **SQL Server Reporting Services** service.

6. Confirm that the SQL Server Report Manager works successfully before proceeding with the installation of the Operations Manager Report Server role.

## Next steps

To configure SSL encryption and FIPS compliance for the Web console server, see [Configure Authentication with the Web console](manage-config-authentication-web-console.md).
