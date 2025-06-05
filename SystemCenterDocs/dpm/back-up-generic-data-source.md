---
description: You can back up a generic data source with DPM.
ms.topic: article
ms.service: system-center
keywords:
ms.date: 11/01/2024
title: Prepare to back up a generic data source
ms.subservice: data-protection-manager
ms.assetid: 8ad00a50-108a-4212-ad43-c12a8f8f5587
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency3, engagement-fy24
---

# Prepare to back up a generic data source

System Center Data Protection Manager (DPM) provides the Generic Data Source (GDS) infrastructure  so that you can protect any Microsoft workload as long as it has a VSS writer.

Here's what you can do:

- Complete backup using Express full backup

- Recovery to the original location

- Back up referential data sources

- Back up data source with shared disk clusters

- Back up in multiple domains

- Back up to tape

## <a name="GenericDataSource"></a>Registering a new data source

You'll need to run the Modify-RegisteredWriters command to add, remove, or modify the VSS writer ID for a data source to the list that's registered with DPM.

**Syntax**

Modify-RegisteredWriters.ps1 [[-DpmServerName] \<String\>] [-List] [\<CommonParameters\>]

Modify-RegisteredWriters.ps1 [[-DpmServerName] \<String\>] [-Remove] [-Writers] \<String\> [\<CommonParameters\>]

Modify-RegisteredWriters.ps1 [[-DpmServerName] \<String\>] [-Add] [-Writers] \<String\> [\<CommonParameters\>]

|Parameter|Type|Description|
|-------------|--------|---------------|
|DPMServerNAme|String|Specifies the DPM server against which this command should run. By default, the command is run against the local DPM server.|
|List|SwitchParameter|Indicates that the command should display the list of registered writer IDs.|
|Add|SwitchParameter|Indicates that the command should add the list of writer IDs to the list of the writer IDs that's registered with DPM.|
|Remove|SwitchParameter|Indicates that the given list of writer IDs must be removed from the list of the writer IDs that's registered with DPM.|
|Writers|String|Comma-separated list of writer IDs.|

## Example 1

The Modify-RegisteredWriters command displays the list of writers that are currently registered with the local DPM server.

`Modify-RegisteredWriters -List`

## Example 2

The Modify-RegisteredWriters command adds the two new writer IDs to the list of registered writers on the local DPM server.

`Modify-RegisteredWriters -Add -Writers "46eef637-28ca-4223-8bb6-2e87bd945179,e1cdedc6-d9d2-4fc3-8af6-5d0d0fe3e8af"`

## Example 3

The Modify-RegisteredWriters command removes the specified writer ID from the list of registered writers on DPM server dpm1.contoso.com.

`Modify-RegisteredWriters -DpmServerName dpm1.contoso.com -Remove -Writers 46eef637-28ca-4223-8bb6-2e87bd945179`
