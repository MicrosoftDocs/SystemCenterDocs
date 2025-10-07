---
ms.assetid: 
title: Supported UNIX and Linux operating system versions
description: This article lists the supported versions of Linux and UNIX operating system for System Center Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 04/09/2025
ms.topic: include
ms.service: system-center
ms.subservice: operations-manager
---

## Red Hat Enterprise Linux Server 7

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc|C Standard Libraries|2.17|
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.1e-fips|
|PAM|Pluggable Authentication Modules|1.1.8-1|

>[!NOTE]
>Red Hat Enterprise Linux Server 7 (Power) isn't supported in Operations Manager 2022 and later.

## SUSE Linux Enterprise Server 12

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0, 1.1 or 3.0 and later|

>[!NOTE]
>SUSE Linux Enterprise Server 12 (Power) isn't supported in Operations Manager 2022 and later.

## Universal Linux (Debian package)

Supported versions:

- Debian 8, 9, 10, 11, and 12
- Ubuntu 16.04, 18.04, 20.04, 22.04 and 24.04

>[!Note]
>- Ubuntu 22.04 is supported from Operations Manager 2022 UR1 and later when you apply [this hotfix](https://support.microsoft.com/topic/system-center-operations-manager-2022-now-has-openssl3-0-integration-kb-5024286-331bd221-10f9-42d5-bc06-775eaabe3081).
>- Ubuntu 24.04 is supported from Operations Manager 2022 UR2 and later.

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|libc6|C Standard shared library|2.24-11|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0, 1.1 or 3.0 and later|
|PAM|Pluggable Authentication Modules|1.1.8-3.1|

## Universal Linux (RPM package)

Supported versions:

- Oracle Linux 7, 8, and 9
- SLES 15
- openSUSE Leap 15t
- Rocky 8 and 9
- Alma 8 and 9
- Red Hat Enterprise Linux (RHEL) Server 8 and 9
- CentOS 7 and 8

>[!Note]
>- Oracle Linux 9, Rocky 9, and Alma 9 are supported from Operations Manager 2022 UR1 and later when you apply this [hotfix](https://support.microsoft.com/topic/system-center-operations-manager-2022-now-has-openssl3-0-integration-kb-5024286-331bd221-10f9-42d5-bc06-775eaabe3081).
>- RHEL 9 is supported from Operations Manager 2022 UR1 and later when you apply [this hotfix](https://support.microsoft.com/topic/system-center-operations-manager-2022-now-has-openssl3-0-integration-kb-5024286-331bd221-10f9-42d5-bc06-775eaabe3081). 
>- Manually update the OpenSSH version in your environment to >= 8.7p1-29 to monitor RHEL 9.1 servers.

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc|C Standard shared library|2.5-12|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0, 1.1 or 3.0 and later|
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|

>[!NOTE]
>If you encounter a discovery error **Azure Linux and Arc Linux Machines are unsupported** for any Linux VMs deployed in Azure, see [Troubleshoot discovery error - Azure Linux not supported](/system-center/scom/troubleshoot-discovery-error).
 