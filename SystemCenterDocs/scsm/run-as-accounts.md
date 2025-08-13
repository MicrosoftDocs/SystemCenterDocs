---
title: Manage Run As accounts
description: Describes how to manage Run As accounts in Service Manager.
ms.topic: how-to
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 03/28/2025
ms.subservice: service-manager
ms.assetid: 556f240e-d032-406a-ba10-2404fb591d04
ms.custom: UpdateFrequency2
---

# Manage Run As accounts in Service Manager



During the setup of Service Manager, you specified credentials for the workflow and service accounts, for Microsoft SQL Server Analysis Services, and for SQL Server Reporting Services (SSRS). If, because of the configurations of password security requirements used in your organization, these passwords expire, you must update the new passwords in Service Manager. In addition, if you decide that the user names must change, you also must change them in Service Manager. This section describes how to make those changes.

It's a best practice never to delete Run As accounts from the Service Manager console. The Service Manager management pack monitors Run As accounts. At regular intervals, the Health service attempts to log on as the Run As accounts. If this fails, Event ID 7000 is invoked that causes an alert. The best way to avoid this issue is never to delete Run As accounts from the Service Manager console. You can reuse existing Run As accounts by changing their name or credentials. If you want to stop using a Run As account, you can change its credentials to Local System and change the name to something easy to remember, such as *Inactive*.

## Change the user credentials for the Operational Database account used by Service Manager

If the user account for the Operational Database Account in Service Manager changes, you must make the following changes:

1. Add the new account to the Service Manager Administrators user role for both the Service Manager and data warehouse management servers.
2. Create a SQL Server logon account for the new user on computers hosting Service Manager databases. On the computer hosting the Service Manager database, assign the new user to the skd_users and configsvc_users roles.
3. Make the new account a local administrator on the Service Manager computers.
4. Make the new user account the logon account for the Service Manager Data Access Service and  Service Manager Management Configuration services, and then restart these services.

    > [!NOTE]
    > The logon account for the Service Manager Management service is always the local system account and must not be changed.

5. Restart the Service Manager Management service.
6. Make the new user the Operational Run As account.

Use the following procedures to make these changes in Service Manager.

> [!IMPORTANT]
> Don't configure the Operational Database Account to use the Network Service account.

### Add the user to the local administrators account

Add the new user as a member of the Administrators local group in Windows on the computers hosting the following:
    - Service Manager management server
    - Data warehouse management server
    - Self-Service Portal
    - Service Manager database
    - Data warehouse databases

### Add the user to the Administrators user role

To add the user to the Administrators user role, follow these steps:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, expand **Security**, and select **User Roles**.
3. In the **User Roles** pane, select **Administrators**.
4. In the **Tasks** pane, select **Properties**.
5. In the Edit User Role Wizard, select **Users**.
6. Select **Remove** to remove the existing credentials, select **Add** and add the new credentials, and select **OK**.
7. In the Service Manager console, select **Data Warehouse**.
8. In the **Data Warehouse** pane, expand **Data Warehouse**, expand **Security**, and select **User Roles**.
9. Repeat steps 3 through 6.

### Change the logon account for the Service Manager Data Access Service and Service Manager Management Configuration services

To change the logon account for the Service Manager Data Access Service and Service Manager Management Configuration services, follow these steps:

1. On the computer that hosts the Self-Service Portal, on the Windows desktop, select **Start**, and select **Run**.
2. In the **Run** dialog, in the **Open** box, enter **services.msc**, and select **OK**.
3. In the **Services** window, in the **Services (Local)** pane, right-click **System Center Data Access Service**, and select **Properties**.
4. In the **System Center Data Access Service Properties (Local Computer)** dialog, select **Log On**, and select **Browse**.
5. In the **Select User or Group** dialog, complete these steps:
    1. Select **Locations**, in the **Locations** dialog, select **Entire Directory**, and select **OK**.
    2. In the **Enter the object name to select** box, enter the name of the new Operational Database Account, select **Check Names**, and select **OK**.
    3. In the **Password** and **Confirm Password** boxes, enter the password for the new user, and select **OK**.
