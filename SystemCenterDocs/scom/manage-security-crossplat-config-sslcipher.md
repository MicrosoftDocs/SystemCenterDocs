---
ms.assetid: 8b01d791-e5b9-475a-b789-6162e6120397
title: Configuring SSL Ciphers
description: This article describes how to configure SSL encrypted communication for UNIX and Linux computers and Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: na
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Configuring SSL ciphers



System Center - Operations Manager correctly manages UNIX and Linux computers without changes to the default Secure Sockets Layer (SSL) cipher configuration. For most organizations, the default configuration is acceptable, but you should check your organization's security policies to determine whether changes are required.  

## Using the SSL cipher configuration  

The Operations Manager UNIX and Linux agent communicate with the Operations Manager management server by accepting requests on port 1270 and supplying information in response to those requests. Requests are made by using the WS-Management protocol that is running on an SSL connection.  

When the SSL connection is first established for each request, the standard SSL protocol negotiates the encryption algorithm, known as a cipher for the connection to use. For Operations Manager, the management server always negotiates to use a high strength cipher so that strong encryption is used on the network connection between the management server and the UNIX or Linux computer.  

The default SSL cipher configuration on UNIX or Linux computer is governed by the SSL package that is installed as part of the operating system. The SSL cipher configuration typically allows connections with various ciphers, including older ciphers of lower strength. While Operations Manager doesn't use these lower strength ciphers, having port 1270 open with the possibility of using a lower strength cipher contradicts the security policy of some organizations.  

If the default SSL cipher configuration meets your organization's security policy, no action is needed.  

If the default SSL cipher configuration contradicts your organization's security policy, the Operations Manager UNIX and Linux agent provides a configuration option to specify the ciphers that SSL can accept on port 1270. This option can be used to control the ciphers and bring the SSL configuration into conformance with your policies. After the Operations Manager UNIX and Linux agent are installed on each managed computer, the configuration option must be set by using the procedures described in the next section. Operations Manager doesn't provide any automatic or built-in way to apply these configurations; each organization must perform the configuration by using an external mechanism that works best for it.  

### Setting the sslCipherSuite configuration option

The SSL ciphers for port 1270 are controlled by setting the **sslciphersuite** option in the OMI configuration file, **omiserver.conf**. The **omiserver.conf** file is located in the directory `/etc/opt/omi/conf/`.  

The format for the sslciphersuite option in this file is:  

```  
sslciphersuite=<cipher spec>  
```  

Where \<cipher spec\> specifies the ciphers that are allowed, disallowed, and the order in which the allowed ciphers are chosen.  

