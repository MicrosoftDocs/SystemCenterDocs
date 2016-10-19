---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  How to install Orchestrator on a single computer
ms.technology:  orchestrator
ms.assetid:  7c72117a-8742-4a68-90d1-00c6d9dcd012
---

# How to Install Orchestrator on a Single Computer

>Applies To: System Center 2016 - Orchestrator

Use the following steps to install all Orchestrator features on a single computer.

### To install Orchestrator on a single computer

1.  To start the Orchestrator Setup Wizard on the server where you want to install Orchestrator, double\-click **SetupOrchestrator.exe**.

    > [!IMPORTANT]
    > Before you begin setup, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using Orchestator or have applied a security update, you might have to restart the computer, and then log on to the computer with the same user account to finish the installation of the server role or the security update.

    > [!NOTE]
    > If User Account Control is enabled, then you will be prompted to verify that you want to allow the setup program to run. This is because it requires administrative access to make changes to the system.

2.  On the main setup page, click **Install**.

    > [!WARNING]
    > If Microsoft .NET Framework 3.5 Service Pack 1 is not installed on your computer, a dialog box appears asking if you want to install .NET Framework 3.5 SP1. Click **Yes** to proceed with the installation.

3.  On the **Product registration** page, provide the name and company for the product registration, and then click **Next**.

    > [!NOTE]
    > For this evaluation release, a product key is not required.

4.  On the **Please read this License Terms** page, review and accept the Microsoft Software License Terms, and then click **Next**.

5. On the **Diagnostic and Usage data** page, review the Diagnostic and Usage data notice, and then click **Next**.

5.  On the **Select features to install** page, verify that all features are selected, and then click **Next**.

    > [!NOTE]
    > You can choose to remove individual features. The management server is mandatory and is selected by default. The check boxes for the other features can be cleared as required.

    > [!TIP]
    > If you want to install only an individual feature after installing a management server, use the information in [Install Individual Orchestrator Features](How-to-Install-Orchestrator-Features.md).

6.  Your computer is checked for required hardware and software. If your computer meets all of the requirements, the **All prerequisites are installed** page appears. Click **Next** and proceed to the next step.

    If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Follow these steps to resolve the failed prerequisite check:

    1.  Review the items that did not pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services \(IIS\) role.

        > [!WARNING]
        > If you enable prerequisites during setup, such as Microsoft .NET Framework 4, your computer can require a restart. If you restart your computer, you must run setup again from the beginning.

    2.  After you resolve the missing prerequisites, click **Verify prerequisites again**.

7.  On the **Configure the service account** page, enter the user name and password for the Orchestrator Management Service account. Click **Test** to verify the account credentials. If the credentials are accepted, click **Next**.

    > [!IMPORTANT]
    > The Orchestrator Management Service account must be created before this step. For more information about the Orchestrator Management Service account, see [Orchestrator Management Service account](https://technet.microsoft.com/en-us/library/hh912319.aspx).

8.  On the **Configure the database server** page, enter the name of the server and the name of the instance and port number of the Microsoft SQL Server that you want to use for Orchestrator. You can also specify whether to use Windows Authentication or SQL Server Authentication, and whether to create a new database or use an existing database.

9. Click **Test Database Connection** to verify the account credentials. If the credentials are accepted, click **Next**.

10. On the **Configure the database** page, select an existing database or specify the name of a new database, and then click **Next**.

11. On the **Configure Orchestrator users group** page, accept the default configuration or enter the name of the user group to manage Orchestrator permissions, and then click **Next**.

    > [!NOTE]
    > For more information about the Orchestrator users group, see [Orchestrator Users Group](https://technet.microsoft.com/en-us/library/hh912314.aspx).

12. On the **Configure the port for the web service** page, verify the port numbers for the Orchestrator web service and the Orchestration console, and then click **Next**.

    > [!NOTE]
    > For more information about the TCP ports, see [TCP Port Requirements](https://technet.microsoft.com/en-us/library/hh420382.aspx).

13. On the **Select the installation location** page, verify the installation location for Orchestrator and change it if you want to, and then click **Next**.

14. On the **Microsoft Update** page, optionally indicate whether you want to use the Microsoft Update services to check for updates, and then click **Next**.

    > [!NOTE]
    > If you have previously accepted Microsoft Update on this computer, this page is skipped.

15. On the **Help improve Microsoft System Center Orchestrator** page, optionally indicate whether you want to participate in **Error Reporting**, and then click **Next**.

16. Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

17. On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and then click **Close** to complete the installation.

### To install the Service Management Automation web service

1.  Follow the steps that are detailed in the [Web Service Installation](http://go.microsoft.com/fwlink/p/?LinkID=309098).

### To enable network discovery for the Runbook Designer

1.  On the desktop of the computer that is running Windows Server, click **Start**, click **Control Panel**, click **Network and Internet**, click **Network and Sharing Center**, click **Choose Home group and Sharing Options**, and then click **Change advanced sharing settings**.

2.  For the **Domain** profile, if needed, click the **Arrow** icon to expand the section options.

3.  Select **Turn on network discovery**, and then click **Save changes**.

    If you are prompted for an administrator password or confirmation, type the password or provide confirmation.

## See Also
[Install Individual Orchestrator Features](How-to-install-orchestrator-features.md)

[Orchestrator Security Planning](assetId:///358c5344-8649-4d40-a53c-37f8e70e58f6)

[TCP Port Requirements](assetId:///dc879c86-4855-4fd0-808d-06f64a9657ca)
