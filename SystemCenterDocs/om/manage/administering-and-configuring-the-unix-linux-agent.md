---
title: Administering and Configuring the UNIX - Linux Agent
description:
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-12
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Administering and Configuring the UNIX - Linux Agent

This topic describes options to administer and configure the UNIX/Linux agent for System Center 2016 - Operations Manager.  
  
## Agent Directories  

-  Open Management Infrastructure (OMI) is installed to the directory: `/opt/omi`

-  The UNIX/Linux agent installs to the directory: `/opt/microsoft/scx/`

-  The UNIX/Linux agent maintains log files in the directory: `/var/opt/microsoft/scx/log/`

-  OMI maintains log files in the directory: `/var/opt/omi/log/`

-  Agent configuration files, including certificates, are stored in the directory: `/etc/opt/microsoft/scx/`

-  OMI configuration files are stored in the directory: `/etc/opt/omi`

  
## Agent administration tools  

In this section, tools to administer and configure the UNIX\/Linux agent are described.  
  
### Running the agent administration tools  

The tools for configuring the UNIX/Linux Agent are located in the directory:  
  
```  
/opt/microsoft/scx/bin/tools  
```    
  
## Scxadmin  

The **scxadmin** tool is used to control the state of the UNIX/Linux agent (start, stop, or restart) as well as control logging performed by the agent.  The usage of the tool can be displayed with the following command: `scxadmin -?`  
  
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
./scxadmin –log-set all intermediate
```  
  
**Increase all logging to the Intermediate level:**  
  
```  
cd /opt/microsoft/scx/bin/tools/
./scxadmin –log-set all intermediate 
```  
  
## scxsslconfig  

The **scxsslconfig** tool is used to generate the certificate in `/etc/opt/Microsoft/scx/ssl/`. This tool is useful in correcting issues in which the fully\-qualified domain name cannot be determined from the UNIX or Linux host itself, or the FQDN known to the UNIX\/Linux host does not match the FQDN used by the management server to reach the host.  
  
> [!NOTE]  
> The generated certificate must be signed by Operations Manager management server in order to be used in WS-Management communication.  Overwriting a previously signed certificate will require that the certificate be signed again.  
  
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
  
## Additional configuration topics  
  
### SSL Ciphers 
 
If required, the SSL cipher list used by the UNIX/Linux agent can be customized. For more information about this configuration, see the [Configuring SSL Ciphers](configuring-ssl-ciphers.md) topic.  
  
### Specifying an alternate temporary path for scripts

If you create a UNIX/Linux Script rule or monitor in a custom management pack, the script contents will be written to a file in /tmp on the agent computer before being run. You may wish to specify an alternate directory for script execution. To specify an alternate directory, overwrite the symbolic link at: `/etc/opt/microsoft/scx/conf/tmpdir` to point to another directory. The destination of this symbolic link must be writeable by the user account defined in the UNIX/Linux Action Account and/or UNIX/Linux Privileged Account RunAs Profiles. 

### Universal Linux - Operating System Name/Version  

The Universal Linux Agent, which supports Linux operating systems such as CentOS, Debian GNU\/Linux, Oracle Linux, and Ubuntu Server, parses release files to determine the host's operating system name and version. If required, these properties can be customized. To customize the operating system properties presented to Operations Manager for a Universal Linux Agent host, use the following procedure:  
  
Create the file `disablereleasefileupdates` in the directory: `/etc/opt/microsoft/scx/conf/`.  
  
```  
touch /etc/opt/microsoft/scx/conf/disablereleasefileupdates  
```  
  
If this file exists, the agent will not attempt to update the operating system properties that are returned to Operations Manager. This ensures that the customizations are preserved.  
  
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
> The OSAlias property should not be edited. All properties in this file (except for OSManufacturer) are mandatory and should not be null.  
  
## Next steps

- For more information on how to install the agent and understand the steps for signing the agent certificate, see [Install Agent and Certificate on UNIX and Linux Computers Using the Command Line](Install-Agent-and-Certificate-on-UNIX-and-Linux-Computers-Using-the-Command-Line.md)

- To understand how to perform agent maintenance on UNIX and Linux computers, see [Upgrading and Uninstalling Agents on UNIX and Linux Computers](Upgrading-and-Uninstalling-Agents-on-UNIX-and-Linux-Computers.md)

  
