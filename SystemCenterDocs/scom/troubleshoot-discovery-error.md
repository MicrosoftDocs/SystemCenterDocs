---
ms.assetid: 
title: Troubleshoot discovery error - Azure Linux and Arc Linux machines are unsupported
description: This article describes how to resolve an error indicating Azure Linux is unsupported in System Center Operations Manager 2025.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 04/09/2025
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Troubleshoot discovery error - Azure Linux and Arc Linux machines are unsupported

This article describes how to resolve an error indicating Azure Linux is unsupported in System Center Operations Manager 2025.

**Issue**: In System Center Operations Manager 2025, you may encounter an error when you attempt to discover Linux machines running in Azure. 

Error message - **Azure Linux and Arc Linux Machines are unsupported**.

:::image type="content" source="media/troubleshoot-discovery-error/error-message.png" alt-text="Screenshot of error message.":::

>[!NOTE]
>This workaround applies only to System Center Operations Manager 2025. If you encounter this error in SCOM Managed Instance, see [Monitor Linux machines](/azure/azure-monitor/scom-manage-instance/monitor-linux-machines) as monitoring of Azure Linux VMs is not supported on SCOM Managed Instance.

**Workaround**:

To resolve this error, do the following on all Management Servers in the Linux Resource Pools: 

1. Copy the following script and replace with the contents of the *GetOSVersion.sh* file located in the UnixAgents directory - `C:\Program Files\Microsoft System Center\ Operations Manager\Server\AgentManagement\UnixAgents\`.

     ```
     Hostname=`uname -n`
     OSName=`uname -s`
     Version=`uname -r`  # Version command for Unix; For Linux we look in /etc/issue
     Arch=`uname -m`     # Overridden as uname -p on some platforms
     OSAlias="Unknown"   # OSAlias is used by discovery wizard
     IsLinux="false"     # Used by the discovery wizard for workflow
     ReleaseFile=`echo $PLATFORM_RELEASE_FILE_SCX_INSTALLER_INPUT`
     EtcPath="/etc"
 
     ## Function used to get Linux Distro and Version
     ######################################################################
     GetKitType() {
         # The os-release file doesn't tell us the type of kit, so try to determine
         if [ `rpm -q rpm 2> /dev/null | /bin/egrep '^rpm-[0-9].*' | wc -l` = 1 ]; then
             OSAlias="UniversalR"
         elif [ `dpkg -l dpkg 2> /dev/null | egrep "^ii.*"| wc -l` = 1 ]; then
             OSAlias="UniversalD"
         else
             OSAlias="Universal?"
         fi
     }
 
     GetLinuxInfo() {
         IsLinux="true"
 
         # Return kernel version as OS version - will be updated for specific cases below
         Version=`uname -r | cut -d. -f1,2`
 
         # Determine release file
 
         # Try to find -release file
         if [ -z ${ReleaseFile} ]; then 
             ReleaseFile=`ls -F ${EtcPath}/*-release 2>/dev/null | grep -v lsb-release |grep -v release@| grep -v scx-release| sed -n '1p'`
         fi
 
         # Fall back to lsb-release (e.g. Ubunutu)
         if [ -z ${ReleaseFile} ]; then 
             if [ -e "${EtcPath}/lsb-release" ]; then ReleaseFile="${EtcPath}/lsb-release"; fi
         fi
 
         # Debian (no lsb-release, but debian_version exists)
         if [ -z ${ReleaseFile} ]; then 
             TestFile="${EtcPath}/debian_version"
             if [ -e $TestFile ]; then ReleaseFile=$TestFile; fi
         fi
 
         # Try RHEL/CentOS
         TestFile="${EtcPath}/redhat-release"
         if [ ! -h $TestFile -a -e $TestFile ]; then ReleaseFile=$TestFile; fi
 
         # Try OEL
         TestFile="${EtcPath}/oracle-release"
         if [ ! -h $TestFile -a -e $TestFile ]; then ReleaseFile=$TestFile; fi
 
         # Try NeoKylin
         TestFile="${EtcPath}/neokylin-release"
         if [ ! -h $TestFile -a -e $TestFile ]; then ReleaseFile=$TestFile; fi
 
         # Try SLES
         TestFile="${EtcPath}/SuSE-release"
         if [ ! -h $TestFile -a -e $TestFile ]; then ReleaseFile=$TestFile; fi
 
 
         # Get OS Name
         if [ ! -z $ReleaseFile ]; then
           OSName=`/bin/egrep -o 'Red Hat Enterprise Linux|SUSE Linux Enterprise Server|SUSE LINUX Enterprise Server' $ReleaseFile`
         fi
         ## Extract Version from file
         ## Could also use /etc/*release (not Ubuntu)
         if [ "${OSName}" = "Red Hat Enterprise Linux" ]; then
             Version=`grep 'Red Hat Enterprise' $ReleaseFile | sed s/.*release\ // | sed s/\ .*//`
             if [ "${Version}" != "" ]; then
                 OSAlias="RHEL"
                 OSManufacturer="Red Hat, Inc."
             fi
         elif [ "${OSName}" = "SUSE Linux Enterprise Server" ]; then
             # SLES 10 uses "Linux". Need to parse the minor version as SLES 10.0 is not supported, only 10.1 and up
             # SLES 15 uses /etc/os-release as $ReleaseFile. It contains all information inside "" so Version appears like 15". Need to parse the Version to remove "
             Version=`grep 'SUSE Linux Enterprise Server' $ReleaseFile | sed 's/.*Server\ \| (.*\|\"//g'`
             # Discovery Wizard wants "10.X" not "10 SPX"
             if [ `echo ${Version} | grep 'SP' | wc -l` -eq 1 ]; then
                 Version=`echo ${Version} | awk '{print $1"."$2}'| sed s/SP//`
             else
                 VersionPL=`grep PATCHLEVEL $ReleaseFile | sed s/.*PATCHLEVEL\ =\ //`
                 if [ "${VersionPL}" !=  "" ]; then
                     Version=`echo ${Version}.${VersionPL}`
                 fi
             fi
             if [ "${Version}" != "" ]; then
                 OSAlias="SLES"
                 OSManufacturer="SUSE GmbH"
             fi
         elif [ "${OSName}" = "SUSE LINUX Enterprise Server" ]; then
             # SLES 9 uses "LINUX". No need to parse minor version as Agent supports 9.0 and up.
             Version=`grep 'SUSE LINUX Enterprise Server' $ReleaseFile | sed s/.*Server\ // | sed s/\ \(.*//`
             if [ "${Version}" != "" ]; then
                 OSAlias="SLES"
                 OSManufacturer="SUSE GmbH"
             fi
         else
             OSAlias="Universal"
             OSName="Linux"
             Version=`uname -r | cut -d. -f1,2`
 
             # Do we have the (newer) os-release standard file?
             # If so, that trumps everything else
             if [ -e "${EtcPath}/os-release" ]; then
                 ReleaseFile="${EtcPath}/os-release"
                 GetKitType
 
                 # The os-release files contain TAG=VALUE pairs; just read it in
                 . $ReleaseFile
 
                 # Some fields are optional, for details see the WWW site:
                 #   http://www.freedesktop.org/software/systemd/man/os-release.html
                 [ ! -z "$NAME" ] && OSName="$NAME"
                 [ ! -z "$VERSION_ID" ] && Version="$VERSION_ID"
 
                 # Set the manufacturer if we know this ID
                 # (Set OSAlias for unit test purposes; test injection won't inject that)
                 [ -z "$ID" ] && ID="linux"
                 case $ID in
                     debian)
                         OSManufacturer="Softare in the Public Interest, Inc."
                         OSAlias="UniversalD"
                         ;;
 
                     opensuse)
                         OSManufacturer="SUSE GmbH"
                         OSAlias="UniversalR"
                         ;;
                 esac
 
             elif [ ! -z $ReleaseFile ]; then
                 # Set OSName to release file contents for evaluation.  If parsing logic is not known, Release File contents will be used as OSName.
                 OSName=`sed '/^$/d' ${ReleaseFile} | head -1`
 
                 # Try known cases for OSName/Version
 
                 # ALT Linux
                 if [ `echo $OSName | grep "ALT Linux" | wc -l` -gt 0 ]; then
                     OSName="ALT Linux"
                     OSAlias="UniversalR"
                     OSManufacturer="ALT Linux Ltd"
                     Version=`grep 'ALT Linux' $ReleaseFile | sed s/.*Linux\ // | sed s/\ \.*//`
                 fi
 
                 # Enterprise Linux Server
                 if [ `echo $OSName | grep "Enterprise Linux Enterprise Linux Server" | wc -l` -gt 0 ]; then
                     OSName="Enterprise Linux Server"
                     OSAlias="UniversalR"
                     OSManufacturer="Oracle Corporation"
                     Version=`grep 'Enterprise Linux Enterprise Linux Server' $ReleaseFile | sed s/.*release\ // | sed s/\ \(.*//`
                 fi
 
                 # Oracle Enterprise Linux Server
                 if [ `echo $OSName | grep "Oracle Linux Server" | wc -l` -gt 0 ]; then
                     OSName="Oracle Linux Server"
                     OSAlias="UniversalR"
                     OSManufacturer="Oracle Corporation"
                     Version=`grep 'Oracle Linux Server release' $ReleaseFile | sed s/.*release\ // | sed s/\ \(.*//`
                 fi
 
                 # NeoKylin Linux Advanced Server
                 if [ `echo $OSName | grep "NeoKylin Linux Advanced Server" | wc -l` -gt 0 ]; then
                     OSName="NeoKylin Linux Server"
                     OSAlias="UniversalR"
                     OSManufacturer="China Standard Software Co., Ltd."
                     Version=`grep 'NeoKylin Linux Advanced Server release' $ReleaseFile | sed s/.*release\ // | sed s/\ \(.*//`
                 fi
 
                 # OpenSUSE
                 if [ `echo $OSName | grep -i "openSUSE" | wc -l` -gt 0 ]; then
                     Version=`echo $OSName | awk '{print $2}'`
                     OSName="openSUSE"
                     OSAlias="UniversalR"
                     OSManufacturer="SUSE GmbH"
                 fi
 
                 # Debian
                 if [ "$ReleaseFile" = "${EtcPath}/debian_version" ]; then
                     OSName="Debian"
                     OSAlias="UniversalD"
                     OSManufacturer="Softare in the Public Interest, Inc."
                     Version=`cat ${EtcPath}/debian_version`
                 fi
                        
                 # Ubuntu
                 if [ `echo $OSName | grep "Ubuntu" | wc -l` -gt 0 ]; then
                     OSName="Ubuntu"
                     OSAlias="UniversalD"
                     OSManufacturer="Canonical Group Limited "
                     Version=`grep 'DISTRIB_RELEASE' $ReleaseFile | cut -d'=' -f2`
                 fi
 
                 # Fedora
                 if [ `echo $OSName | grep "Fedora" | wc -l` -gt 0 ]; then
                     OSName="Fedora"
                     OSAlias="UniversalR"
                     OSManufacturer="Red Hat, Inc."
                     Version=`grep 'Fedora' $ReleaseFile | sed s/.*release\ // | sed s/\ .*//`
                 fi
 
                 # CentOS
                if [ `echo $OSName | grep "CentOS" | wc -l` -gt 0 ]; then
                    OSName="CentOS"
                    OSAlias="UniversalR"
                     OSManufacturer="Central Logistics GmbH"
                     Version=`grep 'CentOS' $ReleaseFile | sed s/.*release\ // | sed s/\ .*//`
                 fi
 
                 # If distro is not known, determine whether RPM or DPKG is installed
                if [ "${OSAlias}" = "Universal" ]; then
                    # Identify package manager
                    GetKitType
                 fi
 
                 # If Version is null, something went wrong in release file parsing, reset to kernel version
                 if [ "$Version" = "" ]; then
                     Version=`uname -r`
                 fi
 
                 # If OSName is null, something went wrong in release file parsing, reset to Linux
                 if [ "$OSName" = "" ]; then
                     OSName="Linux"
                     OSManufacturer="Universal"
                 fi
 
             else
                 GetKitType
 
                 Version=`uname -r`
                 OSName="Linux"
                 OSManufacturer="Universal"
             fi
         fi
 
         if [ -z `echo ${Version} | grep '\.'` ]; then
             Version="$Version.0"
         fi
 
         # Construct OSFullName string
         OSFullName="$OSName $Version ($Arch)"
     }
 
     ## End Linux distro function
     ######################################################################
 
 
     ## Determine Version of Unix Platforms
     if [ "${OSName}" = "HP-UX" ]
     then
     #    Version=`uname -r | awk -FB. '{print $2}'`
         Version=`uname -r`
         OSAlias="HPUX"
     elif [ "${OSName}" = "AIX" ]
     then
      Version=`oslevel`
         OSAlias="AIX"
         Arch=`uname -p`
     elif [ "${OSName}" = "SunOS" ]
     then
     # Keeping commented code for changing "5.10" to "10"
     #    Version=`uname -r | awk -F. '{print $2}'`
         Version=`uname -r`
      OSAlias="Solaris"
         Arch=`uname -p`
         echo $OSName
     ## If the OS is Linux, then we need to call the function to get our data
     elif [ "${OSName}" = "Linux" ]
     then
         GetLinuxInfo
    
     else
     echo "<OSName>Unknown</OSName>"
     exit 0
     fi
 
 
     ## Format in XML ouput readable by OpsMgr
     echo "<DiscoveredOS><Hostname>${Hostname}</Hostname><OSName>${OSName}</OSName><OSAlias>${OSAlias}</OSAlias><Version>${Version}</Version><Arch>${Arch}</Arch><IsLinux>${IsLinux}</IsLinux></DiscoveredOS>"
     ```

2. Restart the Operations Manager console and reattempt to discover the Linux machines running in Azure. 