---
title: Manage UNIX and Linux Log Files
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 350e272b-7cb8-4364-9278-1fe685c953a3
author:mgoedtel
manager:cfreemanwa
---
# Manage UNIX and Linux Log Files
The Operations Manager Agents for UNIX and Linux do not limit the size of the agent log files.  In order to control the maximum size of the log files, implement a process to manage the log files.  For example, the standard utility logrotate is available on many UNIX and Linux operating systems. The logrotate utility can be configured to control the log files used by the Operations Manager Agents for UNIX or Linux. After rotating or modifying the log files of the agent, the agent must be signaled that logs have rotated in order to resume logging.  The scxadmin command can be used with the -log\-rotate parameter with the following syntax:  
  
`scxadmin -log-rotate all`  
  
## Example Logrotate configuration file  
The following example demonstrates a configuration file to rotate the scx.log files as well as omiserver.log with the logrotate utility of Linux. Typically, logrotate will run as a scheduled job \(with crond\) and act on configuration files found in \/etc\/logrotate.d.  To test and use this configuration file, modify the configuration to be appropriate for your environment, and link or save the file in \/etc\/logrotate.d.  
  
\#opsmgr.lr  
  
\#Rotate scx.log  
  
\#Weekly rotation, retain 4 weeks of compressed logs  
  
\#Invoke scxadmin \-log\-rotate to resume logging after rotation  
  
\/var\/opt\/microsoft\/scx\/log\/scx.log {  
  
rotate 4  
  
weekly  
  
compress  
  
missingok  
  
notifempty  
  
postrotate  
  
\/usr\/sbin\/scxadmin \-log\-rotate all  
  
endscript  
  
}\#Rotate scx.log for the monitoring user account named: monuser  
  
\#Weekly rotation, retain 4 weeks of compressed logs  
  
\#Invoke scxadmin \-log\-rotate to resume logging after rotation  
  
\/var\/opt\/microsoft\/scx\/log\/monuser\/scx.log {  
  
rotate 4  
  
weekly  
  
compress  
  
missingok  
  
notifempty  
  
postrotate  
  
\/usr\/sbin\/scxadmin \-log\-rotate all  
  
endscript  
  
}  
  
\#Optionally, rotate omiserver.log. This requires that OMI be stopped and started to prevent  
  
\#impact to logging. Monthly rotation, retain 2 weeks of compressed logs  
  
\#Uncomment these lines if rotation of omiserver.log is needed  
  
\#\/var\/opt\/microsoft\/scx\/log\/omiserver.log{  
  
\#        rotate 2  
  
\#        monthly  
  
\#        compress  
  
\#        missingok  
  
\#        notifempty  
  
\#        prerotate  
  
\#        \/usr\/sbin\/scxadmin \-stop  
  
\#        endscript  
  
\#        postrotate  
  
\#        \/usr\/sbin\/scxadmin \-start  
  
\#        endscript\#}  
  
