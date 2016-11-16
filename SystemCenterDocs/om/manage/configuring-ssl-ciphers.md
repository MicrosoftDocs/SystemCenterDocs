---
ms.assetid: 8b01d791-e5b9-475a-b789-6162e6120397
title: Configuring SSL Ciphers
description: This article describes how to configure SSL encrypted communication for UNIX and Linux computers and Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Configuring SSL ciphers

>Applies To: System Center 2016 - Operations Manager

System Center 2016 - Operations Manager correctly manages UNIX and Linux computers without changes to the default Secure Sockets Layer (SSL) cipher configuration. For most organizations, the default configuration is acceptable, but you should check your organization's security policies to determine whether changes are required.  
  
## Using the SSL cipher configuration  

The Operations Manager UNIX and Linux agent communicates with the Operations Manager management server by accepting requests on port 1270 and supplying information in response to those requests. Requests are made by using the WS-Management protocol that is running on an SSL connection.  
  
When the SSL connection is first established for each request, the standard SSL protocol negotiates the encryption algorithm, known as a cipher for the connection to use. For Operations Manager, the management server always negotiates to use a high strength cipher so that strong encryption is used on the network connection between the management server and the UNIX or Linux computer.  
  
The default SSL cipher configuration on UNIX or Linux computer is governed by the SSL package that is installed as part of the operating system. The SSL cipher configuration typically allows connections with a variety of ciphers, including older ciphers of lower strength. While Operations Manager does not use these lower strength ciphers, having port 1270 open with the possibility of using a lower strength cipher contradicts the security policy of some organizations.  
  
If the default SSL cipher configuration meets your organization's security policy, no action is needed.  
  
If the default SSL cipher configuration contradicts your organization's security policy, the Operations Manager UNIX and Linux agent provides a configuration option to specify the ciphers that SSL can accept on port 1270. This option can be used to control the ciphers and bring the SSL configuration into conformance with your policies. After the Operations Manager UNIX and Linux agent is installed on each managed computer, the configuration option must be set by using the procedures described in the next section. Operations Manager does not provide any automatic or built-in way to apply these configurations; each organization must perform the configuration by using an external mechanism that works best for it.  
  
### Setting the sslCipherSuite configuration option for System Center 2016 

The SSL ciphers for port 1270 are controlled by setting the **sslciphersuite** option in the OMI configuration file, **omiserver.conf**. The **omiserver.conf** file is located in the directory `/etc/opt/omi/conf/`.  
  
The format for the sslciphersuite option in this file is:  
  
```  
sslciphersuite=<cipher spec>  
```  
  
where <cipher spec> specifies the ciphers that are allowed, disallowed, and the order in which allowed ciphers are chosen.  
  
The format for <cipher spec> is the same as the format for the **sslCipherSuite** option in the Apache HTTP Server version 2.0. For detailed information, see [SSLCipherSuite Directive](http://go.microsoft.com/fwlink/?LinkId=318052) in the Apache documentation. All information on this site is provided by the owner or the users of the website. Microsoft makes no warranties, express, implied or statutory, as to the information at this website.  
  
After setting the **sslCipherSuite** configuration option, you must restart the UNIX and Linux agent for the change to take effect. To restart the UNIX and Linux agent, run the following command, which is located in the **/etc/opt/microsoft/scx/bin/tools** directory.  
  
```  
. setup.sh  
scxadmin -restart  
```  

### Enabling or Disabling the SSLv3 Protocol

Operations Manager communicates with UNIX and Linux agents over HTTPS, using either TLS or SSL encryption. The SSL handshaking process negotiates the strongest encryption that is mutually available on the agent and the management server. You may wish to prohibit SSLv3 so that an agent that cannot negotiate TLS encryption does not fall back to SSLv3. 

For System Center 2016 – Operations Manager, omiserver.conf is located at: 
`/etc/opt/omi/conf/omiserver.conf`

#### To disable SSLv3

Modify omiserver.conf, set the **NoSSLv3** line to be: 
`NoSSLv3=true`

#### To enable SSLv3

Modify omiserver.conf, set the **NoSSLv3** line to be: 
`NoSSLv3=false`

  
## Next steps

- To understand how to authenticate and monitor your UNIX and Linux computers, review [Credentials You Must Have to Access UNIX and Linux Computers](../plan/planning-security-credentials-for-accessing-unix-and-linux-computers.md)

- To configure Operations Manager to authenticate with your UNIX and Linux computers, please see [How to Set Credentials for Accessing UNIX and Linux Computers](How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md)  

- To understand how to elevate an unprivileged account for effective monitoring of UNIX and Linux computers, review [How to Configure sudo Elevation and SSH Keys](How-to-Configure-sudo-Elevation-and-SSH-Keys.md)  

  
  
