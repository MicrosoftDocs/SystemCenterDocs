---
title: Scoping the Fabric Health Dashboard to a Specific Cloud and Investigating Details
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 83f1231f-ed0e-4daf-8c08-f72c5b5708e5
---
# Scoping the Fabric Health Dashboard to a Specific Cloud and Investigating Details
Using the Fabric Health Dashboard, you can see the overall cloud health and the health of its underlying fabric, but you can also use the Fabric Health Dashboard see the fabric health of any cloud you select. When you scope the dashboard to a particular cloud in the **Cloud State** view, the Fabric Health Dashboard you see a grouping of all of the components that are relevant for that cloud only. When you see a health issue with one component, you can then drill down to investigate a single component in terms of that cloud only. In this way, a fabric administrator can do root cause analysis by digging deeper into an issue, which can lead to other dashboard views, such as the network monitoring dashboard.

## Looking at the Health Cloud by Cloud

#### To scope to a particular cloud

1.  In the [!INCLUDE[omblue_2](./Token/omblue_2_md.md)] console, click **Monitoring**, expand **Cloud Health Dashboard**, click **Cloud Health**, and you see the private clouds you are monitoring in the **Cloud State** pane.

2.  Select the cloud you want to investigate, then, in the **Tasks** pane, click **Fabric Health Dashboard**.

3.  The Fabric Health Dashboard shows only what is related to the particular cloud you selected. You can see the health of each component, Host state, Storage, Networks, and active alerts. It displays a mixture of physical and virtual devices.

From the Fabric Health Dashboard for a particular cloud, you can investigate problems for each component of that particular cloud. In the Tasks pane, in Navagation, you can select from several views and a dashboard to get different information and insight about cloud health.

-   **Alert View** shows active alerts related to the cloud.

-   **Diagram View** shows a view of cloud health as a tree diagram that you can expand to drill down to the level where problems are occurring.

-   **Event View** shows events related to the cloud.

-   **Performance View** shows performance events related to the cloud.

-   **State View** shows the state of the different parts of your cloud fabric.

-   The **Network Vicinity Dashboard** shows information about your current network node in relation to other network nodes that it is attached to.

For example, if you saw a problem with the Network Node State, from the Fabric Health Dashboard, in the **Tasks** pane, click **Network Vicinity Dashboard**, and you can dig deeper into the problem of that particular cloud to see how this network node is affecting other network nodes that this one is attached to. It also places the network problem in context. The Network Node Dashboard shows the Vicinity view of nodes that are connected, an average availability, average response time, and details about the node. This is helpful when investigating particular deep diagnostic information about a networking device or processor use, go down deeper into the health of interfaces on this node.

**More on fabric monitoring**

-   [Monitoring a Private Cloud \- video series](https://curah.microsoft.com/217123/monitoring-a-private-cloud-video-series)

-   [How Healthy is Your Cloud? Fabric Monitoring Can Tell...](http://curah.microsoft.com/42340/how-healthy-is-your-cloud-fabric-monitoring-can-tell)


