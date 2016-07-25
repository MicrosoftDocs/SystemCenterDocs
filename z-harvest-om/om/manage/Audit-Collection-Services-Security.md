---
title: Audit Collection Services Security
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52b248df-6ce7-4553-be57-c1e94ba9bd2c
author:mgoedtel
manager:cfreemanwa
---
# Audit Collection Services Security
In [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], Audit Collection Services \(ACS\) requires mutual authentication between the ACS collector and each ACS forwarder. By default, Windows authentication, which uses the Kerberos protocol, is used for this authentication. After authentication is complete, all transmissions between ACS forwarders and the ACS collector are encrypted. You do not need to enable additional encryption between ACS forwarders and the ACS collector unless they belong to different Active Directory forests that have no established trusts.  
  
By default, data is not encrypted between the ACS collector and the ACS database. If your organization requires a higher level of security, you can use Secure Sockets Layer \(SSL\) or Transport Layer Security \(TLS\) to encrypt all communication between these components. To enable SSL encryption between the ACS database and the ACS collector, you need to install a certificate on both the database server and the computer hosting the ACS Collector service. After these certificates are installed, configure the SQL client on the ACS collector to force encryption.  
  
For more information about installing certificates and enabling SSL or TLS, see  [SSL and TLS in Windows Server&nbsp;2003](http://go.microsoft.com/fwlink/?LinkId=76134) and  [Obtaining and installing server certificates](http://go.microsoft.com/fwlink/?LinkId=76135). For a list of the steps to force encryption on a SQL client, see [How to enable SSL encryption for SQL Server 2000 if you have a valid Certificate Server](http://go.microsoft.com/fwlink/?LinkId=76136).  
  
## Limited Access to Audit Events  
Audit events that are written to a local Security log can be accessed by the local administrator, but audit events that are handled by ACS, by default, do not allow users \(even users with administrative rights\) to access audit events in the ACS database. If you need to separate the role of an administrator from the role of a user who views and queries the ACS database, you can create a group for database auditors and then assign that group the necessary permissions to access the audit database. For step\-by\-step instructions, see [How to Deploy Audit Collection Services \(ACS\)](assetId:///7686cf46-0792-4057-8d47-920063fc8928).  
  
## Limited Communication for ACS Forwarders  
Configuration changes to the ACS forwarder are not allowed locally, even from user accounts that have the rights of an administrator. All configuration changes to an ACS forwarder must come from the ACS collector. For additional security, after the ACS forwarder authenticates with the ACS collector, it closes the inbound TCP port used by ACS so that only outgoing communication is allowed. The ACS collector must terminate and then reestablish a communication channel to make any configuration changes to an ACS forwarder.  
  
## ACS Forwarders Separated from the ACS Collector by a Firewall  
Because of the limited communication between an ACS forwarder and an ACS collector you only need to open the inbound TCP port 51909 on a firewall to enable an ACS forwarder, separated from your network by a firewall, to reach the ACS collector.  
  
## See Also  
[Collecting Security Events Using Audit Collection Services in Operations Manager](../../om/manage/Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)  
[How to Configure Certficates for ACS Collector and Forwarder](../../om/manage/How-to-Configure-Certficates-for-ACS-Collector-and-Forwarder.md)  
[Audit Collection Services Capacity Planning](../../om/manage/Audit-Collection-Services-Capacity-Planning.md)  
[Audit Collection Services Performance Counters](../../om/manage/Audit-Collection-Services-Performance-Counters.md)  
[How to Enable Audit Collection Services &#40;ACS&#41; Forwarders](../../om/manage/How-to-Enable-Audit-Collection-Services--ACS--Forwarders.md)  
[How to Enable Event Logging and ACS Rules on Solaris and AIX Computers](../../om/manage/How-to-Enable-Event-Logging-and-ACS-Rules-on-Solaris-and-AIX-Computers.md)  
[How to Filter ACS Events for UNIX and Linux Computers](../../om/manage/How-to-Filter-ACS-Events-for-UNIX-and-Linux-Computers.md)  
[Monitoring Audit Collection Services Performance](../../om/manage/Monitoring-Audit-Collection-Services-Performance.md)  
[How to Remove Audit Collection Services &#40;ACS&#41;](../../om/manage/How-to-Remove-Audit-Collection-Services--ACS-.md)  
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)  
  
