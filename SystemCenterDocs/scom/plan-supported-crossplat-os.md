---
ms.assetid: 50504e6d-945f-43e6-8faf-33fe870c623d
title: Supported UNIX and Linux operating system versions
description: This article lists the supported versions of Linux and UNIX operating system for System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 08/11/2022
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Supported UNIX and Linux operating system versions

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

::: moniker range="sc-om-2022"

The following tables describe the required UNIX and Linux operating systems and package dependencies for System Center 2022 - Operations Manager.

>[!IMPORTANT]
>Operations Manager automatically stops supporting the operating systems and packages for which the vendor owner has stopped the support.

::: moniker-end

::: moniker range="sc-om-2019"

The following tables describe the required UNIX and Linux operating systems and package dependencies for System Center 2019 - Operations Manager.

>[!IMPORTANT]
>Operations Manager automatically stops supporting the operating systems and packages for which the vendor owner has stopped the support.

## IBM AIX 7.1

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|
|OS version|Version of operating system|7100-01-06-1241|
|xlC.rte|XL C/C++ Runtime|11.1.0.2|
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|1.0.2o|


## IBM AIX 7.2

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|OS version|Version of operating system|7200-00-02-1614|
|xlC.rte|XL C/C++ Runtime|13.1.3.1|
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|1.0.2p|

::: moniker-end

::: moniker range=">=sc-om-2019"

## Red Hat Enterprise Linux Server 8 (applicable for 2019 UR1 and later)

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc|C Standard Libraries|2.28|
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.1.1c-fips|
|PAM|Pluggable Authentication Modules|1.3.1-4|

## Red Hat Enterprise Linux Server 7

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc|C Standard Libraries|2.17|
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.1e-fips|
|PAM|Pluggable Authentication Modules|1.1.8-1|

::: moniker-end

::: moniker range="sc-om-2022"
>[!NOTE]
>Red Hat Enterprise Linux Server 7 (Power) is not supported in Operations Manager 2022.
::: moniker-end

::: moniker range="sc-om-2019"

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
>Solaris zone-level monitoring is not supported.

## Solaris 10 SPARC

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|SUNWlibC |Sun Workshop Compilers Bundled libC|5.10, REV=2004.12.22|
|SUNWlibms|Math & Microtasking Libraries (Usr)|5.10, REV=2004.11.23|
|SUNWlibmsr|Math & Microtasking Libraries (Root)|5.10, REV=2004.11.23|
|SUNWcslr|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.15.53|
|SUNWcsl|Core Solaris Libraries (Root)|11.10.0, REV=2005.01.21.15.53|
|SUNWopenssl-libraries|SUNopenssl-libraries (Usr) <br /><br /> **Note**: For TLS1.2, to get OpenSSL 1.0.1p, apply the following patch: 151912-02 (or greater) (This patch is applicable for 2019 UR3 and later).|11.10.0, REV=2005.01.21.15.53|
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

::: moniker-end

::: moniker range=">=sc-om-2019"

## SUSE Linux Enterprise Server 12

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0|

::: moniker-end

::: moniker range="sc-om-2022"
>[!NOTE]
>SUSE Linux Enterprise Server 12 (Power) is not supported in Operations Manager 2022.
::: moniker-end

::: moniker range="sc-om-2019"

## SUSE Linux Enterprise Server 12 (Power)

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0|

## SUSE Linux Enterprise Server 15

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

- Debian 9, 10, and 11
- Ubuntu 16.04, 18.04, and 20.04

>[!NOTE]
> Debian 10, 11 and Ubuntu 20.04 are compatible with SCOM 2019 UR3 and later.

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|libc6|C Standard shared library|2.24-11|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0 or 1.1|
|PAM|Pluggable Authentication Modules|1.1.8-3.1|

## Universal Linux (RPM package)

Supported versions:

- CentOS 7
- Oracle Linux 7, and 8
- Rocky 8 (supported from Operations Manager 2019 UR4 and later)
- Alma 8 (supported from Operations Manager 2019 UR4 and later)

