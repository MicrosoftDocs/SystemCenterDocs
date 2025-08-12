---
title: Stop Maintenance Mode
description: The Stop Maintenance Mode activity takes a monitor out of maintenance mode.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 2358a3dd-2f24-46f6-b7b9-4a5d0952b887
author: jyothisuri
ms.author: jsuri
---
# Stop Maintenance Mode

The Stop Maintenance Mode activity takes a monitor out of maintenance mode. If you put a monitor into maintenance mode using the Start Maintenance Mode Activity, you can use the Stop Maintenance Mode activity to put that monitor back in service before the configured duration has elapsed.

If you choose to take a computer (Microsoft.Windows.Computer or Microsoft.Unix.Computer) out of maintenance mode, then all child monitors for that computer will also be taken out of maintenance mode.

The following tables list the properties and published data for this activity. The activity publishes all the data from the required and optional properties into published data.

## Stop Maintenance Mode Required Properties

| Element   | Description   | Valid Values | Lookup |
|:---|:---|:---|:---|
| Connection | The Operations Manager connection that this activity will use   | String   | Yes   |
| Monitor   | The name of the monitor that is being taken out of maintenance mode | String   | Yes   |

## Stop Maintenance Mode Published Data

| Element   | Description   |
|------------|--------------------------------------------------------------------------|
| Connection | The connection string to the Operations Manager server for this activity |
| Domain   | The domain that the alert came from   |
| FullName   | The full name of the Operations Manager monitoring object   |
| Server   | The name of the Operations Manager server   |
| StopTime   | The stop time of maintenance mode   |
| Username   | The user name that was used to access the Operations Manager server   |
