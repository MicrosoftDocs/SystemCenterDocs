---
ms.assetid: 
title:  Sample configuration file for collecting Linux log files
description: This article describes a sample configuration file for collecting Linux log files on Linux in System Center Preview 1711 Operations Manager.    
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 11/3/2017
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1711'
ms.technology: operations-manager
ms.topic: article
---

# Sample configuration file for collecting Linux log files
This is a sample configuration file for collecting log files from Linux with System Center Preview 1711 - Operations Manager.

    # Have a source directive for each log file source file.
    <source>

        # Fluentd input tail plugin, will start reading from the tail of the log

        type tail

        # Specify the log file path. This supports wild card character
        path /root/demo/log/demo*.log
        
        # This is recommended – Fluentd will record the position it last read into this file. Change this folder according to your server
        pos_file /home/ user1/fluent-test/demo_simple_match.log.pos
        
        # tag is used to correlate the directives. For example, source with corresponding filter and match directives. 
        tag scom.log
        
        reads the  fields from the log file in the specified format
        format /(?<message>.*)/

    </source>
    
    <source>
        # Fluentd input tail plugin, will start reading from the tail of the log
        type tail

        # Specify the log file path. 
        path /var/log/mongodb/mongod.log

        # tag is used to correlate the directives.
        tag  scom.mongo.log

        #reads the  fields from the log file in the specified format

        format /(?<timestamp>[^ ]*) (?<severity>[A-Z]) (?<component>(-|([^ ]*)))\s* \[(?<context>[^\]]*)\] ((?<query>.*) (?<querytime_ms>[\d\.]+(?=ms))|(?<message>.*))/
        </source>

    <source>
        # Fluentd input tail plugin, will start reading from the tail of the log
        type tail
    
        # Specify the log file path. This supports wild card character
        path /var/log/syslog
    
        # This is recommended – Fluentd will record the position it last read into this file
        pos_file /home/user1/fluent-test/demo_syslog.log.pos
    
        # tag is used to correlate the directives. For example, source with corresponding filter and match directives. 
        tag scom.log.syslog
        
        format /(?<message>.*)/
    
    </source>
    
    <source>
                    
        type tail

                        # Log file that needs to be monitored
        path /var/log/mongodb/mongod.log

                        # tag to correlate with filter and match directives
        tag  scom.log.mongo

        # reads the following fields from the log file
        format /(?<timestamp>[^ ]*) (?<severity>[A-Z]) (?<component>(-|([^ ]*)))\s* \[(?<context>[^\]]*)\] ((?<query>.*) (?<querytime_ms>[\d\.]+(?=ms))|(?<message>.*))/
        
        #type of the parsed field
        types querytime_ms:float

    </source>
    
    <filter scom.log>

        # new scom fluentd plugin for simple match - Input – Pattern A;  Action: log record = A à Send Event

        type filter_scom_simple_match

        # Input Pattern to look for. In this case looking for Invalid guest user
        regexp1 message Invalid user guest 

        # Event to be generated and sent to SCOM OMED service.
        event_id1 6201

        # Event description to be sent to SCOM
        event_desc Failed login attempt. Invalid User guest attempted to log in
    
    </filter>
    
    <filter scom.mongo.log>

        # Standard published Fluentd grep filter plugin,
        type grep

        # Filters the log record with the match pattern specified here
        regexp1 message AuthenticationFailed
        </filter>

        <filter scom.mongo.log>
        # new scom converter fluentd plugin. This plugin converts data from generic fluentd filter plugins to format acceptable by SCOM
        type filter_scom_converter

        # Event to be generated and sent to SCOM OMED service.
        event_id 6207

        # Event description to be sent to SCOM

        event_desc MongoDB Authentication Failed
        
    </filter>

    <filter scom.log.syslog>

        # SCOM filter plugin for exclusive match - 2 Inputs – Pattern A and B; Action: (log record = A & log record != B) then Send Event.
        type filter_scom_excl_match
        
        # Example where user monitors if insertion of a record in MongoDB succeeds.
        regexp1 message Insertion of [a-z0-9]*
        regexp2 message succeeded

        event_id 6206
        event_desc Failed to insert a record in MongoDB
        </filter>
        
        <filter scom.log.syslog>
                        # SCOM filter plugin for correlated match - 3 Inputs – Pattern A, B and Timer T; Action: (log record = A; within T if log record = B)  then 
                        send Event.
        type filter_scom_cor_match

        # User verifies if a particular package installation fails
        regexp1 message Starting install of package [A-Za-z0-9]*
        regexp2 message Install failed for package [A-Za-z0-9]*

        event_id 6210
        event_desc Package installation failed
    </filter>
    
    <filter scom.log.mongo>
                    
        # SCOM filter plugin for Repeated correlation - 3 Inputs – Pattern A, Timer T and Count N; Action: (within T if log record = A, N number 
        of times) then send an Event
        type filter_scom_repeated_cor

        # If a user tries to log into MongoDB using incorrect credentials and authentication fails for 5 times, an event is generated.
        regexp1 message AuthenticationFailed:
        num_occurences 5
        time_interval 5

        event_id 6206
        event_desc User Authentication failed 5 times. User had tried to authenticate with incorrect credentials.
        
    </filter>
    
    <filter scom.log.mongo>
                    
        # SCOM filter plugin for Exclusive correlation - 3 Inputs – Pattern A, B and Timer T; Action: (log record = A, within T if log record != B)   
        then send an Event.

        type filter_scom_excl_correlation
        
        # If Mongo DB fails to restart, an event would be sent. 
        regexp1 message dbexit:
        regexp2 message waiting for connections
        time_interval 5

        
        event_id 6210
        event_desc MongoDB restart failure
    </filter>
    
    
    <match scom.log.** scom.event>

        # output plugin to use – this is a dedicated output plugin for SCOM
        type out_scom

        log_level trace
        num_threads 5

        # size of the buffer chunk. If the top chunk exceeds this limit or the time limit flush_interval, a new empty chunk is pushed to the top of the queue and bottom chunk is written out.
        buffer_chunk_limit 5m
        flush_interval 15s

        # specifies the buffer plugin to use. Here buffer type used it “file”
        buffer_type file

        # specifies the file path for buffer. Make sure fluentd has write access to the directory.
        buffer_path /var/opt/microsoft/omsagent/scom/state/out_scom_common*.buffer

        # If queue length exceeds the specified limit, events are rejected.
        buffer_queue_limit 10
        
        # Control the buffer behavior when the queue becomes full – 3 modes supported – exception, block, drop oldest chunk
        buffer_queue_full_action drop_oldest_chunk
        

        retry_limit 10
        # If the bottom chunk fails to be written out, it will remain in the queue and Fluentd will retry after waiting retry_wait seconds
        retry_wait 30s

        # The retry wait time doubles each time until max_retry_wait.
        max_retry_wait 9m

    </match>
