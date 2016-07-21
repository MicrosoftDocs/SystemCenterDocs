---
title: After Upgrading to System Center 2012 SP1 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a21c98a9-c10a-41db-8d8c-9eac164c2517
 

















---
# After Upgrading to System Center 2012 SP1 - Service Manager
This topic describes how to restart the Data Access service if it fails to start after an upgrade to System Center 2012 - Service Manager SP1. After the upgrade, you will also have to start the Service Manager workflows and restart the data warehouse jobs. This topic also describes how to stop and then start SQL&nbsp;Server Reporting Services \(SSRS\) after an upgrade.  
  
## Restart the Data Access Service and Workflows on the Data Warehouse Management Server  
 If necessary, use the following procedures to restart the service and workflows.  
  
#### To restart the Data Access service  
  
1.  On the computer that hosts the data warehouse management server, on the Windows desktop, click **Start**, and then click **Run**.  
  
2.  In the **Run** dialog box, in **Open**, type **services.msc**, and then click **OK**.  
  
3.  In the **Services** window, in the **Services \(Local\)** pane, right\-click **System Center Data Access Service**, and then click **Start**.  
  
#### To start Service Manager workflows  
  
1.  On the computer that hosts the Service Manager management server, on the Windows desktop, click **Start**, and then click **Run**.  
  
2.  In the **Run** dialog box, in **Open**, type **services.msc**, and then click **OK**.  
  
3.  In the **Services** window, in the **Services \(Local\)** pane, right\-click **System Center Management**, and then click **Start**.  
  
## Restart Data Warehouse Jobs  
 After you upgrade the data warehouse management server, you might need to restart the data warehouse \(extraction, transformation, and load \(ETL\)\) jobs. You can use the following procedure to restart the data warehouse jobs. In this procedure, you enable data warehouse job schedules by using Windows&nbsp;PowerShell cmdlets.  
  
#### To restart data warehouse jobs  
  
1.  On the computer that hosts the data warehouse management server, click **Start**, point to **Programs**, point to **Accessories**, click **Windows PowerShell**, right\-click **Windows PowerShell**, and then click **Run as administrator**.  
  
2.  Type the following commands and then press Enter after each command.  
  
    > [!NOTE]  
    >  It is assumed in the following command examples that Service Manager was installed in its default location on the C: drive. If necessary, change directories to the location where you installed Service Manager.  
  
    ```  
    cd 'C:\Program Files\Microsoft System Center 2012\Service Manager'  
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
  
## Stop and Then Start SSRS  
 After you perform an upgrade to System Center 2012 - Service Manager SP1, use the following procedure to stop and then start SSRS.  
  
#### To stop and then start SSRS  
  
1.  On the computer that hosts SSRS, on the Windows desktop, click **Start**, and then click **Run**.  
  
2.  In the **Run** dialog box, type **services.msc**, and then click **OK**.  
  
3.  In the **Services** window, in the **Services \(Local\)** pane, right\-click **SQL Server Reporting Services**, and then click **Stop**.  
  
4.  In the **Services** window, in the **Services \(Local\)** pane, right\-click **SQL Server Reporting Services**, and then click **Start**.
