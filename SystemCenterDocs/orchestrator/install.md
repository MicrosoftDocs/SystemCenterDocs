---
title: Install Orchestrator
description: Provides instructions for installing System Center - Orchestrator
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 03/19/2025
ms.service: system-center
ms.subservice: orchestrator
ms.topic: article
ms.custom: UpdateFrequency.5, intro-installation, engagement-fy23
---

# Install System Center - Orchestrator

::: moniker range=">=sc-orch-2022"

A complete Orchestrator installation includes:

- a management server
- one or more runbook servers
- a SQL Server for hosting the Orchestrator database
- a web server for hosting the Orchestrator web API service
- a server for hosting the Runbook Designer and Runbook Tester
- a web server for hosting the Orchestration Console

It's possible to install all these roles and components on a single computer, but it's more common to distribute the roles across several computers or virtual machines.

For a detailed description of the Orchestrator architecture, see [Learn about Orchestrator](./learn-about-orchestrator.md).

To know about the prerequisites, see [System requirements for System Center Orchestrator](./system-requirements-orch.md).

This article provides detailed installation instructions for the various Orchestrator roles.

>[!NOTE]
>Install the [Microsoft Visual C++ Redistributable](/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022&preserve-view=true) package before running the Setup executable (SetupOrchestrator.exe).

::: moniker-end

::: moniker range="<=sc-orch-2019"

A complete Orchestrator installation includes a management server, one or more runbook servers, a SQL Server for hosting the Orchestrator database, a web server for hosting the Orchestrator web service, and a server for hosting the Runbook Designer and Runbook Tester. It's possible to install all these roles on a single computer, but it's more common to distribute the roles across several computers or virtual machines.

For a detailed description of the Orchestrator architecture, see [Learn about Orchestrator](learn-about-orchestrator.md).

This article provides detailed installation instructions for the various Orchestrator roles.

::: moniker-end

::: moniker range=">=sc-orch-2019"

[!INCLUDE [validation-orchestrator.md](../includes/validation-orchestrator.md)]

::: moniker-end

## Install an Orchestrator management server

::: moniker range=">=sc-orch-2022"

1. On the server where you want to install the Orchestrator, install the [Microsoft Visual C++ Redistributable](/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022&preserve-view=true) package and start the Orchestrator Setup Wizard.

    To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!IMPORTANT]
    > Before you begin setup, close any open programs, and ensure that there are no pending restarts on the computer. For example, if you've installed a server role by using System Center - Service Manager or have applied a security update, you might have to restart the computer, and then sign in to the computer with the same user account to finish the installation of the server role or the security update.

    > [!NOTE]
    > If User Account Control is enabled, you will be prompted to verify that you want to allow the setup program to run. This is because it requires administrative access to make changes to the system.

2. On the main page of the wizard, select **Install**.

3. On the **Product registration** page, provide the name and company for the product registration, and select **Next**.

    > [!NOTE]
    > For this evaluation release, a product key isn't required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms and select **Next**.

    On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice and then select **Next**.

5. On the **Select features to install** page, ensure that **Management Server** is the only feature selected and select **Next**.

6. Your computer is checked for required hardware and software. If your computer meets all the requirements, the **All prerequisites are installed** page appears. Select **Next** and proceed to the next step.

If a prerequisite isn't met, a page displays the information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

1. Review the items that didn't pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

   > [!WARNING]
   > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer can require a restart. If you restart your computer, you must run setup again from the beginning.

2. After you resolve the missing prerequisites, select **Verify prerequisites again**.

3. Select **Next** to continue.

4. On the **Configure the service account** page, enter the username and password for the Orchestrator service account. Select **Test** to verify the account credentials. If the credentials are accepted, select **Next**.

::: moniker-end

::: moniker range="sc-orch-2022"
5. On the **Configure the database server** page, enter the name of the server and the name of the instance of Microsoft SQL Server that you want to use for Orchestrator. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Select **Test Database Connection** to verify the account credentials. If the credentials are accepted, select **Next**.
::: moniker-end

::: moniker range="sc-orch-2025"
5. On the **Configure the database server** page, enter the name of the server and the name of the instance of Microsoft SQL Server that you want to use for Orchestrator. Connection with SQL server is encrypted by default. You must install a certificate that client can trust or you can follow the [Secure Connection to SQL server](#secure-connection-to-sql-server) to bypass the recommended trust mechanism. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Select **Test Database Connection** to verify the account credentials. If the credentials are accepted, select **Next**.
::: moniker-end

::: moniker range=">=sc-orch-2022"
6. On the **Configure the database** page, select a database or create a new database, and select **Next**.

7. On the **Configure Orchestrator users group** page, accept the default configuration or enter the name of the Active Directory user group to manage Orchestrator, and select **Next**.

8. On the **Select the installation location** page, verify the installation location for Orchestrator and change it if you want to, and select **Next**.

9. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and select **Next**.

10. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and select **Next**.

11. Review the **Installation summary** page, and select **Install**.

    The **Installing features** page appears and displays the installation progress.

12. On the **Setup completed successfully** page, optionally indicate whether you want to start Runbook Designer, and select **Close** to complete the installation.

::: moniker-end

::: moniker range="<=sc-orch-2019"

1.  On the server where you want to install Orchestrator, start the Orchestrator Setup Wizard.

    To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!IMPORTANT]
    > Before you begin setup, close any open programs and ensure that there are no pending restarts on the computer. For example, if you've installed a server role by using System Center - Service Manager or have applied a security update, you might have to restart the computer, and then sign in to the computer with the same user account to finish the installation of the server role or the security update.

    > [!NOTE]
    > If User Account Control is enabled, then you will be prompted to verify that you want to allow the setup program to run. This is because it requires administrative access to make changes to the system.

