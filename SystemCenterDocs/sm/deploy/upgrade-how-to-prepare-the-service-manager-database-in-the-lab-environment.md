---
title: Prepare the Service Manager database in the lab environment
description: Prepare the Service Manager database in the lab environment before you upgrade.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d3b8b19-77f9-4a96-a117-8ffef08da01a
---

# Prepare the Service Manager database in the lab environment before you upgrade.

>Applies To: System Center 2016 - Service Manager

Use the following procedure to prepare the Service Manager database in the lab environment. Perform this procedure on the computer that is hosting the Service Manager database that is being used by the secondary management server, the management server in your lab environment.  

### To configure the database  

1.  On the computer hosting the Service Manager database for the secondary management server, click **Start**, click **All Programs**, click **Microsoft SQL Server 2016**, and then click **SQL Server Management Studio**.  

2.  In the **Connect to Server** dialog box, follow these steps:  

    1.  In the **Server Type** list, select **Database Engine**.  

    2.  In the **Server Name** list, select the server name for your Service Manager or data warehouse databases.  

    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  

3.  In the **Object Explorer** pane, expand **Databases**, and then click **ServiceManager**.  

4.  In the toolbar, click **New Query**.  

5.  In the center pane, type the following commands, and then click **Execute**.  

    ```  
    sp_configure 'clr enabled', 1  
    go  
    reconfigure  
    go   
    ```  

6.  In the center pane, remove the commands you typed in the previous step, type the following commands, and then click **Execute**.  

    ```  
    ALTER DATABASE ServiceManager SET SINGLE_USER WITH ROLLBACK IMMEDIATE  
    ```  

7.  In the center pane, remove the commands you typed in the previous step, type the following commands, and then click **Execute**.  

    ```  
    ALTER DATABASE ServiceManager SET ENABLE_BROKER  
    ```  

8.  In the center pane, remove the commands you typed in the previous step, type the following commands, and then click **Execute**.  

    ```  
    ALTER DATABASE ServiceManager SET MULTI_USER  
    ```  

### To configure the service account  

1.  In the **Object Explorer** pane, expand **Security**, and then expand **Logins**.  

2.  Right\-click **Logins**, and then click **New Login**  

3.  Perform the following procedures in the **Login - New** wizard:  

    1.  Click **Search**.  

    2.  Type the username \(domain\\username\) for the service account for Service Manager database in the lab environment, click **Check Names**, and then click **OK**.  

        > [!NOTE]  
        >  If the Data Access Account is running as LocalSystem, use the format \<domain\\computername$\> in SQL Logins, where \<computername\> is the name of the management server.  

    3.  In the **Select a page** pane, click **User Mapping**.  

    4.  In the **Users mapped to this login** area, in the **Map** column, click the row that represents the name of the Service Manager database \(**ServiceManager** is the default database name\).  

    5.  In the **Database role membership for: ServiceManager** area, make sure that the following entries are selected:  

        -   **configsvc\_users**  

        -   **db\_accessadmin**  

        -   **db\_datareader**  

        -   **db\_datawriter**  

        -   **db\_ddladmin**  

        -   **db\_securityadmin**  

        -   **dbmodule\_users**  

        -   **public**  

        -   **sdk\_users**  

        -   **sql\_dependency\_subscriber**  

    6.  Click **Ok**  

### To configure Service Manager tables  

1.  In the **Object Explorer** pane, expand **Databases**, expand **ServiceManager**, and then expand **Tables**.  

2.  Right\-click **dbo.MT\_Microsoft$SystemCenter$ManagementGroup**, and then click **Edit Top 200 Rows**.  

3.  In the center pane, locate the column **SQLServerName\_ 48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA**.  

4.  In the first row and second rows of this column, type the computer name of the computer hosting the Service Manager database in the lab environment. In the case of named instances, type computer name\\instance name.  

5.  Right\-click **dbo. MT\_Microsoft$SystemCenter$ResourceAccessLayer$SqlResourceStore**, and then click **Edit Top 200 Rows**.  

6.  In the center pane, locate the column **Server\_48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA**.  

7.  In the first row of this column, type the computer name of the computer hosting the SQL Server for the Service Manager database in the lab environment. In the case of named instances, type computer name\\instance name.  

8.  Right\-click **LFX.DataSource**, and then click **Edit Top 200 Rows**.  

9. In the center pane, locate the column **DataSourceAddress**.  

10. In the first row of this column, locate the entry that starts with **Data Source \= \<server name\>; Initial Catalog \= ServiceManager; Persist Security Info\=False**. Type the name of the computer hosting SQL Server in the lab environment in place of **\<server name\>**.  

11. Right\-click **dbo. MT\_Microsoft$SystemCenter$ResourceAccessLayer$SdkResourceStore**, and then click **Edit Top 200 Rows**.  

12. In the center pane, locate the column **Server\_48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA**.  

13. In all of the rows in this column, type the name of the computer hosting the Service Manager management server in the lab environment.  

14. Right\-click&nbsp;**\[dbo\].\[MT\_Microsoft$SystemCenter$ResourceAccessLayer$CmdbResourceStore\]**, and then click&nbsp;**Edit Top 200 Rows**.  

15. In all rows update the column&nbsp;**Server\_48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA**, type the name of the SQL computer hosting the Service Manager database in the lab environment  

16. In the toolbar, click **New Query**.  

17. In the center pane, type the following command, and then click **Execute**.  

    ```  
    Delete from dbo.MT_Microsoft$SystemCenter$ResourceAccessLayer$DwSdkResourceStore  
    ```  

18. Close **Microsoft SQL Server Management Studio**.  

### To configure the lab Service Manager management server to use the lab database  

-   Using Registry Editor, expand the following path and update **DatabaseServerName** :  

     HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\2010\\Common\\Database
