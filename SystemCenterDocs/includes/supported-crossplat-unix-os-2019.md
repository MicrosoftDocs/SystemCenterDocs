---
ms.assetid: 
title: Supported UNIX operating system versions
description: This article lists the supported versions of UNIX operating system for System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 01/29/2025
ms.topic: include
ms.service: system-center
ms.subservice: operations-manager
---

>[!NOTE]
>OpenSSL3.0 is not supported

## IBM AIX 7.2

>[!NOTE]
>OpenSSH 9.2 or later isn't supported.

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|OS version|Version of operating system|7200-00-02-1614|
|xlC.rte|XL C/C++ Runtime|13.1.3.1|
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|1.0.2p|

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
