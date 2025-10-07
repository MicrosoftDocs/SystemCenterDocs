---
title: Run iLO Command
description: The Run iLO Command activity is used in a runbook to run a command that can be used to perform management activities such as Create User, Get Power State, and Set Configuration.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 21614e77-3027-49a7-8545-27349b71d392
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Run iLO Command

The **Run iLO Command** activity is used in a runbook to run a command that can be used to perform management activities, such as **Create User**, **Get Power State**, and **Set Configuration**.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Run iLO Command required properties

| **Element**   | **Description**   | **Valid Values**   | **Lookup** |
|:---|:---|:---|:---|
| The iLO command to run | The iLO command to run   | Create user<br>Delete user<br>Get user (iLO v2)<br>Get user (iLO v3)<br>Modify user (iLO v2)<br>Modify user (iLO v3)<br>System reset<br>Hard system reset<br>Soft system reset<br>Start system<br>Stop system<br>Get power state<br>Get configuration<br>Set configuration<br>Set virtual floppy<br>Set virtual CDROM<br>Update firmware (iLO v2) | Yes   |
| Fields   | Required fields for the selected command. | String   | No   |

## Run iLO Command optional properties

| **Element** | **Description**   | **Valid Values** | **Lookup** |
|:---|:---|:---|:---|
| Fields   | Optional fields can be added to the Fields list by clicking Select fields. | String   | No   |

## Run iLO Command published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Command   | Selected command   | String   |
| Command line   | Command line for command   | String   |
| Connection name | Named connection   | String   |
| Command status  | Status of command   | String   |
| Error output   | Command error output   | String   |
| Exit code   | Exit code of command   | String   |
| Private Key   | SSH private key   | String   |
| SSH Address   | IP address or network name | String   |
| SSH user   | SSH username   | String   |
| Standard output | Standard output of command | String   |

>[!WARNING]
>The Run iLO Command activity in runbooks imported from Opalis 6.3 when opened for editing in the Runbook Designer will display an error dialog with no message. To remove this error, close the error message by selecting **OK**. Record your command and field values for re-entry. Then reselect the command and re-enter the field values. When importing runbooks that contain **Get user** or **Modify user** activities from Opalis 6.3, selecting the activities **Get user**, or **Modify user** will display a message " Command not found". The commands should be updated to the specific version activity, that is, **Get user (iLO v2)** or **Get user (iLO v3)** manually.

## Other activities

The Integration Pack for HP iLO and OA contains the following additional activity:

- [Run OA Command](run-oa-command.md)
