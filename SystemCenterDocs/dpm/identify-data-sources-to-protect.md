---
description: This article helps you identify data sources you want to protect with DPM.
ms.topic: concept-article
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.update-cycle: 1095-days
title: Identify data sources you want to protect
ms.subservice: data-protection-manager
ms.assetid: 4774dd1a-f50a-4a75-8783-abb5d134298a
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency3, engagement-fy24
---

# Identify data sources you want to protect

To protect data sources with System Center Data Protection Manager (DPM), you'll need to do the following:

- Read [What can DPM back up?](dpm-protection-matrix.md) to understand what's supported for DPM backup.

- DPM applies backup settings to all data sources in a particular protection group. You'll need to figure out how you want to gather data you want to protect into those groups. Examples include:

    - **By computer** - So that all data sources for a computer belong to the same protection group. This provides a single point of adjustment for the computer's performance loads. However, all data sources will then have the same backup and recovery settings.

    - **By workload** - So that you separate files and each application data type into different protection groups. This allows you to manage workloads as a group. However, recovering a multi-application server might require multiple tapes from different protection groups.

    - **By RPO/RTO** - Gather data sources with similar Recovery Point Objectives (RPOs) and Recovery Time Objectives (RTOs). You control the RPO by setting the synchronization frequency for the protection group, which determines the amount of potential data loss (in time) in the case of unexpected outages. The RTO measures the acceptable amount of time that data is unavailable and is affected by the storage methods your select for the protection group.

    - **By data characteristics** - For example, how often data changes, how rapidly it grows, or its storage requirements.

## Next steps

[Deploy the DPM protection agent](~/dpm/deploy-dpm-protection-agent.md)
