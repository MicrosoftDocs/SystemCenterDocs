---
title: Database sizing and performance
description: Provides guidance for sizing the System Center - Orchestrator database
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
ms.custom: engagement-fy23
---

# Database sizing and performance

Database sizing is the key to understanding the performance of System Center - Orchestrator. The runbook servers, management server, and web components all depend on the Orchestrator database for their operations. Problems with Orchestrator deployments can arise from an incomplete understanding of the types of data in the database and how to manage them.  

Because the Runbook Designer communicates with the Orchestrator database (through the management server), poor database performance will impede that communication.  

The Orchestrator operator experience is based on two components: The **Orchestration Console** and the Web Service. The **Orchestration Console** is a Silverlight-based application that depends on the Web Service for its connection to the Orchestrator database. The Web Service is an IIS application that connects to the database. So, the Web Service and **Orchestration Console** are both dependent on the performance of the Orchestrator database.  

Additionally, while the **Orchestration Console** is dependent on the Web Service, it also has logic unique to its function as a user interface and its own performance characteristics.  

## Configuration Data and Log Data

At a high level, the Orchestrator database contains two kinds of data:  

### Configuration Data  

The Orchestrator infrastructure contains configuration data. This data isn't a concern in the context of database growth because the storage requirements for this type of data are small.  

### Log Data  

Orchestrator creates different types of log data, all of which can be viewed and managed in the **Runbook Designer**. The storage requirements for this data can vary in size and can be large.  

The following table lists the types of log data that can be stored in the Orchestrator database. Orchestrator also stores data in separate log files (outside of the database) for audit trails and tracing. For more information about all the types of log data, see [Orchestrator Logs](orchestrator-logs.md).  

|Type of Log Data|Location in Runbook Designer|Managed by Log Purge?|  
|--------------------|--------------------------------|-------------------------|  
|Runbook logs|**Log** and **Log History** tabs|Yes|  
|Activity (Platform) events|**Events** tab|No|  
|Audit history|**Audit History** tab|No|  

## Platform Code and Domain Code

Orchestrator runbook activities contain two distinct types of code:  

- *Platform Code*

  This is the common code shared by most activities and is used to run common tasks performed by Orchestrator activities. Platform code generates Common Published Data.  

- *Domain Code*

  Runs various tasks that are specific for the actions for each activity, which are typically not associated with the Orchestrator platform itself. Potentially, there can be a great variation between platform code and domain code.  

The logging data generated for a given activity can contain data elements that are single or multi\-valued. Every activity produces a single record of single\-value data. Domain code can produce multiple records of multi\-value data and is therefore responsible for determining what the activity does with the common published data it has received from prior activities.  

Essentially, Orchestrator runbooks are designed to pass data between discrete elements of domain code. Also, domain code can optionally generate Activity\-specific Published Data.  

All runbooks have core similarity in that they run activities that consist of domain code and platform code, they loop workflows and they branch. Branching is when a runbook calls other runbooks to do a specific task. When a runbook is first invoked, it consists of a single thread. When this thread encounters a runbook activity whose links require a branch, additional threads are created, one for each branch. Each thread takes as input the common published data from the activity that created the branch. This data is correlated back to the prior activities in the runbook to update the common published data that the activities subscribe to.  

Domain code potentially affects database performance more than multi\-threading generated by branching. This is because domain code can potentially generate large amounts of activity\-specific published data.  

## Logging Options

The **Logging** tab on the **Properties** for a runbook allows you to optionally store logging entries. The term *default logging* refers to having neither of the two published data options selected, which amounts to 524 bytes generated for each activity. The logging options provide for two categories of common published data:  

- *Common Published Data*  

    The set of data items common to all activities. For a list, see the [Runbook Log Options](design-and-build-runbooks.md).  

    This logging option generates 6082 bytes for each activity.  

- *Activity\-specific Published Data*  

    The set of data that is specific to the activity that is optionally created by domain code.  

    This logging option generates 6082 bytes in addition to the bytes logged by specific activities.  

    > [!TIP]  
    > This option is selected primarily for debugging purposes. Leave unchecked to limit logging growth.  

Setting logging options can significantly affect performance and increase database growth. Consider the scenario where the same runbook activity is run twice, first with data logging at the default level (no published data options selected) and then set with common published data selected. The domain code should take the same amount of time to complete. However, the platform code will take longer to run because it has to support 12 times the amount of common published data logging than it does with just default logging.  

## Purge Logs

The default options specified for the **Log Purge** feature in the **Runbook Designer** are configured to provide the best user experience for an out\-of\-the\-box Orchestrator deployment. Changing these values can change the performance characteristics of the environment and should be implemented gradually and high\-watermarked so that the effect of the change can be evaluated.  

For more information on automatic and manual purging of logs, see the [Purging Runbook Logs](design-and-build-runbooks.md).  

