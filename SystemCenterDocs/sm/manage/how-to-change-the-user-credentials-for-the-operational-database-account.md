---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Change the User Credentials for the Operational Database Account
ms.technology:  service-manager
ms.assetid:  04c4c092-e4e4-4e09-bfed-b3f83bb7ae43
---

# How to Change the User Credentials for the Operational Database Account

>Applies To: System Center 2016 Technical Preview - Service Manager

If the user account for the Operational Database Account in Service Manager changes, you must make the following changes:

1.  Add the new account to the Service Manager Administrators user role for both the Service Manager and data warehouse management servers

2.  Create a SQL Server logon account for the new user on computers hosting Service Manager databases. On the computer hosting the Service Manager database, assign the new user to the skd_users and configsvc_users roles.

3.  Make the new account a local administrator on the Service Manager computers.

4.  Make the new user account the logon account for the Service Manager Data Access Service and  Service Manager Management Configuration services, and then restart these services.

    > [!NOTE]
    > The logon account for the Service Manager Management service is always the local system account and must not be changed.

5.  Restart the Service Manager Management service.

6.  Make the new user the Operational Run As account.

Use the following procedures to make these changes in Service Manager.

> [!IMPORTANT]
> Do not configure the Operational Database Account to use the Network Service account.

### To add the user to the local administrators account

1.  Add the new user as a member of the Administrators local group in Windows on the computers hosting the following:

    -   Service Manager management server

    -   Data warehouse management server

    -   Self-Service Portal

    -   Service Manager database

    -   Data warehouse databases

### To add the user to the Administrators user role

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, expand **Security**, and then click **User Roles**.

3.  In the **User Roles** pane, click **Administrators**.

4.  In the **Tasks** pane, click **Properties**.

5.  In the Edit User Role Wizard, click **Users**.

6.  Click **Remove** to remove the existing credentials, click **Add** and add the new credentials, and then click **OK**.

7.  In the Service Manager console, click **Data Warehouse**.

8.  In the **Data Warehouse** pane, expand **Data Warehouse**, expand **Security**, and then click **User Roles**.

9. Repeat steps 3 through 6.

### To change the logon account for the Service Manager Data Access Service and Service Manager Management Configuration services

1.  On the computer that hosts the Self-Service Portal, on the Windows desktop, click **Start**, and then click **Run**.

2.  In the **Run** dialog box, in the **Open** box, type **services.msc**, and then click **OK**.

3.  In the **Services** window, in the **Services (Local)** pane, right-click **System Center Data Access Service**, and then click **Properties**.

4.  In the **System Center Data Access Service Properties (Local Computer)** dialog box, click **Log On**, and then click **Browse**.

5.  In the **Select User or Group** dialog box, complete these steps:

    1.  Click **Locations**, in the **Locations** dialog box, click **Entire Directory**, and then click **OK**.

    2.  In the **Enter the object name to select** box, type the name of the new Operational Database Account, click **Check Names**, and then click **OK**.

    3.  In the **Password** and **Confirm Password** boxes, type the password for the new user, and then click **OK**.

6.  Restart the Service Manager Data Access Service.

7.  Right-click **System Center Management Configuration**, and then click **Properties**.

8.  In the **System Center Management Configuration Properties (Local Computer)** dialog box, click **Log On**, and then click **Browse**.

9. In the **Select User or Group** dialog box, complete these steps:

    1.  Click **Locations**, and in the **Locations** dialog box, click **Entire Directory**, and then click **OK**.

    2.  In the **Enter the object name to select** box, type the name of the new Operational Database Account, click **Check Names**, and then click **OK**.

    3.  In the **Password** and **Confirm Password** boxes, type the password for the new user, and then click **OK**.

10. Restart the Service Manager Management Configuration service.

### To create a SQL Server logon

1.  On the computers hosting the Service Manager and data warehouse databases, open **SQL Server Management Studio**.

2.  In the **Connect to Server** dialog box, complete these steps:

    1.  In the **Server Type** list, select **Database Engine**.

    2.  In the **Server Name** list, select the server name for your Service Manager or data warehouse databases.

    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.

3.  In the **Object Explorer** pane, expand **Security**, and then expand **Logins**.

4.  Right-click **Logins**, and then click **New Login**.

5.  In the **Login - New** dialog box, in the **Select a page** pane, click **General**, and then click **Search**.

6.  In the **Select User or Group** dialog box, complete these steps:

    1.  Click **Locations**, in the **Locations** dialog box, click **Entire Directory**, and then click **OK**.

    2.  In the **Enter the object name to select** box, type the name of the new Operational Database Account, click **Check Names**, and then click **OK**.

7.  In the **Select a page** pane, click **Server Roles**, and in the **Server roles** list, ensure that **sysadmin** and **public** are selected, and then click **OK**.

### To change the Service ManagerSelf-Service Portal application pool account

1.  On the Windows desktop, click **Start**, point to **Programs**, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.

2.  In the **Internet Information Services (IIS) Manager** window, in the **Connections** pane, expand the name of your computer, and then click **Application Pools**.

3.  In the **Application Pools** pane, right-click **SM_AppPool**, and then click **Advanced Settings**.

4.  In the **Advanced Settings** dialog box, in the **Process Model** area, click **Identity**, and then click the ellipsis (**...**) button.

5.  In the **Application Pool Identity** dialog box, select **Custom account**, and then click **Set**.

6.  In the **Set Credentials** dialog box, in the **User name** box, type the user name for the Operational Database Account. In the **Password** and **Confirm password** boxes, type the password for the new Operational Database Account, and then click **OK**.

7.  In the **Application Pool Identity** dialog box, click **OK**.

8.  In the **Advanced Settings** dialog box, click **OK**.

9. Close Internet Information Services (IIS) Manager.

### To change the Operational Database Account

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, expand **Security**, and then click **Run As Accounts**.

3.  In the **Run As Accounts** pane, click **Operational Database Account**.

4.  In the **Tasks** pane, click **Properties**.

5.  In the **Operational Database Account** page, in the **User name**, **Password**, and **Domain** boxes, type the new credentials for the Operational Database Account, and then click **OK**.
