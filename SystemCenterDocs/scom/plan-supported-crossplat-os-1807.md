---
ms.assetid: 50504e6d-945f-43e6-8faf-33fe870c623d
title: Supported UNIX and Linux Operating System Versions
description: This article lists the supported versions of Linux and UNIX operating system for System Center Operations Manager version 1807.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 07/20/2018
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1807'
ms.technology: operations-manager
ms.topic: article
---

# Supported UNIX and Linux operating systems

The following tables describe the required UNIX and Linux operating systems and package dependencies for System Center Operations Manager version 1807.  


## IBM AIX 6.1  

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|OS version|Version of operating system|6100-07-06-1241|  
|xlC.rte|XL C/C++ Runtime|11.1.0.2|  
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8.1800|


## IBM AIX 7 (Power)  

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|OS version|Version of operating system|7100-01-06-1241|  
|xlC.rte|XL C/C++ Runtime|11.1.0.2|  
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|1.0.0|  

## HP-UX 11i v3 IA64  

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.31.1109|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Specific IA development libraries|B.11.31|  
|SysMgmtMin|Minimum Software Deployment Tools|B.11.31.1109|  
|SysMgmtMin.openssl|OpenSSL Libraries; Secure Network Communications Protocol|A.00.09.08q.003|  
|PAM|Pluggable Authentication Modules|On HP-UX, PAM is part of the core operating system components. There are no other dependencies.|  

## Red Hat Enterprise Linux Server 6  

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.12-1.7|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

## Red Hat Enterprise Linux Server 7

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.17|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.1e-fips|  
|PAM|Pluggable Authentication Modules|1.1.8-1|  

## Red Hat Enterprise Linux Server 7 (Power)  

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.17|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.1e-fips|  
|PAM|Pluggable Authentication Modules|1.1.8|  

## Solaris 10 SPARC  

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|SUNWlibC |Sun Workshop Compilers Bundled libC|5.10, REV=2004.12.22|
|SUNWlibms|Math & Microtasking Libraries (Usr)|5.10, REV=2004.11.23|
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.10, REV=2004.11.23|
|SUNWcslr|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.15.53|
|SUNWcsl|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.15.53|
|SUNWopenssl-libraries|SUNopenssl-libraries (Usr)|11.10.0, REV=2005.01.21.15.53|
|SUNWcsr|Core Solaris (Root)|11.10.0, REV=2005.01.21.15.53|
|Release|Oracle Solaris 10 1/13|s10s_u11wos_24a SPARC|  

## Solaris 10 x86  

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.10, REV=2004.12.20|
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.10, REV=2004.12.18|
|SUNWcsl|Core Solaris (Shared Libs)|11.10.0, REV=2005.01.21.16.34|
|SUNWcslr|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.16.34|
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.10.0, REV=2005.01.21.16.34|
|SUNWcsr|Core Solaris (Root)|11.10.0, REV=2005.01.21.16.34|
|Release|Oracle Solaris 10 9/10|s10x_u9wos_14a x86|

## Solaris 11 SPARC  

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.11, REV=2011.04.11|
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|
|SUNWcsl|Core Solaris (Shared Libs)|11.11, REV=2009.11.11|
|SUNWcsr|Core Solaris (Root)|11.11, REV=2009.11.11|
|SUNWopenssl-libraries|OpenSSL Libraries (Usr)|11.11.0, REV=2010.05.25.01.00|
|Release|Oracle Solaris 11|11/11 SPARC|

## Solaris 11 x86  

|Required Package|Description|Minimum Version|  
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

## SUSE Linux Enterprise Server 11   

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc-2.9-13.2|C Standard shared library|2.9-13.2|  
|PAM|Pluggable Authentication Modules|pam-1.0.2-20.1|  

## SUSE Linux Enterprise Server 12   

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|  
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0|

## Universal Linux (Debian package)

Debian 8, 9 and Ubuntu 14.04, 16.04, 18.04 are supported   

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|libc6|C Standard shared library|2.24-11|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0 or 1.1|  
|PAM|Pluggable Authentication Modules|1.1.8-3.1|  

## Universal Linux (RPM package)

CentOS 6 and 7, Oracle Linux 6 and 7

|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard shared library|2.12-1|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0 or 1.1|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

## Supported SSH Key Algorithms  

- diffie-hellman-group14-sha256
- diffie-hellman-group-exchange-sha256
- ecdh-sha2-nistp256
