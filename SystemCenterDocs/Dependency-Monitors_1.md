---
title: Dependency Monitors_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f05e762-27f2-4001-8243-44cc30a193da
---
# Dependency Monitors_1
*Dependency monitors* let the health of one object be affected by the health of another object. This allows for health rollup between specific related instances of different classes.

Each dependency monitor is based on a specific hosting or containment relationship. Just creating a relationship between two objects does not alone provide rollup between their health states. A dependency monitor must be associated with the relationship for rollup of health to be performed.

The source and target class for a dependency monitor are defined by the relationship that the monitor is based on. The monitor must additionally specify a specific unit monitor or aggregate monitor on the target class and an aggregate monitor on the source class. Only the health of the target monitor is considered when calculating the health of the dependency monitor, and it only affects the health of the specified aggregate monitor on the target object.

**Dependency monitor based on unit monitor**

![](../Image/AuthGuide_10_DependencyMonitorUnit.gif)

**Dependency monitor based on aggregate monitor**

![](../Image/AuthGuide_11_DependencyMonitorAggregate.gif)

Multiple dependency monitors can be created on a single relationship if the health of the source class should be affected by multiple unit or aggregate monitors on the target class. For example, a dependency monitor might be created for each standard aggregate monitor as shown in the following image.

**Multiple dependency monitors for a single class**

![](../Image/AuthGuide_12_DependencyMonitorMutiple.gif)

## Health Rollup Policy
There may be multiple instances of the target class, each with a different health state. Each dependency monitor must define a health rollup policy to define the logic that is used to determine the health of the dependency monitor based on the health of the instances of its target monitor. The possible health rollup policies for a dependency monitor are as follows:

### Worst state policy
The source object matches the state of the target object that has the worst health state. This is used when the source object should only be healthy if all the target objects are healthy. This is the most common policy used by dependency monitors.

**Worst state health policy**

![](../Image/AuthGuide_13_DependencyWorstOf.gif)

### Best state policy
The source object matches the state of the target object that has the best health state. This policy is used when only one of the source objects has to be healthy for the target object to be healthy.

For example, the **Microsoft Windows Hyper\-V 2008 Monitoring** management pack has a dependency monitor on the hosting relationship from **Microsoft.Windows.HyperV.ServerRole** to **Microsoft.Windows.HyperV.VirtualNetwork** that uses a best state policy. This is because the server running Hyper\-V is functional as long as it has one functional virtual network. The logic defined by this management pack is that the server class should show an error state if no virtual networks are available.

**Best state health policy**

![](../Image/AuthGuide_14_DependencyBestOf.gif)

### Percentage policy
The source object matches the worst state of a single member of a specified percentage of target objects in the best state. This policy is used when a certain percentage of target objects must be healthy for the target object to be considered healthy.

For example an application might run on a web farm that includes multiple Web servers. Because of the redundancy offered in this kind of deployment, the application might be considered healthy if a particular percentage of servers is available. The farm itself could be represented in the management pack by a health rollup class based on System.ApplicationComponent with a containment relationship to the Web servers. A dependency monitor could be created on this containment relationship with a health rollup policy specifying a percentage. Even if one or more Web servers had a problem, as long as the specified percentage were in a healthy state then the class representing the web farm would also be healthy.

**Percentage health policy**

![](../Image/AuthGuide_15_DependencyPercentage.gif)

## Health rollup between agents
Health state can only be rolled up between objects managed by the same agent unless the source object is managed by the Root Management Server. Groups and classes used for health rollup are typically unhosted. This means that they are managed by the RMS so that they can roll up health from objects managed by different agents. A relationship can be discovered between objects managed by different agents, but any dependency monitor associated with that relationship will not work as expected.

**Health rollup between agents**

![](../Image/AuthGuide_16_RollupBetweenAgents.gif)

