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
ms.update-cycle: 1095-days
---

>[!NOTE]
> Monitoring Linux computers with System Center Operations Manager 2012 R2 management server is supported when using the System Center 2016 - Operations Manager agent with the Operations Manager 2012 R2 Linux management packs. You can't import the required Operations Manager 2016 management packs for the specific version of Linux and discover and deploy the Operations Manager 2016 agent from the **Computer and Device Management** wizard in your 2012 R2 management group. This task must be performed manually following the command-line-based deployment.

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

>[!NOTE]
>Solaris zone-level monitoring isn't supported.

## SUSE Linux Enterprise Server 12

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc-2.19-17.72|C Standard shared library|2.19-17.72|  
|PAM|Pluggable Authentication Modules|pam-1.1.8-11.57|  

## Universal Linux

Ubuntu 14.04, 16.04 are supported.

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|libc6|C Standard shared library|2.3.6|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.79-3|  

## Universal Linux (RPM package)

Oracle Linux 7 is supported.

|Required package|Description|Minimum version|  
|--------------------|---------------|-------------------|  
|glibc|C Standard shared library|2.5-12|  
|OpenSSL|OpenSSL Libraries; Secure Network Communications Protocol|0.9.8 or 1.0|  
|PAM|Pluggable Authentication Modules|0.99.6.2-3.14|
