---
description: This article provides the new features and feature updates supported by System Center DPM 2025.
ms.topic: include
author: jyothisuri
ms.author: jsuri
ms.service: system-center
ms.date: 11/04/2024
title: What's new in System Center DPM
ms.subservice: data-protection-manager
ms.assetid:
ms.custom: intro-whats-new
---

## New features in DPM 2025

See the following sections for detailed information about the new features/feature updates supported in DPM 2025.

### Windows Server 2025 support

DPM 2025 supports the installation of DPM 2025 on Windows Server 2025 and the protection of Windows Server 2025 workloads. You can now Backup system state, file, folder and volume, and applications supported by DPM 2025. [Learn more](/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2025)

### Enhanced Passphrase save mechanism for MARS Agent

Save passphrases to the Azure Key vault to reduce the risk of losing them due to server corruption, compromise, or accidental file deletion. Warnings are displayed when saved locally.

### DPM database Backup notifications

Backup the DPM database to disk and Azure to mitigate and reconstruct the DPM server after the original server is lost. Use the `DPMSync` Tool to resynchronize the database.

### Support for SharePoint subscription edition

Use the `ConfigureSharepoint.exe` command line tool to support the SharePoint subscription edition.

### Support for VMs with vTPM device configured

Backup and restore vTPM configured VMs, preserving vTPM device settings during the restoration process. The Alternate Location Restore (ALR) flow for vTPM VMs assumes that the selected target vCenter has access to the same Key Provider.

### Support for SQL OLEDB 19

DPM 2025 uses OLEDB 19 driver to communicate and backup SQL instances. This is applicable for SharePoint backups also.