2.  On the main page of the wizard, select **Install**.

    > [!WARNING]
    > If Microsoft .NET Framework 3.5 Service Pack 1 isn't installed on your computer, a dialog appears asking if you want to install .NET Framework 3.5 SP1. Select **Yes** to proceed with the installation.

3.  On the **Product registration** page, provide the name and company for the product registration, and select **Next**.

    > [!NOTE]
    > For this evaluation release, a product key isn't required.

4.  On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and select **Next**.

    On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and select **Next**.

5.  On the **Select features to install** page, ensure that **Management Server** is the only feature selected, and select **Next**.

6.  Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Select **Next** and proceed to the next step.

::: moniker-end

::: moniker range="<=sc-orch-2019"

   If a prerequisite isn't met, a page displays information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

1. Review the items that didn't pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

   > [!WARNING]
   > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer can require a restart. If you restart your computer, you must run setup again from the beginning.

2. After you resolve the missing prerequisites, select **Verify prerequisites again**.

3. Select **Next** to continue.

4. On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. Select **Test** to verify the account credentials. If the credentials are accepted, select **Next**.

5. On the **Configure the database server** page, enter the name of the server and the name of the instance of Microsoft SQL Server that you want to use for Orchestrator. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Select **Test Database Connection** to verify the account credentials. If the credentials are accepted, select **Next**.

6. On the **Configure the database** page, select a database or create a new database, and select **Next**.

7. On the **Configure Orchestrator users group** page, accept the default configuration or enter the name of the Active Directory user group to manage Orchestrator, and select **Next**.

8. On the **Select the installation location** page, verify the installation location for Orchestrator and change it if you want to, and select **Next**.

9. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and select **Next**.

10. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and select **Next**.

11. Review the **Installation summary** page, and select **Install**.

    The **Installing features** page appears and displays the installation progress.

12. On the **Setup completed successfully** page, optionally indicate whether you want to start Runbook Designer, and select **Close** to complete the installation.

::: moniker-end

## Install Orchestrator runbook server

::: moniker range=">=sc-orch-2022"

1. On the server where you want to install the Orchestrator runbook server, install the [Microsoft Visual C++ Redistributable](/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022&preserve-view=true) package and start the Orchestrator Setup Wizard.

   To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

   > [!NOTE]
   > Before you begin setup, close any open programs, and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using System Center - Service Manager or have applied a security update, you might have to restart the computer, and then sign in to the computer with the same user account to finish the installation of the server role or the security update.

2. On the main setup page, under **Standalone installations**, select **Runbook server**.

3. On the **Product registration** page, provide the name and company for the product registration and select **Next**.

   > [!NOTE]
   > For this evaluation release, a product key isn't required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and select **Next**.

   On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice and select **Next**.

5. Your computer is checked for the required hardware and software. If your computer meets all the requirements, the **All prerequisites are installed** page appears. Select **Next** and proceed to the next step.

   If a prerequisite isn't met, a page displays information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

   1. Review the items that didn't pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

      > [!WARNING]
      > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer may require a restart. If you restart your computer, you must run setup again from the beginning.

   2. After you resolve the missing prerequisites, select **Verify prerequisites again**.

   3. Select **Next** to continue.

6. On the **Configure the service account** page, enter the username and password for the Orchestrator service account. Select **Test** to verify the account credentials. If the credentials are accepted, select **Next**.
::: moniker-end
::: moniker range="sc-orch-2022"
7. On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Select **Test Database Connection** to verify the account credentials. If the credentials are accepted, select **Next**.
::: moniker-end

