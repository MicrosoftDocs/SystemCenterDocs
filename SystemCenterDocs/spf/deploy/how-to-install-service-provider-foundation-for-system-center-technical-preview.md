---
description:  
manager:  cfreeman
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to Install Service Provider Foundation for System Center  Technical Preview
ms.technology:  service-provider-foundation
ms.assetid:  ce22e119-71d2-4a0c-a9a0-99b886ce392f
---

# How to Install Service Provider Foundation for System Center  Technical Preview

>Applies To: System Center Technical Preview

You can install Service Provider Foundation on a single server or on multiple servers, with at least one server that has Microsoft SQL Server installed to contain the Service Provider Foundation database.

A side-by-side installation of different Service Provider Foundation versions that are on the same server is not supported.

The Setup wizard configures Service Provider Foundation along with the web services that you select for that computer. Installation of Service Provider Foundation onto a virtual machine is supported.

Before you install Service Provider Foundation, do the following:

-   Make sure that each computer has sufficient RAM and hard disk space for all the web services that you intend to install. Also, be sure to have the prerequisite software installed. For more information, see [System Requirements for System Center Technical Preview](../../system-requirements/System-Requirements-for-System-Center-Technical-Preview.md).

-   Make sure that you have a domain user account with administrative privileges on the computers on which you want to install Service Provider Foundation.

-   Close any open programs, and make sure that the computer does not have a restart pending.

If there is a problem with the installation completing successfully, refer to the log files, named "Microsoft Service Provider*.log", in the %SYSTEMDRIVE%\\%TEMP%  folder.

### To install Service Provider Foundation

1.  On the server where you want to install Service Provider Foundation, double-click **SetupOrchestrator.exe** on the installation media to start the System Center 2016 Technical Preview - Orchestrator Setup Wizard.

    > [!NOTE]
    > We recommend that you run setup as Administrator. Doing so allows Customer Experience and Microsoft Update choices to be retained later in the setup.

2.  On the main Setup page, click **Service Provider Foundation**.

3.  On the **Service Provider Foundation** Setup page, click **Install**.

4.  On the **License Terms** page, review the license agreement. If you agree with the terms, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.

5.  On the **Prerequisites** page, wait for the wizard to complete the prerequisite verification, and then review the results. If any of the prerequisites are missing, install the missing prerequisites, and then click **Check prerequisites again**.

    When all of the prerequisites are met, click **Next**.

6.  On the **Configure the database server** page, in the **server** text box, enter the name of the server that hosts SQL Server, or accept the default localhost. In **Port Number**, type the port number that accesses the database, or accept the default of 1433, and then click **Next**.

7.  On the **Specify a location for the SPF files** page, accept or change the location for the web service files by using the **Change Folder** button. Optionally, change **Website name**. In the **Port Number** section, enter the Internet Information Services (IIS) port number that you want to use, or accept the default of 8090.

    The **Server certificate** refers to a certificate to configure the site bindings for the Service Provider Foundation website in Internet Services Information (IIS) Manager. You can either generate a self-signed certificate or use an existing certificate.

    > [!IMPORTANT]
    > We recommend that generated self-signed certificates be used only for a testing purposes in a non-production environment.

    Click **Next**.

8.  On the **Configure the Admin web service** page, in the **Domain security groups or users** text box, type the domain and user name of each security group or user who will use this web service. Use the format **domain\user name**, and use a semicolon to separate multiple entries, for example, **CONTOSO\JohnDoe; CONTOSO\TestGroup**.

    For application pool credentials, select the type of account that you want to use:

    -   Select **Service Account**, and then type the domain name, user name, and password of the account that you want the application pool to use.

        Make sure that the application pool account exists in the domain and that it has sufficient permissions to manage the server.

    -   To use an internal system account, select **Network Service**.

        We recommend that you do not use **Network Service** but instead use a **Service Account** using domain credentials.

        If you select **Network Service**, the account must be a System Center 2016 Technical Preview - Virtual Machine Manager administrator, or it must have enough permission to perform the Service Provider Foundation requests.

    Click **Next**.

9. In the same manner, specify the settings for **Configure the Provider web service**, and then click **Next**.

10. In the same manner, specify the settings for **Configure the VMM web service**, and then click **Next**.

11. In the same manner, specify the settings for **Configure the Usage web service**, and then click **Next**.

12. Choose the desired options on the **Microsoft Update** page, and then click **Next**.

    Choices made on this page are not retained unless setup was run as Administrator.

13. On the **Installation summary** page, review your selections, and then do one of the following:

    -   Click **Previous** to change any selections.

    -   Click **Install** to install Service Provider Foundation.

    After you click **Install**, the installation progress indicator appears.

14. Click **Close** when the message "Setup is complete" appears.

Repeat this procedure for each installation, such as for a web farm.
