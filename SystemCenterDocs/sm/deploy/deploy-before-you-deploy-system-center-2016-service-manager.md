---
title: Before You Deploy System Center - Service Manager
manager:  cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a7bfe29-aa96-434f-b17f-a07990ca5549
---

# Before You Deploy System Center - Service Manager

>Applies To: System Center 2016 - Service Manager

Before you start the deployment process, prepare your environment for System Center - Service Manager, as described in the [Planning Guide for Service Manager for System Center ](http://go.microsoft.com/fwlink/p/?LinkID=209672). The Planning Guide contains information about the various parts of Service Manager, the hardware and software requirements, the port assignments, and the information about the accounts you must use to deploy Service Manager. The Planning Guide also contains information about the accounts that you need to create for use with Service Manager.  

 In addition, you have to install the Authorization Manager hotfix and the Microsoft Report Viewer Redistributable security update before you start Service Manager deployment.  

## Install the Authorization Manager Hotfix \(KB975332\)  
 If the Service Manager management server, data warehouse management server, or the Self-Service Portal lose connection to the SQL&nbsp;Server databases-even briefly-the connection is not automatically re\-established. The Windows team recently released a hotfix to address this issue. It is extremely import that this hotfix be installed on your computers that host a Service Manager management server, data warehouse management server, or the Self-Service Portal.  

> [!NOTE]  
>  The Authorization Manager hotfix was included with Windows&nbsp;Server&nbsp;2008&nbsp;R2 with Service Pack&nbsp;1 \(SP1\). If you are installing Service Manager on a computer running Windows&nbsp;Server&nbsp;2008&nbsp;R2 with SP1, you already have the Authorization Manager hotfix installed.  

### Download and Install the Authorization Manager Hotfix

The Authorization Manager hotfix is included with Windows&nbsp;Server&nbsp;2008&nbsp;R2 with Service Pack&nbsp;1 \(SP1\). Therefore, if you are using Windows&nbsp;Server&nbsp;2008&nbsp;R2 with SP1, you can disregard this section.  

 You can obtain the Authorization Manager hotfix \(KB975332\) by connecting to a website and requesting an email containing download instructions. This hotfix is available for both 32\-bit and 64\-bit operating systems and for both the Windows&nbsp;Server&nbsp;2008 with SP1 operating system and the Windows&nbsp;Server&nbsp;2008&nbsp;R2 operating system. The type of files that you are allowed to download is determined when you connect to the website to request an email. Therefore, you should connect to the website from the computer that hosts the Service Manager parts. Use the following steps to download and install the Authorization Manager hotfix.  

 Install this hotfix on computers that host the following Service Manager parts:  

-   Service Manager management server or servers  

-   Data warehouse management server  

-   Self-Service Portal  

> [!NOTE]  
>  The installation of this hotfix on the Service Manager and data warehouse management servers requires a computer restart.  

#### To download the Authorization Manager hotfix  

1.  On the computer that hosts the Service Manager management server or data warehouse management server,  open a browser and connect to [article 975332](http://go.microsoft.com/fwlink/p/?LinkID=183635) in the Microsoft Knowledge Base. Users and applications cannot access authorization rules that are stored in Authorization Manager.  

2.  On the knowledge base article page, click **View and request hotfix downloads**.  

3.  Read the **Agreement for Microsoft Services** terms and conditions, and if applicable, click **I Accept**.  

4.  On the **Hotfix Request** page, select the appropriate link based on your operating system, as shown in the following table.  

    - Windows Server&nbsp;2008 with SP1 - Windows Vista  
    - Windows Server 2008 R2 - Windows 7 - Windows Server 2008 R2  

5.  On the **Hotfix Request** page, enter your email address, type the characters in the CAPTCHA image, and then click **Request hotfix**.  

6.  In the email that you receive, you are provided with a URL. Click the URL to start the download and save the file to your computer.  

#### To install the Authorization Manager hotfix  

1.  Open Windows Explorer, locate the folder where you downloaded the hotfix, and then double\-click the file to extract the hotfix files.  

2.  Double\-click the file that you extracted.  

3.  In the **Windows Update Standalone Installer** dialog box, click **OK**.  

4.  On the **Installation complete** page, on the computers that host the Service Manager and data warehouse management servers, click **Restart Now**.  

###$ To verify the installation of the Authorization Manager hotfix  

1.  On the Windows desktop, open the Control Panel.  

2.  In the **Control Panel** window, double\-click **Programs and Features**.  

3.  In the **Programs and Features** window, in the **Tasks** area, click **View installed updates**.  

4.  Scroll through the list and locate **Microsoft Windows**, and then confirm that **Hotfix for Microsoft Windows \(KB975332\)** is listed.

## Install the Microsoft Report Viewer Redistributable Security Update \(KB971119\)  
 During installation of a Service Manager management server or Service Manager console, the prerequisite checker checks to see whether the security update for Microsoft Report Viewer&nbsp;2008 Service Pack&nbsp;1 Redistributable Package has been installed. If you have not installed this security update, you will have the opportunity to do so during the installation. As an alternative, you can deploy this security hotfix before starting the installation of Service Manager.  

### Install the Microsoft Report Viewer Redistributable Security Update

You can use the following procedure to install the Microsoft Report Viewer Redistributable security update for a deployment of System Center - Service Manager.  

> [!NOTE]  
>  If your system is configured to use a language other than English, you must manually install the Report Viewer Language Pack for that language. You can download the [Microsoft Report Viewer Redistributable 2008 SP1 Language Pack](http://go.microsoft.com/fwlink/p/?LinkID=191491) from the Microsoft Download Center.  

#### To install the Microsoft Report Viewer Redistributable security update  

1.  On the computer that will host a Service Manager management server, open Windows Explorer.  

2.  Locate the drive that contains the Service Manager installation media, and then open the Prerequisites folder  

3.  Double\-click the **ReportViewer** file.  

4.  On the **Welcome to Microsoft Report Viewer Redistributable 2008 \(KB971119\) Setup** page, click **Next**.  

5.  On the **License Terms** page, read the Microsoft Software License Terms, and, if applicable, click **I have read and accept the license terms**, and then click **Install**.  

6.  On the **Setup Complete** page, click **Finish**.
