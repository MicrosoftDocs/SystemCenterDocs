---
ms.assetid: 
title:  Log file monitoring in System Center Preview 1711 - Operations Manager
description: This article provides an overview of the Linux log file monitoring in System Center Preview 1711 Operations Manager.    
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/6/2017
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1711'
ms.technology: operations-manager
ms.topic: article
---

# Linux Log file monitoring in System Center Preview 1711 - Operations Manager
System Center Preview 1711 - Operations Manager now has enhanced log file monitoring capabilities for Linux servers by using the newest version of the agent that uses Fluentd. This update provides the following improvements over previous log file monitoring:

- Wild card characters in log file name and path.
- New match patterns for customizable log search like simple match, exclusive match, correlated match, repeated correlation and exclusive correlation.
- Support for generic Fluentd plugins published by the fluentd community.


## Basic operation
The basic operation of log file monitoring in Linux includes the following steps:

1. Record is written to a log on a Linux agent.
2. Fluentd collects the record and creates an event on pattern match.
3. Event is sent to OMED service on management server.
3. Rules and monitors in a custom management pack collect events and create alerts in Operations Manager.


## Overview of configuration
The following steps are required to enable log file monitoring on Linux agents.  Each of these steps is described in detail in the following sections.

1. Import the latest Linux management pack.
2. Install the latest version of the Linux agent on each Linux computer to be monitored.
2. Create Fluentd configuration file to collect logs.
3. Copy configuration file to Linux agents.
3. Create rules and monitors using the management pack to collect events from the log and create alerts.


## Install the latest version of the Linux agent
The latest version of the Linux agent supports Fluentd which is required for enhanced log file monitoring.  You can get details and the installation process for the new agent at [Install agent on UNIX and Linux from command line](deploy-linux-agent-install.md).

## Configure Linux Log File monitoring
The Linux Management pack bundle has the latest Operations Manager agent (with Fluentd). To configure Linux log file monitoring, users should perform the following:

1. Import the latest Linux Management pack using the standard process for installing a management pack.
2. Install the new Linux agent on the Linux servers, this can be done through discovery wizard or manually.
3. Enable the OMED service on each management server in the resource pool managing the Linux agents. 

The OMED service collects events from Fluentd and converts them to Operations Manager events. Users should import a custom management pack which can generate alerts based on the events received from the Linux servers.

You enable the OMED service using the following process.

1. From the Operations Console, go to **Monitoring** > **Operations Manager** > **Management Server** > **Management Servers State**.
2. Select the management server in the **Management Servers** state pane.
3. In the **Tasks** pane, select **Health Service Tasks** > **Enable System Center OMED Server**.

## Create FluentD configuration file
You configure Fluentd operation with a configuration file.  For log monitoring, you need to create a configuration file that includes such information as source log file name and path and filters to define which data to collect.

