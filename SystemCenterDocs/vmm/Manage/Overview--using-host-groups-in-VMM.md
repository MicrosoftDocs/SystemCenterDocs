---
title: Overview: using host groups in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b564083-652d-4ab4-ac20-62f7abc967c7
---
# Overview: using host groups in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager



In VMM you add and manage virtualization hosts in the VMM fabric. A VMM host group is a logical entity in the VMM fabric that groups virtualization hosts together.

 After you've created host groups you assign and configure resources at the host group level that apply to all virtualization hosts in the group. You can override host group settings for a specific server in the group. You can create host groups based on different criteria. For example based on physical location, hardware capabilities, or specific workloads.
 

When you create private clouds in VMM,  you select which host groups will be included in the cloud, and then allocate resources to those groups in the cloud. 

You can assign host groups to the Delegated Administrator and the Read-Only Administrator user roles, to scope the user roles to specific host groups. Members of these user roles can view and manage the fabric resources that are assigned to them at the host group level.



