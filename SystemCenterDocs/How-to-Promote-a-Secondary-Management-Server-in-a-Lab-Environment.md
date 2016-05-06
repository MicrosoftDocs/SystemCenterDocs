---
title: How to Promote a Secondary Management Server in a Lab Environment
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df0bc01c-a314-441f-a983-27dfd92f95c0
---
# How to Promote a Secondary Management Server in a Lab Environment
Use the following procedure to promote the secondary management server.

### To promote the secondary management server

1.  On the secondary management server, do the following:

    1.  Close the Service Manager console.

    2.  On the Windows desktop, click **Start**, and then click **Run**.

    3.  In the **Run** dialog box, in the **Open** text field, type **services.msc**, and then click **OK**.

    4.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services and for each one, click **Stop**:

        -   System Center Data Access Service

        -   System Center Management

        -   System Center Management Configuration

    5.  Leave the **Services** window open.

    6.  Open Windows Explorer. Locate the \\Program Files\\Microsoft System Center 2012\\Service Manager folder.

    7.  In this folder, delete the Health Service State folder and all of its contents.

2.  Do the following on the ServiceManager database on the Test SQL Server instance:

    1.  On the Windows desktop, click **Start**, point to **Programs**, point **to Microsoft SQL Server 2008**, and then click **SQL Server Management Studio**.

    2.  In the Connect to Database Engine dialog box, follow these steps:

        1.  In the **Server name** box, type the name of the server that hosts the ServiceManager database.

        2.  In the **Authentication** box, select **Windows Authentication**.

        3.  Click **Connect**.

    3.  In the **Object Explorer** pane, expand **Databases**, and then click **ServiceManager**.

    4.  On the toolbar, click **New Query**.

    5.  In the **SQLQuery1.sql** pane \(center pane\), type the following, where <FQDN of your server> is the FQDN of the management server that you are promoting:

        **EXEC p\_PromoteActiveWorkflowServer '<FQDN of your server>'**

        On the toolbar, click **Execute**.

    6.  At the bottom of the **SQLQuery1.sql** pane \(center pane\), observe that **Query executed successfully** is displayed.

    7.  Exit Microsoft SQL Server Management Studio.

3.  Do the following on the secondary management server:

    1.  On the Windows desktop, click **Start**, and then click **Run**.

    2.  In the **Run** dialog box, in the **Open** field, type **services.msc**, and then click **OK**.

    3.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services and for each one, click **Start**.

        -   System Center Data Access Service

        -   System Center Management

        -   System Center Management Configuration

Your secondary management server is now the primary management server for the management group.

