---
title: Creating a host cluster in VMM from existing Windows servers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa816494-2a57-40bc-8b89-99b054713b26
---
# Creating a host cluster in VMM from existing Windows servers
The topics in this section describe the process for creating a host cluster in Virtual Machine Manager \(VMM\), using existing servers running a Windows Server operating system:

-   [Prerequisites: creating a host cluster in VMM from existing Windows servers](Prerequisites--creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)

This topic also provides information about [VMM actions during cluster creation](Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md#BKMK_workflow) and lists [Example resource names](Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md#BKMK_example). For information about other ways of creating or adding clusters, see the links at the end of this topic.

## <a name="BKMK_workflow"></a>How VMM creates a Hyper\-V host cluster
During the cluster creation process, after you click **Finish** on the cluster creation wizard, VMM does the following:

1.  Validates that all hosts meet the prerequisites, such as required operating system and domain membership

2.  Enables the Failover Clustering feature on each host

3.  Unmasks the selected storage logical units to each host

4.  Runs the cluster validation process

5.  Creates the cluster with quorum settings, configures any cluster static IP settings that you specified, and enables Cluster Shared Volumes \(CSV\)

6.  For each logical unit that is designated as a CSV, assigns the logical unit as a CSV on the cluster

## <a name="BKMK_example"></a>Example resource names
The example names in this section are intended to demonstrate the concepts used when creating a cluster in VMM from existing servers. The following table summarizes the example names that could be used in this scenario. Some of these names are also used in examples in procedures in this section.

> [!NOTE]
> The example resource names and configuration are used to help demonstrate the concepts. You can adapt them to your test environment.

The following table summarizes the example resource names that you can use:

|Resource|Example resource name|
|------------|-------------------------|
|Stand\-alone Hyper\-V hosts|**HyperVHost05** and **HyperVHost06**|
|Domain|**contoso.com**|
|Cluster name|**HyperVClus01.contoso.com**|
|Host group where added|**New York\\Tier0\_NY**|
|Logical network|**MANAGEMENT**|




