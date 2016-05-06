---
title: Correlated Missing Events
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71cbd5d7-d84e-4e1b-ac8e-35005890a84a
---
# Correlated Missing Events
A correlated missing event monitor in [!INCLUDE[om12short](../Token/om12short_md.md)] determines an error by the absence of a particular event after the occurrence of another. This resembles the missing event monitor except that instead of searching for the missing event in a particular time window, the monitor searches for the event in a particular time after another event is first detected.

For example, consider an application that performs a backup each evening and creates an event when it starts and a second event when it has completed successfully. A correlated missing event monitor could be created that searches for the event in a particular time window each evening. If both events are detected, then the monitor remains in a healthy state. If the first is found, then the timer starts. If the time is reached before the second event is detected, then the state change is triggered to indicate that the last backup did not occur successfully.

## Correlated Missing Events Example
The following table provides an example of a correlated missing event monitor by using the first and the last occurrence of the first event.  The monitor uses the following details:

-   Missing Event Log A: Event 1

-   Missing Event Log B: Event 2

-   Correlation interval: 2 minutes

-   Number of occurrences of Event 2: 3

-   Health state on correlation: Critical

-   Reset Logic: Event reset using Event 3

|Time|Event|First Occurrence|Last Occurrence|
|--------|---------|--------------------|-------------------|
|00:00:00|\-|Healthy|Healthy|
|00:01:00|Event 1|Healthy|Healthy|
|1:30|Event 2|Healthy|Healthy|
|00:02:00|Event 2|Healthy|Healthy|
|00:02:30|Event 1|Healthy|Healthy|
|00:03:00|\-|Critical|Healthy|
|00:03:30|Event 2|Critical|Healthy|
|00:04:00|Event 2|Critical|Healthy|
|00:04:30|\-|Critical|Critical|
|00:05:00|Event 3|Healthy|Healthy|

-   The First Occurrence triggers a critical state at 00:03:00 because Event 2 has not been detected 3 times in the 2 minute interval since the first occurrence of Event 1 at 00:01:00.

-   The Last Occurrence does not trigger a critical state at 00:03:00 because Event 1 occurs at 00:02:30 resetting the timer. The critical state is not triggered until 00:04:30 when Event 2 has not been detected in the 2 minutes interval since the last occurrence of Event 1 at 00:02:30.

-   The single occurrence of Event 3 at 00:05:00 resets both monitors to healthy.

## See Also
[Event Monitors and Rules](../Topic/Event-Monitors-and-Rules.md)
[Windows Events](../Topic/Windows-Events.md)