## Create Performance Benchmarks

To create a simple runbook to test logging growth, you can use the Standard Activity **Compare Values** to create benchmarks of an Orchestrator environment.  

The following procedure creates a runbook that runs a **Compare Values** activity 10,000 times. **Compare Values** is a simple activity whose domain code is minimal. This runbook can be invoked under various circumstances to characterize the overall performance of a given Orchestrator runtime environment.  

### Create a runbook that can be used to benchmark your Orchestrator environment  

1. Create a new runbook.  

2. Add a **Compare Values** activity from the Standard Activity palette. Double\-click the activity to configure it.  

3. Select the **General** tab and configure this activity to compare strings (the default value).  

4. Select the **Details** tab, enter the value **STRING** in the **Test** box, and select **is empty**.  

5. Select **Finish** to save the updates to the activity.  

6. Right-click the activity and select **Looping**.  

7. Select the **Enable** checkbox and enter the number **0** (zero) for **Delay between attempts**.  

8. Select the **Exit** tab.  

9. Change the default exit condition. Select **Compare Values**, check the **Show Common Published Data** checkbox, and select **Loop:  Number of attempts**. Select **OK** to save this change.  

10. Select **value** from the updated exit condition and enter the number **10000** (ten\-thousand). Select **OK** to save this change.

11. Select **Finish** to save these updates.  

12. Select **Check In** to save the changes to the Orchestrator database.  

This runbook can be used to experiment with different configurations of Orchestrator. For example, you can create the benchmark runbooks to determine the performance of four Runbook Servers deployed to different data centers.  

|Data Center|Logging Configuration|Platform Code Run Time (milliseconds)|Milliseconds per Activity|Scale Factor|  
|---------------|-------------------------|-------------------------------------------|-----------------------------|----------------|  
|Location 1|Default logging|819|82|1.0 (reference)|  
|Location 1|Logging common published data|2012|201|2.5|  
|Location 2|Default logging|1229|123|1.5|  
|Location 2|Logging common published data|3686|369|4.5|  
|Location 3|Default logging|2457|426|3.0|  
|Location 3|Logging common published data|4422|442|5.4|  
|Location 4|Default logging|1474|147|1.8|  
|Location 4|Logging common published data|2654|265|3.2|  

Notice the significant decrease in platform performance caused by logging of common published data. The worst scenario appears to be logging of common published data at Location 2. On the surface, this appears to be a clear and relevant conclusion.  

However, it should be noted that these figures reflect the overhead of the platform code, not the domain code. Domain code runtimes can be longer. For example, the **Create VM from Template** activity in the Virtual Machine Manager Integration Pack may run for several minutes as the VM is created. Expanding on the previous example, consider the platform code costs on a runbook activity that takes 1 minute to run (1 minute \= 60,000 milliseconds) regardless of the location.  

|Data Center|Logging Configuration|Platform Code Run Time (milliseconds)|% Domain Code|% Platform Code|  
|---------------|-------------------------|-------------------------------------------|-----------------|-------------------|  
|Location 1|Default logging|819|98.6%|1.4%|  
|Location 1|Logging common published data|2012|96.7%|3.3%|  
|Location 2|Default logging|1229|98.0%|2.0%|  
|Location 2|Logging common published data|3686|93.9%|6.1%|  
|Location 3|Default logging|2457|95.9%|4.1%|  
|Location 3|Logging common published data|4422|92.6%|7.4%|  
|Location 4|Default logging|1474|97.5%|2.5%|  
|Location 4|Logging common published data|2654|95.6%|4.4%|  

A clearer picture begins to emerge from the data. The scenario where logging of common published data is enabled at Location 2 continues to be the worst performer. However, the platform code and logging only accounts for 6% of the total runtime. While this is a significant figure, the best\-case scenario is 1.4%. Essentially, the time spent in the domain code in the example far outweighs the time spent running platform code. To put this in perspective, if you were able to completely eliminate the platform code costs, you would only see runbook performance improvements in the range of 1.4% to 7.4%.  

Most real\-world scenarios will be different. Activity behavior may change depending on what the domain code is told to do. For example, a **Clone VM from Template** activity may take one minute to clone a VM from Server Template A, but take 5 minutes to clone a VM from Server Template B. Also, Runbook Servers may reside on different networks with different performance characteristics, which can potentially affect both domain code performance and Orchestrator data logging performance.  

## Determine Database Growth

Your database administrator for the Orchestrator database can use the following guidelines for determining database file growth strategy:  

- In general, the database files won't increase in size with each invocation of a runbook. The files will grow when the data contained within them reaches a certain high watermark configured by your database administrator, at which time the file will generally be expanded.  

- Each time a runbook activity runs, it should be counted individually, which should be considered when looping features can cause a single activity to run multiple times.  

