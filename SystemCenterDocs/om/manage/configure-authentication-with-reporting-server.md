---
title: Configure Authentication with Reporting server
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Configure Authentication with Reporting server

>Applies To: System Center 2016 - Operations Manager

In order to use algorithms that are FIPS compliant, follow these steps for the Operations Manager Reporting server component. Enabling FIPS compliance for System Center 2016 - Operations Manager requires that the underlying infrastructure used (Server OS, Active Directory etc.), also be FIPS compliant.  


##  Enable FIPS on the Reporting server

To enable FIPS on the reporting server, change the configuration in the application-level Web.config file to specify that ASP.NET use the Triple Data Encryption Standard (3DES) algorithm. To do this, follow these steps.

1.	In a text editor such as Notepad, open the **Web.config** file in the **ReportManager** and ReportServer** sub-folders under the SQL Server Reporting Services installation root folder  `C:\Program Files\Microsoft SQL Server\<InstanceName>\Reporting Services`. 

2.	In the **Web.config** file, locate the `<system.web>` section.

3.	Add the following `<machineKey>` section to in the `<system.web>` section:
`<machineKey validationKey="AutoGenerate,IsolateApps" decryptionKey="AutoGenerate,IsolateApps" validation="3DES" decryption="3DES"/>`.

4.	Save the **Web.config** file.

5.	Restart **SQL Server Reporting Services** service.

6.	Confirm SQL Server Report Manager works successfully before proceeding with the installation of the Operations Manager Report Server role.

## Next steps

- To configure SSL encryption and FIPS compliance for the Web console server, see [Configure Authentication with the Web console](configure-authentication-with-web-console.md) 