6. Restart the Service Manager Data Access Service.
7. Right-click **System Center Management Configuration**, and select **Properties**.
8. In the **System Center Management Configuration Properties (Local Computer)** dialog, select **Log On**, and select **Browse**.
9. In the **Select User or Group** dialog, complete these steps:
    1. Select **Locations**, and in the **Locations** dialog, select **Entire Directory**, and select **OK**.
    2. In the **Enter the object name to select** box, enter the name of the new Operational Database Account, select **Check Names**, and select **OK**.
    3. In the **Password** and **Confirm Password** boxes, enter the password for the new user, and select **OK**.
10. Restart the Service Manager Management Configuration service.

### Create a SQL Server logon

To create a SQL Server logon, follow these steps:

1. On the computers hosting the Service Manager and data warehouse databases, open **SQL Server Management Studio**.
2. In the **Connect to Server** dialog, complete these steps:
    1. In the **Server Type** list, select **Database Engine**.
    2. In the **Server Name** list, select the server name for your Service Manager or data warehouse databases.
    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.
3. In the **Object Explorer** pane, expand **Security**, and then expand **Logins**.
4. Right-click **Logins**, and select **New Login**.
5. In the **Login - New** dialog, in the **Select a page** pane, select **General**, and select **Search**.
6. In the **Select User or Group** dialog, complete these steps:
    1. Select **Locations**, in the **Locations** dialog, select **Entire Directory**, and select **OK**.
    2. In the **Enter the object name to select** box, enter the name of the new Operational Database Account, select **Check Names**, and select **OK**.
7. In the **Select a page** pane, select **Server Roles**, and in the **Server roles** list, ensure that **sysadmin** and **public** are selected, and select **OK**.

### Change the Service Manager Self-Service Portal application pool account

To change the Service Manager Self-Service Portal application pool account, follow these steps:

1. On the Windows desktop, select **Start**, point to **Programs**, point to **Administrative Tools**, and select **Internet Information Services (IIS) Manager**.
2. In the **Internet Information Services (IIS) Manager** window, in the **Connections** pane, expand the name of your computer, and select **Application Pools**.
3. In the **Application Pools** pane, right-click **SM_AppPool**, and select **Advanced Settings**.
4. In the **Advanced Settings** dialog, in the **Process Model** area, select **Identity**, and select the ellipsis (**...**) button.
5. In the **Application Pool Identity** dialog, select **Custom account**, and select **Set**.
6. In the **Set Credentials** dialog, in the **User name** box, enter the user name for the Operational Database Account. In the **Password** and **Confirm password** boxes, enter the password for the new Operational Database Account, and select **OK**.
7. In the **Application Pool Identity** dialog, select **OK**.
8. In the **Advanced Settings** dialog, select **OK**.
9. Close **Internet Information Services (IIS) Manager**.

### Change the Operational Database Account

To change the Operational Database Account, follow these steps:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, expand **Security**, and select **Run As Accounts**.
3. In the **Run As Accounts** pane, select **Operational Database Account**.
4. In the **Tasks** pane, select **Properties**.
5. In the **Operational Database Account** page, in the **User name**, **Password**, and **Domain** boxes, enter the new credentials for the Operational Database Account, and select **OK**.

## Change the password for the Operational Database account used by Service Manager

To change the login password for the Service Manager Data Access and Service Manager Management Configuration services, follow these steps:

1. On the Windows desktop, select **Start**, and select **Run**.
2. In the **Run** dialog, in the **Open** box, enter **services.msc**, and select **OK**.
3. In the **Services** window, in the **Services (Local)** pane, right-click **System Center Data Access Service**, and select **Properties**.
4. In the **System Center Data Access Service Properties (Local Computer)** dialog, select **Log On**.
5. Type the new password in the **Password** and **Confirm Password** text boxes, and select **OK**.
6. Restart the Service Manager Data Access Service.
7. Right-click **System Center Management Configuration**, and select **Properties**.
8. In the **System Center Management Configuration Properties (Local Computer)** dialog, select **Log On**.
9. Enter the new password in the **Password** and **Confirm Password** text boxes, and select **OK**.
10. Restart the System Center Management Configuration service.

## Change the workflow Run As account credentials used by Service Manager

During setup, you defined the account to be assigned to the Service Manager Workflow Run As account. If the password for that account changes, you must update the Workflow Run As account with the new password. If you want to change the account for the Service Manager Workflow Run As account, you must change both the Workflow Run As account and the Workflow User Role.

