---
title: Getting Started with Service Manager Cmdlets for Windows PowerShell
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 961b1998-10b7-4f01-92b7-3b1daf5de732
---
# Getting Started with Service Manager Cmdlets for Windows PowerShell
Windows PowerShell is a Windows command\-line shell that includes an interactive prompt and a scripting environment. Windows PowerShell uses cmdlets to manipulate the Windows PowerShell objects. Service Manager includes many cmdlets that you can use to perform various [!INCLUDE[smshort](./Token/smshort_md.md)]\-related tasks without using the [!INCLUDE[smcons](./Token/smcons_md.md)]. For example, you can use the **Import\-SCSMManagementPack** cmdlet to import a management pack.

The [!INCLUDE[smshort](./Token/smshort_md.md)] cmdlets are delivered in two modules that are listed below. In [!INCLUDE[smshort](./Token/smshort_md.md)], these cmdlet modules are not installed in the typical path that is listed in the $env:PSModulePath variable. Therefore, if you run the `Get-Module –List` cmdlet, the [!INCLUDE[smshort](./Token/smshort_md.md)] modules are not listed.

-   Administrator cmdlets: The System.Center.Service.Manager module which contains the cmdlets that are needed for common administrative tasks.

-   Data warehouse cmdlets: The Microsoft.EnterpriseManagement.Warehouse.Cmdlets module which contains the cmdlets that are needed for operating on the [!INCLUDE[smshort](./Token/smshort_md.md)] data warehouse.

The data warehouse cmdlets operate on the data warehouse database, and you can run them on both the  [!INCLUDE[smshort](./Token/smshort_md.md)] management server or the data warehouse management server.

Data returned from Windows PowerShell command might contain more information than can be displayed in a default Windows PowerShell command window. We recommend increasing the width of the command window: Right\-click the title bar, click **Properties**, and in the **Layout** tab, set the **Screen Buffer Size** width to 120.

The following procedures help you to get started with Service Manager cmdlets.

### To open a [!INCLUDE[smshort](./Token/smshort_md.md)] Windows PowerShell session from the [!INCLUDE[smcons](./Token/smcons_md.md)]

1.  In the [!INCLUDE[smcons](./Token/smcons_md.md)], click **Administration**.

2.  On the **Tasks** pane, click **Start PowerShell Session**.

The administrator cmdlet module is automatically pre\-imported in this session.

### To open a [!INCLUDE[smshort](./Token/smshort_md.md)] Windows PowerShell session from Windows

1.  On the computer that hosts the [!INCLUDE[smshort](./Token/smshort_md.md)] management server, on the taskbar, click **Start**, point to **All Programs**, and then click **Microsoft System Center**.

2.  Click **Service Manager 2016**, and then click **Service Manager Shell**.

The administrator cmdlet module is automatically pre\-imported in this session.

### To list all [!INCLUDE[smshort](./Token/smshort_md.md)] cmdlets

1.  Open a [!INCLUDE[smshort](./Token/smshort_md.md)] Windows PowerShell session.

2.  To list the cmdlets that are included in the administrator module, in the [!INCLUDE[smshort](./Token/smshort_md.md)] Windows PowerShell session, type the following, and then press ENTER:

    ```
    Get-Command -module System.Center.Service.Manager
    ```

3.  To list the cmdlets that are included in the data warehouse module, in the [!INCLUDE[smshort](./Token/smshort_md.md)] Windows PowerShell session, type the following, and then press ENTER:

    ```
    Get-Command –module Microsoft.EnterpriseManagement.Warehouse.Cmdlets
    ```

### To get Help for a cmdlet

1.  Open a [!INCLUDE[smshort](./Token/smshort_md.md)] Windows PowerShell session.

2.  You can now access the on\-the\-box Help, or you can use the **–online** parameter to access the most up\-to\-date online Help:

    -   On\-the\-box Help: Type the following command. Replace <*cmdlet\-name*> with the name of the cmdlet that you want to get help for, for example, **Import\-SCSMManagementPack**:

        ```
        Get-help <cmdlet-name> -detailed
        ```

    -   Online, up\-to\-date Help: Type the following command, and then press ENTER:

        ```
        Get-help <cmdlet-name> -online
        ```

        This command uses the **–online** parameter to access the latest online Help for a cmdlet. It opens a web browser and displays the online Help that is available for <*cmdlet\-name*>.


