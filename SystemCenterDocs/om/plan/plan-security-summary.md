---
ms.assetid: eda0345b-cbef-494d-8c15-f782ad47500e
title: Security Design
description: This article is the landing page for security design guidance for Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Security Design

>Applies To: System Center 2016 - Operations Manager

This section provides you with security-related information as it pertains to the planning of security accounts, roles and privileges required for your deployment of System Center 2016 - Operations Manager.

## Security planning topics

- Understand the security requirements and how to prepare your environment for Operations Manager by reviewing the [Security Accounts for Operations Manager](planning-security-accounts.md) guidance.

- Review how [Run As accounts and Run As profiles](planning-security-run-as-accounts-profiles.md) allow you to run workflows from management packs under different accounts on different computers securely.  

- Before monitoring Office 365 and workloads hosted in the cloud with Operations Manager, review  [Integration with Microsoft Azure and Office 365](planning-security-microsoft-cloud.md).

- The [Firewall Configuration for Operations Manager](planning-security-configuring-a-firewall.md) topic will help you understand the required network ports and communication path between Operations Manager roles and components.

- [Planning Security Credentials for Accessing UNIX and Linux Computers](planning-security-credentials-for-accessing-unix-and-linux-computers.md) describes the security considerations for monitoring UNIX and Linux computers with Operations Manager.

- If you are planning on monitoring your .NET web-based applications with Operations Manager Application Performance Monitoring to detect performance or faults, read [User Roles for Application Performance Monitoring](planning-security-user-roles-for-apm.md).

- The [Planning Security Authentication and Data Encryption in Operations Manager](planning-security-authentication-data-encryption-in-operations-manager.md) describes how authentication is performed and identifies connection channels where the data is encrypted between all of the server roles and agents in a management group.
