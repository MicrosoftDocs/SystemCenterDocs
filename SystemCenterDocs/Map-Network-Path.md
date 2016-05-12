---
title: Map Network Path
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8954602d-8f80-4a5d-8e69-fd8148122ac6
---
# Map Network Path
The Map Network Path activity enables you to map a network path using a UNC path.

## Configuring the Map Network Path Activity
Before you configure the Map Network Path activity, you need to determine the following:

-   The UNC path you want to map.

-   The user account and password you need to log into that path; if required.

Use the following information to configure the Map Network Path activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Network path**|Type the network path that you want to connect to in UNC format \(\\\\servername\\foldername\), or click the ellipsis button **\(...\)** and browse for it.<br /><br />Verify that the network path that you want to map does not already exist.|
|**User account**|Type the user account that you need to access the network path.|
|**Password**|Type the password that you need to access the network path.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Network path|The network path that you are mapping.|
|User account|The user account that you used to access the network path.|


