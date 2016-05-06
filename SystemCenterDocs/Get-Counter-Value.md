---
title: Get Counter Value
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe935ce1-871b-451b-8ce7-e2d3084463d6
---
# Get Counter Value
The Get Counter Value activity retrieves the value of a counter and returns it as a published data item. Wherever you need to use the value of a counter, use the published data that is published by the Get Counter Value to retrieve that value.

## Configuring the Get Counter Value Activity
Before you configure the Get Counter Value activity, you need to determine which counter you will retrieve.

> [!WARNING]
> Before you can use this activity, you must configure a Counter. To modify a counter, use the [Modify Counter](./Modify-Counter.md) activity

Use the following information to configure the Get Counter Value activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|Counter|Click the ellipsis **\(...\)** button to select the **Counter** that you are retrieving.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Counter Value|The value of the counter.|


