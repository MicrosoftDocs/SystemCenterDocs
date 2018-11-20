---
ms.assetid: ba58d433-17ea-4ddc-af8d-42748ad2d349
title: Encrypt SMA web service to SQL connection by using SSL
description: This article provides information about how to encrypt SMA web service to SQL connection by using SSL.
author:  JYOTHIRMAISURI
ms.author: v-jysur
manager:  vvithal
ms.date:  11/14/2018
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology: service-management-automation
---

# Encrypt SMA web service connection using SSL

This article provides information about how to encrypt SMA Web Service to SQL connection by using Secure Socket Layer (SSL).

Use the following procedure:

1.	Open an elevated PowerShell console.
2.	Navigate to your .NET Framework home directory.  e.g. C:\Windows\Microsoft.NET\Framework64\v4.0.30319
3.	Decrypt the config file section using the following command:

    ```powershell
    .\aspnet_regiis.exe -pdf "connectionStrings" 'C:\inetpub\Service Management Automation'
    ```
    ![Decrypt config file](system-center/architecture-of-service-management-automation/media/architecture-of-service-management-automation/decrypt-config-file.png)

4.	Open the web.config file in Notepad from the path **C:\inet\Service Management Automation** and append the Connection String with **“;encrypt=true;trustServerCertificate=true”** as shown below:

    ![Append connection](/media/encrypt-sma-web-service/append-connection.png)

5.	Encrypt the Config file section by running the following command:

    ```powershell
.\aspnet_regiis.exe -pef "connectionStrings" 'C:\inetpub\Service Management Automation'
```

    ![Encrypt config file](./media/encrypt-sma-web-service/encrypt-config-file.png)

6.	Restart the SMA App Pool from **Computer Management**> **Service and Applications** > **Internet Information Service(IIS) Manager**.

## Next steps
[Manage runbooks](manage-runbooks.md)
