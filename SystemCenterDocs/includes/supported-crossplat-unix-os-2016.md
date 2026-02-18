---
ms.assetid: 
title: Supported UNIX operating system versions
description: This article lists the supported versions of UNIX operating system for System Center Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 01/29/2025
ms.topic: include
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

>[!NOTE]
> Monitoring UNIX computers with System Center Operations Manager 2012 R2 management server is supported when using the System Center 2016 - Operations Manager agent with the Operations Manager 2012 R2 UNIX management packs. You can't import the required Operations Manager 2016 management packs for the specific version of UNIX and discover and deploy the Operations Manager 2016 agent from the **Computer and Device Management** wizard in your 2012 R2 management group. This task must be performed manually following the command-line-based deployment.

## IBM AIX 7 (Power)  

>[!NOTE]
>OpenSSH 9.2 or later isn't supported.

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|OS version|Version of operating system|7100-01-06-1241|  
|xlC.rte|XL C/C++ Runtime|11.1.0.2|  
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8.1800|  

## HP-UX 11i v3 IA64  

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.31.1109|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Specific IA development libraries|B.11.31|  
|SysMgmtMin|Minimum Software Deployment Tools|B.11.31.1109|  
|SysMgmtMin.openssl|OpenSSL Libraries; Secure Network Communications Protocol|A.00.09.08q.003|  
|PAM|Pluggable Authentication Modules|On HP-UX, PAM is part of the core operating system components. There are no other dependencies.|

## Solaris 10 SPARC

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|SUNWlibC |Sun Workshop Compilers Bundled libC|5.10, REV=2004.12.22|
|SUNWlibms|Math & Microtasking Libraries (Usr)|5.10, REV=2004.11.23|
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.10, REV=2004.11.23|
|SUNWcslr|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.15.53|
|SUNWcsl|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.15.53|
|SUNWopenssl-libraries|SUNopenssl-libraries (Usr)|11.10.0,REV=2005.01.21.15.53|
|SUNWcsr|Core Solaris (Root)|11.10.0, REV=2005.01.21.15.53|
|Release|Oracle Solaris 10 1/13|s10s_u11wos_24a SPARC|  

## Solaris 10 x86  

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.10, REV=2004.12.20|
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.10, REV=2004.12.18|
|SUNWcsl|Core Solaris (Shared Libs)|11.10.0, REV=2005.01.21.16.34|
|SUNWcslr|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.16.34|
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.10.0, REV=2005.01.21.16.34|
|SUNWcsr|Core Solaris (Root)|11.10.0, REV=2005.01.21.16.34|
|Release|Oracle Solaris 10 9/10|s10x_u9wos_14a x86|

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

## Solaris 11 x86  

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|
|SUNWcsl|Core Solaris (Shared Libs)|11.11, REV=2009.11.11|
|SUNWcsr|Core Solaris (Root)|11.11, REV=2009.11.11|
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0, REV=2010.05.25.01.00|
|Release|Oracle Solaris 11|11/11 X86|  

## Solaris UTF\-8 Support

The Operations Manager agent requires Solaris UTF-8 code set conversion support under some circumstances. Consult the Solaris documentation for details on installing UTF-8 code set conversion support. The Operations Manager agent functions without UTF-8 support on Solaris, but unrecognized characters are translated to question mark (?) characters.  
