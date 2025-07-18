---
title: Prepare remote SQL Server Reporting Services for System Center - Service Manager
description: Describes how to prepare remote SQL Server Reporting Services for System Center - Service Manager upgrade.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.subservice: service-manager
ms.topic: upgrade-and-migration-article
ms.custom: UpdateFrequency2, engagement-fy24
---

# Prepare remote SQL Server Reporting Services in a Service Manager upgrade



When you installed System Center - Service Manager, you may have specified a different computer to host Microsoft SQL&nbsp;Server Reporting Services \(SSRS\) than the computer that hosted the data warehouse management server. If in your environment, SSRS is remote from the data warehouse management server, you must use the following procedures to prepare the computer that hosts SSRS for the upgrade:  

- Copy Microsoft.EnterpriseManagement.Reporting.Code.dll from the Service Manager installation media to the computer that is hosting SSRS.  

- Add an Extension tag to the existing Data segment in the rsreportserver configuration file on the same computer.  

If you used the default instance of SQL Server, use Windows Explorer to drag Microsoft.EnterpriseManagement.Reporting.Code.dll \(which is located in the Prerequisites folder on your Service Manager installation media\) to the folder \\Program Files\\Microsoft SQL Server\\MSRS13.MSSQLSERVER\\Reporting Services\\ReportServer\\Bin on the computer that is hosting SSRS. If you didn't use the default instance, the path of the required folder is \\Program Files\\Microsoft SQL Server\\MSRS10.\<INSTANCE\_NAME\>\\Reporting Services\\ReportServer\\Bin. In the following procedure, the default instance name is used.  

## Copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file  

1. On the computer that will host the remote SSRS, open an instance of Windows Explorer.  

2. Locate the folder \\Program Files\\Microsoft SQL Server\\MSRS10\_50.MSSQLSERVER\\Reporting Services\\ReportServer\\Bin.  

3. Start a second instance of Windows Explorer, locate the drive that contains the Service Manager installation media, and then open the Prerequisites folder.  

4. In the Prerequisites folder, select **Microsoft.EnterpriseManagement.Reporting.Code.dll** and drag it to the folder that you located in step 2.  

## Add an Extension tag to the rsreportserver.conf file  

1. On the computer that is hosting SSRS, locate the file rsreportserver.config in the following folder:  

     \\Program Files\\Microsoft SQL Server\\MSRS10\_50.MSSQLSERVER\\Reporting Services\\ReportServer  

2. Using an XML editor of your choice \(such as Notepad\), open the rsreportserver.config file.  

3. Scroll through the rsreportserver.config file, and locate the `<Data>` code segment. There's only one `<Data>` code segment in this file.  

4. Add the following **Extension** tag to the `<Data>` code segment where all the other **Extension** tags are:  

    ```  
    <Extension Name="SCDWMultiMartDataProcessor" Type="Microsoft.EnterpriseManagement.Reporting.MultiMartConnection, Microsoft.EnterpriseManagement.Reporting.Code" />  
    ```  

5. Save the changes, and close the XML editor.

## Next steps

- To upgrade the Self Service portal for various possible configurations, review [Upgrade configurations for the Self-Service portal](upgrade-configs-portal.md).
