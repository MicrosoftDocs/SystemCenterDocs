---
title: Correlated Events
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1646873-2515-4876-b03a-353e1735c0b4
---
# Correlated Events
A correlated event monitor in [!INCLUDE[om12short](./Token/om12short_md.md)] uses two separate events in a particular time period to detect a single issue. This kind of monitor supports conditions where an issue cannot be identified by a single event alone.

When the first event is detected, a timer is triggered. If the second event is received within that period, the state change is triggered. If the second event is not received in the period, the timer is reset until the first event is received again. The monitor may be configured to better tune the specific conditions that must be met in order to perform correlation. These options include the following:

-   Whether the events must be in chronological order. One of the events may always be expected before the other one, or they may be expected in either order.

-   Whether the first or last occurrence of the first event should be used. If the first occurrence is specified, then each occurrence of the first event will have its own time window and search for corresponding occurrences of the second event. With the last occurrence specified, if the first event reoccurs with the time window, then the time window is extended based on the last event. The monitor can also be configured to reset the time window every time that the first event occurs. When the time window is reset, all previous occurrences of both events are ignored.

-   The number of occurrences of the second event that must be received to trigger the state change. Instead of changing the health state after receiving a single instance of the two events, multiple instances of the second event may be required.

-   Properties between the first and second event that must match for correlation to be performed. Instead of detecting two occurrences of each event, additional comparison may be required to determine whether the events are related. The monitor can, for example, confirm that a particular parameter matches between the two events to make sure that they match.

## Correlated Events Example
The following table provides an example of a correlated event monitor by using the first and the last occurrence of the first event.  The monitor uses the following details:

-   Event Log A: Event 1

-   Event Log B: Event 2

-   Correlation interval: 2 minutes

-   Number of occurrences of Event 2: 3

-   Health state on correlation: Critical

-   Reset Logic: Event reset using Event 3

|Time|Event|First Occurrence|Last Occurrence|
|--------|---------|--------------------|-------------------|
|00:00:00|\-|Healthy|Healthy|
|00:01:00|Event 1|Healthy|Healthy|
|01:30|Event 2|Healthy|Healthy|
|00:02:00|Event 2|Healthy|Healthy|
|00:02:30|\-|Healthy|Healthy|
|00:03:00|Event 1|Healthy|Healthy|
|00:03:30|Event 2|Healthy|Healthy|
|00:04:00|Event 2|Healthy|Healthy|
|00:04:30|Event 1|Healthy|Healthy|
|00:05:00|Event 2|Critical|Healthy|
|05:30:00|Event 3|Healthy|Healthy|
|06:00:00|Event 1|Healthy|Healthy|
|06:30:00|Event 2|Healthy|Healthy|
|07:00:00|Event 1|Healthy|Healthy|
|07:30:00|Event 2|Healthy|Healthy|
|08:00:00|Event 2|Critical|Healthy|
|08:30:00|Event 2|Critical|Critical|
|09:00:00|Event 3|Healthy|Healthy|

-   The First Occurrence does not trigger a critical state when Event 2 is detected at 00:03:00 because the timer was reset at 00:03:00 which is 2 minutes after the first occurrence of Event 1 at 00:01:00.

-   The First Occurrence triggers a critical state at 00:05:00 because Event 2 is detected 3 times within the 2 minutes since the first occurrence of Event 1 at 00:03:00. Event 1 starts a new time window at 00:03:00 because the time window from Event 1 at 00:01:00 would have expired.

-   The First Occurrence triggers a critical state at 00:08:00 because Event 2 is detected 3 times within 2 minutes from Event 1 at 00:06:00.

-   The First Occurrence resets its state to healthy at 00:05:30 and 00:09:00 because Event 3 is detected.

## See Also
[Event Monitors and Rules](./Event-Monitors-and-Rules.md)
[Windows Events](./Windows-Events.md)


