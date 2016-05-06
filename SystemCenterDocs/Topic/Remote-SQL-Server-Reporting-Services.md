---
title: Remote SQL Server Reporting Services
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d41be74c-5773-4152-8155-d455f7947144
---
# Remote SQL Server Reporting Services
When you installed [!INCLUDE[smlong12](../Token/smlong12_md.md)], you may have specified a different computer to host Microsoft SQL Server Reporting Services \(SSRS\) than the computer that hosted the data warehouse management server. If, in your environment, SSRS is remote from the data warehouse management server, you must use the following procedures to prepare the computer that hosts SSRS for the upgrade:

-   Copy Microsoft.EnterpriseManagement.Reporting.Code.dll from the Service Manager installation media to the computer that is hosting SSRS.

-   Add an Extension tag to the existing Data segment in the rsreportserver configuration file on the same computer.

If you used the default instance of SQL Server, use Windows Explorer to drag Microsoft.EnterpriseManagement.Reporting.Code.dll \(which is located in the Prerequisites folder on your [!INCLUDE[smshort](../Token/smshort_md.md)] installation media\) to the folder \\Program Files\\Microsoft SQL Server\\MSRS10.MSSQLSERVER\\Reporting Services\\ReportServer\\Bin on the computer that is hosting SSRS. If you did not use the default instance, the path of the required folder is \\Program Files\\Microsoft SQL Server\\MSRS10.<INSTANCE\_NAME>\\Reporting Services\\ReportServer\\Bin. In the following procedure, the default instance name is used.

### To copy the Microsoft.EnterpriseManagement.Reporting.Code.dll file

1.  On the computer that will host the remote SSRS, open an instance of Windows Explorer.

2.  Locate the folder \\Program Files\\Microsoft SQL Server\\MSRS10\_50.MSSQLSERVER\\Reporting Services\\ReportServer\\Bin.

3.  Start a second instance of Windows Explorer, locate the drive that contains the [!INCLUDE[smshort](../Token/smshort_md.md)] installation media, and then open the Prerequisites folder.

4.  In the Prerequisites folder, click **Microsoft.EnterpriseManagement.Reporting.Code.dll** and drag it to the folder that you located in step 2.

### To add an Extension tag to the Data segment in the rsreportserver.conf file

1.  On the computer that is hosting SSRS, locate the file rsreportserver.config in the following folder:

    \\Program Files\\Microsoft SQL Server\\MSRS10\_50.MSSQLSERVER\\Reporting Services\\ReportServer

2.  Using an XML editor of your choice \(such as Notepad\), open the rsreportserver.config file.

3.  Scroll through the rsreportserver.config file, and locate the **<Data>** code segment. There is only one **<Data>** code segment in this file.

4.  Add the following **Extension** tag to the **<Data>** code segment where all the other **Extension** tags are:

    ```
    <Extension Name="SCDWMultiMartDataProcessor" Type="Microsoft.EnterpriseManagement.Reporting.MultiMartConnection, Microsoft.EnterpriseManagement.Reporting.Code" />
    ```

5.  Save the changes, and close the XML editor.