The format for \<cipher spec\> is the same as the format for the **sslCipherSuite** option in the Apache HTTP Server version 2.0. For detailed information, see [SSLCipherSuite Directive](https://go.microsoft.com/fwlink/?LinkId=318052) in the Apache documentation. All the information on this site is provided by the owner or the users of the website. Microsoft makes no warranties, express, implied or statutory, as to the information at this website.  

After setting the **sslCipherSuite** configuration option, you must restart the UNIX and Linux agent for the change to take effect. To restart the UNIX and Linux agent, run the following command, which is located in the **/etc/opt/microsoft/scx/bin/tools** directory.  

```  
. setup.sh  
scxadmin -restart  
```  

### Enabling or Disabling the TLS Protocol Versions

For System Center – Operations Manager, omiserver.conf is located at:
`/etc/opt/omi/conf/omiserver.conf`

The following flags need to be set in order to enable/disable the TLS protocol versions. For more information, see [Configuring OMI Server](https://github.com/microsoft/omi#configuring-omi-server).

|Property|Purpose|
|-----|-----|
| NoTLSv1_0   | When true, the TLSv1.0 protocol is disabled.    |
|NoTLSv1_1   |When true, and if available on the platform, the TLSv1.1 protocol is disabled.|
|NoTLSv1_2	  |When true, and if available on the platform, the TLSv1.2 protocol is disabled.|

### Enabling or Disabling the SSLv3 Protocol

Operations Manager communicates with UNIX and Linux agents over HTTPS, using either TLS or SSL encryption. The SSL handshaking process negotiates the strongest encryption that is mutually available on the agent and the management server. You may wish to prohibit SSLv3 so that an agent that can't negotiate TLS encryption doesn't fall back to SSLv3.

For System Center – Operations Manager, omiserver.conf is located at:
`/etc/opt/omi/conf/omiserver.conf`

#### To disable SSLv3

Modify omiserver.conf, set the **NoSSLv3** line to be:
`NoSSLv3=true`

#### To enable SSLv3

Modify omiserver.conf, set the **NoSSLv3** line to be:
`NoSSLv3=false`

::: moniker range="=sc-om-2019"
>[!NOTE]
> The following update is applicable for Operations Manager 2019 UR3 and later.

::: moniker-end

## Cipher Suite Support Matrix

|Distro|Kernel&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|OpenSSL&nbsp;Version|Highest&nbsp;Supported&nbsp;Cipher&nbsp;Suite/Preferred&nbsp;Cipher&nbsp;Suite|Cipher&nbsp;Index|
|---------------------------------------------|--------------------------------------|----------------------------------|-------------------------------------------------------|----------------|
|Red&nbsp;Hat&nbsp;Enterprise&nbsp;Linux&nbsp;Server&nbsp;7.5&nbsp;(Maipo)|Linux&nbsp;3.10.0-862.el7.x86_64|OpenSSL&nbsp;1.0.2k-fips&nbsp;(26&nbsp;Jan&nbsp;2017)|TLS_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0x00,&nbsp;0x9D&nbsp;}|
|Red&nbsp;Hat&nbsp;Enterprise&nbsp;Linux&nbsp;8.3&nbsp;(Ootpa)|Linux&nbsp;4.18.0-240.el8.x86_64|OpenSSL&nbsp;1.1.1g&nbsp;FIPS&nbsp;(21&nbsp;Apr&nbsp;2020)|TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0xC0,&nbsp;0x30&nbsp;}|
|Oracle&nbsp;Linux&nbsp;Server&nbsp;release&nbsp;6.10|Linux4.1.12-124.16.4.el6uek.x86_64|OpenSSL&nbsp;1.0.1e-fips&nbsp;(11&nbsp;Feb&nbsp;2013)|TLS_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0x00,&nbsp;0x9D&nbsp;}|
|Oracle&nbsp;Linux&nbsp;Server&nbsp;7.9|Linux&nbsp;5.4.17-2011.6.2.el7uek.x86_64|OpenSSL&nbsp;1.0.2k-fips&nbsp;(26&nbsp;Jan&nbsp;2017)|TLS_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0x00,&nbsp;0x9D&nbsp;}|
|Oracle&nbsp;Linux&nbsp;Server&nbsp;8.3|Linux&nbsp;5.4.17-2011.7.4.el8uek.x86_64|OpenSSL&nbsp;1.1.1g&nbsp;FIPS&nbsp;(21&nbsp;Apr&nbsp;2020)|TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0xC0,&nbsp;0x30&nbsp;}|
|Linux&nbsp;8&nbsp;(Core)|Linux&nbsp;4.18.0-193.el8.x86_64|OpenSSL&nbsp;1.1.1c&nbsp;FIPS&nbsp;(28&nbsp;May&nbsp;2019)|TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0xC0,&nbsp;0x30&nbsp;}|
|Ubuntu&nbsp;16.04.5&nbsp;LTS|Linux&nbsp;4.4.0-131-generic|OpenSSL&nbsp;1.0.2g&nbsp;(1&nbsp;Mar&nbsp;2016)|TLS_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0x00,&nbsp;0x9D&nbsp;}|
|Ubuntu&nbsp;18.10|Linux&nbsp;4.18.0-25-generic|OpenSSL&nbsp;1.1.1&nbsp;(11&nbsp;Sep&nbsp;2018)|TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0xC0,&nbsp;0x30&nbsp;}|
|Ubuntu&nbsp;20.04&nbsp;LTS|Linux&nbsp;5.4.0-52-generic|OpenSSL&nbsp;1.1.1f&nbsp;(31&nbsp;Mar&nbsp;2020)|TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0xC0,&nbsp;0x30&nbsp;}|
|SUSE&nbsp;Linux&nbsp;Enterprise&nbsp;Server&nbsp;12&nbsp;SP5|Linux&nbsp;4.12.14-120-default|OpenSSL&nbsp;1.0.2p-fips&nbsp;(14&nbsp;Aug&nbsp;2018)|TLS_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0x00,&nbsp;0x9D&nbsp;}|
|Debian&nbsp;GNU/Linux&nbsp;10&nbsp;(buster)|Linux&nbsp;4.19.0-13-amd64|OpenSSL&nbsp;1.1.1d&nbsp;(10&nbsp;Sep&nbsp;2019)|TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384|{&nbsp;0xC0,&nbsp;0x30&nbsp;}|

### Ciphers, MAC algorithms, and key exchange algorithms 

In System Center Operations Manager 2016 and later, the below ciphers, MAC algorithms, and key exchange algorithms are presented by the System Center Operations Manager SSH module.

**Ciphers offered by SCOM SSH module:**

- aes256-ctr 
- aes256-cbc 
- aes192-ctr 
- aes192-cbc 
- aes128-ctr 
- aes128-cbc 
- 3des-ctr 
- 3des-cbc 
 
**MAC algorithms offered by SCOM SSH module:**

- hmac-sha10 
- hmac-sha1-96 
- hmac-sha2-256 
 
**Key Exchange algorithms offered by SCOM SSH module:**

- diffie-hellman-group-exchange-sha256  
- diffie-hellman-group-exchange-sha1 
- diffie-hellman-group14-sha1 
- diffie-hellman-group14-sha256 
- diffie-hellman-group1-sha1 
- ecdh-sha2-nistp256 
- ecdh-sha2-nistp384 
- ecdh-sha2-nistp521 

::: moniker range=">=sc-om-2019"

## Disabled SSL renegotiations in Linux agent

For the Linux agent, SSL renegotiations are disabled.

SSL renegotiations might cause vulnerability in SCOM-Linux agent, which might make it easier for the remote attackers to cause a denial of service by performing many renegotiations within a single connection.  

Linux agent uses opensource OpenSSL for SSL purposes.

The following versions are supported for renegotiation only:

 - OpenSSL <= 1.0.2
 - OpenSSL >= 1.1.0h

For OpenSSL versions 1.10 - 1.1.0g, you can't disable renegotiation because OpenSSL doesn't support renegotiation.

::: moniker-end

## Next steps

- To understand how to authenticate and monitor your UNIX and Linux computers, review [Credentials You Must Have to Access UNIX and Linux Computers](plan-security-crossplat-credentials.md).

- To configure Operations Manager to authenticate with your UNIX and Linux computers, see [How to Set Credentials for Accessing UNIX and Linux Computers](manage-security-create-crossplat-credentials.md).  

- To understand how to elevate an unprivileged account for effective monitoring of UNIX and Linux computers, review [How to Configure sudo Elevation and SSH Keys](manage-security-create-crossplat-sudo-sshkeys.md). 
