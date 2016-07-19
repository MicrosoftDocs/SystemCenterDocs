---
title: How to Enable Event Logging and ACS Rules on Solaris and AIX Computers
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 816c9151-eb03-4dca-9829-fed400c0524e
author:mgoedtel
manager:cfreemanwa
---
# How to Enable Event Logging and ACS Rules on Solaris and AIX Computers
This topic does not apply to Windows computers.  
  
By default, Solaris and AIX computers do not log audit events. The logging configuration is controlled by the file located at \/etc\/syslog.conf. You must make edits to this file and then enable ACS rules.  
  
### To Configure the Solaris Syslog  
  
1.  Add the following code to the syslog.conf file:  
  
    `auth.info;local2.info                                        /var/log/authlog`  
  
    > [!NOTE]  
    > Use the TAB key to separate log components from the log file names. Spaces do not work.  
  
2.  Restart the Syslog daemon.  
  
3.  On Solaris 5.8 and 5.9, enter the following commands:  
  
    `/etc/init.d/syslog stop`  
  
    `/etc/init.d/syslog start`  
  
    On Solaris 5.10, enter the following commands:  
  
    `svcadm refresh svc:/system/system-log`  
  
You now must enable the ACS rules.  
  
### To Configure the AIX Syslog  
  
1.  Add the following code to the syslog.conf file:  
  
    `*.info  /var/log/syslog.log   rotate size 1m files 10`  
  
    The Syslog file is rotated when it becomes larger than 1 megabyte \(MB\) and the number of rotated files is limited to 10.  
  
    > [!NOTE]  
    > Use the TAB key to separate log components from the log file names. Spaces do not work.  
  
2.  Enter the following command to refresh the computer’s configuration:  
  
    `# refresh –s syslogd`  
  
You now must enable the ACS rules.  
  
### To Enable ACS Rules  
  
1.  In the **Operations** console, click **Authoring**.  
  
2.  In the navigation pane, click **Authoring**, click **Management Pack Objects**, and then click **Rules**.  
  
3.  In the rules pane, search for the rule to be enabled. If the **Look for** bar is not available above the **Rule** list, navigate from the **View** menu, and then click **Find**.  
  
4.  Right\-click the rule name for the rule that you want to enable, navigate to **Overrides** , click **Override the Rule**, and then click **For all object of class** for a class of objects to be monitored by the rule.  
  
5.  Set the **Enabled** parameter to **True**, modify the **Override Value** to **True**, and then click **OK**.  
  
## See Also  
[Collecting Security Events Using Audit Collection Services in Operations Manager](../../om/manage/Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)  
[How to Configure Certficates for ACS Collector and Forwarder](../../om/manage/How-to-Configure-Certficates-for-ACS-Collector-and-Forwarder.md)  
[Audit Collection Services Capacity Planning](../../om/manage/Audit-Collection-Services-Capacity-Planning.md)  
[Audit Collection Services Performance Counters](../../om/manage/Audit-Collection-Services-Performance-Counters.md)  
[How to Enable Audit Collection Services &#40;ACS&#41; Forwarders](../../om/manage/How-to-Enable-Audit-Collection-Services--ACS--Forwarders.md)  
[Audit Collection Services Security](../../om/manage/Audit-Collection-Services-Security.md)  
[How to Filter ACS Events for UNIX and Linux Computers](../../om/manage/How-to-Filter-ACS-Events-for-UNIX-and-Linux-Computers.md)  
[Monitoring Audit Collection Services Performance](../../om/manage/Monitoring-Audit-Collection-Services-Performance.md)  
[How to Remove Audit Collection Services &#40;ACS&#41;](../../om/manage/How-to-Remove-Audit-Collection-Services--ACS-.md)  
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../../om/manage/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)  
  
