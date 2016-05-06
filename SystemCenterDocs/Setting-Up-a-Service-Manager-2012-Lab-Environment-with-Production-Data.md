---
title: Setting Up a Service Manager 2012 Lab Environment with Production Data
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34e9880c-5faf-4e67-ac1b-7043ab4dc8ad
---
# Setting Up a Service Manager 2012 Lab Environment with Production Data
This section explains how to create a lab environment and populate it with production data so that upgrades can be performed and tested before an actual upgrade in the production environment. The procedures in this section show you how to configure [!INCLUDE[smlong12](./Token/smlong12_md.md)] in a lab environment with production data. You then perform an in\-place upgrade to [!INCLUDE[smlong12](./Token/smlong12_md.md)] SP1. It is important to follow the steps in this section in sequence.

1.  [How to Install an Additional Management Server in the Production Service Manager Management Group](./How-to-Install-an-Additional-Management-Server-in-the-Production-Service-Manager-Management-Group.md)

2.  Install any cumulative updates that you installed on the Primary Management server on the Secondary Management Server.

3.  [How to Copy the Workflow Assembly Files](./How-to-Copy-the-Workflow-Assembly-Files.md)

4.  [How to Disable Service Manager Connectors in the Production Environment](./How-to-Disable-Service-Manager-Connectors-in-the-Production-Environment.md)

5.  [How to Disable Email Notifications  in the Production Environment](./How-to-Disable-Email-Notifications--in-the-Production-Environment.md)

6.  Disable all workflows in the production environment that you do not want to be running in the lab environment.

7.  [How to Stop Service Manager Services on the Secondary Management Server](./How-to-Stop-Service-Manager-Services-on-the-Secondary-Management-Server.md)

8.  [How to Back Up the Production Service Manager Database](./How-to-Back-Up-the-Production-Service-Manager-Database.md)

9. [How to Enable Service Manager Connectors in the Production Environment](./How-to-Enable-Service-Manager-Connectors-in-the-Production-Environment.md)

10. [How to Disable Email Notifications  in the Production Environment](./How-to-Disable-Email-Notifications--in-the-Production-Environment.md)

11. Enable all workflows in the Production Service Manager environment that you disabled in step 6.

12. [How to Restore the Service Manager Database in the Lab Environment](./How-to-Restore-the-Service-Manager-Database-in-the-Lab-Environment.md)

13. [How to Prepare the Service Manager Database in the Lab Environment](./How-to-Prepare-the-Service-Manager-Database-in-the-Lab-Environment.md)

14. If possible, block communications to SQL from the Secondary Management server to the production Service Manager Database server.

15. [How to Start Service Manager Services on the Secondary Management Server](./How-to-Start-Service-Manager-Services-on-the-Secondary-Management-Server.md)

16. Verify that the lab environment works. Try to open the console on the Secondary Management server and see if you can connect to the console. Confirm that the Data Warehouse and Reporting do not appear. After you confirm that this works, complete the rest of the steps.

17. [How to Promote a Secondary Management Server in a Lab Environment](./How-to-Promote-a-Secondary-Management-Server-in-a-Lab-Environment.md)

18. [How to Enable the Connectors in the Lab Environment](./How-to-Enable-the-Connectors-in-the-Lab-Environment.md)

    > [!NOTE]
    > Do not enable or delete the Operations Manager alert connector in the lab environment. This will cause the alert connector in the production environment to fail.

19. If you want to test the email notification and incoming email functionality, use a separate SMTP instance to send emails to eliminate flooding the inboxes of users with test emails. To test the incoming email feature, you can point to a test share and drop the eml files into this share when you are ready to test.

20. [How to Install a New Data Warehouse Server in the Lab Environment](./How-to-Install-a-New-Data-Warehouse-Server-in-the-Lab-Environment.md)

21. [How to Register the Data Warehouse Server in the Lab Environment](./How-to-Register-the-Data-Warehouse-Server-in-the-Lab-Environment.md)

22. Back up this lab environment; for example, back up the database and encryption keys and VM Snapshots This gives you the ability to recover in case the upgrade fails.

23. If you are able to successfully complete all the previous steps, you are ready to attempt the in\-place upgrade.

24. Test everything. Document any discrepancies and fixes. Send feedback through the MS Connect web site.

25. Backup the [!INCLUDE[smshort](./Token/smshort_md.md)] lab environment; for example, back up the database and encryption keys and VM Snapshots This gives you the ability to recover in case the upgrade fails.

26. The lab environment is now ready for [!INCLUDE[smlong12](./Token/smlong12_md.md)] SP1 in\-place upgrade.


