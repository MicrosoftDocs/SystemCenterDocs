---
title: How to Install Service Provider Foundation for System Center 2012 SP1
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cc1b981-5226-4387-97f2-945ca3e06d67
author:bwren
manager:cfreemanwa
---
# How to Install Service Provider Foundation for System Center 2012 SP1
You can install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] on a single server or on multiple servers, with at least one server that has Microsoft SQL&nbsp;Server installed to contain the [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] database.  
  
The Setup wizard configures an instance of [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)], along with the web services that you select for that computer. However, at this time, only the [!INCLUDE[vmm12long](../../spf/Deploy/includes/vmm12long_md.md)] web service is available for deployment. Installation of [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] onto a virtual machine is supported.  
  
Before you install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)], do the following:  
  
-   Make sure that each computer has sufficient RAM and hard disk space for all the web services that you intend to install. Also, be sure to have the prerequisite software installed. For more information, see [System Requirements for Service Provider Foundation for System Center 2012 SP1](../../spf/Deploy/System-Requirements-for-Service-Provider-Foundation-for-System-Center-2012-SP1.md).  
  
-   Make sure that you have a domain user account with administrative privileges on the computers on which you want to install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
-   Close any open programs, and make sure that the computer does not have a restart pending.  
  
If there is a problem with the installation completing successfully, refer to the log files, named "Microsoft Service Provider\*.log", in the %SYSTEMDRIVE%\\%TEMP%  folder.  
  
You can also run a silent, unattended, installation. For more information, see [Setup Command-Line Options for Service Provider Foundation](../../spf/Deploy/Setup-Command-Line-Options-for-Service-Provider-Foundation.md).  
  
### To install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)]  
  
1.  On the server where you want to install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)], double\-click **SetupOrchestrator.exe** on the installation media to start the [!INCLUDE[orchlong](../../orch/deploy/includes/orchlong_md.md)] Setup Wizard.  
  
    > [!NOTE]  
    > We recommend that you run setup as Administrator. Doing so allows Customer Experience and Microsoft Update choices to be retained later in the setup.  
  
2.  On the main Setup page, click **Service Provider Foundation**.  
  
3.  On the **Service Provider Foundation** Setup page, click **Install**.  
  
4.  On the **License Terms** page, review the license agreement. If you agree with the terms, select the **I have read, understood, and agree with the terms of the license agreement** check box, and then click **Next**.  
  
5.  On the **Select the web services to install** page, select the check box for **System Center Virtual Machine Manager 2012 Web Service**, and then click **Next**.  
  
6.  On the **Prerequisites** page, wait for the wizard to complete the prerequisite verification, and then review the results. If any of the prerequisites are missing, install the missing prerequisites, and then click **Check prerequisites again**.  
  
    When all of the prerequisites are met, click **Next**.  
  
