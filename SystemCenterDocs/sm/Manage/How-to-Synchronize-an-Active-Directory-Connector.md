---
title: How to Synchronize an Active Directory Connector
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4938b79-f8ff-4c8f-85da-beebb9d44fb2
---
# How to Synchronize an Active Directory Connector

>Applies To: System Center 2016 Technical Preview - Service Manager

To ensure that the Service Manager database is up to date, the Active Directory connector synchronizes with Active Directory Domain Services (AD DS) every hour after the initial synchronization. However, you can use the following procedure to manually synchronize the connector and validate that it is synchronized.

### To manually synchronize an Active Directory connector

1.  In the Service Manager console, click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.

3.  In the **Connectors** pane, select the Active Directory connector that you want to synchronize.

4.  In the **Tasks** pane, under the name of the connector, click **Synchronize Now**.

    > [!NOTE]
    > Depending on the amount of data that is imported, you might have to wait for the import to be completed.

### To validate that an Active Directory connector synchronized

1.  In the Service Manager console, click **Configuration Items**.

2.  In the **Configuration Items** pane, expand **Printers**, and then click **All Printers**. Verify that any new printers in AD DS appear in the middle pane.

3.  Expand **Computers**, and then click **All Windows Computers**. Verify that any new computers in AD DS appear in the middle pane.

4.  In the Service Manager console, click **Configuration Items**.

5.  In the **Configuration Items** pane, click **Users**. Verify that any new users and groups in AD DS appear in the middle pane.



