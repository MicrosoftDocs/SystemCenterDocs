---
title: How to Configure a Product Connector Subscription
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5de28eac-5d62-47bf-bc20-0d1897868a5d
---
# How to Configure a Product Connector Subscription
[!INCLUDE[om12long](../Token/om12long_md.md)] supports the ability to synchronize alert data with other applications, such as other management systems, using product connectors. After a product connector is installed, by default, all alerts are forwarded through the product connector. In the following procedure, you use the Product Connector Subscription Wizard to specify which alerts you want the product connector to forward.

> [!NOTE]
> You must have a product connector installed prior to beginning this procedure. Install the product connector according to the product connector vendor's installation instructions.

### To configure a subscription for a product connector

1.  Log on to the computer with an account that is a member of the Operations Manager Administrators user role.

2.  In the Operations console, click **Administration**.

3.  In the Administration pane, click **Product Connectors**. In the Product Connectors pane, right\-click the product connector and then click **Properties**. The **Product Connector Properties** dialog box displays. In the **Subscriptions** section, click the **Add** button. The **Product Connector Subscription Wizard** starts.

    > [!NOTE]
    > Operations Manager internal product connectors are listed in the Operations console. These connectors are used for discovery workflows. Do not create subscriptions for these internal product connectors.

4.  On the **General** page, type a name and a short description for the subscription you are creating, and then click **Next**.

5.  On the **Groups** page, you can filter which alerts this connector forwards to an external management system based on groups. By default, all check boxes are selected, so alerts from all groups are forwarded. To enable the child check boxes, clear the top\-level check box. After you make your selections, click **Next**.

6.  On the **Targets** page, you can filter which alerts this connector forwards based on object type. By default, alerts are accepted from all object types in all management packs. You can specify particular management packs or certain monitored objects from which you want to forward alerts. To accept alerts from only specified types of objects, click **Forward alerts from targets explicitly added to the 'Approved targets' grid are approved** and then click the **Add** button to select individual targets.

7.  On the **Criteria** page, you can filter which alerts this connector forwards based on the severity, priority, resolution state, and category of the alert. By default, all criteria are selected, so all alerts are forwarded. However, you can individually select which alerts you want forwarded. After you make your selections, click **Create** to create the product connector subscription. You can view the newly created subscription in the details pane.

## See Also
[Connecting Operations Manager With Other Management Systems](../Topic/Connecting-Operations-Manager-With-Other-Management-Systems.md)