::: moniker range="sc-orch-2025"
7. On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. Connection with SQL server is encrypted by default. You must install a certificate that client can trust or you can follow the [Secure Connection to SQL server](#secure-connection-to-sql-server) to bypass the recommended trust mechanism. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Select **Test Database Connection** to verify the account credentials. If the credentials are accepted, select **Next**.
::: moniker-end
::: moniker range=">=sc-orch-2022"
8. On the **Configure the database** page, select the Orchestrator database for your deployment, and select **Next**.

9. On the **Select the installation location** page, verify the installation location for Orchestrator, and select **Next**.

10. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and select **Next**.

11. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and select **Next**.

12. Review the **Installation summary** page, and select **Install**.

    The **Installing features** page appears and displays the installation progress.

13. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and select **Close** to complete the installation.

::: moniker-end

::: moniker range="<=sc-orch-2019"
1. On the server where you want to install an Orchestrator runbook server, start the Orchestrator Setup Wizard.

   To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

   > [!NOTE]
   > Before you begin setup, close any open programs and ensure that there are no pending restarts on the computer. For example, if you've installed a server role by using System Center - Service Manager or have applied a security update, you might have to restart the computer, and then sign in to the computer with the same user account to finish the installation of the server role or the security update.

2. On the main setup page, under **Standalone installations**, select **Runbook server**.

   > [!WARNING]
   > If Microsoft .NET Framework 3.5 Service Pack 1 isn't installed on your computer, a dialog appears asking whether you want to install .NET Framework 3.5 SP1. Select **Yes** to proceed with the installation.

3. On the **Product registration** page, provide the name and company for the product registration and select **Next**.

   > [!NOTE]
   > For this evaluation release, a product key isn't required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and select **Next**.

   On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and select **Next**.

5. Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Select **Next** and proceed to the next step.

::: moniker-end

::: moniker range="<=sc-orch-2019"

   If a prerequisite isn't met, a page displays information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

   1. Review the items that didn't pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

      > [!WARNING]
      > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer can require a restart. If you restart your computer, you must run setup again from the beginning.

   2. After you resolve the missing prerequisites, select **Verify prerequisites again**.

   3. Select **Next** to continue.

6. On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. Select **Test** to verify the account credentials. If the credentials are accepted, select **Next**.

7. On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Select **Test Database Connection** to verify the account credentials. If the credentials are accepted, select **Next**.

8. On the **Configure the database** page, select the Orchestrator database for your deployment, and select **Next**.

9. On the **Select the installation location** page, verify the installation location for Orchestrator, and select **Next**.

10. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and select **Next**.

11. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and select **Next**.

12. Review the **Installation summary** page, and select **Install**.

    The **Installing features** page appears and displays the installation progress.

13. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and select **Close** to complete the installation.

::: moniker-end

## Install Orchestrator Web API service

::: moniker range=">=sc-orch-2022"

Since Orchestrator 2022, the Web API service and Orchestration Console can be installed separately on different machines.

1. On the server where you want to install the Orchestrator web API, install the [Microsoft Visual C++ Redistributable](/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022&preserve-view=true) package and start the Orchestrator Setup Wizard.

   To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

   > [!NOTE]
   > Before you begin the installation of the Orchestrator Web API service, close any open programs, and ensure that there're no pending restarts on the computer. Then sign in to the computer with the same user account to finish the installation of the server role or the security update.

2. On the main setup page, under **Standalone installations**, select **Web API Service**.

3. On the **Product registration** page, provide the name and company for the product registration and select **Next**.

   > [!NOTE]
   > For this evaluation release, a product key isn't required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and select **Next**.

   On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and select **Next**.

::: moniker-end

::: moniker range="sc-orch-2022"

5. Your computer is checked for required the hardware and software. If your computer meets all the requirements, the **All prerequisites are installed** page appears. Select **Next** and proceed to the next step.

   If a prerequisite isn't met, a page displays information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

   1. Review the items that didn't pass the prerequisite check. The Web API requires .NET Hosting bundle v5.x and some IIS extensions. Download and install them from the official sites:
      -	.NET Hosting bundle
      -	IIS CORS (Cross-Origin Resource Sharing) module

   2. After you resolve the missing prerequisites, select **Verify prerequisites again**.

   3. Select **Next** to continue.

::: moniker-end

::: moniker range="sc-orch-2025"

5. Your computer is checked for required the hardware and software. If your computer meets all the requirements, the **All prerequisites are installed** page appears. Select **Next** and proceed to the next step.

   If a prerequisite isn't met, a page displays information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

   1. Review the items that didn't pass the prerequisite check. The Web API requires .NET Hosting bundle v8.x and some IIS extensions. Download and install them from the official sites:
      -	.NET Hosting bundle
      -	IIS CORS (Cross-Origin Resource Sharing) module

   2. After you resolve the missing prerequisites, select **Verify prerequisites again**.

   3. Select **Next** to continue.

::: moniker-end


::: moniker range=">=sc-orch-2022"

6. On the **Configure the service account** page, enter the username and password for the Orchestrator service account. The Web API runs under an IIS App Pool with this identity. Select **Test** to verify the account credentials. If the credentials are accepted, select **Next**.

    > [!NOTE]
    > If the service account you enter here is not a member of the local Administrators group, you must grant the user permissions in the IIS Metabase. To do this, open an administrative command window, navigate to the directory **C:\Windows\Microsoft.NET\Framework64\v4.0.30319** and run the below command. Replace DOMAIN\USER with the domain and username of the service account.
    > ```
    > aspnet_regiis.exe -ga DOMAIN\USER
    > ```
::: moniker-end

::: moniker range="sc-orch-2022"
7. On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. If Windows Authentication is selected, the service account credentials from previous steps are used to connect to the database. Select **Test Database Connection** to verify the account credentials. If the credentials are accepted, select **Next**.
::: moniker-end

::: moniker range="sc-orch-2025"
7. On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. Connection with SQL server is encrypted by default. You must install a certificate that client can trust or you can follow the [Secure Connection to SQL server](#secure-connection-to-sql-server) to bypass the recommended trust mechanism. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. If Windows Authentication is selected, the service account credentials from previous steps are used to connect to the database. Select **Test Database Connection** to verify the account credentials. If the credentials are accepted, select **Next**.
::: moniker-end

::: moniker range=">=sc-orch-2022"

8. On the **Configure the database** page, select the Orchestrator database for your deployment, and select **Next**.

9. On the **Configure CORS (Cross-Origin Resource Sharing) and the port for the Web API** page, verify the port numbers for the Orchestrator Web API service and the URL of the Orchestration console, and select **Next**.

10. On the **Select the installation location** page, verify the installation location for Orchestrator, and select **Next**.

11. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and select **Next**.

12. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and select **Next**.

13. Review the **Installation summary** page, and select **Install**.

[Learn](#configure-your-installation) how to configure the API after installation.

::: moniker-end

::: moniker range="sc-orch-2025"

>[!NOTE]
>The setup tries to enable some IIS features, this fails if those features are already enabled. This is true for machines where (even previous version of) Orchestrator Web API was previously installed. You can check this in the Setup logs on `%AppData%\Local\Microsoft System Center 2012\Orchestrator\LOGS\*.log` where you’ll see the error about IIS features. To skip this step, run Setup.exe from the command prompt.  

::: moniker-end

::: moniker range=">=sc-orch-2022"

The **Installing features** page appears and displays the installation progress.

::: moniker-end

::: moniker range="<=sc-orch-2019"

1. On the server where you want to install the Orchestrator web service, start the Orchestrator Setup Wizard.

   To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

   > [!NOTE]
   > Before you begin the installation of the Orchestrator web service, close any open programs and ensure that there are no pending restarts on the computer. Then sign in to the computer with the same user account to finish the installation of the server role or the security update.

2. On the main setup page, under **Standalone installations**, select **Orchestration Console and Web Service**.

   > [!WARNING]
   > If Microsoft .NET Framework 3.5 Service Pack 1 isn't installed on your computer, a dialog appears asking if you want to install .NET Framework 3.5 SP1. Select **Yes** to proceed with the installation.

3. On the **Product registration** page, provide the name and company for the product registration, and select **Next**.

   > [!NOTE]
   > For this evaluation release, a product key isn't required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and select **Next**.

   On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and select **Next**.

5. Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Select **Next** and proceed to the next step.

   If a prerequisite isn't met, a page displays information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

   1. Review the items that didn't pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

      > [!WARNING]
      > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer can require a restart. If you restart your computer, you must run setup again from the beginning.

   2. After you resolve the missing prerequisites, select **Verify prerequisites again**.

   3. Select **Next** to continue.

6. On the **Configure the service account** page, enter the user name and password for the Orchestrator service account. Select **Test** to verify the account credentials. If the credentials are accepted, select **Next**.

7. On the **Configure the database server** page, enter the name of the database server associated with your Orchestrator management server. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database. Select **Test Database Connection** to verify the account credentials. If the credentials are accepted, select **Next**.

8. On the **Configure the database** page, select the Orchestrator database for your deployment, and select **Next**.

9. On the **Configure the port for the web service** page, verify the port numbers for the Orchestrator web service and the Orchestration console, and select **Next**.

10. On the **Select the installation location** page, verify the installation location for Orchestrator, and select **Next**.

11. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and select **Next**.

12. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and select **Next**.

13. Review the **Installation summary** page, and select **Install**.

    The **Installing features** page appears and displays the installation progress.

14. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and select **Close** to complete the installation.

::: moniker-end

::: moniker range=">=sc-orch-2022"

## Install Orchestration Console

Since Orchestrator 2022, the Web API service and Orchestration Console can be installed separately on different machines.

1.	On the server where you want to install the Orchestration Console, install the [Microsoft Visual C++ Redistributable](/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022&preserve-view=true) package and start the Orchestrator Setup Wizard. To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

2.	On the main **Setup** page, under **Standalone installations**, select **Orchestration Console**.

3.	On the **Product registration** page, provide the name and company for the product registration, and select **Next**.

    >[!NOTE]
    >For this evaluation release, a product key isn't required.

4.	On the **Please read this License Terms** page, review, and accept the Microsoft Software License Terms, and select **Next**.

    On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and select **Next**.

5.	Your computer is checked for required hardware and software. If your computer meets all the requirements, **All prerequisites are installed** page appears. Select **Next** and proceed to the next step.

    If a prerequisite isn't met, a page displays information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

    Orchestration Console requires IIS URL Rewrite module; download from here.

6. On the **Configure the service account** page, enter the username and password for the Orchestrator service account. The Console runs under an IIS App Pool with this identity. Select **Test to verify the account credentials**. If the credentials are accepted, select **Next**.

    > [!NOTE]
    > If the service account you enter here is not a member of the local Administrators group, you must grant the user permissions in the IIS Metabase. To do this, open an administrative command window, navigate to the directory **C:\Windows\Microsoft.NET\Framework64\v4.0.30319** and run the below command. Replace DOMAIN\USER with the domain and username of the service account.
    > ```
    > aspnet_regiis.exe -ga DOMAIN\USER
    > ```

7.	On the **Configure the ports for the Web Console** page, verify the port numbers for the Orchestration Console service and the URL of the Web API service, and select **Next**.

    >[!NOTE]
    >The Web API URL should not have a trailing forward slash `/`.

8.	On the **Select the installation location** page, verify the installation location for Orchestrator, and select **Next**.

9. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates and select **Next**.

10. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in Error Reporting, and select **Next**.

11. Review the **Installation summary** page and select **Install**.

[Learn](#configure-your-installation) how to configure the Console after installation.

The **Installing features** page appears and displays the installation progress.

::: moniker-end

::: moniker range="<=sc-orch-2019"

## Install the Orchestrator Runbook Designer on a single computer

1.  On the server where you want to install the Orchestrator Runbook Designer, start the Orchestrator Setup Wizard.

    To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!NOTE]
    > Before you begin the install of the Runbook Designer, close any open programs and ensure that there are no pending restarts on the computer. Then, sign in to the computer with the same user account to finish the installation of the server role or the security update.

2.  On the main wizard page, select **Runbook Designer**.

    > [!WARNING]
    > If Microsoft .NET Framework 3.5 Service Pack 1 isn't installed on your computer, a dialog appears asking if you want to install .NET Framework 3.5 SP1. Select **Yes** to proceed with the installation.

3. On the **Product registration** page, provide the name and company for the product registration, and select **Next**.

      > [!NOTE]
      > For this evaluation release, a product key isn't required.

4. On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and select **Next**.

5. On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and select **Next**.

6.  Your computer is checked for required hardware and software. If your computer meets all of the requirements, proceed to the next step.

   If a prerequisite isn't met, a page displays information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

1.  Review the items that didn't pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

   2.  After you resolve the missing prerequisites, select **Verify prerequisites again**.

   3.  Select **Next** to continue.

4. On the **Select the installation location** page, verify the installation location for Orchestrator and change it if you want to, and select

5. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and select **Next**.

6. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and select **Next**.

7. Review the **Installation summary** page, and select **Install**.

    The **Installing features** page appears and displays the installation progress.

8. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and select **Close** to complete the installation.

::: moniker-end

## Connect a Runbook Designer to a management server

1. In the Runbook Designer, select the **Connect to a server** icon in the navigation pane under the **Connections** pane.

    > [!NOTE]
    > If the Runbook Designer is connected to another management server, the **Connect to a server** icon is disabled. Select the **Disconnect** icon before you connect to a different management server.

2. In **System Center Orchestrator Connection**, enter the name of the server that hosts your Orchestrator management server, and select **OK**.

## Enable network discovery

1. On the desktop of your computer running Windows server, select **Start**, select **Control Panel**, select **Network and Internet**, select **Network and Sharing Center**, select **Choose Home group and Sharing Options**, and select **Change advanced sharing settings**.

2. To change the **Domain** profile, if needed, select the **Arrow** icon to expand the section options and make any necessary changes.

3. Select **Turn on network discovery**, and select **Save changes**.

    If you're prompted for an administrator password or confirmation, enter the password or provide confirmation.

::: moniker range="sc-orch-2025"

## Secure connection to SQL server

Due to breaking changes in EFCore 8 and OLEDB 19, SQL Server connection is encrypted by default and requires a certificate that client can trust which means:
- The SQL Server must be configured with a valid certificate
- The client must trust this certificate

If these conditions aren't met, then a SqlException is thrown. For example:

A connection was successfully established with the server, but then an error occurred during the login process. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)

Following are the three ways to mitigate this error:

- Option 1: [Install a valid certificate on a server](/sql/database-engine/configure-windows/configure-sql-server-encryption?view=sql-server-ver16).
  
    >[!Note]
    > It is recommended to obtain a certificate and ensure it is signed by an authority trusted by the client.
    
- Option 2: `TrustServerCertificate=True` to allow bypassing the normal trust mechanism (not recommended). For more information, see [How encryption and certificate validation works](/sql/connect/oledb/features/encryption-and-certificate-validation?view=sql-server-ver16#encryption-and-certificate-validation-behavior).

    1. Set registry setting for Trust Server Certificate to **True** (Set this flag Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI19.0\GeneralFlags\Flag2). [Learn more](/sql/connect/oledb/features/registry-settings?view=sql-server-ver16#trust-server-certificate).
    1. During installation, check the checkbox **Yes, Trust Server Certificate (not recommended)**.
       Following configuration occurs:
          1. For SQL Connection string, adds *Trust Server Certificate=true*.
          1. In webapi.config, adds \<environmentVariable name="Database__TrustServerCertificate" value="true"/\>

       :::image type="content" source="media/install/configuration.png" alt-text="Screenshot showing configuration screen.":::

       Alternatively, On the **Data Store Configuration** page, in **Server**, enter `localhost;Trust Server Certificate=True` and this results in the following:


       :::image type="content" source="media/install/server-details.png" alt-text="Screenshot showing server details.":::


- Option 3: Use Data Store configuration to explicitly set *Server = localhost;Use encryption for Data=False* to the connection string (not recommended) to not encrypt the connection.

>[!Warning]
> Options 2 and 3 both leave the server in a potentially insecure state.

::: moniker-end

## Install Orchestrator Runbook Designer

1. On the server where you want to install the Orchestrator Runbook Designer, install the [Microsoft Visual C++ Redistributable](/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022&preserve-view=true) package and start the Orchestrator Setup Wizard.

    To start the wizard on your product media or network share, double-click **SetupOrchestrator.exe**.

    > [!NOTE]
    > Before you begin the install of the Runbook Designer, close any open programs, and ensure that there are no pending restarts on the computer. Then, sign in to the computer with the same user account to finish the installation of the server role or the security update.

2. On the main wizard page, select **Runbook Designer**.

3. On the **Product registration** page, provide the name and company for the product registration, and select **Next**.

   > [!NOTE]
   > For this evaluation release, a product key isn't required.

4. On the **Please read this License Terms** page, review, and accept the Microsoft Software License Terms, and select **Next**.

   On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice and select **Next**.

5. Your computer is checked for the required hardware and software. If your computer meets all the requirements, proceed to the next step.

   If a prerequisite isn't met, a page displays information about the prerequisite that hasn't been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

   1. Review the items that didn't pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services (IIS) role.

   2. After you resolve the missing prerequisites, select **Verify prerequisites again**.

   3. Select **Next** to continue.

6. On the **Select the installation location** page, verify the installation location for Orchestrator and change it if you want to, and select **Next**.

7. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and select **Next**.

8. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and select **Next**.

9. Review the **Installation summary** page, and select **Install**.

    The **Installing features** page appears and displays the installation progress.

10. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and select **Close** to complete the installation.

## Install from the command prompt

To install Orchestrator at a command prompt, use Setup.exe with the command-line options in the following table.

::: moniker range="<=sc-orch-2022"

|Option|Description|
|----------|---------------|
|/Silent|Installation is performed without displaying a dialog.|
|/Uninstall|Product is uninstalled. This option is performed silently.|
|/Key:[Product Key]|Specifies the product key. If no product key is specified, Orchestrator is installed as an evaluation edition.|
|/ServiceUserName:[UserName]|Specifies the user account for the Orchestrator Management Service. This value is required if you're installing Management Server, Runbook Server, or web services.|
|/ServicePassword:[Password]|Specifies the password for the user account for the Orchestrator Management Service. This value is required if you're installing Management Server, Runbook Server, or web services.|
|/Components:[Feature 1, Feature 2,"]|Specifies the features to install (comma separated). Possible values are ManagementServer, RunbookServer, RunbookDesigner, WebAPI, WebConsole and All.|
|/InstallDir:[Path]|Specifies the path to install Orchestrator. If no path is specified, C:\Program Files\Microsoft System Center\<version\>\Orchestrator is used.|
|/DbServer:[Computer[\Instance]]|Specifies the computer name and instance of the database server. This value is required if you're installing Management Server, Runbook Server, or web services.|
|/DbUser:[UserName]|Specifies the user account to access the database server. This value is only required for SQL Authentication. If Windows Authentication is used, no value should be specified.|
|/DbPassword:[Password]|Specifies the password for the user account to access the database server. This value is only required for SQL Authentication. If Windows Authentication is used, then no value should be specified.|
|/DbNameNew:[Database Name]|Specifies the database name if a new database is being created. Can't be used with DbNameExisting.|
|/DbNameExisting:[Database Name]|Specifies the database name if an existing database is being used. Can't be used with DbNameNew.|
|/WebServicePort:[Port]|Specifies the port to use for the Web API service. Required if Web API service is installed.|
|/WebConsolePublicUrl: [URL]|Specifies the URL of the Orchestration Console that should be used to configure CORS on the Web API. Required if Web API service is installed.|
|/WebConsolePort:[Port]|Specifies the port to use for the Orchestrator console. Required if Orchestrator Console is installed.|
|/WebServicePublicUrl:[URL]|Specifies the URL of the web API service that should be used by the Orchestration Console. Required if Orchestration Console is installed.|
|/OrchestratorUsersGroup:[Group SID]|Specifies the SID of the domain or local group that will be granted access to Management server. If no value is specified, the default local group is used.|
|/OrchestratorRemote|Specifies that remote access should be granted to the Runbook Designer.|
|/UseMicrosoftUpdate:[0&#124;1]|Specifies whether to opt in for Microsoft Update. A value of 1 will opt in. A value of 0 doesn't change the current opt-in status of the computer.|
|/SendTelemetryReports:[0&#124;1]|Specifies Orchestrator to send Diagnostics and Usage data to Microsoft. 0 to opt out from sending Telemetry. **Telemetry is on by default.**|
|/EnableErrorReporting:[value]|Specifies that Orchestrator should send program error reports to Microsoft. Possible values are always, queued, and never.|

::: moniker-end

::: moniker range="sc-orch-2025"

|Option|Description|
|----------|---------------|
|/Silent|Installation is performed without displaying a dialog.|
|/Uninstall|Product is uninstalled. This option is performed silently.|
|/Key:[Product Key]|Specifies the product key. If no product key is specified, Orchestrator is installed as an evaluation edition.|
|/ServiceUserName:[UserName]|Specifies the user account for the Orchestrator Management Service. This value is required if you're installing Management Server, Runbook Server, or web services.|
|/ServicePassword:[Password]|Specifies the password for the user account for the Orchestrator Management Service. This value is required if you're installing Management Server, Runbook Server, or web services.|
|/Components:[Feature 1, Feature 2,"]|Specifies the features to install (comma separated). Possible values are ManagementServer, RunbookServer, RunbookDesigner, WebAPI, WebConsole and All.|
|/InstallDir:[Path]|Specifies the path to install Orchestrator. If no path is specified, C:\Program Files\Microsoft System Center\<version\>\Orchestrator is used.|
|/DbServer:[Computer[\Instance]]|Specifies the computer name and instance of the database server. This value is required if you're installing Management Server, Runbook Server, or web services.|
|/DbUser:[UserName]|Specifies the user account to access the database server. This value is only required for SQL Authentication. If Windows Authentication is used, no value should be specified.|
|/DbPassword:[Password]|Specifies the password for the user account to access the database server. This value is only required for SQL Authentication. If Windows Authentication is used, then no value should be specified.|
|/DbNameNew:[Database Name]|Specifies the database name if a new database is being created. Can't be used with DbNameExisting.|
|/DbNameExisting:[Database Name]|Specifies the database name if an existing database is being used. Can't be used with DbNameNew.|
|/TrustServerCertificate[true\false]|Specifies whether to trust SQL Server Certificate. **Set to false by default**.|
|/WebServicePort:[Port]|Specifies the port to use for the Web API service. Required if Web API service is installed.|
|/WebConsolePublicUrl: [URL]|Specifies the URL of the Orchestration Console that should be used to configure CORS on the Web API. Required if Web API service is installed.|
|/WebConsolePort:[Port]|Specifies the port to use for the Orchestrator console. Required if Orchestrator Console is installed.|
|/WebServicePublicUrl:[URL]|Specifies the URL of the web API service that should be used by the Orchestration Console. Required if Orchestration Console is installed.|
|/OrchestratorUsersGroup:[Group SID]|Specifies the SID of the domain or local group that will be granted access to Management server. If no value is specified, the default local group is used.|
|/OrchestratorRemote|Specifies that remote access should be granted to the Runbook Designer.|
|/UseMicrosoftUpdate:[0&#124;1]|Specifies whether to opt in for Microsoft Update. A value of 1 will opt in. A value of 0 doesn't change the current opt-in status of the computer.|
|/SendTelemetryReports:[0&#124;1]|Specifies Orchestrator to send Diagnostics and Usage data to Microsoft. 0 to opt out from sending Telemetry. **Telemetry is on by default.**|
|/EnableErrorReporting:[value]|Specifies that Orchestrator should send program error reports to Microsoft. Possible values are always, queued, and never.|

::: moniker-end

For example, you could use the following command to install all the Orchestrator components using Windows Authentication.

```
.\Setup.exe /Silent /ServiceUserName:<UserName> /ServicePassword:<password> /Components:All /DbServer:<DBServerName> /DbNameNew:Orchestrator /WebServicePort:81 /WebConsolePublicUrl:”http://localhost:82” /WebConsolePort:82 /WebServicePublicUrl:”http://localhost:81”   /UseMicrosoftUpdate:1 /SendTelemetryReports:1 /EnableErrorReporting:always
```

## View runbook server properties

The properties for a runbook server include an optional description and the account information to use for the Runbook Service. You can modify the description but can only view the service credentials.

1.  In the **Connections**  pane, select the Runbook Servers folder. In the right pane, right-click the runbook server to select **Properties**.  

2.  If you want to add or change the **Description** box, enter a description for this runbook server, and select **Finish**.

::: moniker range=">=sc-orch-2022"
## Configure your installation

### Enable API logging to file

Toggle the XML attribute `stdoutLogEnabled` to `true` in your `web.config` under `system.WebServer` > `aspNetCore`.

Irrespective of this setting, you can view logs in **Event Viewer** > **Windows Applications** > **Applications**.

### Change your database settings for Web API

The API is configured using the `web.config` file as mentioned [here](/system-center/orchestrator/how-to-change-the-orchestrator-database#change-the-database-settings-for-the-orchestrator-web-service).

::: moniker-end

## Troubleshoot your installation

The following information provides additional instructions and caveats that you can use during the installation to resolve problems you might experience. 

### Orchestrator log files

If you experience problems during installation, installation log files are located in the folder **C:\\Users\\%USERNAME%\\AppData\\Local\\SCO\\LOGS**.  

If you experience problems when you're running Orchestrator, the product log files are located in the folder **C:\\ProgramData\\Microsoft System Center \<version\>\\Orchestrator\\**.  

### Windows Firewall

When you deploy additional Runbook Designer applications to your environment, you might see a failed installation message. To correctly install the Runbook Designer, enable the following firewall rules as they apply to your operating system and deployment configuration.  

### Windows Firewall with advanced security

By default, **Windows Firewall with Advanced Security** is enabled on all Windows Server computers, and blocks all incoming traffic unless it's a response to a request by the host or it's specifically allowed. You can explicitly allow traffic by specifying a port number, application name, service name, or other criteria by configuring Windows Firewall with Advanced Security settings.  

Enable the following rules to allow all Monitor Event activities to function correctly:  

- Windows Management Instrumentation \(Async\-In\)  

- Windows Management Instrumentation \(DCOM\-In\)  

- Windows Management Instrumentation \(WMI\-In\)  

### Automated deployment

When a runbook server or Runbook Designer is installed behind a firewall, specific firewall rules are required between the remote computers that are used to deploy the runbook server and Runbook Designer. An additional rule is required for the remote connection between the Runbook Designer and the runbook server to allow the Orchestrator management service to accept remote connections. If you're using the **Monitor WMI** task, the runbook server requires a special firewall rule on the computer that uses PolicyModule.exe.  

Enable the following firewall rules on your computer:  

#### Firewall rule between the Runbook Designer and the Orchestrator management server  

::: moniker range=">=sc-orch-2022"
|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles%\\Microsoft System Center \<version\>\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|

::: moniker-end

::: moniker range="<=sc-orch-2019"

|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles \(x86\)%\\Microsoft System Center \<version\>\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|  
|32\-bit|%ProgramFiles%Microsoft System Center \<version\>\\Orchestrator\\Management Server\\OrchestratorManagementService.exe|  

::: moniker-end

#### Firewall rules between remote computers  

|Operating system|Firewall rules|  
|--------------------|------------------|  
|Windows Server | - File and Printer Sharing<br>- Windows Management Instrumentation \(WMI\)<br>- Program rule for OrchestratorRemotingService to accept remote connections. This rule must be enabled through the Advanced Firewall mode for path %ProgramFiles%\Microsoft System Center \Orchestrator\Management Server\Deployment Manager\OrchestratorRemotingService.exe|

#### Firewall rules between the runbook server and the computer that uses PolicyModule.exe 

::: moniker range=">=sc-orch-2022" 

|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles%\\Microsoft System Center \<version\>\\Orchestrator\\Runbook Server\\PolicyModule.exe|  

For more information about adding firewall rules, see [Add or Edit a Firewall Rule](/previous-versions/orphan-topics/ws.11/cc753558(v=ws.11)).  

::: moniker-end

::: moniker range="<=sc-orch-2019"

|Operating system|Firewall rule|  
|--------------------|-----------------|  
|64\-bit|%ProgramFiles \(x86\)%\\Microsoft System Center \<version\>\\Orchestrator\\Runbook Server\\PolicyModule.exe|  
|32\-bit|%ProgramFiles\\Microsoft System Center \<version\>\\Orchestrator\\Runbook Server\\PolicyModule.exe|  

For more information about adding firewall rules, see [Add or Edit a Firewall Rule](/previous-versions/orphan-topics/ws.11/cc753558(v=ws.11)).  

::: moniker-end

### <a name="BKMK_RunbookServicefailstostart"></a>RunbookService fails to start after computer reboot  
When you reboot your runbook server, the RunbookService attempts to connect to the orchestration database. If the database isn't available, the RunbookService fails. The event log message is **This computer was unable to communicate with the computer providing the server**. Typically, this can occur when the SQL server and the runbook server are installed on the same computer.  

To solve this problem, you can manually start the RunbookService or configure the RunbookService to make multiple attempts during start-up to connect to database before failing.  

### Can't restart runbook service if you uninstall with an account without administrator permissions

If you attempt to uninstall Orchestrator while signed in with an account that is a member of OrchestratorSystemGroup but isn't an administrator, uninstall removes all accounts from OrchestratorSystemGroup. If you stop the runbook service and attempt to restart the service, the service fails because the user account doesn't have the correct permissions to retrieve the orchestration database connection. An account that is an administrator or a member of the OrchestratorSystemGroup is required to retrieve the orchestration database connection.  

To solve this problem, an administrator can add the user back to OrchestratorSystemGroup.

## Next steps

- To learn more about building runbooks, see [Design and build runbooks](./design-and-build-runbooks.md).
- To learn more about deploying runbooks, see [Deploy runbooks](deploy-runbooks.md).
