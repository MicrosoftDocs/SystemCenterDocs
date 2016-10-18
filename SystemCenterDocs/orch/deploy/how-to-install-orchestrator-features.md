---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  How to install Orchestrator Features
ms.technology:  orchestrator
ms.assetid:  cd0b7e89-7bd2-482a-b840-f3f119e6f9ea
---

# How to install Orchestrator Features

>Applies To: System Center 2016 - Orchestrator

Use the following steps to install an System Center 2016 - Orchestrator management server.

### To install an Orchestrator management server

1.  On the server where you want to install Orchestrator, start the **System Center 2016 - Orchestrator Setup Wizard**.

    To start the **System Center 2016 - Orchestrator Setup Wizard**, on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!IMPORTANT]
    > Before you begin setup, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using System Center 2016 - Service Manager or have applied a security update, you might have to restart the computer, and then log on to the computer with the same user account to finish the installation of the server role or the security update.

    > [!NOTE]
    > If User Account Control is enabled, then you will be prompted to verify that you want to allow the setup program to run. This is because it requires administrative access to make changes to the system.

2.  On the main page of the **System Center 2016 - Orchestrator Setup Wizard**, click **Install**.

    > [!WARNING]
    > If Microsoft .NET Framework 3.5 Service Pack 1 is not installed on your computer, a dialog box appears asking if you want to install .NET Framework 3.5 SP1. Click **Yes** to proceed with the installation.

3.  On the **Product registration** page, provide the name and company for the product registration, and then click **Next**.

    > [!NOTE]
    > For this evaluation release, a product key is not required.

4.  On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and then click **Next**.

    On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and then click **Next**.

5.  On the **Select features to install** page, ensure that **Management Server** is the only feature selected, and then click **Next**.

6.  Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Click **Next** and proceed to the next step.

    If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

    1.  Review the items that did not pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

        > [!WARNING]
        > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer can require a restart. If you restart your computer, you must run setup again from the beginning.

    2.  After you resolve the missing prerequisites, click **Verify prerequisites again**.

    3.  Click **Next** to continue.

7.  On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. Click **Test** to verify the account credentials. If the credentials are accepted, then click **Next**.

8.  On the **Configure the database server** page, enter the name of the server and the name of the instance of Microsoft SQL Server that you want to use for Orchestrator. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Click **Test Database Connection** to verify the account credentials. If the credentials are accepted, click **Next**.

9. On the **Configure the database** page, select a database or create a new database, and then click **Next**.

10. On the **Configure Orchestrator users group** page, accept the default configuration or enter the name of the Active Directory user group to manage Orchestrator, and then click **Next**.

11. On the **Select the installation location** page, verify the installation location for Orchestrator and change it if you want to, and then click **Next**.

12. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and then click **Next**.

13. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and then click **Next**.

14. Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

15. On the **Setup completed successfully** page, optionally indicate whether you want to start Runbook Designer, and then click **Close** to complete the installation.

### To install an Orchestrator runbook server

1.  On the server where you want to install an Orchestrator runbook server, start the System Center 2016 - Orchestrator Setup Wizard.

    To start the **System Center 2016 - Orchestrator Setup Wizard**, on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!NOTE]
    > Before you begin setup, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using System Center 2016 - Service Manager or have applied a security update, you might have to restart the computer, and then log on to the computer with the same user account to finish the installation of the server role or the security update.

2.  On the main setup page, under **Standalone installations**, click **Runbook server**.

    > [!WARNING]
    > If Microsoft .NET Framework 3.5 Service Pack 1 is not installed on your computer, a dialog box appears asking whether you want to install .NET Framework 3.5 SP1. Click **Yes** to proceed with the installation.

3.  On the **Product registration** page, provide the name and company for the product registration, and then click **Next**.

    > [!NOTE]
    > For this evaluation release, a product key is not required.

4.  On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and then click **Next**.

    On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and then click **Next**.

5.  Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Click **Next** and proceed to the next step.

    If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

    1.  Review the items that did not pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

        > [!WARNING]
        > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer can require a restart. If you restart your computer, you must run setup again from the beginning.

    2.  After you resolve the missing prerequisites, click **Verify prerequisites again**.

    3.  Click **Next** to continue.

6.  On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. Click **Test** to verify the account credentials. If the credentials are accepted, click **Next**.

7.  On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Click **Test Database Connection** to verify the account credentials. If the credentials are accepted, click **Next**.

8.  On the **Configure the database** page, select the Orchestrator database for your deployment, and then click **Next**.

9. On the **Select the installation location** page, verify the installation location for Orchestrator, and then click **Next**.

10. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and then click **Next**.

11. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and then click **Next**.

12. Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

13. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and then click **Close** to complete the installation.

### To install the Orchestrator web service

1.  On the server where you want to install the Orchestrator web service, start the **System Center 2016 - Orchestrator Setup Wizard**.

    To start the **System Center 2016 - Orchestrator Setup Wizard**, on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!NOTE]
    > Before you begin the installation of the Orchestrator web service, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using System Center 2016 Technical Preview - Service Manager or have applied a security update, you might have to restart the computer, and then log on to the computer with the same user account to finish the installation of the server role or the security update.

2.  On the main setup page, under **Standalone installations**, click **Orchestration Console and Web Service**.

    > [!WARNING]
    > If Microsoft .NET Framework 3.5 Service Pack 1 is not installed on your computer, a dialog box appears asking if you want to install .NET Framework 3.5 SP1. Click **Yes** to proceed with the installation.

3.  On the **Product registration** page, provide the name and company for the product registration, and then click **Next**.

    > [!NOTE]
    > For this evaluation release, a product key is not required.

4.  On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and then click **Next**.

    On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and then click **Next**.

5.  Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Click **Next** and proceed to the next step.

    If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

    1.  Review the items that did not pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

        > [!WARNING]
        > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer can require a restart. If you restart your computer, you must run setup again from the beginning.

    2.  After you resolve the missing prerequisites, click **Verify prerequisites again**.

    3.  Click **Next** to continue.

6.  On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. Click **Test** to verify the account credentials. If the credentials are accepted, click **Next**.

7.  On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Click **Test Database Connection** to verify the account credentials. If the credentials are accepted, click **Next**.

8.  On the **Configure the database** page, select the Orchestrator database for your deployment, and then click **Next**.

9. On the **Configure the port for the web service** page, verify the port numbers for the Orchestrator web service and the Orchestration console, and then click **Next**.

10. On the **Select the installation location** page, verify the installation location for Orchestrator, and then click **Next**.

11. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and then click **Next**.

12. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and then click **Next**.

13. Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

14. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and then click **Close** to complete the installation.

### To install the Orchestrator Runbook Designer on a single computer

1.  On the server where you want to install the Orchestrator Runbook Designer, start the **System Center 2016 - Orchestrator Setup Wizard**.

    To start the **System Center 2016 - Orchestrator Setup Wizard**, on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!NOTE]
    > Before you begin the install of the Runbook Designer, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using System Center 2016 Technical Preview - Service Manager or have applied a security update, you might have to restart the computer, and then log on to the computer with the same user account to finish the installation of the server role or the security update.

2.  On the main **System Center 2016 - Orchestrator Setup Wizard** page, click **Runbook Designer**.

    > [!WARNING]
    > If Microsoft .NET Framework 3.5 Service Pack 1 is not installed on your computer, a dialog box appears asking if you want to install .NET Framework 3.5 SP1. Click **Yes** to proceed with the installation.

3. On the **Product registration** page, provide the name and company for the product registration, and then click **Next**.

      > [!NOTE]
      > For this evaluation release, a product key is not required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and then click **Next**.

5. On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and then click **Next**.

6.  Your computer is checked for required hardware and software. If your computer meets all of the requirements, proceed to the next step.

    If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

    1.  Review the items that did not pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

    2.  After you resolve the missing prerequisites, click **Verify prerequisites again**.

    3.  Click **Next** to continue.

7.  On the **Select the installation location** page, verify the installation location for Orchestrator and change it if you want to, and then click **Next**.

8. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and then click **Next**.

9. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and then click **Next**.

10.  Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

11.  On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and then click **Close** to complete the installation.

### To connect a Runbook Designer to a management server

1.  In the Runbook Designer, select the **Connect to a server** icon in the navigation pane under the **Connections** pane.

    > [!NOTE]
    > If the Runbook Designer is connected to another management server, the **Connect to a server** icon is disabled. Click the **Disconnect** icon before you connect to a different management server.

2.  In the **System Center Orchestrator 2016 Connection** dialog box, enter the name of the server that hosts your Orchestrator management server, and then click **OK**.

### To enable network discovery

1.  On the desktop of your computer running Windows server, click **Start**, click **Control Panel**, click **Network and Internet**, click **Network and Sharing Center**, click **Choose Home group and Sharing Options**, and then click **Change advanced sharing settings**.

2.  To change the **Domain** profile, if needed, click the **Arrow** icon to expand the section options and make any necessary changes.

3.  Select **Turn on network discovery**, and then click **Save changes**.

    If you are prompted for an administrator password or confirmation, type the password or provide confirmation.
