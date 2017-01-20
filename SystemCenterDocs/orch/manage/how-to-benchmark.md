---
title: How to Benchmark
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0755be30-3648-47c0-a009-e2f0ff85040d
author: cfreemanwa
ms.author: cfreeman
ms.date: 10/12/2016
manager: cfreeman
---
# How to Benchmark

> Applies To: System Center 2016 - Orchestrator

Orchestrator runbook activities can be thought of as having two distinct types of code:  platform code and domain code. The term *domain code* is used to identify code within a runbook activity that is typically not associated with the Orchestrator platform itself \(with notable exceptions, such as **Invoke Runbook**, **Junction**, and others\). For example, the **Invoke Web Service** standard activity would contain Orchestrator platform code \(the "plumbing" of the activity\) as well as domain code unique to invoking a SOAP\-based web service. The platform code will be very similar for most activities, since it is built on a common framework. However, there will potentially be great variation in domain code for different activities.  

## Data Logging  
Another aspect of runbook performance is data logging. For the purpose of understanding performance consider two logging configurations: Default logging and Common Published Data logging. Default logging results in approximately 524 bytes of data being written to the Orchestrator database each time an activity is run. Logging of common published data writes approximately 6,082 bytes of data \(12 times the default logging level\). There is a notable difference in performance between these logging levels.  

Consider the scenario where the same runbook activity is run twice, once with data logging at the default level and once with logging of common published data enabled. The domain code should take the same amount of time to complete. However, the platform code will take longer to run with common published data logging enabled. Essentially, the platform code has to support logging 12 times more data with common published data enabled than it did when running at the default logging level.  

The Standard Activity **Compare Values** can been used to create benchmarks of an Orchestrator environment.  

#### To create a runbook that can be used to benchmark your Orchestrator environment  

1.  Create a new runbook.  

2.  Add a **Compare Values** activity from the Standard Activity palette. Double\-click the activity to configure it.  

3.  Click the **General** tab and configure this activity to compare strings \(the default value\).  

4.  Click the **Details** tab, type the value **STRING** in the **Test** box and select **is empty**.  

5.  Click **Finish** to save the updates to the activity.  

6.  Right-click the activity and select **Looping**.  

7.  Select the **Enable** checkbox and enter the number **0** \(zero\) for **Delay between attempts**.  

8.  Click the **Exit** tab.  

9. Change the default exit condition. Click **Compare Values**, check the **Show Common Published Data** checkbox, and select **Loop:  Number of attempts**. Click **OK** to save this change.  

10. Select **value** from the updated exit condition and type the number **10000** \(ten\-thousand\). Click **OK** to save this change.  

11. Click **Finish** to save these updates.  

12. Click **Check In** to save the changes to the Orchestrator database.  

This simple one\-activity runbook will run a **Compare Values** activity 10,000 times. **Compare Values** is a very simple activity whose domain code is quite minimal. This runbook can be invoked under a variety of circumstances to characterize the overall performance of a given Orchestrator runtime environment.  

This runbook can be used to experiment with different configurations of Orchestrator. For example, supposed you wanted to determine the performance of four Runbook Servers deployed to different data centers.  

|Data Center|Logging Configuration|Platform Code Run Time \(seconds\)|ms\/Activity|Scale Factor|  
|---------------|-------------------------|--------------------------------------|----------------|----------------|  
|Location 1|Default logging|819|82|1.0 \(reference\)|  
|Location 1|Logging common published data|2012|201|2.5|  
|Location 2|Default logging|1229|123|1.5|  
|Location 2|Logging common published data|3686|369|4.5|  
|Location 3|Default logging|2457|426|3.0|  
|Location 3|Logging common published data|4422|442|5.4|  
|Location 4|Default logging|1474|147|1.8|  
|Location 4|Logging common published data|2654|265|3.2|  

Notice the significant decrease in platform performance caused by logging of common published data. The worst scenario appears to be logging of common published data at Location 2. On the surface, this appears to be a clear and relevant conclusion.  

However, it should be noted that these figures reflect the overhead of the platform code, not the domain code. Domain code runtimes can be significantly longer. For example, the **Create VM from Template** activity in the Virtual Machine Manager Integration Pack may run for several minutes as the VM is created. Expanding on the previous example, consider the platform code costs on a runbook activity that takes 1 minute to run \(1 minute \= 60,000 milliseconds\) regardless of location.  

|Data Center|Logging Configuration|Platform Code Run Time \(seconds\)|% Domain Code|% Platform Code|  
|---------------|-------------------------|--------------------------------------|-----------------|-------------------|  
|Location 1|Default logging|819|98.6%|1.4%|  
|Location 1|Logging common published data|2012|96.7%|3.3%|  
|Location 2|Default logging|1229|98.0%|2.0%|  
|Location 2|Logging common published data|3686|93.9%|6.1%|  
|Location 3|Default logging|2457|95.9%|4.1%|  
|Location 3|Logging common published data|4422|92.6%|7.4%|  
|Location 4|Default logging|1474|97.5%|2.5%|  
|Location 4|Logging common published data|2654|95.6%|4.4%|  

A clearer picture begins to emerge from the data. The scenario where logging of common published data is enabled at Location 2 continues to be the worst performer. However, the platform code and logging only accounts for 6% of the total runtime. While this is a significant figure, the best\-case scenario is 1.4%. Essentially, the time spent in the domain code in the example far outweighs the time spent running platform code. To put this in perspective, if you were able to completely eliminate the platform code costs, you would only see runbook performance improvements in the range of 1.4 to 7.4%.  

Of course most real\-world scenarios will be different. Activity behavior may change depending on what the domain code is told to do. For example, a **Clone VM from Template** activity may take one minute to clone a VM from Server Template A, but take 5 minutes to clone a VM from Server Template B. Also, Runbook Servers may reside on different networks with different performance characteristics which can potentially impact both domain code performance as well as Orchestrator data logging performance.  

To summarize:  

-   Make careful decisions about when to log published data.  

-   Carefully consider the impact of logging common published data. Remember that the number of times activities run determines the volume of logged data. A runbook with a small number of activities run many times can result in more data logging than a larger runbook run a small number of times.  

-   Do not enable logging of activity specific published data in production environments.  

-   Develop an understanding of how much time your runbooks spend running domain code compared to running platform code.  

-   Estimate platform code costs using the techniques outlined in this document. Use as a reference in considering where to make improvements in runbook performance.  

-   Use the techniques outlined in this document to gain a deeper understanding of the relative performance of your different runtime environments. Identify opportunities for improvement by making normalized comparisons of your measurements.  
