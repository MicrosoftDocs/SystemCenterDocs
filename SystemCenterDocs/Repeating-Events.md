---
title: Repeating Events
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9dacca1d-43be-4caa-ad2a-2183c14a0286
---
# Repeating Events
Repeated event detection in [!INCLUDE[om12short](./Token/om12short_md.md)] uses one or more occurrences of a particular event in a time window to indicate an error condition in a monitor. Repeated event logic is available for the following monitors:

-   Windows Events

-   Text Logs

-   WMI Events

This typically applies to conditions in an application where a single event on its own can be ignored, but multiple occurrences of that event in a particular time window indicate a potential error. There are different algorithms that can be used for this detection, depending on the logic that best identifies the specific application issue. The following are details of the different algorithms:

## Trigger on Timer
*Trigger on timer* consolidation of events uses a specified time window and is not dependent on the number of events received. A single event can trigger an error in the health state as in simple detection. Unlike simple detection which sets the health state immediately upon detection of the specified event, however trigger on timer consolidation waits until a specified time window to set the health state of the monitor. The time window can be a rotating time duration of specified length or a specific window based on day of the week.

Trigger on timer consolidation is useful for errors that should only be detected in a certain time window. Used with a time window based on a specific time of day, this disables the monitor outside that time period. It can also have the effect of delaying the change of state for a particular time during which an event that indicates a healthy state could be received. In this case, the health state would never be changed.

## Trigger on Count
*Trigger on count* consolidation of events lets a monitor require multiple occurrences of the same event in a specified time window before it changes the health state to an error. The time window can be rotating time duration of specified length or a specific window based on day of the week.

Trigger on count consolidation resembles trigger on timer consolidation except that multiple occurrences of the event are required instead of just one. When the time window is reached, the event count is returned to zero, and the specific number of events must detected before the time window expires again for the health state to be changed.

## Trigger on Count, Sliding
*Trigger on count, sliding* consolidation of events is similar to trigger on count consolidation except that the time window is reset every time that the specified event is received. The time window only expires if the time is reached after the occurrence of the last event.

Trigger on count, sliding consolidation is useful for error conditions that are detected by a certain number of events in a particular length of time. By using trigger on count consolidation, some events could be received in one time window and then other events received in the next time window with the result that the health state is never changed. Using trigger on count, sliding consolidation, the time window depends on when the event occurs preventing this condition.

## Repeated Events Example
To help with understanding the different algorithms used for repeated event detection, the following table shows the effect on health state for monitors based on the different kinds of consolidation. This is based on a repeated event monitor that uses the following details:

-   Consolidation interval: 2 minutes

-   Compare count: 3 \(ignored by Trigger on Timer\)

-   Health state on repeated event: Critical

-   Reset Logic: Event reset using Event 3

|Time|Event|Trigger on Timer|Trigger on Count|Trigger on Count, Sliding|
|--------|---------|--------------------|--------------------|-----------------------------|
|00:00:00|\-|Healthy|Healthy|Healthy|
|00:01:00|Event 1|Healthy|Healthy|Healthy|
|00:02:00|\-|Healthy|Healthy|Healthy|
|00:02:30|\-|Healthy|Healthy|Healthy|
|00:03:00|\-|Critical|Healthy|Healthy|
|00:03:30|Event 3|Healthy|Healthy|Healthy|
|00:04:00|Event 1|Healthy|Healthy|Healthy|
|00:04:30|\-|Healthy|Healthy|Healthy|
|00:05:00|Event 1|Critical|Healthy|Healthy|
|00:05:30|\-|Critical|Healthy|Healthy|
|00:06:00|\-|Critical|Healthy|Healthy|
|06:30:00|Event 1|Critical|Healthy|Healthy|
|07:00:00|Event 1|Critical|Healthy|Critical|
|07:30:00|\-|Critical|Healthy|Critical|
|00:08:00|Event 1|Critical|Healthy|Critical|
|00:08:30|\-|Critical|Critical|Critical|
|00:09:00|Healthy|Critical|Healthy|Healthy|

-   Using trigger on timer, a critical state is set at 00:03:00 event though the event is received at 00:01:00 because the time window starts when the monitor is loaded. The start is reset to healthy at 00:03:30, but the critical state is again triggered at 00:05:00 from the time window started at 00:03:00.

-   Using trigger on count, the event at 00:05:00 does not trigger a critical state because the time window started by the event at 00:01:00 would have expired at 00:03:00. This event is instead part of the time window started by the event at 00:04:00 which expires at 00:06:00. The monitor triggers a critical state at 00:08:30 because of the 3 events detected in the time window started with the event at 00:06:30.

