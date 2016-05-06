---
title: How to Install SharePoint Web Parts for the Self-Service Portal
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 59135873-31ac-4dd3-bba7-c6e40131c6a7
robots: noindex,nofollow
---
# How to Install SharePoint Web Parts for the Self-Service Portal
The home page for the [!INCLUDE[smssp](./Token/smssp_md.md)] in [!INCLUDE[scsm_threshold_1](./Token/scsm_threshold_1_md.md)] is on the SharePoint Web Parts server. We recommend that you use Secure Sockets Layer \(SSL\) and install the SharePoint Web Parts using port 443.

When you installed Internet Information Services \(IIS\), the default website was configured to use port 80. If you want to install the SharePoint Web Parts on port 80, you must first move the default website in IIS to a different port—for example, port 8080—and then install the SharePoint Web Parts on port 80.

You can use this information to share Excel workbooks using SharePoint. For an example, see [Configure Excel Services for a BI test environment](http://go.microsoft.com/fwlink/p/?LinkId=232429).

Use the following procedure to install the SharePoint Web Parts server.

### To install the SharePoint Web Parts server

1.  Using the Operational Database Account, log on to the computer that will host the [!INCLUDE[smssp](./Token/smssp_md.md)].

2.  On the [!INCLUDE[scsm_threshold_1](./Token/scsm_threshold_1_md.md)] installation media, double\-click the **Setup.exe** file.

3.  On the **Service Manager Setup Wizard** page, click **Service Manager web portal**.

4.  On the **Portal Parts** page, click **SharePoint Web Parts**.

5.  On the **Product registration** page, read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license terms**, and then click **Next**.

6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.

7.  On the **Configure the Service Manager SharePoint site** page, complete these steps:

    1.  In the **SSL certificate** list, select the Secure Sockets Layer \(SSL\) certificate that you want to use with the [!INCLUDE[smssp](./Token/smssp_md.md)], and then click **Next**.

    2.  In the **Port** text box, accept the default port, or type a new port. For example, type **443**.

    3.  In the **URL** text box, type the URL for the web content server in the form of http:\/\/<computername>:<port> or https:\/\/<computername>:<port>.

    4.  Click in any of the other text boxes, and then click **Next**.

    > [!NOTE]
    > We strongly recommend the use of SSL. If you are using a self\-signed certificate, make sure that the certification authority \(CA\) that issues the certificate has been added to the Trusted Root Certification Authorities store. You must use the same HTTP protocol \(HTTP or HTTPS\) with both portal parts.

8.  On the **Configure the account for the Service Manager SharePoint app pool** page, type a domain user and password, and then click **Test Credentials**. After you verify that you received a “The credentials were accepted” message, click **Next**.

9. On the **Help improve System Center Service Manager** page, indicate your preference for participation in the Customer Experience Improvement Program. As an option, click **Tell me more about the program**, and then click **Next**.

10. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for [!INCLUDE[smshort12](./Token/smshort12_md.md)] updates. If you want Windows Update to check for updates, select **Initiate machine wide Automatic update**. Click **Next**.

11. On the **Installation summary** page, click **Install**.

12. On the **Setup completed successfully** page, click **Close**.

## See Also
[How to Grant Permissions on the SharePoint Site](./How-to-Grant-Permissions-on-the-SharePoint-Site.md)


