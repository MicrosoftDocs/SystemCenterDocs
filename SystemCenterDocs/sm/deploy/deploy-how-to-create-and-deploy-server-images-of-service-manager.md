---
title: Create and deploy server images of Service Manager
description: This article helps you create a system image that contains software needed for use as a template so that you can apply it to new servers.
manager:  carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22f049e0-a591-447c-b299-df44e3d95784
---

# Create and deploy server images of Service Manager

>Applies To: System Center 2016 - Service Manager

You can use the information in this article to create a system image that contains Windows server, SQL Server, and Service Manager for use as a template that you can apply to new servers. Follow the basic steps below to prepare the image. You can modify them, as needed for your environment. For more information about the Windows System Preparation Tool, [What is Sysprep?](http://go.microsoft.com/fwlink/p/?LinkId=271473)  

> [!NOTE]  
>  Details about installing SQL Server using a configuration file are not covered in this topic. For more information about using a configuration file to install SQL Server, see [Install SQL Server Using a Configuration File](http://go.microsoft.com/fwlink/p/?LinkId=271474).  

 Afterward, modify and save the sample CMD file below to create your own customized version and then run the file.  

### To prepare the server for imaging  

1.  Install Windows Server on the new server.  

2.  Install SQL Server in *Prepare for imaging* mode. This installs the binary files, but does not configure SQL server.  

    > [!NOTE]  
    >  SQL server is unusable at this point.  

3.  Copy the SQL Server installation files to a temporary location on the server. For example, c:\\Runonce\\ SQLFULL\_ENU.  

4.  Copy the System Center 2016 Service Manager installation files to a temporary location on the server. For example, c:\\Runonce\\SCSM.  

5.  Save the example CMD file shown below and customize it for your environment, where necessary. This file will run SQL Server setup to complete the SQL Server installation and then run an unattended installation of Service Manager. Save this file to a temporary location such as C:\\Runonce\\FirstRun.cmd.  

6.  Run the System Preparation Tool \(Sysprep\) with the \/generalize command to generalize the server.  

7.  Capture the Windows installation with ImageX, by creating a reference images with which to install servers with the same hardware configuration.  

8.  Create a Windows Unattend.xml file to customize Windows when the image is booted and have it run FirstRun.cmd.  

### To create a CMD file that completes image installation  

-   Copy the following sample and modify it, as needed.  

    ```  
    @echo off  

    set ServiceAccountDomain=contoso  
    set ServiceAccountName=Administrator  
    set ServiceAccountPassword=P@$$word  

    echo Finalizing SQL installation...  
    start /wait c:\RunOnce\SQLFULL_ENU\setup.exe /ConfigurationFile=c:\RunOnce\SQL2012Complete.ini  

    echo Installing additional SQL features...  
    start /wait c:\RunOnce\SQLFULL_ENU\setup.exe /ConfigurationFile=c:\RunOnce\SQL2012Shared.ini  

    echo Installing System Center Service Manager...  
    start /wait C:\RunOnce\SCSM\setup.exe /Install:Server /AcceptEula /RegisteredOwner:SCSM /RegisteredOrganization:Microsoft /CreateNewDatabase /SqlServerInstance:%computername% /ManagementGroupName:%computername% /AdminRoleGroup:%ServiceAccountDomain%\%ServiceAccountName% /ServiceRunUnderAccount:%ServiceAccountDomain%\%ServiceAccountName%\%ServiceAccountPassword% /WorkflowAccount:%ServiceAccountDomain%\%ServiceAccountName%\%ServiceAccountPassword% /CustomerExperienceImprovementProgram:Yes /EnableErrorReporting:Yes /silent  

    ```  


## Next steps

- Review [Guidance for installing Service Manager on virtual machines](deploy-guidance-for-installing-system-center-2016-service-manager-on-virtual-machines.md) for information that you should consider when you install Service Manager in a Hyper-V virtual environment.
