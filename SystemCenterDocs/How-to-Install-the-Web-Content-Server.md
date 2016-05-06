---
title: How to Install the Web Content Server
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdd64df6-ed0d-445d-b13b-1b1f2bf82681
robots: noindex,nofollow
---
# How to Install the Web Content Server
Use the following procedure to install the [!INCLUDE[smssp](Token/smssp_md.md)] web content server in [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)].

### To install the web content server

1.  Using the Operational Database Account, log on to the computer that will host the [!INCLUDE[smssp](Token/smssp_md.md)].

2.  On the [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)] installation media, double\-click the **Setup.exe** file.

3.  On the **Service Manager Setup Wizard** page, click **Service Manager web portal**.

4.  On the **Portal Parts** page, click **Web Content Server**, and then click **Next**.

5.  On the **Product registration** page, read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

6.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the installation location of the web content server.

    > [!NOTE]
    > We recommend that you install the [!INCLUDE[smssp](Token/smssp_md.md)] in the default location. Installing the [!INCLUDE[smssp](Token/smssp_md.md)] in another location will require that you make configuration changes in Internet Information Services \(IIS\).

7.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.

8.  On the **Configure the Service Manager self\-service portal name and port** page, do the following:

    1.  In the **Web site name** text box, accept the default name, or type a new name.

    2.  In the **Port** text box, accept the default port, or type a new port.

    3.  In the **SSL certificate** list, select the Secure Sockets Layer \(SSL\) certificate that you want to use with the [!INCLUDE[smssp](Token/smssp_md.md)], and then click **Next**.

    > [!NOTE]
    > We strongly recommend the use of SSL. If you are using a self\-signed certificate, make sure that the certification authority \(CA\) that issues the certificate has been added to the Trusted Root Certification Authorities store. You must use the same HTTP protocol \(HTTP or HTTPS\) with both portal parts.

9. On the **Select the Service Manager database** page, do the following:

    1.  In the **Database server** text box, type the name of the computer that hosts the [!INCLUDE[smshort12](Token/smshort12_md.md)] database, and then press TAB.

    2.  In the **SQL Server instance** list, select the instance name for the [!INCLUDE[smshort12](Token/smshort12_md.md)] database. \(**Default** is the default selection.\)

    3.  In the **Database** list, select the database that hosts the [!INCLUDE[smshort12](Token/smshort12_md.md)] database. \(**ServiceManager** is the default database name.\)

    4.  Click **Next**.

10. On the **Configure account for the Service Manager self\-service portal** page, click **Domain account**.

    > [!NOTE]
    > Make sure that the credentials you enter here are for the sdk\_users users role on the SQL Server that is hosting the [!INCLUDE[smshort12](Token/smshort12_md.md)] database.

11. Specify the user name, password, and domain for the [!INCLUDE[smshort12](Token/smshort12_md.md)] services account that you specified during installation of [!INCLUDE[smshort12](Token/smshort12_md.md)]. For example, enter the account information for the SM\_Acct domain user.

12. Click **Test Credentials**. After you verify that you received a “The credentials were accepted message,” click **Next**.

13. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click **Tell me more about the program**, and then click **Next**.

14. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for [!INCLUDE[smshort12](Token/smshort12_md.md)] updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Click **Next**.

15. On the **Installation summary** page, click **Install**.

16. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**. For more information about backing up the encryption key, see [Completing Deployment by Backing Up the Encryption Key](assetId:///dbb276a9-7df5-4cd9-ae75-9099aabcaa93).

## See Also
[How to Install SharePoint Web Parts for the Self-Service Portal](How-to-Install-SharePoint-Web-Parts-for-the-Self-Service-Portal.md)


