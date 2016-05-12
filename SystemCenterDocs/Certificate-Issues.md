---
title: Certificate Issues
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: af71b0c9-c9c4-4790-8511-513658bec529
---
# Certificate Issues
This topic describes resolutions to certificate issues for monitoring UNIX or Linux computers.

## Certificate Signing Error Message
During the installation of UNIX\/Linux agents, you might see the following error.

```
Event Type:        Error
Event Source:    Cross Platform Modules
Event Category:                None
Event ID:              256
Date:                     4/1/2009
Time:                     4:02:27 PM
User:                     N/A
Computer:          COMPUTER1
Description:
Unexpected ScxCertLibException: Can't decode from base64
; input data is:

```

This error occurs when the certificate signing module is called but the certificate itself is empty. This error can be caused by an SSH connection failure to the remote system.

If you see this error, do the following:

1.  Make sure that the SSH daemon on the remote host is running.

2.  Make sure that you can open an SSH session with the remote host by using the credentials specified in the Discovery Wizard.

3.  Make sure that the credentials specified in the Discovery Wizard have the required privileges for discovery. For more information see [Required Capabilities for UNIX and Linux Accounts](Required-Capabilities-for-UNIX-and-Linux-Accounts.md).

## Certificate Name and Host Name do not Match
The common name \(CN\) that is used in the certificate must match the fully qualified domain name \(FQDN\) that is resolved by Operations Manager.  If the CN does not match, you will see the following error when you run the Discovery Wizard:

```
The SSL certificate contains a common name (CN) that does not match the hostname
```

You can view the basic details of the certificate on the UNIX or Linux computer by entering the following command:

```
openssl x509 -noout -in /etc/opt/microsoft/scx/ssl/scx.pem -subject -issuer -dates
```

When you do this, you will see output that is similar to the following:

```
subject= /DC=name/DC=newdomain/CN=newhostname/CN=newhostname.newdomain.name
issuer= /DC=name/DC=newdomain/CN=newhostname/CN=newhostname.newdomain.name
notBefore=Mar 25 05:21:18 2008 GMT
notAfter=Mar 20 05:21:18 2029 GMT

```

Validate the hostnames and dates and ensure that they match the name being resolved by the Operations Manager management server.

If the hostnames do not match, use one of the following actions to resolve the issue:

-   If the UNIX or Linux hostname is correct but the Operations Manager management server is resolving it incorrectly, either modify the DNS entry to match the correct FQDN or add an entry to the hosts file on the Operations Manager server.

-   If the UNIX or Linux hostname is incorrect, do one of the following:

    -   Change the hostname on the UNIX or Linux host to the correct one and create a new certificate.

    -   Create a new certificate with the desired hostname.

**To Change the Name on the Certificate:**

If the certificate was created with an incorrect name, you can change the host name and re\-create the certificate and private key. To do this, run the following command on the UNIX or Linux computer:

```
/opt/microsoft/scx/bin/tools/scxsslconfig -f -v
```

The **–f** option forces the files in \/etc\/opt\/microsoft\/scx\/ssl to be overwritten.

You can also change the hostname and domain name on the certificate by using the **–h** and **–d** switches, as in the following example:

```
/opt/microsoft/scx/bin/tools/scxsslconfig -f -h <hostname> -d <domain.name>
```

Restart the agent by running the following command:

```

/opt/microsoft/scx/bin/tools/scxadmin -restart

```

**To add an entry to the hosts file:**

If the FQDN is not in Reverse DNS, you can add an entry to the hosts file located on the management server to provide name resolution. The hosts file is located in the \\Windows\\System32\\Drivers\\etc folder.  An entry in the hosts file is a combination of the IP address and the FQDN.

For example, to add an entry for the host named “newhostname.newdomain.name” with an IP address of 192.168.1.1, add the following to the end of the hosts file:

```
192.168.1.1     newhostname.newdomain.name
```

## See Also
[Using Templates for Additional Monitoring of UNIX and Linux](Using-Templates-for-Additional-Monitoring-of-UNIX-and-Linux.md)
[Troubleshooting UNIX and Linux Monitoring](Troubleshooting-UNIX-and-Linux-Monitoring.md)
[Accessing UNIX and Linux Computers in Operations Manager](Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)
[Required Capabilities for UNIX and Linux Accounts](Required-Capabilities-for-UNIX-and-Linux-Accounts.md)
[Management Pack Issues](Management-Pack-Issues.md)
[Operating System Issues](Operating-System-Issues.md)
[Logging and Debugging](Logging-and-Debugging.md)
[Managing Certificates for UNIX and Linux Computers](Managing-Certificates-for-UNIX-and-Linux-Computers.md)
[Managing Resource Pools for UNIX and Linux Computers](Managing-Resource-Pools-for-UNIX-and-Linux-Computers.md)
[Install Agent on UNIX and Linux Using the Discovery Wizard](Install-Agent-on-UNIX-and-Linux-Using-the-Discovery-Wizard.md)