Use the following procedures to define a new user account for the Workflow Run As account and to update a new password for the existing account.

### Change the Workflow Run As account using new credentials

To change the Workflow Run As account using new credentials, follow these steps:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, expand **Security**, and select **Run As Accounts**.
3. In the **Run As Accounts** pane, select **Workflow Account**.
4. In the **Tasks** pane, select **Properties**.
5. In the **Workflow Account** page, in the **User name**, **Password**, and **Domain** boxes, enter the new credentials for the Workflow Run As account, and select **OK**.
6. In the **Administration** pane, select **User Roles**.
7. In the **User Roles** pane, select **Workflows**.
8. In the **Tasks** pane, select **Properties**.
9. In the Edit User Role Wizard, select **Users**.
10. Select **Remove** to remove the existing credentials, select **Add** to add the credentials you specified in step 5, and select **OK**.

    > [!IMPORTANT]
    > Failure to configure the new account for the Workflow Run As account and User Role causes Service Manager to stop functioning.

### Change the password for the Workflow Run As account credentials

To change the password for the Workflow Run As account credentials, follow these steps:

1. In the Service Manager console, select **Administration**.
2. In the **Administration** pane, expand **Administration**, expand **Security**, and select **Run As Accounts**.
3. In the **Run As Accounts** pane, select **Workflow Account**.
4. In the **Tasks** pane, select **Properties**.
5. In the **Workflow Account** page, in the **Password** box, enter the new password for the Workflow Run As account, and select **OK**.

## Change the credentials for a SQL Server Analysis Services account used by Service Manager

If the account that is used for the SQL Server Analysis Services account changes in Service Manager, you must also change the credentials for the account. Use the following procedure to change the credentials for the SQL Server Analysis Services account.

To change the credentials for the SQL Server Analysis Services account, follow these steps:

1. On the computer hosting SQL Server Analysis Server (SSAS), open **SQL Server Management Studio**.
2. In the **Connect to Server** dialog, complete these steps:
    1. In the **Server Type** list, select **Analysis Services**.
    2. In the **Server Name** list, select the server name for your Service Manager or data warehouse databases.
    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.
3. In **Microsoft SQL Server Management Studios**, in the **Object Explorer** pane, expand **Databases**, expand **DWASDataBase**, expand **Data Sources**, and then double-click **DWDataMart**.
4. In **Data Source Properties - DWDataMart**, under **Security Settings**, select the ellipsis button (**...**) next to **ImpersonateAccount**.
5. In the **Impersonation Information** window, select **Use a specific Windows user name and password**, enter the credentials for the new account, and select **OK**.
6. Select **OK** to close **Data Source Properties - DWDataMart**, and then close Microsoft SQL Server Management Studio.

## Change the credentials for the SQL Server Reporting Services account used by Service Manager

If the account that is used for the SQL Server Reporting Services account changes in Service Manager, you must change the credentials for the account. Use the following procedure to change the credentials for the SQL Server Reporting Services account.

To change the credentials for the SQL Server Reporting Services account, follow these steps:

1. On the computer hosting SQL Server Reporting Server (SSRS), start a browser, and connect to `http://<server name>/reports`.
2. On the **SQL Server Reporting Services Home** page, double-click **Service Manager**, and then double-click **DWStagingAndConfig**.
3. In the **Connect using** area, select **Credentials stored securely in the report server**, enter the current credentials in the **User name** and **Password** boxes, and select **Apply**.
4. In the browser tool bar, select the **Back** button to return to the **Service Manager** page.
5. Repeat steps 2 and 3 for the remaining Service Manager data sources.

## Change the default language for the SQL login accounts

We recommend English as the default language for the SQL users' login accounts.

As date format is based on the language, if the language of SQL user login accounts isn't English, then, a few data warehouse jobs, especially the jobs that use SQL *SET_DateFormat* function, fail. These jobs don't push the data into the data warehouse from Service Manager or might send incorrect data into the data warehouse, leading to data corruption in the data warehouse.

You can set the default language as English for a new SQL login account or change the default language for an existing account. [Learn more](deploy-sm.md#manage-default-language-for-sql-login-accounts).

## Next steps

- [Manage knowledge articles](knowledge-articles.md).
