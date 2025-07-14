---
title: Get Network Adapter
description: The Get Network Adapter activity is used to retrieve an existing Virtual Network Adapter based on the filters you specify.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 114d69dd-6ae6-488a-bb61-483df029728a
author: jyothisuri
ms.author: jsuri
---

# Get Network Adapter

The Get Network Adapter activity is used to retrieve an existing Virtual Network Adapter based on the filters you specify.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Network Adapter Filters

| Element   | Description   |
|:---|:---|
| Accessibility   | Public or Internal   |
| Added Time   | The date and time that the Virtual Network Adapter was added, in the yyyy-mm-dd hh:mm:ss AM or PM   |
| Enabled   | True or False   |
| Ethernet Address   | The Virtual Network Adapter address, in the format 00:00:00:00:00:00   |
| Ethernet Address Type   | Dynamic or Static   |
| ID  | The unique identifier (GUID) of the virtual machine for which the network adapter is being created.   |
| MAC Addresses Spoofing Enabled | True or False   |
| Modified Time   | The most recent date and time that the Virtual Network Adapter was modified, in the format yyyy-mm-dd hh:mm:ss AM or PM   |
|  Name | Name of the Network Adapter |
| Port Classification   | Name of the Port Classification   |
| Virtual Network  | Name of the virtual network specified at the host level of the Virtual Machine Manager configuration.   |
| Virtual Network Adapter Type   | Emulated or Synthetic   |
| VLAN Enabled   | True or False   |
| VLAN ID   |   The unique identifier (GUID) of the VLAN, if enabled. |
| VM Network |  Name of the VM network  |

## Get Network Adapter Published Data

| Element   | Description   |
|:---|:---|
| Accessibility   | Public or Internal   |
| Added Time   | The date and time that the Virtual Network Adapter was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |
| Enabled   | True or False   |
| Ethernet Address   | The Virtual Network Adapter address, in the format 00:00:00:00:00:00   |
| Ethernet Address Type   | Dynamic or Static   |
| MAC Addresses Spoofing Enabled | True or False   |
| Modified Time   | The most recent date and time that the Virtual Network Adapter was modified, in the yyyy-mm-dd hh:mm:ss AM or PM   |
| Port Classification   | Name of the Port Classification   |
| VLAN Enabled   | True or False   |
| VLAN ID   | The unique identifier (GUID) of the VLAN, if enabled   |
| VM Network |  Name of the VM network  |
| Virtual Network Adapter ID   | The unique identifier (GUID) of the Virtual Network Adapter   |
| Virtual Network Adapter Name   | The name of the Network Adapter, which is auto-generated.   |
| Virtual Network Adapter Type   | Emulated or Synthetic   |
| Virtual Network Name   | The name of the Virtual Network specified at the host level of the Virtual Machine Manager configuration   |
