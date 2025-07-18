---
title: Common Activity Properties
description: This article describes the common activity properties including the run behavior, published data behavior, event notifications and security credentials.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 1f3f12bf-e2c2-405c-9205-8d6de6d199d2
author: jyothisuri
ms.author: jsuri
ms.update-cycle: 1095-days
ms.date: 03/31/2025
---
# Common Activity Properties



All activities have properties. The Properties dialog box for each activity has multiple tabs that provide access to the settings for the activity. The particular set of tabs varies between activities, but there are several common property types.  

This article describes the common activity properties including the run behavior, published data behavior, event notifications and security credentials.

## Details

This tab contains various properties specific to an activity. Many activities require you to at least enter a computer name, IP address, file name, file path, or file folder location.  

## Run Behavior

This tab contains the properties that determine how the activity handles multi\-value Published Data. It also defines the notifications created if the activity fails or runs for an excessive period.  

### Published Data Behavior

By default, Published Data is passed as multiple individual outputs. You can alternatively specify that all values be flattened into a single comma\-delimited value \(.csv\) file.  

When you enable the Flatten feature, you also choose a multi\-value formatting option.  

> [!NOTE]  
> The Flatten feature does not flatten data across multiple instances of the same activity. It only flattens multiple values returned from a single instance of the activity.  

|Flatten behavior|Description|  
|--------------------|---------------|  
|Separate with line breaks|Each item is on a separate line. This is the format for the output text files.|  
|Separate with|Each item is separated by one or more characters, for example, a semicolon \(;\).|  
|Use CSV format|All items are in comma\-separated value format \(.csv file\), which is useful for importing into spreadsheets or databases.|  

### Event Notifications

Some activities are expected to take a limited amount of time to finish. If the activity does not finish within the specified period, the activity can be stalled or another issue prevents the activity from finishing. You can define the number of seconds to wait for completion of the activity, after which a platform event is sent to report the delay in completion. You can also choose whether to generate a platform event if the activity returns a failure. For more information about event notifications, see [Orchestrator Logs](~/orchestrator/orchestrator-logs.md).  

|Event notification setting|Description|  
|------------------------------|---------------|  
|Report when the activity runs for more than|Enter the number of seconds of run time to elapse before generating a notification.|  
|Report if the activity fails to run|Select this option to generate a run failure notification.|  

## Security Credentials

The settings on the Security Credentials tab let you specify the account that runs the Runbook Server Service. This is useful when the activity performs activities with resources on a remote computer.  

> [!IMPORTANT]  
> Note that the account used to start the runbook must have permission on the local computer to run successfully.  

> [!IMPORTANT]  
> If you use the Invoke Runbook activity and you modify Security Credentials, the account you use must be a member of the Orchestrator System group to run successfully.  

> [!CAUTION]  
> If permissions on the Orchestrator installation path are changed and the activity's Security Credentials has a custom user account that does not include **Read/Execute** permissions to **ExecutionData.dll** on the runbook server, the activity will fail.  

|Option|Behavior|  
|----------|------------|  
|Use the security of the account assigned to the service|Select this option to run the activity with the account used by the runbook server. For more information, see [Orchestrator Security Planning](/previous-versions/system-center/system-center-2012-R2/hh420367(v=sc.12)).|  
|This account|Select this option to run this activity with another account. Specify the account user name and password to run this activity. Verify that the account has the credentials to perform this action. If the credentials you provided fail validation, the account assigned to the runbook server account is used.|  

## Related content

[Orchestrator Security Planning](/previous-versions/system-center/system-center-2012-R2/hh420367(v=sc.12)).
