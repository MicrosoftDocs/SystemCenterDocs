---
title: Set up a Service Manager 2016 lab environment with production data
description: Create a lab environment and populate it with production data so that upgrades can be performed and tested before you upgrade a production environment.
manager: carmonm
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
ms.assetid: 34e9880c-5faf-4e67-ac1b-7043ab4dc8ad
---

# Set up a Service Manager 2016 lab environment with production data to prepare for upgrade

This article explains how to create a lab environment and populate it with production data so that upgrades can be performed and tested before an actual upgrade in the production environment. The procedures in this article show you how to configure Service Manager in a lab environment with production data. You then perform an in-place upgrade to System Center 2016 – Service Manager. It is important to follow the steps in this article in the order that they appear.

In the [production environment](prod-env.md):

1. [Install an Additional Management Server in the Production Service Manager Management Group](prod-env.md#install-an-additional-management-server-in-the-production-service-manager-management-group)
2. Install any cumulative updates that you installed on the Primary Management server on the Secondary Management Server.
3. [Copy the Workflow Assembly Files](prod-env.md#copy-customized-workflow-assembly-files)
4. [Disable Service Manager Connectors in the Production Environment](prod-env.md#disable-service-manager-connectors-in-the-production-environment)
5. [Disable Email Notifications in the Production Environment](prod-env.md#disable-email-notifications-in-the-production-environment)
6. Disable all workflows in the production environment that you do not want to be running in the lab environment.
7. [Stop Service Manager Services on the Secondary Management Server](prod-env.md#stop-service-manager-services-on-the-secondary-management-server)
8. [Back Up the Production Service Manager Database](prod-env.md#back-up-the-production-service-manager-database-for-future-recovery)
9. [Enable Service Manager Connectors in the Production Environment](prod-env.md#enable-service-manager-connectors-in-the-production-environment)
10. [Enable Email Notifications in the Production Environment](prod-env.md#enable-email-notifications-in-the-production-environment)
11. Enable all workflows in the Production Service Manager environment that you disabled in step 6.

In the [lab environment](lab-env.md):

1. [Restore the Service Manager Database in the Lab Environment](lab-env.md#restore-the-service-manager-database-in-the-lab-environment)
2. [Prepare the Service Manager Database in the Lab Environment](lab-env.md#prepare-the-service-manager-database-in-the-lab-environment)
3. If possible, block communications to SQL from the Secondary Management server to the production Service Manager Database server.
4. [Start Service Manager Services on the Secondary Management Server](lab-env.md#start-service-manager-services-on-the-secondary-management-server)
5. Verify that the lab environment works. Try to open the console on the Secondary Management server and see if you can connect to the console. Confirm that the Data Warehouse and Reporting do not appear. After you confirm that this works, complete the rest of the steps.
6. [Promote a Secondary Management Server in a Lab Environment](lab-env.md#promote-a-secondary-management-server-in-a-lab-environment)
7. [Enable the Connectors in the Lab Environment](lab-env.md#enable-the-connectors-in-the-lab-environment)
  >[!NOTE]
  Do not enable or delete the Operations Manager alert connector in the lab environment. This will cause the alert connector in the production environment to fail.

8. If you want to test the email notification and incoming email functionality, use a separate SMTP instance to send emails to eliminate flooding the inboxes of users with test emails. To test the incoming email feature, you can point to a test share and drop the eml files into this share when you are ready to test.
9. [Install a New Data Warehouse Server in the Lab Environment](lab-env.md#install-a-new-data-warehouse-server-in-the-lab-environment)
10. [Register the Data Warehouse Server in the Lab Environment](lab-env.md#register-the-data-warehouse-server-in-the-lab-environment)
11. Back up this lab environment; for example, back up the database and encryption keys and VM Snapshots This gives you the ability to recover in case the upgrade fails.
12. If you are able to successfully complete all the previous steps, you are ready to attempt the in-place upgrade.
13. Test everything. Document any discrepancies and fixes. Send feedback through the MS Connect web site.
14. Backup the Service Manager lab environment; for example, back up the database and encryption keys and VM Snapshots This gives you the ability to recover in case the upgrade fails.
15. The lab environment is now ready for System Center 2016 – Service Manager in-place upgrade.

## Next steps

- [Prepare the production environment](prod-env.md)
