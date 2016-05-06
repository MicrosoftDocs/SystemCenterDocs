---
title: How to Recover a Data Warehouse Management Server
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dbf72122-9c66-48e8-bbd4-dd1f2c740872
---
# How to Recover a Data Warehouse Management Server
You can use the following procedure to reinstall a data warehouse management server for [!INCLUDE[smlong12](../Token/smlong12_md.md)].

> [!NOTE]
> You must restore the encryption key before starting this procedure. For more information, see [How to Restore the Service Manager Encryption Key](../Topic/How-to-Restore-the-Service-Manager-Encryption-Key.md).

### To recover a data warehouse management server

1.  Log on to the computer that will host the new data warehouse management server using an account that has administrator rights.

2.  On the [!INCLUDE[smshort](../Token/smshort_md.md)] installation media, double\-click the **Setup.exe** file.

3.  On the **Service Manager Setup Wizard** page, click **Service Manager data warehouse management server**.

4.  On the **Product registration** page, type the information in the boxes. If applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.

5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which you want to install the [!INCLUDE[smshort](../Token/smshort_md.md)] data warehouse management server.

6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.

7.  On the **Configure the data warehouse database** page, do the following:

    1.  In the **Select a database to change its default properties** area, select **Staging and Configuration**.

    2.  In **Database server**, type the name of the computer that is hosting data warehouse databases, and then press the TAB key.

    3.  Select **Use an existing database**.

    4.  Click the **Database** list, select the database name for the Staging and Configuration database \(the default name is **DWStagingAndConfig**\), and then click **Next**.

8.  On the **Configure the data warehouse management group** page, wait until the **Management group name** and **Management group administrators** fields have been populated, and then click **Next**.

9. On the **Configure the reporting server for the data warehouse** page, in the **Report server** text box, type the computer name of the computer that hosts SQL Server Reporting Services \(SSRS\), and then click **Next**.

    > [!NOTE]
    > You must use the original URL for the Reporting Server.

10. On the **Configure the account for Service Manager services** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. Make sure that you receive the following message: "The credentials were accepted.", and then click **Next**.

11. On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a “The credentials were accepted” message, click **Next**.

12. On the **Help improve System Center** page, indicate your preference for participation in both the Customer Experience Improvement Program and Error Reporting. For more information, click **Tell me more about the program**, and then click **Next**.

13. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for [!INCLUDE[smshort](../Token/smshort_md.md)] updates, and then click **Next**.

14. On the **Installation summary** page, click **Install**.

15. On the **Setup completed successfully** page, click **Close**.

