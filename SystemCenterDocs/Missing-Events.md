---
title: Missing Events
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8a08de4-2f18-4fd8-a2eb-a151b4488c66
---
# Missing Events
Instead of detecting a particular event to identify an error condition, a missing event monitor in [!INCLUDE[om12short](../Token/om12short_md.md)] uses the absence of a particular event in a particular time window to determine an error. This supports applications that are expected to generate an informational event that indicates a successful operation or the success of a particular action.

For example, consider an application that performs a scheduled data transfer each evening and creates an event when it has completed successfully. A missing event monitor could be created that searches for the event in a particular time window each evening. If the event is detected, then the monitor remains in a healthy state. If it is not found, then it enters error state that indicates that the last transfer did not occur successfully.

## Missing Event Example
The following table provides an example of a missing event monitor by using the following details:

-   Event: Event 1

-   Fixed Schedule: Su\-Sa 2:00 AM – 3:00 AM

-   Health state on missing event: Critical

-   Reset Logic: Event reset using Event 3

|Time|Event|Health State|
|--------|---------|----------------|
|00:00:00|\-|Healthy|
|00:01:00|Event 1|Healthy|
|00:02:00|\-|Healthy|
|00:03:00|\-|Critical|
|00:04:00|\-|Critical|
|00:05:00|Event 3|Healthy|

-   The critical state is triggered at 00:03:00 when Event 1 is not detected within the specified window.

## See Also
[Event Monitors and Rules](../Topic/Event-Monitors-and-Rules.md)
[Windows Events](../Topic/Windows-Events.md)