The master Fluentd configuration file **omsagent.conf** is located in **/etc/opt/microsoft/omsagent/scom/conf/**. You can add log file monitoring configuration directly to this file, but you should create a separate configuration file to better manage the different settings.  You then use an @include directive in the master file to include your custom file.

For example, if you created **logmonitoring.conf** in  **/etc/opt/microsoft/omsagent/scom/conf/omsagent.d**, you would add one of the following lines to **fluent.conf**:

    #Include all configuration files
    @include omsagent.d/*.conf

or

    #include single configuration file
    @include omsagent.d/logmonitoring.conf


You can get details on Fluentd configuration files at [Fluentd Configuration file syntax](https://docs.fluentd.org/v0.12/articles/config-file).  The following sections describe settings in different directives of the configuration file unique to log file monitoring.  Each includes sample settings that you can paste into a configuration file and modify for your requirements.

A complete sample configuration file for log monitoring is available at [Sample configuration file for lo monitoring].


#### Source
The **Source** directive defines the source of the data you're collecting.  This is where you define the details of your log file. Fluentd picks up each record written to the source and submits an event for it into Fluentd's routing engine.  You need to specify a tag here in this directive. The tag is a string that is used as the directions for Fluentd’s internal routing engine to correlate different directives.

This example shows syslog records collected and tagged for processing by Operations Manager.

    <source>

        # Specifies input plugin. Tail is a fluentd input plugin - http://docs.fluentd.org/v0.12/articles/in_tail
        type tail

        # Specify the log file path. Supports wild cards.
        path /var/log/syslog

        # Recommended so that Fluentd will record the position it last read into this file.
        pos_file /home/user1/fluent-test/demo_syslog.log.pos

        # Used to correlate the directives. 
        tag scom.log.syslog

        format /(?<message>.*)/

    </source>

#### Match
The **match** directive defines how to process events collected from the source with matching tags.  Only events with a **tag** matching the pattern will be sent to the output destination.  When multiple patterns are listed inside one **match** tag, events can match any of the listed patterns.  The **type** parameter that specifies which plugin to use for these events.  

This example processes events with tags matching **scom.log.**** and  **scom.alert** (** matches zero or more tag parts). It specifies the **out_scom** plugin which allows the events to be collected by the Operations Manager management pack.

    <match scom.log.** scom.event>

        # Output plugin to use
        type out_scom

        log_level trace
        num_threads 5

        # Size of the buffer chunk. If the top chunk exceeds this limit or the time limit flush_interval, a new empty chunk is pushed to the top of the  
        queue and bottom chunk is written out.
        buffer_chunk_limit 5m
        flush_interval 15s

        # Specifies the buffer plugin to use.
        buffer_type file

        # Specifies the file path for buffer. Fluentd must have write access to this directory.
        buffer_path /var/opt/microsoft/omsagent/scom/state/out_scom_common*.buffer

        # If queue length exceeds the specified limit, events are rejected.
        buffer_queue_limit 10
        
        # Control the buffer behavior when the queue becomes full: exception, block, drop_oldest_chunk
        buffer_queue_full_action drop_oldest_chunk
        
        # Number of times Fluentd will attempt to write the chunk if it fails.
        retry_limit 10

        # If the bottom chunk fails to be written out, it will remain in the queue and Fluentd will retry after waiting retry_wait seconds
        retry_wait 30s

        # The retry wait time doubles each time until max_retry_wait.
        max_retry_wait 9m

    </match>


### Filter
The **filter** directive has same syntax as **match** but allows for more complex filtering of which data to process. Collected events must match the criteria of all filters to be added to the output.

There are six filter plugins for log file monitoring described here.  Use one or more of these filters to define the events that you want to collect from your log file.  

#### Simple match: filter_scom_simple_match

Takes up to 20 input patterns.  Sends an event to Operations Manager whenever any pattern is matched. 

    <filter tag>
        type filter_scom_simple_match
        regexp1 <key> <pattern>
        event_id1 <event ID>
        regexp2 <key> <pattern>
        event_id2 <event ID>
        .
        .
        .
        regexp20 <key> <pattern>
        event_id20 <event ID>
    </filter>


#### Exclusive match: filter_scom_excl_match
Takes two input patterns. Sends an event to Operations Manager when a single record matches pattern 1 but does not match pattern 2.

    <filter tag>
        type filter_scom_excl_match
        regexp1 <key> <pattern1>
        regexp2 <key> <pattern2>
        event_id <event ID>
    </filter>

#### Repeated correlation: filter_scom_repeated_cor
Takes three inputs: a patterns, a time interval, and a number of occurrences. When a match is found for the first pattern, a timer starts.  An event is sent to Operations Manager if the pattern is matched the specified number of times before the timer ends.

    <filter tag>
        type filter_scom_repeated_cor
        regexp <key> <pattern>
        event_id <event ID>
        time_interval <interval in seconds>
        num_occurences <number of occurrences>
    </filter>


#### Correlated match: filter_scom_cor_match
Takes three inputs: two patterns and a time interval. When a match is found for the first pattern, a timer starts.  An event is sent to Operations Manager if there is a match for the second pattern before the timer ends.

    <filter tag>
        type filter_scom_cor_match
        regexp1 <key> <pattern1>
        regexp2 <key> <pattern2>
        event_id <event ID>
        time_interval <interval in seconds>
    </filter>


#### Exclusive correlation: filter_scom_excl_correlation
Takes three inputs: two patterns and a time interval. When a match is found for the first pattern, a timer starts.  An event is sent to Operations Manager if there is no match for the second pattern before the timer ends.

    <filter tag>
        type filter_scom_excl_correlation
        regexp1 <key> <pattern1>
        regexp2 <key> <pattern2>
        event_id <event ID>
        time_interval <interval in seconds>
    </filter>

#### Operations Manager converter: filter_scom_converter
Sends an event to Operations Manager for all records it receives. Sends the specified event id and description as part of the event. 

    <filter tag>
        type filter_scom_converter
        event_id <event ID>
        event_desc <event description>
    </filter>


## Copy configuration file to agent
The fluentd configuration file must be copied to **/etc/opt/microsoft/omsagent/scom/conf/omsagent.d** on all Linux computers you want to monitor. You must also add an @include directive in the master configuration file as described above.


## Create rules and monitors
The Linux MP does not provide modules to collect events from FluentD. The Linux MP is bundled with the Linux agent. It is the fluentd module in the Linux agent and the OMED service on the management and gateway server that provides the capabilities for enhanced log file monitoring.

You need to create your own management pack with custom rules and monitors that use the module **Microsoft.Linux.OMED.EventDataSource** which collects the events from Fluentd.  

The following table lists the parameters of **Microsoft.Linux.OMED.EventDataSource**.

| Parameter | Type | Description |
|:---|:---|:---|
| ComputerName | String | Required. Specifies the name of the Linux computer for which events to be read. The ComputerName parameter is most commonly passed to the module by using the $Target notation, although it can be specified as any string. This module attempts to read events generated by the given Linux computer. |
| ManagedEntityId | String | Required. Specifies the managed entity ID of monitored entity. The ManagedEntityId parameter is most commonly passed to module by using $Target\Id$.  |
| EventNumber | Integer | Optional. Indicates the event number of the event to retrieve. If this option is omitted, the module returns all events generated for that computer and managed entity. |


