---
title: How to Recover a Service Manager Management Server
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45806547-b23c-4e01-a503-02d2666fd737
---
# How to Recover a Service Manager Management Server
You can use the following procedure to reinstall a management server in [!INCLUDE[smlong12](./Token/smlong12_md.md)].

> [!NOTE]
> You must restore the encryption key before starting this procedure. For more information, see [How to Restore the Service Manager Encryption Key](./How-to-Restore-the-Service-Manager-Encryption-Key.md).

### To recover a Service Manager management server

1.  Log on to the computer that will host the new [!INCLUDE[smshort](./Token/smshort_md.md)] management server using an account that has administrator rights.

2.  On the [!INCLUDE[smshort](./Token/smshort_md.md)] installation media, double\-click the **Setup.exe** file.

3.  On the **Service Manager Setup Wizard** page, click **Service Manager management server**.

4.  On the **Product registration** page, type the information in the text boxes. If applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which you want to install the [!INCLUDE[smshort](./Token/smshort_md.md)] management server.

6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.

7.  On the **Configure the Service Manager database** page, do the following:

    1.  In **Database server**, type the name of the computer that is hosting the [!INCLUDE[smshort](./Token/smshort_md.md)] database, and then press the TAB key.

    2.  Select **Use an existing database**.

    3.  Click the **Database** list, select the database name for the Service Manager database \(the default name is **ServiceManager**\), and then click **Next**.

8.  On the **Configure the Service Manager management group**, wait until the **Management group name** and **Management group administrators** fields have been populated. Then, click **Next**.

9. On the **Configure the account for Service Manager services** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. Make sure that you receive the following message: "The credentials were accepted." and then click **Next**.

10. On the **Help improve System Center** page, indicate your preference for participation in both the Customer Experience Improvement Program and Error Reporting. For more information, click **Tell me more about the program**, and then click **Next**.

11. On the **Installation summary** page, click **Install**.

12. On the **Setup completed successfully** page, click **Close**.


