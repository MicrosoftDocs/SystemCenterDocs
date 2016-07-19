---
title: How to Install Service Provider Foundation for System Center 2012 R2
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1465767-7522-48eb-b8a5-cfa5e12d5632
author:bwren
manager:cfreemanwa
---
# How to Install Service Provider Foundation for System Center 2012 R2
You can install [!INCLUDE[spflong](../../spf/Deploy/includes/spflong_md.md)] on a single server or on multiple servers, with at least one server that has Microsoft SQL Server installed to contain the [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] database.  
  
A side\-by\-side installation of different [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] versions that are on the same server is not supported.  
  
The Setup wizard configures [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] along with the web services that you select for that computer. Installation of [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] onto a virtual machine is supported.  
  
Before you install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)], do the following:  
  
-   Make sure that each computer has sufficient RAM and hard disk space for all the web services that you intend to install. Also, be sure to have the prerequisite software installed. For more information, see [Preparing your environment for System Center 2012 R2 Service Provider Foundation](assetId:///f7c87718-29bb-4fdd-8e2d-82c81936b346).  
  
-   Make sure that you have a domain user account with administrative privileges on the computers on which you want to install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
-   Close any open programs, and make sure that the computer does not have a restart pending.  
  
If there is a problem with the installation completing successfully, refer to the log files, named “Microsoft Service Provider\*.log”, in the %SYSTEMDRIVE%\\%TEMP%  folder.  
  
You can also run a silent, unattended, installation. For more information, see [Setup Command-Line Options for Service Provider Foundation](../../spf/Deploy/Setup-Command-Line-Options-for-Service-Provider-Foundation.md).  
  
### To install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)]  
  
1.  On the server where you want to install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)], double\-click **SetupOrchestrator.exe** on the installation media to start the [!INCLUDE[orchlong](../../orch/deploy/includes/orchlong_md.md)] 2012 R2 Setup Wizard.  
  
    > [!NOTE]  
    > We recommend that you run setup as Administrator. Doing so allows Customer Experience and Microsoft Update choices to be retained later in the setup.  
  
2.  On the main Setup page, click **Service Provider Foundation**.  
  
3.  On the **Service Provider Foundation** Setup page, click **Install**.  
  
4.  On the **License Terms** page, review the license agreement. If you agree with the terms, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.  
  
5.  On the **Prerequisites** page, wait for the wizard to complete the prerequisite verification, and then review the results. If any of the prerequisites are missing, install the missing prerequisites, and then click **Check prerequisites again**.  
  
    When all of the prerequisites are met, click **Next**.  
  
6.  On the **Configure the database server** page, in the **server** text box, enter the name of the server that hosts SQL Server, or accept the default localhost. In **Port Number**, type the port number that accesses the database, or accept the default of 1433, and then click **Next**.  
  
7.  On the **Specify a location for the SPF files** page, accept or change the location for the web service files by using the **Change Folder** button. Optionally, change **Website name**. In the **Port Number** section, enter the Internet Information Services \(IIS\) port number that you want to use, or accept the default of 8090.  
  
    The **Server certificate** refers to a certificate to configure the site bindings for the [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] website in Internet Services Information \(IIS\) Manager. You can either generate a self\-signed certificate or use an existing certificate.  
  
    > [!IMPORTANT]  
    > We recommend that generated self\-signed certificates be used only for a testing purposes in a non\-production environment.  
  
    Click **Next**.  
  
8.  On the **Configure the Admin web service** page, in the **Domain security groups or users** text box, type the domain and user name of each security group or user who will use this web service. Use the format **domain\\user name**, and use a semicolon to separate multiple entries, for example, **CONTOSO\\JohnDoe; CONTOSO\\TestGroup**.  
  
    For application pool credentials, select the type of account that you want to use:  
  
    -   Select **Service Account**, and then type the domain name, user name, and password of the account that you want the application pool to use.  
  
        Make sure that the application pool account exists in the domain and that it has sufficient permissions to manage the server.  
  
    -   To use an internal system account, select **Network Service**.  
  
        We recommend that you do not use **Network Service** but instead use a **Service Account** using domain credentials.  
  
        If you select **Network Service**, the account must be a [!INCLUDE[vmmblue_1](../../om/manage/includes/vmmblue_1_md.md)] administrator, or it must have enough permission to perform the [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] requests.  
  
    Click **Next**.  
  
9. In the same manner, specify the settings for **Configure the Provider web service**, and then click **Next**.  
  
10. In the same manner, specify the settings for **Configure the VMM web service**, and then click **Next**.  
  
11. In the same manner, specify the settings for **Configure the Usage web service**, and then click **Next**.  
  
12. Choose the desired options on the **Help improve Microsoft System Center Service Provider Foundation** and **Microsoft Update** page, and then click **Next**.  
  
    Choices made on this page are not retained unless setup was run as Administrator.  
  
13. On the **Installation summary** page, review your selections, and then do one of the following:  
  
    -   Click **Previous** to change any selections.  
  
    -   Click **Install** to install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
    After you click **Install**, the installation progress indicator appears.  
  
14. Click **Close** when the message “Setup is complete” appears.  
  
Repeat this procedure for each installation, such as for a web farm.  
  
### To enable the use of [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] with a portal applications  
  
-   See [Configuring Portals for Service Provider Foundation](../../spf/Deploy/Configuring-Portals-for-Service-Provider-Foundation.md) for instructions on configuring [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] with [!INCLUDE[katal_long](../../spf/Deploy/includes/katal_long_md.md)] and [!INCLUDE[conceroshort](../../om/manage/includes/conceroshort_md.md)].  
  
## See Also  
[Preparing your environment for System Center 2012 R2 Service Provider Foundation](assetId:///f7c87718-29bb-4fdd-8e2d-82c81936b346)  
[Setup Command-Line Options for Service Provider Foundation](../../spf/Deploy/Setup-Command-Line-Options-for-Service-Provider-Foundation.md)  
[How to Uninstall Service Provider Foundation](../../spf/Deploy/How-to-Uninstall-Service-Provider-Foundation.md)  
[Post-Installation Tasks for Service Provider Foundation](../../spf/Deploy/Post-Installation-Tasks-for-Service-Provider-Foundation.md)  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Release Notes for Service Provider Foundation for System Center 2012 R2](../../spf/Deploy/Release-Notes-for-Service-Provider-Foundation-for-System-Center-2012-R2.md)  
  
