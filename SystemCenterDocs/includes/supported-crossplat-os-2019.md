---
ms.assetid: 
title: Supported UNIX and Linux operating system versions
description: This article lists the supported versions of Linux and UNIX operating system for System Center Operations Manager.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 12/18/2024
ms.topic: include
ms.service: system-center
ms.subservice: operations-manager
---

## IBM AIX 7.2

>[!NOTE]
>OpenSSH 9.2 or later isn't supported.

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|OS version|Version of operating system|7200-00-02-1614|
|xlC.rte|XL C/C++ Runtime|13.1.3.1|
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|1.0.2p|

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

## Red Hat Enterprise Linux Server 6  (applicable for 2019 UR3 and later)

Operations Manager 2019 UR3 and later supports RHEL 6 through the RHEL 6 management pack.

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.12-1.7|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

>[!NOTE]
>Solaris zone-level monitoring isn't supported.

## Solaris 10 SPARC

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|SUNWlibC |Sun Workshop Compilers Bundled libC|5.10, REV=2004.12.22|
|SUNWlibms|Math & Microtasking Libraries (Usr)|5.10, REV=2004.11.23|
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.10, REV=2004.11.23|
|SUNWcslr|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.15.53|
|SUNWcsl|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.15.53|
|SUNWopenssl-libraries|SUNopenssl-libraries (Usr) <br /><br /> **Note**: For TLS1.2, to get OpenSSL 1.0.1p, apply the following patch: 151912-02 (or greater) (This patch is applicable for 2019 UR3 and later.)|11.10.0, REV=2005.01.21.15.53|
|SUNWcsr|Core Solaris (Root)|11.10.0, REV=2005.01.21.15.53|
|Release|Oracle Solaris 10 1/13|s10s_u11wos_24a SPARC|

## Solaris 11 SPARC

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|
|SUNWcsl|Core Solaris (Shared Libs)|11.11, REV=2009.11.11|
|SUNWcsr|Core Solaris (Root)|11.11, REV=2009.11.11|
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0, REV=2010.05.25.01.00|
|Release|Oracle Solaris 11|11/11 SPARC|

## Solaris UTF\-8 Support

The Operations Manager agent requires Solaris UTF-8 code set conversion support under some circumstances. Consult the Solaris documentation for details on installing UTF-8 code set conversion support. The Operations Manager agent functions without UTF-8 support on Solaris, but unrecognized characters are translated to question mark (?) characters.

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

- Debian 9, 10, 11, and 12
- Ubuntu 16.04, 18.04, 20.04, 22.04 and 24.04

>[!NOTE]
>- Debian 10, 11, and Ubuntu 20.04 are compatible with System Center - Operations Manager 2019 UR3 and later.
>- Ubuntu 22.04 is compatible with System Center - Operations Manager 2019 UR5 and later.
>- Ubuntu 24.04 is compatible with System Center - Operations Manager 2019 UR6 and later

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|libc6|C Standard shared library|2.24-11|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0, 1.1 or 3.0|
|PAM|Pluggable Authentication Modules|1.1.8-3.1|

## Universal Linux (RPM package)

Supported versions:

- Oracle Linux 7, 8 (supported from Operations Manager 2019 UR3 and later), and 9 (supported from Operations Manager 2019 UR6 and later)
- Rocky 8 (supported from Operations Manager 2019 UR5 and later), and 9 (supported from Operations Manager 2019 UR6 and later)
- Alma 8 (supported from Operations Manager 2019 UR5 and later), and 9 (supported from Operations Manager 2019 UR6 and later)
- Red Hat Enterprise Linux (RHEL) Server 8 (supported from Operations Manager 2019 UR1 and later)
- Red Hat Enterprise Linux (RHEL) Server 9 (supported from Operations Manager 2019 UR6 and later)
- SLES 15 is supported from System Center - Operations Manager 2019 UR1 and later

>[!Note]
>Manually update the OpenSSH version in your environment to >= 8.7p1-29 to monitor RHEL 9.1 servers.

To install the agent on servers, see [Install the agent on RPM based Universal Linux Servers](/SystemCenterDocs/scom/manage-install-crossplat-agent-cmdline.md#install-the-agent-on-rpm-based-universal-linux-servers-oracle).

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc|C Standard shared library|2.5-12|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0, 1.1 or 3.0|
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|
