---
title: Supported UNIX and Linux Operating System Versions
description:
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Supported UNIX and Linux Operating System Versions

>Applies To: System Center 2016 - Operations Manager

The following tables describe the required UNIX and Linux operating systems and package dependencies for System Center 2016 - Operations Manager.  
  
## IBM AIX 5L 5.3 
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|OS version|Version of the operating system|AIX 5.3, Technology Level 6, Service Pack 5|  
|xlC.rte|XL C\/C\+\+ Runtime|9.0.0.2|  
|openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8.4|  
  
## IBM AIX 6.1  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|OS version|Version of operating system|AIX 6.1, any Technology Level and Service Pack|  
|xlC.rte|XL C\/C\+\+ Runtime|9.0.0.5|  
|OpenSSL\/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8.4|  
  
## IBM AIX 7.1 \(Power\)  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|OS version|Version of operating system|AIX 7.1, any Technology Level and Service Pack|  
|xlC.rte|XL C\/C\+\+ Runtime||  
|OpenSSL\/openssl.base|OpenSSL Libraries; Secure Network Communications Protocol||  
  
## HP\-UX 11i v2 IA 64  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|HPUXBaseOS|Base OS|B.11.23|  
|HPUXBaseAux|HP\-UX Base OS Auxiliary|B.11.23.0706|  
|HPUXBaseAux.openssl|OpenSSL Libraries; Secure Network Communications Protocol|A.00.09.07l.003|  
|PAM|Pluggable Authentication Modules|On HP\-UX, PAM is part of the core operating system components. There are no other dependencies.|  
  
## HP\-UX 11i v2 PA\-RISC  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|HPUX11i\-OE|HP\-UX Foundation Operating Environment|B.11.23.0706|  
|OS\-Core.MinimumRuntime.CORE\-SHLIBS|Compatible development tools libraries|B.11.23|  
|HPUXBaseAux|HP\-UX Base OS Auxiliary|B.11.23.0706|  
|HPUXBaseAux.openssl|OpenSSL Libraries; Secure Network Communications Protocol|A.00.09.071.003|  
|PAM|Pluggable Authentication Modules|On HP\-UX, PAM is part of the core operating system components. There are no other dependencies.|  
  
## HP\-UX 11i v3 PA\-RISC  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|HPUX11i\-OE|HP\-UX Foundation Operating Environment|B.11.31.0709|  
|OS\-Core.MinimumRuntime.CORE2\-SHLIBS|Specific IA emulator libraries|B.11.31|  
|openssl\/Openssl.openssl|OpenSSL Libraries; Secure Network Communications Protocol|A.00.09.08d.002|  
|PAM|Pluggable Authentication Modules|On HP\-UX, PAM is part of the core operating system components. There are no other dependencies.|  
  
## HP\-UX 11i v3 IA64  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|HPUX11i\-OE|HP\-UX Foundation Operating Environment|B.11.31.0709|  
|OS\-Core.MinimumRuntime.CORE\-SHLIBS|Specific IA development libraries|B.11.31|  
|SysMgmtMin|Minimum Software Deployment Tools|B.11.31.0709|  
|SysMgmtMin.openssl|OpenSSL Libraries; Secure Network Communications Protocol|A.00.09.08d.002|  
|PAM|Pluggable Authentication Modules|On HP\-UX, PAM is part of the core operating system components. There are no other dependencies.|  
  
## Red Hat Enterprise Linux ES Release 4  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.3.4\-2|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|0.9.7a\-43.1|  
|PAM|Pluggable Authentication Modules|0.77\-65.1|  
  
## Red Hat Enterprise Linux Server release 5.1 \(Tikanga\)  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.5\-12|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8b\-8.3.el5|  
|PAM|Pluggable Authentication Modules|0.99.6.2\-3.14.el5|  
  
## Red Hat Enterprise Linux Server release 6  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.12\-1.7|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.0\-4|  
|PAM|Pluggable Authentication Modules|1.1.1\-4|  
  
## Red Hat Enterprise Linux Server release 7  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard Libraries|2.17|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|1.0.1e\-fips|  
|PAM|Pluggable Authentication Modules|1.1.8\-1|  
  
## Solaris 9 SPARC  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|Required OS patch|PAM memory leak|112960\-48|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.9,REV\=2002.03.18|  
|SUNWlibms|Forte Developer Bundled Shared libm|5.9,REV\=2001.12.10|  
|SMCosslg|OpenSSL<br /><br />Sun does not provide a version of OpenSSL for Solaris 9 SPARC. There is a version available from Sunfreeware.|0.9.7g|  
|SUNWcsl|Core Solaris, \(Shared Libs\)|11.9.0,REV\=2002.04.06.15.27|  
  
