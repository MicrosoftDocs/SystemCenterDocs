---
title: How to Install Both the Web Content Server and SharePoint Web Parts on One Computer
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e59ecfe-6035-47a1-8d7f-588b76107468
robots: noindex,nofollow
---
# How to Install Both the Web Content Server and SharePoint Web Parts on One Computer
When you are installing the web content server and SharePoint Web Parts on the same computer in [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)], you must install both components at the same time. After one component has been installed, you will not be able to run Setup again to install the other component.

Use the following procedure to install both the web content server and SharePoint Web Parts for the [!INCLUDE[smssp](../Token/smssp_md.md)] on the third computer.

### To install the Self\-Service Portal on one computer

1.  Using the Operational Database Account, log on to the computer that will host the [!INCLUDE[smssp](../Token/smssp_md.md)].

2.  On the [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] installation media, double\-click the **Setup.exe** file.

3.  On the **Microsoft System Center Service Manager Setup Wizard** page, click **Service Manager Web portal**.

4.  On the **Portal Parts** page, click **Web Content Server**, click **SharePoint Web Parts**, and then click **Next**.

5.  On the **Product registration** page, read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license terms**, and then click **Next**.

6.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the installation location of the [!INCLUDE[smshort12](../Token/smshort12_md.md)] management server.

    > [!NOTE]
    > We recommend that you install the [!INCLUDE[smssp](../Token/smssp_md.md)] in the default location. Installing the [!INCLUDE[smssp](../Token/smssp_md.md)] in another location will require that you make configuration changes in Internet Information Services \(IIS\).

7.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.

8.  On the **Configure the Service Manager Self\-Service Portal name and port** page, do the following:

    1.  In the **Website name** text box, accept the default name, or type a new name.

    2.  In the **Port** text box, accept the default port, or type a new port.

    3.  In the **SSL certificate** list, select the Secure Sockets Layer \(SSL\) certificate that you want to use with the [!INCLUDE[smssp](../Token/smssp_md.md)], and then click **Next**.

    > [!NOTE]
    > We strongly recommend the use of SSL. If you are using a self\-signed certificate, make sure that the certification authority \(CA\) that issues the certificate has been added to the Trusted Root Certification Authorities store. You must use the same HTTP protocol \(HTTP or HTTPS\) with both portal parts.

9. On the **Select the Service Manager database** page, do the following:

    1.  In the **Database server** text box, type the name of the computer that hosts the [!INCLUDE[smshort12](../Token/smshort12_md.md)] database, and then press TAB.

    2.  In the **SQL Server instance** list, select the instance name for the [!INCLUDE[smshort12](../Token/smshort12_md.md)] database. \(**Default** is the default SQL Server instance.\)

    3.  In the **Database** list, select the database that hosts the [!INCLUDE[smshort12](../Token/smshort12_md.md)] database. \(**ServiceManager** is the default database name.\)

    4.  Click **Next**.

10. On the **Configure the account for the Service Manager Self\-Service Portal** page, click **Domain account**.

11. Specify the user name, password, and domain for the [!INCLUDE[smshort12](../Token/smshort12_md.md)] services account that you specified during installation of [!INCLUDE[smshort12](../Token/smshort12_md.md)]. For example, enter the account information for the SM\_Acct domain user.

12. Click **Test Credentials**. After you verify that you received a “The credentials were accepted” message, click **Next**.

13. On the **Configure the Service Manager SharePoint Web site** page, do the following:

    1.  In the **Web site name** text box, accept the default name, or type a new name.

    2.  In the **SSL certificate** list, select the SSL certificate that you want to use with the [!INCLUDE[smssp](../Token/smssp_md.md)].

    3.  In the **Port** text box, accept the default port, or type a new port.

        > [!NOTE]
        > This is the port number that will be used for accessing the [!INCLUDE[smssp](../Token/smssp_md.md)].

    4.  In the **Database server** text box, type the name of the computer that hosts the SharePoint database, and then press TAB. For example, select the default entry for the computer on which you are installing the SharePoint website.

    5.  In the **SQL Server instance** list, select the instance name for the SharePoint database. \(**Default** is the default SQL Server instance.\)

    6.  In the **Database name** text box, accept the default database name, or type a new name

    7.  Click **Next**.

14. On the **Configure the account for Service Manager SharePoint application pool** page, type a domain user and password, and then click **Test Credentials**. After you verify that you received a “The credentials were accepted” message, click **Next**.

15. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click **Tell me more about the program**, and then click **Next**.

16. On the **Installation summary** page, click **Install**.

17. On the **Setup completed successfully** page, click the link to test the URL for the [!INCLUDE[smssp](../Token/smssp_md.md)]. Make a note of this URL, and then click **Close**.

