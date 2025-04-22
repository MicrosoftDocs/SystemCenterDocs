---
title: Configure a Product Connector Subscription
description: This article describes how to configure a product connector for integrating Operations Manager with an enterprise monitoring solution.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/22/2025
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
ms.assetid: 5de28eac-5d62-47bf-bc20-0d1897868a5d
---

# Configure a product connector subscription

This article describes how to configure a product connector for integrating Operations Manager with an enterprise monitoring solution.

System Center - Operations Manager supports the ability to synchronize alert data with other applications, such as other management systems, using product connectors. After a product connector is installed, by default, all alerts are forwarded through the product connector. In the following procedure, you use the Product Connector Subscription Wizard to specify which alerts you want the product connector to forward.  

> [!NOTE]  
> You must have a product connector installed prior to beginning this procedure. Install the product connector according to the product connector vendor's installation instructions.  

## Configure a subscription for a product connector  

To configure a subscription for a product connector, follow these steps:

1. Sign in to the computer with an account that is a member of the Operations Manager Administrators user role.  

2. In the Operations console, select **Administration**.  

3. In the Administration pane, select **Product Connectors**. In the Product Connectors pane, right-click the product connector and select **Properties**. The **Product Connector Properties** dialog displays. In the **Subscriptions** section, select the **Add** button. The **Product Connector Subscription Wizard** starts.  

    > [!NOTE]  
    > Operations Manager internal product connectors are listed in the Operations console. These connectors are used for discovery workflows. Don't create subscriptions for these internal product connectors.  

4. On the **General** page, enter a name and a short description for the subscription you're creating, and select **Next**.  

5. On the **Groups** page, you can filter which alerts this connector forwards to an external management system based on groups. By default, all checkboxes are selected, so alerts from all groups are forwarded. To enable the child checkboxes, clear the top\-level checkbox. After you make your selections, select **Next**.  

6. On the **Targets** page, you can filter which alerts this connector forwards based on object type. By default, alerts are accepted from all object types in all management packs. You can specify particular management packs or certain monitored objects from which you want to forward alerts. To accept alerts from only specified types of objects, select **Forward alerts from targets explicitly added to the 'Approved targets' grid are approved** and select the **Add** button to select individual targets.  

7. On the **Criteria** page, you can filter which alerts this connector forwards based on the severity, priority, resolution state, and category of the alert. By default, all criteria are selected, so all alerts are forwarded. However, you can individually select which alerts you want forwarded. After you make your selections, select **Create** to create the product connector subscription. You can view the newly created subscription in the details pane.  

## Next steps

To learn how to integrate Operations Manager with another monitoring platform or ITSM system using a product connector developed using the Operations Manager SDK, review [Connect Operations Manager with other management systems](manage-integration-thirdparty-overview.md).  
