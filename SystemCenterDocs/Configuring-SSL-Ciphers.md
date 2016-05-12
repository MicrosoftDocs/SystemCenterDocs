---
title: Configuring SSL Ciphers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fadc6ff-e37c-4c2f-a58a-d7841b39f114
---
# Configuring SSL Ciphers
[!INCLUDE[om12long](Token/om12long_md.md)] correctly manages UNIX and Linux computers without changes to the default Secure Sockets Layer \(SSL\) cipher configuration. For most organizations, the default configuration is acceptable, but you should check your organization’s security policies to determine whether changes are required.

## Using the SSL Cipher Configuration
The [!INCLUDE[om12short](Token/om12short_md.md)] UNIX and Linux agent communicates with the [!INCLUDE[om12short](Token/om12short_md.md)] management server by accepting requests on port 1270 and supplying information in response to those requests. Requests are made by using the WS\-Management protocol that is running on an SSL connection.

When the SSL connection is first established for each request, the standard SSL protocol negotiates the encryption algorithm, known as a cipher for the connection to use. For [!INCLUDE[om12short](Token/om12short_md.md)], the management server always negotiates to use a high strength cipher so that strong encryption is used on the network connection between the management server and the UNIX or Linux computer.

The default SSL cipher configuration on UNIX or Linux computer is governed by the SSL package that is installed as part of the operating system. The SSL cipher configuration typically allows connections with a variety of ciphers, including older ciphers of lower strength. While [!INCLUDE[om12short](Token/om12short_md.md)] does not use these lower strength ciphers, having port 1270 open with the possibility of using a lower strength cipher contradicts the security policy of some organizations.

If the default SSL cipher configuration meets your organization’s security policy, no action is needed.

If the default SSL cipher configuration contradicts your organization’s security policy, the [!INCLUDE[om12short](Token/om12short_md.md)] UNIX and Linux agent provides a configuration option to specify the ciphers that SSL can accept on port 1270. This option can be used to control the ciphers and bring the SSL configuration into conformance with your policies. After the [!INCLUDE[om12short](Token/om12short_md.md)] UNIX and Linux agent is installed on each managed computer, the configuration option must be set by using the procedures described in the next section. [!INCLUDE[om12short](Token/om12short_md.md)] does not provide any automatic or built\-in way to apply these configurations; each organization must perform the configuration by using an external mechanism that works best for it.

### Setting the sslCipherSuite Configuration Option for System Center 2012 R2
The SSL ciphers for port 1270 are controlled by setting the **sslciphersuite** option in the OMI configuration file, **omiserver.conf**. The **omiserver.conf** file is located in the directory \/etc\/opt\/microsoft\/scx\/conf\/.

The format for the sslciphersuite option in this file is:

```
sslciphersuite=<cipher spec>
```

where <cipher spec> specifies the ciphers that are allowed, disallowed, and the order in which allowed ciphers are chosen.

The format for <cipher spec> is the same as the format for the **sslCipherSuite** option in the Apache HTTP Server version 2.0. For detailed information, see [SSLCipherSuite Directive](http://go.microsoft.com/fwlink/?LinkId=318052) in the Apache documentation. All information on this site is provided by the owner or the users of the website. Microsoft makes no warranties, express, implied or statutory, as to the information at this website.

After setting the **sslCipherSuite** configuration option, you must restart the UNIX and Linux agent for the change to take effect. To restart the UNIX and Linux agent, run the following command, which is located in the **\/etc\/opt\/microsoft\/scx\/bin\/tools** directory.

```
. setup.sh
scxadmin -restart
```

### Setting the sslCipherSuite Configuration Option for System Center 2012 SP1 and System Center 2012
The SSL ciphers for port 1270 are controlled by setting the **sslCipherSuite** option by using the **scxcimconfig** command, which is installed as part of the [!INCLUDE[om12short](Token/om12short_md.md)] UNIX and Linux agent in the **\/etc\/opt\/microsoft\/scx\/bin\/tools** directory. To view the full Help, at the command prompt, type  the following command.

```
scxcimconfig –-help
```

To set the **sslCipherSuite** configuration option, the following syntax shows a typical command.

```
scxcimconfig –s sslCipherSuite='<cipher spec>' –p
```

where `<cipher spec>` specifies the ciphers that are allowed, disallowed, and the order in which allowed ciphers are chosen.

The format for `<cipher spec>` is the same as the format for the **sslCipherSuite** option in the Apache HTTP Server version 2.0. For detailed information, see [SSLCipherSuite Directive](http://go.microsoft.com/fwlink/?LinkId=318052) in the Apache documentation. All information on this site is provided by the owner or the users of the website. Microsoft makes no warranties, express, implied or statutory, as to the information at this website.

After setting the **sslCipherSuite** configuration option, you must restart the UNIX and Linux agent for the change to take effect. To restart the UNIX and Linux agent, run the following command, also located in the **\/etc\/opt\/microsoft\/scx\/bin\/tools** directory.

```
scxadmin -restart
```

## See Also
[How to Set Credentials for Accessing UNIX and Linux Computers](How-to-Set-Credentials-for-Accessing-UNIX-and-Linux-Computers.md)
[Accessing UNIX and Linux Computers in Operations Manager](Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)
[How to Configure sudo Elevation and SSH Keys](How-to-Configure-sudo-Elevation-and-SSH-Keys.md)
[Required Capabilities for UNIX and Linux Accounts](Required-Capabilities-for-UNIX-and-Linux-Accounts.md)
[Credentials You Must Have to Access UNIX and Linux Computers](Credentials-You-Must-Have-to-Access-UNIX-and-Linux-Computers.md)


