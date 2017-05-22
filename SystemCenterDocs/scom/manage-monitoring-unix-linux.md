---
title: Monitoring UNIX and Linux Computers by Using Operations Manager
description: 
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 05/22/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 6afa5807-9393-4fc9-92c2-aa7427d72f2f
---

# Monitoring UNIX and Linux Computers by Using Operations Manager

>Applies To: System Center 2016 - Operations Manager

System Center 2016 - Operations Manager provides monitoring of UNIX and Linux computers similar to monitoring of Windows computers. You can monitor health, performance, obtain reports, run tasks, and implement custom monitoring instrumentation.  
  
You can monitor the following aspects of UNIX and Linux computers:  
  
-   Services and applications  
  
-   File system, disk space, swap space, system memory  
  
-   Network interfaces  
  
-   Core processes and attributes  
  
-   Key configurations  

Before you can monitor UNIX and Linux computers, you must complete the following steps:  

1. Import management packs for the by downloading the latest versions from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=29696)  
2. [Create a dedicated resource pool](manage-resource-pools-manage.md) for monitoring UNIX and Linux computers   
3. [Configure the certificates](manage-resource-pools-manage.md#configure-certificates-for- unix-and-linux-dedicated-resource-pools) for each management server in the pool  
4. Create and [configure Run As accounts](manage-security-create-crossplat-credentials.md)    
5. Install agent on UNIX and Linux using the [Discovery Wizard](manage-deploy-crossplat-agent-console.md)  

After you complete the steps above and successfully discover and deploy the agent to one or more UNIX and Linux computers, you should verify they are being monitored correctly.  After an agent is deployed, the Run As accounts are used to perform discoveries running using the applicable discovery rules, and then start monitoring.  After several minutes, under the Administration workspace, navigate to **Device Management\UNIX/Linux Computers**, and verify the computers are not listed as **Unknown**.  They should be discovered and showing the specific version of the OS and distro.   

By default, Operations Manager monitors the following operating system objects:

- Operating System 
- Logical disk 
- Network Adapters

You can provide additional monitoring and interaction capabilities with your managed UNIX and Linux computers by using the UNIX and Linux monitoring pack templates. For more information, see [UNIX or Linux Log File](https://technet.microsoft.com/library/hh457589.aspx) and [UNIX or Linux Process](https://technet.microsoft.com/library/hh457572.aspx) in the Authoring Guide.

## Troubleshooting UNIX and Linux monitoring
The following section provides information about issues that might occur with monitoring UNIX and Linux computers in Operations Manager.     

### Certificate Signing Error Message  
During the installation of UNIX/Linux agents, you might see the following error.  
  
```  
Event Type: Error  
Event Source: Cross Platform Modules  
Event Category: None  
Event ID: 256  
Date: 4/1/2009  
Time: 4:02:27 PM  
User: N/A  
Computer: COMPUTER1  
Description: Unexpected ScxCertLibException: Can't decode from base64  
; input data is:  
  
```  
  
This error occurs when the certificate signing module is called but the certificate itself is empty. This error can be caused by an SSH connection failure to the remote system.  
  
If you see this error, do the following:  
  
1.  Make sure that the SSH daemon on the remote host is running.  
  
2.  Make sure that you can open an SSH session with the remote host by using the credentials specified in the Discovery Wizard.  
  
3.  Make sure that the credentials specified in the Discovery Wizard have the required privileges for discovery. For more information see [Credentials You Must Have to Access UNIX and Linux Computers](plan-security-crossplat-credentials.md).  
  
### Certificate Name and Host Name do not Match  
The common name (CN) that is used in the certificate must match the fully qualified domain name (FQDN) that is resolved by Operations Manager.  If the CN does not match, you will see the following error when you run the Discovery Wizard:  
  
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
  
If the certificate was created with an incorrect name, you can change the host name and re-create the certificate and private key. To do this, run the following command on the UNIX or Linux computer:  
  
```  
/opt/microsoft/scx/bin/tools/scxsslconfig -f -v  
```  
  
The **-f** option forces the files in /etc/opt/microsoft/scx/ssl to be overwritten.  
  
You can also change the hostname and domain name on the certificate by using the **-h** and **-d** switches, as in the following example:  
  
```  
/opt/microsoft/scx/bin/tools/scxsslconfig -f -h <hostname> -d <domain.name>  
```  
  
Restart the agent by running the following command:  
  
```  
  
/opt/microsoft/scx/bin/tools/scxadmin -restart  
  
```  
  
**To add an entry to the hosts file:**  
  
If the FQDN is not in Reverse DNS, you can add an entry to the hosts file located on the management server to provide name resolution. The hosts file is located in the Windows\System32\Drivers\etc folder.  An entry in the hosts file is a combination of the IP address and the FQDN.  
  
For example, to add an entry for the host named "newhostname.newdomain.name" with an IP address of 192.168.1.1, add the following to the end of the hosts file:  
  
```  
192.168.1.1&nbsp;&nbsp;&nbsp;&nbsp; newhostname.newdomain.name  
```  

## Management pack issues

### ExecuteCommand Does Not Support Pipeline Operators or Aliases  
When you use an alias or a pipeline operator with the *ExecuteCommand* parameter, the command fails. The *ExecuteCommand* parameter does not support the pipeline operator, aliases, and shell-specific syntax.  
  
In System Center Operations Manager management packs that are designed to manage UNIX and Linux computers, the *ExecuteCommand* parameter does not start a shell process, causing the custom action to fail.  
  
For each of the following custom action types, you specify how the command arguments are invoked by using either the *ExecuteCommand* parameter or the *ExecuteShellCommand* parameter:  
  
-   Microsoft.Unix.WSMan.Invoke.ProbeAction  
  
-   Microsoft.Unix.WSMan.Invoke.WriteAction  
  
-   Microsoft.Unix.WSMan.Invoke.Privileged.ProbeAction  
  
-   Microsoft.Unix.WSMan.Invoke.Privileged.WriteAction  
  
The *ExecuteCommand* parameter passes the command\-line arguments to the console without starting a shell process.  
  
The *ExecuteShellCommand* parameter passes the command arguments to a shell process using the user's default shell; this shell supports pipeline, aliases, and shell-specific syntax.  
  
> [!NOTE]  
> The *ExecuteShellCommand* parameter uses the default shell of the user who is running the command. If you require a specific shell, use the *ExecuteCommand* parameter, and prefix the command arguments with the required shell.  
  
The following examples show how to use the *ExecuteCommand* and *ExecuteShellCommand* parameters:  
  
-   To pass the command-line arguments to the console without starting a shell process:  
  
    `<p:ExecuteCommand_INPUT xmlns:p="http://schemas.microsoft.com/wbem/wscim/1/cim-schema/2/SCX_OperatingSystem"> <p:Command> service syslog status </p:Command> <p:timeout>10</p:timeout> </p:ExecuteCommand_INPUT>`  
  
-   To pass the command-line arguments to a shell process that references an explicit shell:  
  
    `<p:ExecuteCommand_INPUT xmlns:p="http://schemas.microsoft.com/wbem/wscim/1/cim-schema/2/SCX_OperatingSystem"> <p:Command> /bin/sh ps -ef syslog | grep -v grep </p:Command> <p:timeout>10</p:timeout> </p:ExecuteCommand_INPUT>`  
  
-   To pass the command arguments to a shell process that uses the user's default shell:  
  
    `<p:ExecuteShellCommand_INPUT xmlns:p="http://schemas.microsoft.com/wbem/wscim/1/cim-schema/2/SCX_OperatingSystem"> <p:Command> uptime |&nbsp; awk '{print $10}' |awk -F"," '{print $1}' </p:Command> <p:timeout>10</p:timeout> </p:ExecuteShellCommand_INPUT>`  

## Logging and Debugging
This topic describes how to enable logging and debug tools for troubleshooting issues with monitoring UNIX and Linux computers.  
  
### Enable Operations Manager Module Logging  
The Operations Manager Agents for UNIX and Linux maintain several log files which can be useful when troubleshooting client issues. These log files are located on the managed UNIX or Linux computer The logging level for the agent log files can be configured as needed. More verbose logging can be useful in diagnosing an issue. For normal operation, log levels should not be set to a value more verbose than the default configurations (Intermediate) in order to prevent excessive log file growth  
  
> [!NOTE]  
> Calls made outside of Windows Remote Management (WinRM) are made using SSH/SFTP. These components rely on a separate logging mechanism than Operations Manager.  
  
> [!NOTE]  
> The logging level for the omiserver.log log file cannot be changed from the default in this version of the Operations Manager Agents for UNIX and Linux.  
  
1. Create a blank file named **EnableOpsmgrModuleLogging** in the Temp directory for the user account calling these modules by typing at a command-line prompt **COPY /Y NUL %windir%\TEMP\EnableOpsMgrModuleLogging**.  
  
    > [!NOTE]  
    > Generally, it is the SYSTEM account making the calls, and C:\Windows\Temp is the default SYSTEM temp folder.  
  
2. After creation of the blank file, Operations Manager will immediately begin logging SSH and Certificate activity to the Temp directory. Scripts that call into SSH modules will log to <*Scriptname.vbs*>.log. Other modules have their own logs.  
  
In some cases, it may be required to restart the HealthService to get the EnableOpsmgrModuleLogging logging to take effect.  
  
## Enable Logging on the UNIX Agent  
These logs will report the UNIX agent actions. If there is a problem with the data returned to Operations Manager, look in this log. You can set the amount of information logged with the scxadmin command. The syntax for this command is:  
  
`scxadmin -log-set [all|cimom|provider] {verbose|intermediate|errors}`  
  
The following table lists the possible parameter values:  
  
|Level|Description|  
|---------|---------------|  
|Errors|Log only **Warning** or **Error** messages.|  
|Intermediate|Log **Info**, **Warning** and **Error** messages.|  
|Verbose|Log **Info**, **Warning**, and **Error** messages with debug logging. Note that This level of logging is likely to cause rapid growth in the size of the log files.  It is strongly recommended that this option only be used for short periods of time to diagnose a specific issue.|  
  
### Use DebugView to Troubleshoot Discovery Issues  
DebugView is an alternative method to EnableOpsmgrModuleLogging for troubleshooting discovery issues.  
  
1.  Download DebugView from: [http://go.microsoft.comfwlink/?Linkid=129486](http://go.microsoft.com/fwlink/?Linkid=129486).  
  
2.  Launch DebugView on the Management Server performing the discovery.  
  
3.  Start discovering the UNIX Agents. You should start seeing output in your DebugView windows.  
  
4.  DebugView will present a step-by-step readout of the discovery wizard process. This is often the fastest method of troubleshooting discovery issues.  

### Enable Operations Manager Logging for Windows Remote Management  
This verbose tracing method is used to see the Windows Remote Management (WinRM) queries used by Operations Manager to gather data from the agent. If you suspect there is a problem with the WinRM connection, this log provides detailed information that can help with troubleshooting.  
  
1.  On the Management server that is monitoring the UNIX or Linux agent, open a command prompt.  
  
2.  Type the following commands at the command prompt:  
  
    1.  cd C:\Program Files\Microsoft System Center 2016\Operations Manager\Tools  
  
    2.  StopTracing.cmd  
  
    3.  StartTracing.cmd VER  
  
3.  Reproduce the failing issue in Operations Manager.  
  
4.  Type the following commands at the command prompt:  
  
    1.  StopTracing.cmd  
  
    2.  FormatTracing.cmd  
  
5.  Search for WS-Man in the TracingGuidsNative.log file.  
  
> [!NOTE]  
> WinRM is also known as WS-Management (WS-Man).  
  
> [!NOTE]  
> The FormatTracing command opens a Windows Explorer window displaying the c:\Windows\temp\OpsMgrTrace directory. The TracingGuidsNative.log file is in that directory. 

## Manage UNIX and Linux Log Files
The Operations Manager Agents for UNIX and Linux do not limit the size of the agent log files.  In order to control the maximum size of the log files, implement a process to manage the log files.  For example, the standard utility logrotate is available on many UNIX and Linux operating systems. The logrotate utility can be configured to control the log files used by the Operations Manager Agents for UNIX or Linux. After rotating or modifying the log files of the agent, the agent must be signaled that logs have rotated in order to resume logging.  The scxadmin command can be used with the -log\-rotate parameter with the following syntax:  
  
`scxadmin -log-rotate all`  
  
### Example Logrotate configuration file  
The following example demonstrates a configuration file to rotate the scx.log files as well as omiserver.log with the logrotate utility of Linux. Typically, logrotate will run as a scheduled job (with crond) and act on configuration files found in /etc/logrotate.d.  To test and use this configuration file, modify the configuration to be appropriate for your environment, and link or save the file in /etc/logrotate.d.  
  
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

## Next steps
For additional guidance to help resolve common agent deployment issues, review the [SCOM 2012 Troubleshooting: UNIX/Linux Agent Discovery  Wiki](https://social.technet.microsoft.com/wiki/contents/articles/4966.scom-2012-troubleshooting-unixlinux-agent-discovery.aspx#WSMan_Errors).