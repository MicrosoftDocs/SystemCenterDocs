---
title: Post-upgrade tasks in System Center - Service Manager p
description: Summarizes tasks to complete after you upgrade System Center - Service Manager.
manager: mkluck
ms.prod: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 01/23/2018
ms.technology: service-manager
ms.topic: article
---

# Post-upgrade tasks

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

This article describes the tasks you should complete after upgrading System Center - Service Manager.

## Restart the Data Access service and workflows
 If necessary, use the following procedures to restart the service and workflows.  

#### To restart the Data Access service  

1.  On the computer that hosts the data warehouse management server, on the Windows desktop, select **Start**, and select **Run**.  

2.  In the **Run** dialog, in **Open**, enter **services.msc**, and select **OK**.  

3.  In the **Services** window, in the **Services \(Local\)** pane, right\-click **System Center Data Access Service**, and select **Start**.  

#### To start Service Manager workflows  

1.  On the computer that hosts the Service Manager management server, on the Windows desktop, select **Start**, and select **Run**.  

2.  In the **Run** dialog, in **Open**, enter **services.msc**, and select **OK**.  

3.  In the **Services** window, in the **Services \(Local\)** pane, right\-click **System Center Management**, and select **Start**.  

## Restart data warehouse jobs  
 After you upgrade the data warehouse management server, you might need to restart the data warehouse \(extraction, transformation, and load \(ETL\)\) jobs. You can use the following procedure to restart the data warehouse jobs. In this procedure, you enable data warehouse job schedules by using Windows&nbsp;PowerShell cmdlets.  

#### To restart data warehouse jobs  

1.  On the computer that hosts the data warehouse management server, select **Start**, point to **Programs**, point to **Accessories**, select **Windows PowerShell**, right\-click **Windows PowerShell**, and select **Run as administrator**.  

2.  Enter the following commands and then press Enter after each command.  

    > [!NOTE]  
    >  It's assumed in the following command examples that Service Manager was installed in its default location on the C: drive. If necessary, change directories to the location where you installed Service Manager.  

    ```  
    cd 'C:\Program Files\Microsoft System Center <version>\Service Manager'  
    ```  

    ```  
    import-module $PWD/Microsoft.EnterpriseManagement.Warehouse.Cmdlets.psd1  
    ```  

    ```  
    Get-SCDWJob  
    ```  

    ```  
    Enable-SCDWJobSchedule -JobName Extract_<data warehouse management group name>  
    ```  

    ```  
    Enable-SCDWJobSchedule -JobName Extract_<Service Manager management group name>  
    ```  

    ```  
    Enable-SCDWJobSchedule -JobName Transform.Common  
    ```  

    ```  
    Enable-SCDWJobSchedule -JobName Load.Common  
    ```  

    ```  
    Enable-SCDWJobSchedule -JobName DWMaintenance  
    ```  

    ```  
    Enable-SCDWJobSchedule -JobName MPSyncJob  
    ```  

    ```  
    Start-SCDWJob -JobName MPSyncJob  
    ```  

     The last command, **Start\-SCDWJob - JobName MPSyncJob**, will enable the ETL jobs to run.  

## Stop and then restart SSRS  
 After you perform an upgrade, use the following procedure to stop and then start SSRS.  

#### To stop and then restart SSRS  

1.  On the computer that hosts SSRS, on the Windows desktop, select **Start**, and select **Run**.  

2.  In the **Run** dialog, enter **services.msc**, and select **OK**.  

3.  In the **Services** window, in the **Services \(Local\)** pane, right\-click **SQL Server Reporting Services**, and select **Stop**.  

4.  In the **Services** window, in the **Services \(Local\)** pane, right\-click **SQL Server Reporting Services**, and select **Start**.


## Next steps

- If needed, [troubleshoot upgrade issues](resolve-upgrade-problems.md).
