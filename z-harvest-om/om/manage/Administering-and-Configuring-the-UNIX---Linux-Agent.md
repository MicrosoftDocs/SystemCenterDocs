---
title: Administering and Configuring the UNIX - Linux Agent
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e68b45fd-a9b4-4767-9a79-cf1aee262109
author:mgoedtel
manager:cfreemanwa
---
# Administering and Configuring the UNIX - Linux Agent
This topic describes options to administer and configure the UNIX\/Linux agent for System Center - [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)].  
  
## Agent Directories  
  
-   The UNIX\/Linux agent installs to the directory: `/opt/microsoft/scx/`  
  
-   The UNIX\/Linux agent maintains log files in the directory: `/var/opt/microsoft/scx/log/`  
  
-   Agent configuration files, including certificates, are stored in the directory: `/etc/opt/microsoft/scx/`  
  
## Agent Administration Tools  
In this section, tools to administer and configure the UNIX\/Linux agent are described.  
  
### Running the Agent Administration Tools  
The tools for configuring the UNIX\/Linux Agent are located in the directory:  
  
```  
/opt/microsoft/scx/bin/tools  
```  
  
Prior to running the tools, the file `/opt/microsoft/scx/bin/tools/setup.sh` must be sourced. This can be done with the following command:  
  
```  
. /opt/microsoft/scx/bin/tools/setup.sh  
```  
  
## Scxadmin  
The **scxadmin** tool is used to control the state of the UNIX\/Linux agent \(start, stop, or restart\) as well as control logging performed by the agent.  The usage of the tool can be displayed with the following command: `scxadmin -?`  
  
```  
  
  # /opt/microsoft/scx/bin/tools/scxadmin -?  
  
Usage: scxadmin  
Generic options (for all commands)  
  [-quiet]      Set quiet mode (no output)  
  
        General Options  
scxadmin -version  
  
        Service Management  
scxadmin {-start|-stop|-restart|-status}  [all|cimom|provider]  
  
        Providers Management  
scxadmin -config-list {RunAs}  
scxadmin -config-set {RunAs} {CWD=<directory>|ChRootPath=<directory>|AllowRoot={true|false}}  
scxadmin -config-reset {RunAs} [CWD|ChRootPath|AllowRoot]  
  
        Log Configuration Management  
scxadmin {-log-list|-log-rotate|-log-reset} [all|cimom|provider]  
scxadmin -log-set [all|cimom|provider] {verbose|intermediate|errors}  
scxadmin -log-set provider {{FILE:<path>|STDOUT}:<module-id>={SUPPRESS|ERROR|WARNING|INFO|TRACE|HYSTERICAL}}  
scxadmin {-log-reset|-log-remove} provider [{FILE:<path>|STDOUT}]  
```  
  
### Examples  
**Restarting the agent:**  
  
```  
cd /opt/microsoft/scx/bin/tools/  
./scxadmin -restart  
```  
  
**Increase all logging to the Intermediate level:**  
  
```  
cd /opt/microsoft/scx/bin/tools/  
./scxadmin -log-set all intermediate  
```  
  
## scxsslconfig  
The **scxsslconfig** tool is used to generate the certificate in `/etc/opt/Microsoft/scx/ssl/`. This tool is useful in correcting issues in which the fully\-qualified domain name cannot be determined from the UNIX or Linux host itself, or the FQDN known to the UNIX\/Linux host does not match the FQDN used by the [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] server to reach the host.  
  
> [!NOTE]  
> The generated certificate must be signed by [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] in order to be used in WS\-Management communication.  Overwriting a previously signed certificate will require that the certificate be signed again.  
  
Usage for the **scxsslconfig** tool can be displayed with the following command: `scxsslconfig -?`  
  
```  
# /opt/microsoft/scx/bin/tools/scxsslconfig -?  
Usage: /opt/microsoft/scx/bin/tools/.scxsslconfig [-v] [-s days] [-e days] [-d domain] [-h host] [-g targetpath]  
  
-v             - toggle debug flag  
-g targetpath  - generate certificates in targetpath  
-s days        - days to offset valid start date with (0)  
-e days        - days to offset valid end date with (3650)  
-f             - force certificate to be generated even if one exists  
-d domain      - domain name  
-h host        - host name  
-b bits        - number of key bits  
-?             - this help message  
```  
  
### Examples  
**Regenerate the certificate, forcing overwrite of an existing certificate, with verbose output:**  
  
```  
cd /opt/microsoft/scx/bin/tools/  
. setup.sh  
/opt/microsoft/scx/bin/tools/scxsslconfig -f -v  
```  
  
**Regenerate the certificate, forcing overwrite of an existing certificate, with a specified hostname and DNS domain name:**  
  
```  
cd /opt/microsoft/scx/bin/tools/  
. setup.sh  
/opt/microsoft/scx/bin/tools/scxsslconfig -f -h myserver -d contoso.com  
```  
  
## Additional Configuration Topics  
  
### SSL Ciphers  
If required, the SSL cipher list used by the UNIX\/Linux agent can be customized. For more information about this configuration, see the [Configuring SSL Ciphers](https://technet.microsoft.com/library/hh528918.aspx) topic.  
  
### Universal Linux - Operating System Name\/Version  
The Universal Linux Agent, which supports Linux operating systems such as CentOS, Debian GNU\/Linux, Oracle Linux, and Ubuntu Server, parses release files to determine the host's operating system name and version. If required, these properties can be customized. To customize the operating system properties presented to [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)] for a Universal Linux Agent host, use the following procedure:  
  
Create the file `disablereleasefileupdates` in the directory: `/etc/opt/microsoft/scx/conf/`.  
  
```  
touch /etc/opt/microsoft/scx/conf/disablereleasefileupdates  
```  
  
If this file exists, the agent will not attempt to update the operating system properties that are returned to [!INCLUDE[omblue_2](../../om/manage/includes/omblue_2_md.md)]. This ensures that the customizations are preserved.  
  
Edit the file `scx-release` in the directory: `/etc/opt/microsoft/scx/conf`. This file has the format:  
  
```  
OSName=CentOS  
OSVersion=6.0  
OSFullName=CentOS 6.0 (x86_64)  
OSAlias=UniversalR  
OSManufacturer=  
```  
  
The values of the **OSName**, **OSVersion**, and **OSFullName** properties can be edited to reflect customized values.  
  
> [!NOTE]  
> The OSAlias property should not be edited. All properties in this file \(except for OSManufacturer\) are mandatory and should not be null.  
  
## See Also  
[Managing Discovery and Agents](../Topic/Managing%20Discovery%20and%20Agents.md)  
[Accessing UNIX and Linux Computers in Operations Manager](../../om/manage/Accessing-UNIX-and-Linux-Computers-in-Operations-Manager.md)  
  