Oracle Linux 8 is supported from SCOM 2019 UR3 and later in XPlat agent under Universal Linux (RPM package). To install the agent on servers, see [Install the agent on RPM based Universal Linux Servers](manage-install-crossplat-agent-cmdline.md#to-install-the-agent-on-rpm-based-universal-linux-servers-oracle-and-centos).

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc|C Standard shared library|2.5-12|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0 or 1.1|
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|

::: moniker-end

::: moniker range="sc-om-2022"

## Universal Linux (Debian package)

Supported versions:

- Debian 9, 10 and 11
- Ubuntu 16.04, 18.04 and 20.04

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|libc6|C Standard shared library|2.24-11|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0 or 1.1|
|PAM|Pluggable Authentication Modules|1.1.8-3.1|

## Universal Linux (RPM package)

Supported versions:

- CentOS 7
- Oracle Linux 7 and 8
- SLES 15
- openSUSE Leap 15t
- Rocky 8 
- Alma 8 

|Required package|Description|Minimum version|
|--------------------|---------------|-------------------|
|glibc|C Standard shared library|2.5-12|
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|1.0 or 1.1|
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|

::: moniker-end

::: moniker range="sc-om-2016"

The following tables describe the required UNIX and Linux operating systems and package dependencies for System Center 2016 - Operations Manager.

>[!IMPORTANT]
>Operations Manager automatically stops supporting the operating systems and packages for which the vendor owner has stopped the support.

::: moniker-end

::: moniker range="sc-om-1801"

The following tables describe the required UNIX and Linux operating systems and package dependencies for System Center 1801 - Operations Manager.  

::: moniker-end

::: moniker range="sc-om-1807"

The following tables describe the required UNIX and Linux operating systems and package dependencies for System Center 1807 - Operations Manager.  

::: moniker-end

::: moniker range="<=sc-om-1807"

>[!NOTE]
>Monitoring UNIX and Linux computers with System Center Operations Manager 2012 R2 management server is supported when using the System Center 2016 - Operations Manager agent with the Operations Manager 2012 R2 UNIX and Linux management packs.  You cannot import the required Operations Manager 2016 management packs for the specific version of UNIX/Linux and discover and deploy the Operations Manager 2016 agent from the **Computer and Device Management** wizard in your 2012 R2 management group.  This task must be performed manually following the command-line based deployment.  
>

::: moniker-end

::: moniker range="sc-om-1801"

## IBM AIX 6.1  

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|OS version|Version of operating system|6100-07-06-1241|  
|xlC.rte|XL C/C++ Runtime|11.1.0.2|  
|OpenSSL/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8.1800|

::: moniker-end

::: moniker range="<=sc-om-1807"

## IBM AIX 7 (Power)  

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

::: moniker-end

::: moniker range="<=sc-om-1807 >sc-om-2016"

## Red Hat Enterprise Linux Server 5  

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.12-1.7|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

::: moniker-end

::: moniker range="<=sc-om-1807"

## Red Hat Enterprise Linux Server 6  

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.12-1.7|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.0-4|  
|PAM|Pluggable Authentication Modules|1.1.1-4|  

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

::: moniker -end

::: moniker range="sc-om-2016"

>[!NOTE]
>Solaris zone-level monitoring is not supported.

::: moniker-end

::: moniker range="<=sc-om-1807"

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

::: moniker-end

::: moniker range="<=sc-om-1807 >sc-om-2016"

## SUSE Linux Enterprise Server 11   

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc-2.9-13.2|C Standard shared library|2.9-13.2|  
|PAM|Pluggable Authentication Modules|pam-1.0.2-20.1|  

::: moniker-end

::: moniker range="<=sc-om-1807"

## SUSE Linux Enterprise Server 12   

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|  
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|  

::: moniker-end

::: moniker range="<=sc-om-1807 >sc-om-2016"

## Universal Linux (Debian package)
Debian 8 and Ubuntu 14.04, 16.04 are supported.

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|libc6|C Standard shared library|2.3.6|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.79-3|  

::: moniker-end

::: moniker range="sc-om-2016"

## Universal Linux

Ubuntu 14.04, 16.04 are supported.

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|libc6|C Standard shared library|2.3.6|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.79-3|  

::: moniker-end

::: moniker range="<=sc-om-1807 >sc-om-2016"

## Universal Linux (RPM package)
CentOS 7 and Oracle Linux 6, 7 are supported.

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard shared library|2.5-12|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|


::: moniker-end

::: moniker range="sc-om-2016"

## Universal Linux (RPM package)
CentOS 7 and Oracle Linux 7 are supported.

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard shared library|2.5-12|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|


::: moniker-end
