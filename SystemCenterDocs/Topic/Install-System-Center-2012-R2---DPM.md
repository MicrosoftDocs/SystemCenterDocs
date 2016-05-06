---
title: Install System Center 2012 R2 - DPM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5091972-ff4b-4aaf-91c6-b418678d00cc
---
# Install System Center 2012 R2 - DPM
The [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Setup Wizard guides you through the process of specifying [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] configuration settings, and automatically installs or provides links to install the prerequisite software as part of the integrated [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] installation process.

## Before you begin
Verify that all system requirements and prerequisites are in place. For details see [System requirements for DPM in System Center 2012 R2](assetId:///e2a65d9d-5038-4a86-a495-f4745b78d040).

DPM can be installed on a physical server, as a virtual machine running on an on\-premises Hyper\-V server, or as an Azure virtual machine. You run setup in the same way but if you’re deploying in a virtual environment read the following before you start:

-   [Install DPM as a virtual machine on an on\-premises Hyper\-V server](assetId:///52ba2825-72de-4079-8947-a2e7baf9602c)

-   [Install DPM as an Azure virtual machine](assetId:///ae43b358-bab6-42b8-94b0-ac216cb9ea43)

## Running Setup
Run Setup as follows. Note that Setup stops the Removable Storage service before installing [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)].

1.  On your installation media, right\-click setup.exe, and then click **Run as administrator**.

2.  In the **Install** list, click **Data Protection Manager**.

3.  On the Use the Microsoft Software License Terms page, click I **accept the license terms and conditions** to start Setup. Then click **OK**. If you don’t want to accept the terms, click **Cancel** to exit Setup.

4.  On the Welcome page, click **Next**.

5.  On the Prerequisites Check page, click **Check and Install** to verify that the computer meets the Setup requirements. Note the following:

    -   Before you begin the prerequisites check, you must specify whether the DPM database will use an instance of SQL Server that’s either collocated on the DPM server, or located on a remote server, as

        -   Select **Use stand\-alone SQL Server** if you want to use a standalone instance of SQL Server.

        -   Alternatively, select **Use clustered SQL Server** if you want to use an instance of SQL Server running in a cluster.

        -   In **Instance of SQL Server**, type in the server location. Use the format ***<Computer Name>*\\*<Instance Name>***. If the SQL Server instance is collocated with DPM then type in the name of the DPM server.

        -   Specify credentials, including a user name, domain, and password. Note the following:

            -   The name of the SQL Server shouldn’t include the underscore \(“\_”\) character. If it does the DPM installation might fail.

            -   You shouldn’t use localized characters in the computer name when you want to install DPM using a remote instance of SQL Server.

            -   Use a domain user account that is a member of both the local Administrators group and the SQL Server **Sysadmin** fixed server role on the computer where the remote instance is installed. After setup is complete you can remove the account from the local Administrators group.

            -   A restart is necessary to start the volume filter that [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] uses to track and transfer block\-level changes between [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] and the computers it protects, or between the primary and secondary [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] servers.

        -   After installation, your [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] database will be named **DPMDB\_<DPMServername>** or **DPMDB\_<DPMServername><GUID>**.

    -   When the check prerequisites runs, if the “check item failed” symbol appears for one or more required or recommended components, Setup displays one of the following:

        -   **Warning**. Indicates that a recommended component is missing or noncompliant. Review the alert and determine whether to resolve the issue now or continue with the installation. If any recommended component is missing, you can click **Next**, and [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] will install the required prerequisite software.

            > [!NOTE]
            > The installer does not install Windows updates. You must download and install them yourself.

        -   **Error**. Indicates that a required component is missing or noncompliant. Resolve the error, and then click **Check** to verify all components are installed before you continue with the installation.

        -   When the prerequisite check is complete and all required components are present, Setup displays a confirmation, and the **Next** button becomes available.

6.  On the Product Registration page, specify the identification information that is used to register your copy of [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)], as follows:

    -   In **User name**, Type your name. When you install [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)], provide the name of a user responsible for administering the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server. A user name is required to continue Setup.

    -   In **Company**, optionally specify the name of your organization.

    -   In **Product key**, specify the key that came with your DVD.

    -   In **Client licenses**, specify the number of licenses that you have purchased to authorize protection of client computers \(laptops and desktops\).

    -   In **Standard licenses**, specify the number of licenses that you have purchased to authorize protection of file resources and system state.

    -   In **Enterprise licenses**, specify the number of licenses that you have purchased to authorize protection of both file and application resources.

7.  After you enter your identification information, click **Next**.

8.  On the Installation Settings page, specify where you want to install the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] program and database files. Note the following:

    1.  The files can be installed only on a local drive. They cannot be installed on read\-only folders, hidden folders, or directly on local Microsoft Windows folders, such as Documents and Settings, Windows NT, or Program Files. \(However, the files can be installed on a subfolder in the Program Files folder.\)

    2.  The installation partition must be formatted with the NTFS file system. To ease recovery if a boot partition failure occurs, install [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] on a partition that is separate from the boot partition.

    3.  In **Program Files**, click **Change** to modify the default [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] program files installation location.

    4.  In **Database files**, click **Change** to modify the default installation location for the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] database.

    5.  The **Space Requirements**, verify that the selected drives have enough space for the installation.

9. After you enter your installation settings information, click **Next**.

10. On the Security Settings page, specify security settings as follows:

    -   In **Password**, type a strong password for the restricted MICROSOFT$DPM$Acct and DPMR$<computer name> accounts. For security purposes, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] runs the instance of Microsoft SQL Server and the SQL Server Agent service under the MICROSOFT$DPM$Acct account, which [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Setup creates during the installation. To securely generate reports, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] creates the DPMR$<computer name> account. Note the following:

        -   Setting strong passwords is essential to the security of your system. A strong password is a password that is at least six characters long, does not contain all or part of the user’s account name, and contains at least three of the following four categories of characters: uppercase characters, lowercase characters, base 10 digits, and symbols \(such as \!, @, \#\).

        -   The password that you provide does not expire.

        -   [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] sets the system administrator \(SA\) password for the instance of SQL Server to the same password that you specify for the MICROSOFT$DPM$Acct account.

11. After you reconfirm the password, click **Next**.

12. On the Microsoft Update Opt\-In page, optionally sign up for the Microsoft Update server. To sign up, select **Use Microsoft Update when I check for updates**. Note that signing up for this service delivers not only DPM updates, but all critical and required updates from the Microsoft Update Catalog.

13. After you select the Microsoft Update service option, click **Next**.

14. On the Customer Experience Improvement Program page, select whether you want to participate in the Microsoft Customer Experience Improvement Program \(CEIP\). The CEIP collects data about your use of Microsoft applications to identify possible improvements. To participate, click **Yes, I want to participate anonymously in this program**. Alternatively, click **No, remind me later** to decline enrolment. You can change your CEIP enrollment choice at any time in [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Administrator Console options.

    After you choose your CEIP option, click **Next** to continue.

15. On the Summary page, confirm the installations settings, and click **Install** to continue.

16. On the Installation page you can monitor Setup progress. Click **Cancel** at any time to exit Setup. When the installation is complete, **Finish** to exit the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Setup Wizard.

-   The installation logs are placed in C:\\Program Files\\ Microsoft System Center 2012\\DPM\\DPMLogs.

-   [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] installs its own file filter \(DPMFilter.SYS\). It is Windows Hardware Quality Labs \(WHQL\) certified and is installed as part of [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] installation. This file is not removed if you uninstall [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)].

