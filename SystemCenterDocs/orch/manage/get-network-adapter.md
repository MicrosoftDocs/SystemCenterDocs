---
title: Get Network Adapter
description: The Get Network Adapter activity is used to retrieve an existing Virtual Network Adapter based on the filters you specify.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 114d69dd-6ae6-488a-bb61-483df029728a
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get Network Adapter

Applies To: System Center 2016 - Orchestrator

The Get Network Adapter activity is used to retrieve an existing Virtual Network Adapter based on the filters you specify.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Network Adapter Filters

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the Virtual Network Adapter was added, in the yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Enabled   | True or False   |   |
| Ethernet Address   | The Virtual Network Adapter address, in the format 00:00:00:00:00:00   |   |
| Ethernet Address Type   | Dynamic or Static   |   |
| MAC Addresses Spoofing Enabled | True or False   |   |
| Modified Time   | The most recent date and time that the Virtual Network Adapter was modified, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Network Location   | The Virtual Network Location, for example, contoso.com   |   |
| Network Tag   | An alphanumeric value to differentiate the host's virtual networks, based on a criterion such as throughput or security. Network tags can be used to match virtual machines with suitable hosts. |   |
| Physical Address   | The Virtual Network Adapter physical address, in the format 00:00:00:00:00:00   |   |
| Physical Address Type   | Dynamic or Static   |   |
| Virtual Network Adapter ID   | The unique identifier (GUID) of the Virtual Network Adapter   |   |
| Virtual Network Adapter Name   | The name of the Network Adapter, which is auto-generated.   |   |
| Virtual Network Adapter Type   | Emulated or Synthetic   |   |
| Virtual Network Name   | The name of the Virtual Network specified at the host level of the Virtual Machine Manager configuration   |   |
| VLAN Enabled   | True or False   |   |
| VLAN ID   | The unique identifier (GUID) of the VLAN, if enabled   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine for which the network adapter is being created.   |   |
| VMW Adapter Index   | The index number of the Virtual Network Adapter   |   |

## Get Network Adapter Published Data

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the Virtual Network Adapter was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Enabled   | True or False   |   |
| Ethernet Address   | The Virtual Network Adapter address, in the format 00:00:00:00:00:00   |   |
| Ethernet Address Type   | Dynamic or Static   |   |
| MAC Addresses Spoofing Enabled | True or False   |   |
| Modified Time   | The most recent date and time that the Virtual Network Adapter was modified, in the yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Network Location   | The Virtual Network Location, for example, contoso.com   |   |
| Network Tag   | An alphanumeric value to differentiate the host's virtual networks, based on a criterion such as throughput or security. Network tags can be used to match virtual machines with suitable hosts. |   |
| Physical Address   | The Virtual Network Adapter physical address, in the format 00:00:00:00:00:00   |   |
| Physical Address Type   | Dynamic or Static   |   |
| Virtual Network Adapter ID   | The unique identifier (GUID) of the Virtual Network Adapter   |   |
| Virtual Network Adapter Name   | The name of the Network Adapter, which is auto-generated.   |   |
| Virtual Network Adapter Type   | Emulated or Synthetic   |   |
| Virtual Network Name   | The name of the Virtual Network specified at the host level of the Virtual Machine Manager configuration   |   |
| VLAN Enabled   | True or False   |   |
| VLAN ID   | The unique identifier (GUID) of the VLAN, if enabled   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine for which the network adapter is being created.   |   |
| VMW Adapter Index   | The index number of the Virtual Network Adapter   |   |
