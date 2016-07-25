---
title: How to Promote a Service Manager Management Server
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c835def2-faf0-488d-abbe-2737c2862069


















---
# How to Promote a Service Manager Management Server
When you first ran Setup for System Center 2012 - Service Manager, you installed the initial Service Manager management server and you defined the management group for your installation. The initial management server handles all the workflows in your Service Manager environment. You can use additional Service Manager management servers to load\-balance Service Manager console connections. Also, you can promote one of the additional Service Manager management servers to take over the role of a failed initial Service Manager management server. For more information, see "Deploying Additional Service Manager Management Servers" in the [Deployment Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670)  
  
 You can use the following procedures to promote a secondary Service Manager management server.  
  
### To prepare the secondary management server  
  
1.  On the secondary management server, close the Service Manager console.  
  
2.  On the Windows desktop, click **Start**, and then click **Run**.  
  
3.  In the **Run** dialog box, in the **Open** text field, type **services.msc**, and then click **OK**.  
  
4.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one click **Stop**:  
  
    -   System Center Data Access Service  
  
    -   System Center Management  
  
        > [!NOTE]  
        >  For System Center 2012 R2 Service Manager, the System Center Management service was renamed to Microsoft Monitoring Agent.  
  
    -   System Center Management Configuration  
  
5.  Leave the **Services** window open.  
  
6.  Open Windows Explorer. Locate the folder \\Program Files\\Microsoft System Center 2012\\Service Manager.  
  
7.  In this folder, delete the Health Service State folder and all of its contents.  
  
### To define the computer name for the Service Manager database  
  
1.  On the Service Manager database, on the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.  
  
2.  In the **Connect to Database Engine** dialog box, do the following:  
  
    1.  In **Server name**, type the name of the server that hosts the Service Manager database.  
  
    2.  In **Authentication**, select **Windows Authentication**.  
  
    3.  Click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**, and then click **ServiceManager**.  
  
4.  On the toolbar, click **New Query**.  
  
5.  In the **SQLQuery1.sql** pane \(the center pane\), type the following, where \<FQDN of your server\> is the fully qualified domain name \(FQDN\) of the management server that you are promoting:  
  
    ```  
    EXEC p_PromoteActiveWorkflowServer '<FQDN of your server>'  
    ```  
  
6.  On the toolbar, click **Execute**.  
  
7.  At the bottom of the **SQLQuery1.sql** pane \(the center pane\), confirm that the "Query executed successfully" message appears.  
  
8.  Exit Microsoft SQL&nbsp;Server Management Studio.  
  
### To restart the services on the secondary management server  
  
1.  On the secondary management server, on the Windows desktop, click **Start**, and then click **Run**.  
  
2.  In the **Run** dialog box, in **Open**, type **services.msc**, and then click **OK**.  
  
3.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one click **Start**.  
  
    -   System Center Data Access Service  
  
    -   System Center Management  
  
        > [!NOTE]  
        >  For System Center 2012 R2 Service Manager, the System Center Management service was renamed to Microsoft Monitoring Agent.  
  
    -   System Center Management Configuration  
  
 Your secondary management server is now the primary management server for the management group.
