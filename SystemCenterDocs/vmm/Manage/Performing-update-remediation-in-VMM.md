---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Performing update remediation in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  11d8b9d6-54ce-4bd1-8e27-73a5ae228321
---

# Performing update remediation in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

The procedures in this section describe the operation of bringing a managed computer into compliance with an update baseline, also known as *update remediation*. In Virtual Machine Manager (VMM), you can choose to remediate all update baselines that are assigned to a computer, all noncompliant updates in a single update baseline, or a single update.

**Account requirements** To perform update remediation, you must be an administrator or a delegated administrator in VMM. Delegated administrators can only remediate updates for computers that are within the scope of their user role.

## Prerequisites
Before you can perform these procedures, you must have set up update management in VMM. For more information, see [Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md).

## In this section
Follow these procedures to perform updates on stand-alone Hyper-V hosts, host clusters, or infrastructure servers.

|Procedure|Description|
|-------------|---------------|
|[How to remediate updates on a stand-alone Hyper-V host in VMM](How-to-remediate-updates-on-a-stand-alone-Hyper-V-host-in-VMM.md)|Describes how to install updates on noncompliant Hyper-V hosts.|
|[How to perform rolling updates on a Hyper-V host cluster in VMM](How-to-perform-rolling-updates-on-a-Hyper-V-host-cluster-in-VMM.md)|Describes how to perform rolling update remediation on a Hyper-V host cluster.|
|[How to remediate updates on infrastructure servers in VMM](How-to-remediate-updates-on-infrastructure-servers-in-VMM.md)|Describes how to install updates on infrastructure servers in VMM.|

## See Also
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



