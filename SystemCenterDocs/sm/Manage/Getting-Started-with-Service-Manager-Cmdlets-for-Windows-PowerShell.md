---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Getting Started with Service Manager Cmdlets for Windows PowerShell
ms.technology:  service-manager
ms.assetid:  961b1998-10b7-4f01-92b7-3b1daf5de732
---

# Getting Started with Service Manager Cmdlets for Windows PowerShell

>Applies To: System Center 2016 Technical Preview - Service Manager

Windows PowerShell is a Windows command-line shell that includes an interactive prompt and a scripting environment. Windows PowerShell uses cmdlets to manipulate the Windows PowerShell objects. Service Manager includes many cmdlets that you can use to perform various Service Manager-related tasks without using the Service Manager console. For example, you can use the **Import-SCSMManagementPack** cmdlet to import a management pack.

The Service Manager cmdlets are delivered in two modules that are listed below. In Service Manager, these cmdlet modules are not installed in the typical path that is listed in the $env:PSModulePath variable. Therefore, if you run the `Get-Module �List` cmdlet, the Service Manager modules are not listed.

-   Administrator cmdlets: The System.Center.Service.Manager module which contains the cmdlets that are needed for common administrative tasks.

-   Data warehouse cmdlets: The Microsoft.EnterpriseManagement.Warehouse.Cmdlets module which contains the cmdlets that are needed for operating on the Service Manager data warehouse.

The data warehouse cmdlets operate on the data warehouse database, and you can run them on both the  Service Manager management server or the data warehouse management server.

Data returned from Windows PowerShell command might contain more information than can be displayed in a default Windows PowerShell command window. We recommend increasing the width of the command window: Right-click the title bar, click **Properties**, and in the **Layout** tab, set the **Screen Buffer Size** width to 120.

The following procedures help you to get started with Service Manager cmdlets.

### To open a Service Manager Windows PowerShell session from the Service Manager console

1.  In the Service Manager console, click **Administration**.

2.  On the **Tasks** pane, click **Start PowerShell Session**.

The administrator cmdlet module is automatically pre-imported in this session.

### To open a Service Manager Windows PowerShell session from Windows

1.  On the computer that hosts the Service Manager management server, on the taskbar, click **Start**, point to **All Programs**, and then click **Microsoft System Center**.

2.  Click **Service Manager 2016**, and then click **Service Manager Shell**.

The administrator cmdlet module is automatically pre-imported in this session.

### To list all Service Manager cmdlets

1.  Open a Service Manager Windows PowerShell session.

2.  To list the cmdlets that are included in the administrator module, in the Service Manager Windows PowerShell session, type the following, and then press ENTER:

    ```
    Get-Command -module System.Center.Service.Manager
    ```

3.  To list the cmdlets that are included in the data warehouse module, in the Service Manager Windows PowerShell session, type the following, and then press ENTER:

    ```
    Get-Command �module Microsoft.EnterpriseManagement.Warehouse.Cmdlets
    ```

### To get Help for a cmdlet

1.  Open a Service Manager Windows PowerShell session.

2.  You can now access the on-the-box Help, or you can use the **�online** parameter to access the most up-to-date online Help:

    -   On-the-box Help: Type the following command. Replace <*cmdlet-name*> with the name of the cmdlet that you want to get help for, for example, **Import-SCSMManagementPack**:

        ```
        Get-help <cmdlet-name> -detailed
        ```

    -   Online, up-to-date Help: Type the following command, and then press ENTER:

        ```
        Get-help <cmdlet-name> -online
        ```

        This command uses the **�online** parameter to access the latest online Help for a cmdlet. It opens a web browser and displays the online Help that is available for <*cmdlet-name*>.



