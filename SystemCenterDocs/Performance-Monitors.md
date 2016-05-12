---
title: Performance Monitors
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 97cb90ee-bbaf-4b5f-8ca7-094c89c5e7ba
---
# Performance Monitors
Multiple kinds of calculations may be performed to determine the threshold for a performance monitor in [!INCLUDE[om12short](Token/om12short_md.md)]. These threshold types are listed in the following table:

|Threshold Type|Number of States|Description|
|------------------|--------------------|---------------|
|[Average Threshold](Performance-Monitors.md#AverageThreshold)|2|Compare the average of multiple collected values to a threshold.|
|[Consecutive Samples](Performance-Monitors.md#ConsecutiveSamples)|2|Compare several consecutive values to a threshold. All collected values must match the threshold criteria.|
|[Delta Threshold](Performance-Monitors.md#DeltaThreshold)|2|Compare the change between two consecutive values to a threshold.|
|[Double Threshold](Performance-Monitors.md#DoubleThreshold)|3|Compare a single collected value to two thresholds with one that indicates a Warning state and the other that indicates a Critical state.|
|[Simple Threshold](Performance-Monitors.md#SimpleThreshold)|2|Compare a single collected value to a threshold.|

Each kind of logic is described in detail in the following sections:

## <a name="SimpleThreshold"></a>Simple Threshold
The *simple threshold* type is the most basic kind of performance threshold. A single numeric value is provided for the threshold. This threshold is compared to the measured value of the performance data.

Simple threshold supports a two state monitor. One state is set by a performance value equal to or less than the threshold. The other state is set by a performance value greater than the threshold.

## <a name="DoubleThreshold"></a>Double Threshold
The *double threshold* type is similar to the simple threshold type but allows for two thresholds to be specified. Each threshold is compared to the measured value of the performance data.

Double threshold supports a three state monitor. One state is set by a performance value less than the low threshold. Another state is set by a performance value that is greater than or equal to the low threshold or one that is less than or equal to the high threshold. Another state is set by a value that is greater than the high threshold.

The following table provides an example of a double monitor by using the following details:

-   Sample rate: 5 minutes

-   Low threshold value: 10

-   High threshold value: 15

-   Over Upper Threshold State: Critical

-   Between Thresholds State: Warning

-   Under Lower Threshold State: Healthy

|Time|Value|State|
|--------|---------|---------|
|00:00:00|5|Healthy|
|00:05:00|10|Warning|
|00:10:00|12|Warning|
|00:15:00|9|Healthy|
|00:20:00|12|Warning|
|00:25:00|16|Critical|
|00:30:00|15|Critical|
|00:35:00|8|Healthy|

-   The warning threshold is first exceeded at 00:05:00, but the value does not exceed the critical threshold.

-   The critical threshold is first exceeded at 00:25:00 when the state is changed from warning to critical.

-   The state is returned to a healthy state at 00:15:00 and 00:35:00 when the sampled value is less than the warning threshold.

## <a name="AverageThreshold"></a>Average Threshold
The *average threshold* type calculates the average of a specified number of consecutive samples and compares it to the specified threshold.

Average threshold supports a two state monitor. One state is set by an average performance value equal to or less than the threshold. The other state is set by an average performance value greater than the threshold.

The following table provides an example of an average threshold monitor by using the following details:

-   Sample rate: 5 minutes

-   Threshold value: 10

-   Number of samples: 3

-   Over Threshold State: Critical

-   Under Threshold State: Healthy

|Time|Value|Average|State|
|--------|---------|-----------|---------|
|00:00:00|5|\-|Healthy|
|00:05:00|10|\-|Healthy|
|00:10:00|12|9.0|Healthy|
|00:15:00|9|10.3|Critical|
|00:20:00|12|11.0|Critical|
|00:25:00|14|11.7|Critical|
|00:30:00|11|12.3|Critical|
|00:35:00|4|9.7|Healthy|

-   Because the specified number of samples for the average calculation is 3, no value is evaluated until the third sample.

-   The value of 12 sampled at 00:10:00 exceeds the threshold value, but the calculated average from the last 3 samples is 9.0, which is under the threshold. The state is not changed.

-   The value of 9 sampled at 00:15:00 does not exceed the threshold. But the calculated average from the last 3 samples is 10.3 which does exceed the threshold. The state is changed.

-   The monitor does not return to a healthy state until 00:35:00 when the average from the last 3 samples drops the under the threshold value.

## <a name="ConsecutiveSamples"></a>Consecutive Samples
The *consecutive threshold* type compares the threshold value to the performance counter for several consecutive samples. This supports monitors that should not be triggered by only a single value exceeding a threshold. The threshold must be exceeded multiple consecutive times to trigger a change in state.

Consecutive threshold supports a two state monitor. One state is set by the value being either greater than or less than the threshold value for each consecutive sample. The other state is set by a single sample not matching the other criteria.

The following table provides an example of a consecutive sample monitor by using the following details:

-   Sample rate: 5 minutes

-   Threshold value: greater than or equal to 10

-   Number of samples: 3

-   Over Threshold State: Critical

-   Under Threshold State: Healthy

|Time|Value|State|
|--------|---------|---------|
|00:00:00|5|Healthy|
|00:05:00|10|Healthy|
|00:10:00|12|Healthy|
|00:15:00|9|Healthy|
|00:20:00|12|Healthy|
|00:25:00|14|Healthy|
|00:30:00|11|Critical|
|00:35:00|8|Healthy|

-   The threshold is exceeded by the values sampled at 00:05:00 and 00:10:00, but the value at 00:15:00 is under threshold and resets the count.

-   The value at 0:30:00 is the first time that 3 consecutive values have been sampled that exceed the threshold, so the state is changed.

-   The single value at 00:35:00 is under the threshold and resets the monitor to a healthy state.

## <a name="DeltaThreshold"></a>Delta Threshold
The *delta threshold* type compares the threshold value to the difference between two performance values. This might be two consecutive values or two values separated by a specified number of samples.

Delta threshold supports a two state monitor. One state is set by the difference of two values being greater than the threshold value.  The other state is set by the difference of two samples being equal to or less than the threshold value.

The following table provides an example of a delta threshold monitor by using the following details:

-   Sample rate: 5 minutes

-   Threshold value: 10

-   Number of samples: 3

-   Over Threshold State: Critical

-   Under Threshold State: Healthy

|Time|Value|Delta||
|--------|---------|---------|-|
|00:00:00|7|\-|Healthy|
|00:05:00|8|\-|Healthy|
|00:10:00|13|\-|Healthy|
|00:15:00|16|9|Healthy|
|00:20:00|21|13|Critical|
|00:25:00|24|11|Critical|
|00:30:00|25|9|Healthy|

-   Because the specified number of samples that the delta should be calculated from the current sampled value to the value 3 samples behind, no value is evaluated until the fourth sample.

-   The delta calculation exceeds the threshold value at 00:20:00, and the state is changed.

-   The monitor is reset at 00:30:00 when the delta calculation falls under the threshold.

## To Create

