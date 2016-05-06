---
title: Event Monitor Logic
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b4a1aa8-6ed3-4a34-b7f3-e6cb18962381
---
# Event Monitor Logic
*Event monitors* in [!INCLUDE[om12long](./Token/om12long_md.md)] use one of the event data sources to identify a particular event that indicates an issue. As soon as the specific data source that holds the required information is identified, the logic used to determine different health states must be determined. In addition to the logic that indicates whether an error condition has occurred, additional logic must be defined to determine when the state should be changed back to a healthy condition.

The different kinds of logic that can be used to detect an error condition by using events are listed in the following table. See the individual topic for each condition for details on how its logic is implemented. As noted in the table, some logic can only be used with Windows events.

|Logic|Data Sources|Description|
|---------|----------------|---------------|
|Simple Event|All|Detects an error state from the occurrence of a single event. There is no individual topic for this logic.|
|[Repeating Events](./Repeating-Events.md)|All|Detects an error state from one or more occurrences of a particular event in a specified time window.|
|[Correlated Events](./Correlated-Events.md)|Windows Events|Detects an error state from the occurrence of two events in a specified time window.|
|[Correlated Missing Events](./Correlated-Missing-Events.md)|Windows Events|Detects an error state from an expected event not being detected in a particular time window after the occurrence of another event.|
|[Missing Events](./Missing-Events.md)|Windows Events|Detects an error state from an expected event not being detected in a particular time window.|