-   Using trigger on count, sliding, each occurrence of Event 1 starts its own window. The critical state is triggered at 00:07:00 from the 3 events detected in the time window started with the event at 00:05:00.

## Creating Repeated Event Monitors
The following procedure describes how to create a repeating event monitor with the following details:

-   Positioned under the Availability aggregate monitor.

-   Sets the monitor to a critical state when three events with source **EventCreate** and number **201** are detected in the Application event log within 10 minutes.

-   Resets after fifteen minutes of no event being received.

-   Creates an alert when the monitor enters a critical state.

> [!NOTE]
> **EventCreate** is used as the event source so that the EventCreate utility can be used to create a test event. This utility is available on any Windows Computer and creates test events with a source of **EventCreate**. If you have another method of creating test events, then you can use a different source.

#### To create a repeating event monitor

1.  If you don’t have a management pack for the application that you are monitoring, create one using the process in [Selecting a Management Pack File](./Selecting-a-Management-Pack-File.md).

2.  Create a new target using the process in [To create a Windows Service template](./Windows-Service-Template.md#CreateWindowsServiceTemplate). You can use any service installed on a test agent for this template.

3.  In the Operations console, select the **Authoring** workspace.

4.  Select **Management Pack Objects**.

5.  Right\-click **Monitors**, select **Create and Monitor**, and then select **Unit Monitor**.

6.  On the **Monitor Type** page, do the following:

    1.  In the **Select the type of monitor to create** box, expand **Windows Events** and then **Repeated Event Detection**.

    2.  Select **Timer Reset**.

    3.  In the **Management Pack** dropdown list, select the management pack for the application.

    4.  Click **Next**.

7.  On the General page, do the following:

    1.  In the **Name** box, type **Repeated error event 201** or another name for the monitor. This is the text that will appear in the Health Explorer.

    2.  Click **Select**.

    3.  In the **Select Items to Target** dialog box, select the name that you used for the Windows Service template in step 2.

    4.  The **Parent monitor** box should show **Availability**. You can select a different parent monitor.

    5.  Ensure that **Availability** is selected for the **Parent monitor**.

    6.  The **Monitor is enabled** box should be checked so that the monitor is enabled.

    7.  Click **Next**.

8.  On the **Event Log Name** page, do the following:

    1.  In the **Log Name** box, keep the default value of **Application**.

    2.  Click **Next**

9. On the  **Event Expression** page, do the following:

    1.  For the **Event ID** value, type **201**

    2.  For the **Event Source** value, type **EventCreate**

    3.  Click **Next**.

10. On the **Repeated Settings** page, do the following:

    1.  For the **Counting Mode**, select **Trigger on count, sliding**.

    2.  For the **Compare Count**, type **3**.

    3.  Select **Based on items occurrence within a time interval**.

    4.  For the **Interval**, type **10** and select **Minutes**.

    5.  Click **Next**.

11. On the **Auto Reset Timer** page, do the following:

    1.  For **Specify wait time**, select **15 minutes**.

    2.  Click **Next**

12. On the **Configure Health** page, do the following:

    1.  For **Timer Event Raised**, leave the **Health State** as **Healthy**.

    2.  For **Repeated Event Raised**, set the **Health State** to **Critical**.

    3.  Click **Next**.

13. On the **Configure Alerts** page, do the following:

    1.  Check **Generate alerts for this monitor**.

    2.  For **Generate an alert when:** leave the default of **The monitor is in a critical health state**.

    3.  Leave the box **Automatically resolve the alert when the monitor returns to a health state** checked.

    4.  For the **Alert name**, leave the default which is the name of the monitor or replace it with different text. This will be the name of the alert that appears in the Operations console when the alert is created.

    5.  Leave the default **Priority** of **Medium**.

    6.  Leave the default **Severity** of **Critical**. Note that you can change the alert severity to Warning even though the monitor is set to Critical

    7.  In the **Alert description** box, type **Event 201 was detected $Data\/Context\/Count$ times between $Data\/Context\/TimeWindowStart$ and $Data\/Context\/TimeWindowEnd$.  The first event was at $Data\/Context\/TimeWindowStart$. The last event was at $Data\/Context\/TimeWindowEnd$.**. Rather than typing in each of the $Data variables, you can select them by clicking the ellipse button and then selecting **Data** and the property.

    8.  Click **Create**.

## See Also
[Event Monitors and Rules](./Event-Monitors-and-Rules.md)
[Windows Events](./Windows-Events.md)
[Text Logs](./Text-Logs.md)
[WMI Events](./WMI-Events.md)


