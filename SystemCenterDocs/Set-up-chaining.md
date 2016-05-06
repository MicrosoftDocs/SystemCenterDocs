---
title: Set up chaining
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1f3d538-ac37-4985-beeb-90ecf0dfe213
---
# Set up chaining
You can create a chain of primary and secondary [!INCLUDE[dpm2012long](Token/dpm2012long_md.md)] servers, so that each preceding link in the chain \(acting as a primary server\) is protected by the one that follows it \(its secondary server\). Protection includes the databases in the instance of SQL Server used on theprimary server, all local volumes and application data on the primary, and all replicas on the primary server that the primary directly protects.

Set up chaining as follows:

1.  Install the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] protection agent on the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server that you want to protect from the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server you want to protect it from.

2.  Configure secondary protection for the data sources protected by the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server you are protecting. Note in the DPM console you won’t be able to configure protection for data sources that are already protected by the agent. This prevents you from repeatedly protecting data.

As an example, let’s assume an architecture for two [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] servers, DPM1 and DPM2. Each of these servers protects one or more data sources of their own. To set up chaining for these two servers you’d do the following:

1.  Install the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] protection agent from DPM1 to DPM2 and vice versa.

2.  Configure secondary protection on DPM2 for servers that DPM1 protects.

3.  Configure secondary protection on DPM1 for servers that DPM2 protects.

Note that in a primary to secondary backup configuration \(chained or cyclic\) all DPM servers must be running the same operation system version, service packs, and updates.


