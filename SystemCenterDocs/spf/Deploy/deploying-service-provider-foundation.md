---
title: Deploying Service Provider Foundation
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.date: 8-18-2016
ms.topic: article
ms.assetid: 7c2b9a00-8522-4f67-9853-2a4639442b0d
author:bwren
manager:cfreemanwa
---
# Deploying Service Provider Foundation (SPF)
Deploying SPF is a multi-step process. The first step is to plan for the deployment by reading and following the guidance provided in the following topics:

-  [Capacity Planning for Service Provider Foundation](..spf/plan/Capacity-Planning-for-Service-Provider-Foundation.md)
-  [Recommended Administrator Capabilities for SPF](..spf/plan/recommended-adminstrator-capabilities-in-service-provider-foundation.md)
-  [Security Planning for SPF](..spf/plan/security-planning-for-service-provider-foundation.md)

After you have your deployment plan in place, make sure your environment has the necessary software SPF depends on setup. The following topics describe how to prepare your environment:

-  [Preparing your environment for System Center 2012 R2 Service Provider Foundation]
-  [How to Create an SSL Certificate for Testing Service Provider Foundation]

Once you have your environment setup, you are ready to install SPF. Here are the installation steps:

1.  On the server where you want to install Service Provider Foundation, double-click **SetupOrchestrator.exe** on the installation media to start the System Center 2016 - Orchestrator Setup Wizard.

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

If you plan to setup SPF from the command-line you can also use the following options.

-   [Setup Command-Line Options for Service Provider Foundation](../../spf/Deploy/Setup-Command-Line-Options-for-Service-Provider-Foundation.md)  




## See Also  
[Architecture Overview of Service Provider Foundation](../spf/Deploy/Architecture-Overview-of-Service-Provider-Foundation.md)  
[Administering Service Provider Foundation](../spf/Deploy/Administering-Service-Provider-Foundation.md)  
[Cmdlets in System Center 2012 \- Service Provider Foundation](http://go.microsoft.com/fwlink/p/?LinkId=263677)  
[Service Provider Foundation Developer's Guide](http://go.microsoft.com/fwlink/p/?LinkID=263700)  