7.  On the **Configure the database server** page, in the **server** text box, enter the name of the server that hosts SQL&nbsp;Server, or accept the default localhost. For the **Named SQL instance**, enter the correct port or check the dynamic port checkbox. See [Configuring Service Provider Foundation](http://blogs.msdn.com/b/nick_meader/archive/2014/08/22/configuring-service-provider-foundation.aspx) to learn how to find the port for a named SQL instance. In **Port Number**, type the port number that accesses the database, or accept the default of 1433, and then click **Next**.  
  
    > [!NOTE]  
    > If there is an error in a named instance value, the default SQL Server instance is used.  
  
8.  On the **Specify a location for the SPF files** page, accept or change the location for the web service files by using the **Change Folder** button. Optionally, change **Website name**. In the **Port Number** section, enter the Internet Information Services \(IIS\) port number that you want to use, or accept the default of 8090.  
  
    > [!NOTE]  
    > If you want to change the IIS port that you assign during the installation of [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)], you must uninstall or reinstall [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
    The certificate store and name refers to the certificate that was used to configure the site bindings for the [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] website in **Internet Services Information \(IIS\) Manager**. The currently selected certificate may or may not be the most applicable certificate for your environment. For more information, see [How to Create an SSL Certificate for Testing Service Provider Foundation](../../spf/Deploy/How-to-Create-an-SSL-Certificate-for-Testing-Service-Provider-Foundation.md).  
  
    Click **Next**.  
  
9. On the **Configure the Admin web service** page, in the **Domain security groups or users** text box, type the domain and user name of each security group or user who will use this web service. Use the format **domain\\user name**, and use a semicolon to separate multiple entries, for example, **CONTOSO\\JohnDoe; CONTOSO\\TestGroup**.  
  
    For application pool credentials, select the type of account that you want to use:  
  
    -   Select **Service Account**, and then type the domain name, user name, and password of the account that you want the application pool to use.  
  
        Make sure that the application pool account exists in the domain and that it has sufficient permissions to manage the server.  
  
    -   To use an internal system account, select **Network Service**.  
  
        We recommend that you do not use **Network Service** but instead use a **Service Account** using domain credentials.  
  
        If you select **Network Service**, the account must be a [!INCLUDE[vmmblue_1](../../om/manage/includes/vmmblue_1_md.md)] administrator, or it must have enough permission to perform the [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] requests.  
  
    Click **Next**.  
  
10. In the same manner, specify the settings for **Configure the Provider web service**, and then click **Next**.  
  
11. In the same manner, specify the settings for **Configure the VMM web service**, and then click **Next**.  
  
12. Choose the desired options on the **Help improve Microsoft System Center Service Provider Foundation** and **Microsoft Update** page, and then click **Next**.  
  
    Choices made on this page are not retained unless setup was run as Administrator.  
  
13. On the **Installation summary** page, review your selections, and then do one of the following:  
  
    -   Click **Previous** to change any selections.  
  
    -   Click **Install** to install [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
    After you click **Install**, the installation progress indicator appears.  
  
14. Click **Close** when the message "Setup is complete" appears.  
  
Repeat this procedure for each installation, such as for a web farm.  
  
### To upgrade from previous installations  
  
1.  Stop all web services and portal applications using [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
2.  Uninstall [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] using **Control Panel**. For more information, see [How to Uninstall Service Provider Foundation](../../spf/Deploy/How-to-Uninstall-Service-Provider-Foundation.md).  
  
    The [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] database remains in place, including any extensions and application programming interface \(API\) resources that were added.  
  
    Repeat this step for each installation, such as for a web farm.  
  
3.  Install the new version of [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)].  
  
    On the **Configure the database server** page, specify the name of name of the server that has the [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] database.  
  
    Make any other changes that may be required for the installation, such as on the **Configure the Admin web service** page.  
  
    Repeat this step for each installation, such as for a web farm.  
  
### To enable the use of [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] with a portal applications  
  
-   See [Configuring Portals for Service Provider Foundation](../../spf/Deploy/Configuring-Portals-for-Service-Provider-Foundation.md) for instructions on configuring [!INCLUDE[spfshort](../../spf/Deploy/includes/spfshort_md.md)] with [!INCLUDE[katal_long](../../spf/Deploy/includes/katal_long_md.md)] and [!INCLUDE[conceroshort](../../om/manage/includes/conceroshort_md.md)].  
  
## See Also  
[Setup Command-Line Options for Service Provider Foundation](../../spf/Deploy/Setup-Command-Line-Options-for-Service-Provider-Foundation.md)  
[How to Uninstall Service Provider Foundation](../../spf/Deploy/How-to-Uninstall-Service-Provider-Foundation.md)  
[Post-Installation Tasks for Service Provider Foundation](../../spf/Deploy/Post-Installation-Tasks-for-Service-Provider-Foundation.md)  
[Deploying Service Provider Foundation](../../spf/Deploy/Deploying-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Architecture Overview of Service Provider Foundation](../../spf/Deploy/Architecture-Overview-of-Service-Provider-Foundation.md)  
  