- To determine the storage needed for each invocation of the runbook, multiply the number of activities in the runbook by the number of bytes added to the database according to the selected logging level. These values are as follows:  

    - 524 bytes  

        Default logging configuration.  

    - 6082 bytes  

        Common published data logging level.  

    - 6082 bytes \+ data logged by activity  

        Activity\-specific published data logging level.  

- By default, Orchestrator purges all but the most recent 500 logs for each runbook nightly at 2:00 am. To determine the storage required for each invocation of the runbook, multiply the storage needed for each invocation of the runbook by 500. If you change the Log Purge setting, multiply each invocation by the estimated number of invocations per day, week, or month as needed.  

The following table shows growth and performance estimates for the logging level configurations.  

|Logging Level|DB Growth Factor|Performance Factor|Recommended for Production|  
|-----------------|--------------------|----------------------|------------------------------|  
|Default|1|1|Yes|  
|Common published data|11.6x|2.5x|Limited use with planning|  
|Activity\-specific published data|Greater than 11.6x|Greater than 2.5x|No|  

## Examples  

### Example 1

The following table describes the database sizing considerations for a deployment of Orchestrator.  

|Runbook Name|Number of Activities|Logging Level|Invocations per Day|  
|----------------|------------------------|-----------------|-----------------------|  
|Runbook 1|50|Default|100|  
|Runbook 2|25|Default|50|  
|Runbook 3|12|Common published data|24|  
|Runbook 4|8|Common published data|500|  

Using the database sizing described above, you can estimate the storage requirements for the runbooks.  

|Runbook Name|Bytes per Invocation|Storage in MB<br /><br />Default Log Purge (500 invocations)|Invocations per Month|Storage in MB<br /><br />One Month<br /><br />\(Not Default Log Purge)|% of DB storage after 30 Days|  
|----------------|------------------------|----------------------------------------------------------|-------------------------|-----------------------------------------------------------|---------------------------------|  
|Runbook 1|26,200|12.5|3,000|74.5|9%|  
|Runbook 2|13,100|6.2|1,500|18.7|2%|  
|Runbook 3|72,984|34.8|720|50.1|6%|  
|Runbook 4|48,656|23.2|15,000|696.0|83%|  
|||Total: 76.7 MB||Total: 839.3 MB||  

This example clearly illustrates the importance of making sound decisions for data logging. Runbook 4 contains only eight activities, but when configured at the Common Published Data Logging level, it consumes most of the storage in the database because of the high frequency of invocation. Based on these results, you may prefer to reduce the logging level of Runbook 4 to the Default logging configuration.  

### Example 2

The following table describes the database sizing considerations for another deployment of Orchestrator.  

|Runbook Name|Number of Activities|Logging Level|Invocations per Day|  
|----------------|------------------------|-----------------|-----------------------|  
|Runbook 1|50|Default|100|  
|Runbook 2|25|Default|50|  
|Runbook 3|12|Common published data|24|  
|Runbook 4|8|Default|500|  

Recalculating the storage figures for the updated configuration produces significantly different results.  

|Runbook Name|Bytes per Invocation|Storage in MB<br /><br />Default Log Purge (500 invocations)|Invocations per Month|Storage in MB<br /><br />One Month<br /><br />(Not Default Log Purge)|% of DB storage after 30 Days|  
|----------------|------------------------|----------------------------------------------------------|-------------------------|-----------------------------------------------------------|---------------------------------|  
|Runbook 1|26,200|12.5|3,000|74.5|37%|  
|Runbook 2|13,100|6.2|1,500|18.7|9%|  
|Runbook 3|72,984|34.8|720|50.1|25%|  
|Runbook 4|4,192|2.0|15,000|60.0|29%|  
|||Total: 55.5 MB||Total: 203.3 MB||  

While there's little change in the default logging configuration (500 log entries per runbook), the 30\-day storage requirements have changed greatly. Clearly, the storage cost of using Common Published Data logging for Runbook 4 should be carefully considered since this change results in a 76% reduction in database storage requirements for 30 days of data.  

## Summary

Use the following guidelines to manage database sizing and performance:  

- Enable logging of Common Published Data only if needed.  

- Remember that the number of times activities run determines the volume of logged data. A small runbook with a few of activities run several times can result in more data logging than a larger runbook run a lower number of times.  

- Don't enable logging of Activity\-specific Published Data in production environments, and should only be used for debugging purposes.  

- Develop an understanding of how much time your runbooks spend running domain code compared to running platform code.  

- Estimate platform code costs using the techniques outlined in this document. Use as a reference in considering where to make improvements in runbook performance.  

- Identify opportunities for improvement by making normalized comparisons of your measurements.  

## See Also

- [Orchestrator Logs](orchestrator-logs.md).
- [Orchestrator Architecture](learn-about-orchestrator.md).
