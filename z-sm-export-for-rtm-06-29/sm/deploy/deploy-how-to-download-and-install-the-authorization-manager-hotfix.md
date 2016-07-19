---
title: How to Download and Install the Authorization Manager Hotfix
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 593012d5-9cfa-4911-a2f4-a26de28e8df4
 

















---
# How to Download and Install the Authorization Manager Hotfix
The Authorization Manager hotfix is included with Windows Server 2008 R2 with Service Pack 1 \(SP1\). Therefore, if you are using Windows Server 2008 R2 with SP1, you can disregard this topic.  
  
 You can obtain the Authorization Manager hotfix \(KB975332\) by connecting to a website and requesting an email containing download instructions. This hotfix is available for both 32\-bit and 64\-bit operating systems and for both the Windows Server 2008 with SP1 operating system and the Windows Server 2008 R2 operating system. The type of files that you are allowed to download is determined when you connect to the website to request an email. Therefore, you should connect to the website from the computer that hosts the Service Manager parts. Use the following steps to download and install the Authorization Manager hotfix.  
  
 Install this hotfix on computers that host the following Service Manager parts:  
  
-   Service Manager management server or servers  
  
-   Data warehouse management server  
  
-   Self-Service Portal  
  
> [!NOTE]  
>  The installation of this hotfix on the Service Manager and data warehouse management servers requires a computer restart.  
  
### To download the Authorization Manager hotfix  
  
1.  On the computer that hosts the Service Manager management server or data warehouse management server,  open a browser and connect to [article 975332](http://go.microsoft.com/fwlink/p/?LinkID=183635) in the Microsoft Knowledge Base. Users and applications cannot access authorization rules that are stored in Authorization Manager.  
  
2.  On the knowledge base article page, click **View and request hotfix downloads**.  
  
3.  Read the **Agreement for Microsoft Services** terms and conditions, and if applicable, click **I Accept**.  
  
4.  On the **Hotfix Request** page, select the appropriate link based on your operating system, as shown in the following table.  
  
    |Operating System|Web Page Link|  
    |----------------------|-------------------|  
    |Windows Server 2008 with SP1|Windows Vista|  
    |Windows Server 2008 R2|Windows 7\/Windows Server 2008 R2|  
  
5.  On the **Hotfix Request** page, enter your email address, type the characters in the CAPTCHA image, and then click **Request hotfix**.  
  
6.  In the email that you receive, you are provided with a URL. Click the URL to start the download and save the file to your computer.  
  
### To install the Authorization Manager hotfix  
  
1.  Open Windows Explorer, locate the folder where you downloaded the hotfix, and then double\-click the file to extract the hotfix files.  
  
2.  Double\-click the file that you extracted.  
  
3.  In the **Windows Update Standalone Installer** dialog box, click **OK**.  
  
4.  On the **Installation complete** page, on the computers that host the Service Manager and data warehouse management servers, click **Restart Now**.  
  
### To verify the installation of the Authorization Manager hotfix  
  
1.  On the Windows desktop, open the Control Panel.  
  
2.  In the **Control Panel** window, double\-click **Programs and Features**.  
  
3.  In the **Programs and Features** window, in the **Tasks** area, click **View installed updates**.  
  
4.  Scroll through the list and locate **Microsoft Windows**, and then confirm that **Hotfix for Microsoft Windows \(KB975332\)** is listed.