## Solaris 10 SPARC  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|Required OS patch|PAM memory leak|117463\-05|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.10, REV\=2004.12.22|  
|SUNWlibms|Math & Microtasking Libraries \(Usr\)|5.10, REV\=2004.11.23|  
|SUNWlibmsr|Math & Microtasking Libraries \(Root\)|5.10, REV\=2004.11.23|  
|SUNWcslr|Core Solaris Libraries \(Root\)|11.10.0, REV\=2005.01.21.15.53|  
|SUNWcsl|Core Solaris Libraries \(Root\)|11.10.0, REV\=2005.01.21.15.53|  
|SUNWopenssl\-libraries|SUNopenssl\-libraries \(Usr\)|11.10.0,REV\=2005.01.21.15.53|  
|SUNWcsr|Core Solaris, \(Root\)|11.10.0, REV\=2005.01.21.15.53|  
  
## Solaris 10 x86  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|Required OS patch|PAM memory leak|117464\-04|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.10,REV\=2004.12.20|  
|SUNWlibmsr|Math & Microtasking Libraries \(Root\)|5.10, REV\=2004.12.18|  
|SUNWcsl|Core Solaris, \(Shared Libs\)|11.10.0,REV\=2005.01.21.16.34|  
|SUNWcslr|Core Solaris Libraries \(Root\)|11.10.0, REV\=2005.01.21.16.34|  
|SUNWopenssl\-libraries|OpenSSL Libraries \(Usr\)|11.10.0, REV\=2005.01.21.16.34|  
|SUNWcsr|Core Solaris, \(Root\)|11.10.0,REV\=2005.01.21.16.34|  
  
## Solaris 11 SPARC  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV\=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries \(Root\)|5.11, REV\=2011.04.11|  
|SUNWcslr|Core Solaris Libraries \(Root\)|11.11, REV\=2009.11.11|  
|SUNWcsl|Core Solaris, \(Shared Libs\)|11.11, REV\=2009.11.11|  
|SUNWcsr|Core Solaris, \(Root\)|11.11, REV\=2009.11.11|  
|SUNWopenssl\-libraries|OpenSSL Libraries \(Usr\)|11.11.0,REV\=2010.05.25.01.00|  
  
## Solaris 11 x86  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV\=2011.04.11|  
|SUNWlibmsr|Math & Microtasking Libraries \(Root\)|5.11, REV\=2011.04.11|  
|SUNWcslr|Core Solaris Libraries \(Root\)|11.11, REV\=2009.11.11|  
|SUNWcsl|Core Solaris, \(Shared Libs\)|11.11, REV\=2009.11.11|  
|SUNWcsr|Core Solaris, \(Root\)|11.11, REV\=2009.11.11|  
|SUNWopenssl\-libraries|OpenSSL Libraries \(Usr\)|11.11.0,REV\=2010.05.25.01.00|  
  
## Solaris UTF\-8 Support  
The Operations Manager agent requires Solaris UTF\-8 code set conversion support under some circumstances. Consult the Solaris documentation for details on installing UTF\-8 code set conversion support. The Operations Manager agent functions without UTF\-8 support on Solaris, but unrecognized characters are translated to question mark \(?\) characters.  
  
## SUSE Linux Enterprise Server 9 \(i586\)  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|Service Pack 4|SUSE Linux Enterprise Server 9||  
|OS Patch lib gcc\-41.rpm|Standard shared library|41\-4.1.2\_20070115\-0.6|  
|OS Patch lib stdc\+\+\-41.rpm|Standard shared library|41\-4.1.2\_20070115\-0.6|  
|Openssl|OpenSSL Libraries; Secure Network Communications Protocol|0.9.7d\-15.35|  
|PAM|Pluggable Authentication Modules|0.77\-221\-11|  
  
## SUSE Linux Enterprise Server 10 SP1 \(i586\)  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc\-2.4\-31.30|C Standard shared library|2.4\-31.30|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8a\-18.15|  
|PAM|Pluggable Authentication Modules|0.99.6.3\-28.8|  
  
## SUSE Linux Enterprise Server 11 \(i586\)  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc\-2.9\-13.2|C Standard shared library|2.9\-13.2|  
|PAM|Pluggable Authentication Modules|pam\-1.0.2\-20.1|  
  
## SUSE Linux Enterprise Server 12 \(x64\)  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc\-2.19\-17.72|C Standard shared library|2.19\-17.72|  
|PAM|Pluggable Authentication Modules|pam\-1.1.8\-11.57|  
  
## Universal Linux \(Debian package\)<br>Debian, Ubuntu Server  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|libc6|C Standard shared library|2.3.6|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.79\-3|  
  
## Universal Linux \(RPM package\)<br>CentOS, Oracle Linux  
  
|Required Package|Description|Minimum Version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard shared library|2.5\-12|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.99.6.2\-3.14|  
  

  
