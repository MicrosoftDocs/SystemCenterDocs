---
title: Run DPM PowerShell Script
description: The Run DPM PowerShell Script activity is used in a runbook to provide a flexible way to address more complex scenarios you may have in working with System Center 2016 - Data Protection Manager (DPM).
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e9930789-a527-40c8-8f5f-e67fb5ef5dde
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Run DPM PowerShell Script

Applies To: System Center 2016 - Orchestrator

The Run DPM PowerShell Script activity is used in a runbook to provide a flexible way to address more complex scenarios you may have in working with System Center 2016 - Data Protection Manager (DPM).

This activity allows you to run PowerShell scripts utilizing the pre-configured connection settings for the DPM Integration Pack, instead of having to use the Run .NET Script activity and manually specifying connection credentials and using PowerShell remoting commands yourself. This activity also provides better performance than using the Run .NET Script activity because it re-uses any open connections to the DPM server rather than opening new connections to run commands.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

>[!IMPORTANT]
>When you use the non-FQDN name of a computer in a DPM command, such as the **DPMServername** parameter for the **Get ProductionServer** command, DPM is not able to locate the computer and an error shows that it used the FQDN. To prevent this error, specify the actual FQDN of the target computer.

## Run DPM PowerShell Script Required Properties

| Element   | Sample value   |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PowerShell Script  | The PowerShell command(s) or script to be run on the DPM server   |
| Output Variable 01 | Use a variable name defined in your script that you want to return as Published Data. You can use either the PowerShell notation $var1 or the variable name var1. The value of an element must be a simple type value and not an object or collection of objects. You cannot specify an object property, such as $var1.propertyname, as an output element. The name in the output element must be the name of an actual PowerShell variable. If the PowerShell variable contains a complex type or a collection of objects, the data returned is similar to System.Object or System.Object\[\] because the contents of the outpupt variable cannot be represented as a string. |

## Run DPM PowerShell Script Optional Properties

| Element   | Sample value   |
|-----------------------------------------|-----------------------------------|
| Output Variable 02 - Output Variable 20 | Same as Output Variable 01 above. |

## Run DPM PowerShell Script Published Data

| Element   | Sample value   |
|--------------|---------------------------------------------------------------------------------------------------------|
| Error output | If any errors occur while running the script, the text of the error(s) are saved in this property value |
