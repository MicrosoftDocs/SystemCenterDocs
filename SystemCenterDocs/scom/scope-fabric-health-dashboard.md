---
ms.assetid: e0c24f1f-9457-49f6-8f65-069aa45dbbd8
title: Scope the Fabric Health Dashboard to a Specific Cloud and Investigating Details in System Center Operations Manager
description: This article provides an overview of scoping the Fabric Health Dashboard to a Specific Cloud and Investigating Details
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Scope the Fabric Health Dashboard to a specific cloud

Using the Fabric Health Dashboard, you can see the overall cloud health and the health of its underlying fabric, you can also use the Fabric Health Dashboard to see the fabric health of any cloud you select. When you scope the dashboard to a particular cloud in the **Cloud State** view, the Fabric Health Dashboard displays a grouping of all of the components that are relevant for that cloud only. When you see a health issue with any component, you can then drill down to investigate a single component in terms of that cloud only. In this way, a fabric administrator can do root cause analysis by digging deeper into an issue, which can lead to other dashboard views, such as the network monitoring dashboard.

## Monitor the health of a cloud

### Scope to a particular cloud

1. In the Operations Manager console, select **Monitoring**, expand **Cloud Health Dashboard**, select **Cloud Health**, and you see the private clouds you're monitoring in the **Cloud State** pane.

2. Select the cloud you want to investigate. Then in the **Tasks** pane, select **Fabric Health Dashboard**.

3. The Fabric Health Dashboard shows only what's related to the particular cloud you selected. You can see the health of each component, Host state, Storage, Networks, and active alerts. It displays a mixture of physical and virtual devices.

From the Fabric Health Dashboard for a particular cloud, you can investigate problems for each component of that particular cloud. In the Tasks pane, in Navigation, you can select from several views and a dashboard to get different information and insight about cloud health.

- **Alert View** shows active alerts related to the cloud.

- **Diagram View** shows a view of cloud health as a tree diagram that you can expand to drill down to the level where problems are occurring.

- **Event View** shows events related to the cloud.

- **Performance View** shows performance events related to the cloud.

- **State View** shows the state of the different parts of your cloud fabric.

- **The Network Vicinity Dashboard** shows information about your current network node in relation to other network nodes that it's attached to.

For example, if you saw a problem with the Network Node State, from the Fabric Health Dashboard in the **Tasks** pane, select **Network Vicinity Dashboard**, and you can dig deeper into the problem of that particular cloud to see how this network node is affecting other network nodes that this one is attached to. It also places the network problem in context. The Network Node Dashboard shows the Vicinity view of nodes that are connected, an average availability, average response time, and details about the node. This is helpful when investigating particular deep diagnostic information about a networking device or processor use, go down deeper into the health of interfaces on this node.

## Next steps

- [Fabric Monitoring diagram view](fabric-monitoring-diagram-view.md)
- [Monitor cloud fabric using System Center Advisor](use-system-center-advisor.md)
