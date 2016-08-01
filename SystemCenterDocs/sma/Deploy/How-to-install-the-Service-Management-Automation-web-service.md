---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-07-29
title:  How to install the Service Management Automation web service
ms.technology:  service-management-automation
ms.assetid:  b6044e0c-0caa-459c-9489-c379a154136b
---

# How to install the Service Management Automation web service

>Applies To: Windows Azure Pack for Windows Server, System Center 2012 R2 Orchestrator, System Center 2016 Orchestrator

Service Management Automation enables you to automate IT administration and business processes by using Windows PowerShell based runbooks in Windows Azure Pack for Windows Server.

Use the following information to install and configure the Automation web service in Windows Azure Pack. The Service Management Automation PowerShell module is a required prerequisite of the Service Management Automation web service, so you must install the Service Management Automation PowerShell module before you deploy the Service Management Automation web service.

You can also install the Service Management Automation components by using an unattended installation. For more information, see [Installing Service Management Automation from a Command Prompt](http://go.microsoft.com/fwlink/p/?LinkId=313193).

## Install the Service Management Automation web service
The Service Management Automation web service endpoint provides the connection between Service Management Automation and Windows Azure Pack. The Service Management Automation web service can be installed from the System Center 2016 Orchestrator installation software.

Install the web service on any machine that can communicate with Windows Azure Pack and an instance of SQL Server.

#### To install the Service Automation web service

1.  In the folder where you downloaded the System Center 2016 Orchestrator installation software, click Setup to start the Setup wizard.

2.  Under **Service Management**, click **Web Service**, and then click **Install**.

3.  Complete the product registration information, and then click **Next**.

4.  Review and accept the license terms, and then click **Next**.

5.   Review the Diagnostic and Usage Data Notice, and then click **Next**
6.  This will launch the prerequisite check. Review the results of the check. If all items are installed, click **Next**.

    > [!NOTE]
    > If you see an X next to any of the prerequisite software, you must install the item, and then run the prerequisite check again. You cannot complete installation of the service endpoint until you pass the prerequisite check.

7.  Provide the following information for the database the endpoint to use, and then click **Next**.

    |||
    |-|-|
    |**Server**|Enter the name of the database server. By default, this is localhost.<br /><br />The format is sqlserver\instance, where \instance is optional.|
    |**Port number**|Enter the port number that you want to use for the database. The default is 1433.|
    |**Database name**|Enter the name of the database. The default is SMA.|
    |**Authentication Credentials**|Select the type of authentication that you want to use. You can use Windows authentication or SQL Server authentication.<br /><br />If you choose SQL Server authentication, enter the user name and password for the computer running SQL Server.|

    > [!NOTE]
    > If you are [upgrading from a previous installation](How-to-upgrade-from-a-previous-version-of-Service-Management-Automation.md), please use the database details from the previous installation.

8.  Provide the following information to configure the Internet Information Settings (IIS) for the web service, and then click **Next**.

    |||
    |-|-|
    |**Domain security group or users with access**|Enter a security group or one or more users who can grant access to the web service.|
    |**Application pool name**|SMA<br /><br />This name is not configurable.|
    |**Application pool credentials**|Specify the credentials to use for the application pool. These are the credentials that the web service will run under.|

9. Enter the port number for the web service to use. By default, this is 9090.

10. Choose the security certificate to use to encrypt communication between Windows Azure Pack and the Service Management Automation web service endpoint.

    You can have the installer generate a self-signed certificate to use, or you can select an existing certificate in your local certificate store.

    Click **Next**.

11. Review the location for the web service files. You can accept the default or specify a different location. Click **Next**.

12. Indicate whether you want to use Microsoft Update to keep your software up-to-date. Click **Next**.

13. Review the installation summary, and then click **Install**.

    After the installation is complete, install a runbook worker as described in [How to install the Service Management Automation runbook worker](How-to-install-the-Service-Management-Automation-runbook-worker.md).
