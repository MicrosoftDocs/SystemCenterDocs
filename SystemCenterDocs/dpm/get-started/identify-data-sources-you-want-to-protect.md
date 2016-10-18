---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  Identify data sources you want to protect
ms.technology:  data-protection-manager
ms.assetid:  4774dd1a-f50a-4a75-8783-abb5d134298a
---

# Identify data sources you want to protect

>Applies To: System Center 2016 - Data Protection Manager

To protect data sources with DPM you'll need to do the following:

-   Read [What can DPM back up?](What-can-DPM-back-up-.md) to understand what's supported for DPM backup.

-   DPM applies backup settings to all data sources in a particular protection group. You'll need to figure out how you want to gather data you want to protect into those groups. Examples include:

    -   **By computer** - So that all data sources for a computer belonging to the same protection group. This provides a single point of adjustment for the computer's performance loads. However, all data sources will then have the same backup and recovery settings.

    -   **By workload** - So that you separate files and each application data type into different protection groups. This allows you to manage workloads as a group. However recovering a multi-application server might require multiple tapes from different protection groups.

    -   **By RPO/RTO** - Gather data sources with similar Recovery Point Objectives (RPOs) and Recovery Time Objectives (RTOs). You control the RPO by setting the synchronization frequency for the protection group which determines the amount of potential data loss (in time) in the case of unexpected outages. The RTO measures the acceptable amount of time that data is unavailable and is affected by the storage methods your select for the protection group.

    -   **By data characteristics** - For example how often data changes, how rapidly it grows, or its storage requirements.


## Next steps
[Deploy the DPM protection agent](../Deploy/Deploy-the-DPM-protection-agent.md)
