---
ms.assetid: 
title: Supported Linux operating system versions
description: This article lists the supported versions of Linux operating system for System Center Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 01/29/2025
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

## Red Hat Enterprise Linux Server 7 (Power)

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc|C Standard Libraries|2.17|
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.1e-fips|
|PAM|Pluggable Authentication Modules|1.1.8|

## Red Hat Enterprise Linux Server 6 (applicable for 2019 UR3 and later)

Operations Manager 2019 UR3 and later supports RHEL 6 through the RHEL 6 management pack.

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.12-1.7|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

>[!NOTE]
>Solaris zone-level monitoring isn't supported.

## SUSE Linux Enterprise Server 12

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0|

## SUSE Linux Enterprise Server 12 (Power)

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0|

## SUSE Linux Enterprise Server 15

>[!NOTE]
>System Center Operations Manager 2019 UR1 and later supports SLES 15 under Universal Linux.

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0|

## openSUSE Leap 15

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0|

## Universal Linux (Debian package)

Supported versions:

- Debian 8, 9, 10, 11, and 12
- Ubuntu 16.04, 18.04, 20.04, 22.04 and 24.04

>[!NOTE]
>- Debian 10, 11, and Ubuntu 20.04 are compatible with System Center - Operations Manager 2019 UR3 and later.
>- Ubuntu 22.04 is compatible with System Center - Operations Manager 2019 UR5 and later.
>- Ubuntu 24.04 is compatible with System Center - Operations Manager 2019 UR6 and later

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|libc6|C Standard shared library|2.24-11|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0, 1.1 or 3.0 and later|
|PAM|Pluggable Authentication Modules|1.1.8-3.1|

## Universal Linux (RPM package)

Supported versions:

- CentOS 7 and 8
- Oracle Linux 7<br> Oracle Linux 8 is supported from Operations Manager 2019 UR3 later<br> Oracle Linux 9 is supported from Operations Manager 2019 UR5 and later
- Rocky 8 is supported from Operations Manager 2019 UR4 and later<br>Rocky 9 is supported from Operations Manager 2019 UR5 and later
- Alma 8 is supported from Operations Manager 2019 UR4 and later<br>Alma 9 is supported from Operations Manager 2019 UR5 and later
- Red Hat Enterprise Linux (RHEL) Server 8 is supported from Operations Manager 2019 UR1 and later<br>Red Hat Enterprise Linux (RHEL) Server 9 is supported from Operations Manager 2019 UR5 and later
- SLES 15 is supported from System Center - Operations Manager 2019 UR1 and later

>[!Note]
>Manually update the OpenSSH version in your environment to >= 8.7p1-29 to monitor RHEL 9.1 servers.

To install the agent on servers, see [Install the agent on RPM based Universal Linux Servers](/system-center/scom/manage-install-crossplat-agent-cmdline?view=sc-om-2016#to-install-the-agent-on-rpm-based-universal-linux-servers-oracle&preserve-view=true).

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc|C Standard shared library|2.5-12|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0, 1.1 or 3.0 and later|
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|
