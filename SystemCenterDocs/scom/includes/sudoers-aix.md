---
ms.assetid: 
title: include file
description: include file with sudoers configuration for AIX operating systems
author: sepaugh
ms.author: lornesepaugh
manager: benvan
ms.date: 02/24/2024
ms.topic: include
ms.product: msc-operations-manager
---

<!-----------------

SCOM 2022 does not support AIX 

-------------------------->

<!-----------------

SCOM 2019 

-------------------------->

::: moniker range="sc-om-2019"

```bash
#-----------------------------------------------------------------------------------
# Example user configuration for Operations Manager 2019
# Example assumes users named: scomadm & scomuser
# Replace usernames & corresponding /tmp/scx-\<username\> specification for your environment

# General requirements
Defaults:scomadm !requiretty

# Agent maintenance
## Certificate signing
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c cp /tmp/scx-scomadm/scx.pem /etc/opt/microsoft/scx/ssl/scx.pem; rm -rf /tmp/scx-scomadm; /opt/microsoft/scx/bin/tools/scxadmin -restart
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c cat /etc/opt/microsoft/scx/ssl/scx.pem

## Install or upgrade
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]\[0-9\]-\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --install --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC  
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --install --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --install --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]\[0-9\]-\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --upgrade --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC  
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --upgrade --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --upgrade --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC

## Uninstall
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c /opt/microsoft/scx/bin/uninstall

## Log file monitoring
scomuser ALL=(root) NOPASSWD: /opt/microsoft/scx/bin/scxlogfilereader -p

### Examples ###
## Custom shell command monitoring example – replace \<shell command\> with the correct command string
#scomuser ALL=(root) NOPASSWD: /usr/bin/ksh -c echo error

## Daemon diagnostic and restart recovery tasks example (using cron)
#scomuser ALL=(root) NOPASSWD: /usr/bin/sh -c ps -ef | grep cron | grep -v grep
#scomuser ALL=(root) NOPASSWD: /usr/sbin/cron & 

# End user configuration for Operations Manager 
#-----------------------------------------------------------------------------------
```

### AIX7.2

```bash
#-----------------------------------------------------------------------------------
# Example user configuration for Operations Manager 2019
# Example assumes users named: scomadm & scomuser
# Replace usernames & corresponding /tmp/scx-\<username\> specification for your environment

# General requirements
Defaults:scomadm !requiretty

# Agent maintenance
## Certificate signing
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c cp /tmp/scx-scomadm/scx.pem /etc/opt/microsoft/scx/ssl/scx.pem; rm -rf /tmp/scx-scomadm; /opt/microsoft/scx/bin/tools/scxadmin -restart
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c cat /etc/opt/microsoft/scx/ssl/scx.pem

## Install or upgrade
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]\[0-9\]-\[0-9\].aix.\[0-9\].ppc.sh --install --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC  
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\].aix.\[0-9\].ppc.sh --install --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\].aix.\[0-9\].ppc.sh --install --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]\[0-9\]-\[0-9\].aix.\[0-9\].ppc.sh --upgrade --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC  
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\].aix.\[0-9\].ppc.sh --upgrade --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\].aix.\[0-9\].ppc.sh --upgrade --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC

## Uninstall
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c /opt/microsoft/scx/bin/uninstall

## Log file monitoring
scomuser ALL=(root) NOPASSWD: /opt/microsoft/scx/bin/scxlogfilereader -p

### Examples ###
## Custom shell command monitoring example – replace \<shell command\> with the correct command string
#scomuser ALL=(root) NOPASSWD: /usr/bin/sh -c echo error

## Daemon diagnostic and restart recovery tasks example (using cron)
#scomuser ALL=(root) NOPASSWD: /usr/bin/sh -c ps -ef | grep cron | grep -v grep
#scomuser ALL=(root) NOPASSWD: /usr/sbin/cron & 

# End user configuration for Operations Manager 
#-----------------------------------------------------------------------------------
```

::: moniker-end

<!-----------------

SCOM 1801-1807

-------------------------->

::: moniker range=">= sc-om-1801 <= sc-om-1807"

```bash
#-----------------------------------------------------------------------------------
# Example user configuration for Operations Manager 1801-1807
# Example assumes users named: scomadm & scomuser
# Replace usernames & corresponding /tmp/scx-\<username\> specification for your environment

# General requirements
Defaults:scomadm !requiretty

# Agent maintenance

## Certificate signing
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c cp /tmp/scx-scomadm/scx.pem /etc/opt/microsoft/scx/ssl/scx.pem; rm -rf /tmp/scx-scomadm; /opt/microsoft/scx/bin/tools/scxadmin -restart
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c cat /etc/opt/microsoft/scx/ssl/scx.pem

## Install or upgrade
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --install --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --upgrade --enable-opsmgr ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC

## Uninstall
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c /opt/microsoft/scx/bin/uninstall

## Log file monitoring
scomuser ALL=(root) NOPASSWD: /opt/microsoft/scx/bin/scxlogfilereader -p

### Examples
## Custom shell command monitoring example - replace \<shell command\> with the correct command string
#scomuser ALL=(root) NOPASSWD: /usr/bin/sh -c  \<shell command\>

## Daemon diagnostic and restart recovery tasks example (using cron)
#scomuser ALL=(root) NOPASSWD: /bin/sh -c ps -ef | grep cron | grep -v grep
#scomuser ALL=(root) NOPASSWD: /usr/sbin/cron &

#Defaults logfile=/var/log/sudo.log

# End user configuration for Operations Manager 
#-----------------------------------------------------------------------------------
```

::: moniker-end

<!-----------------

SCOM 2016

-------------------------->

::: moniker range="sc-om-2016"

```bash
#-----------------------------------------------------------------------------------
# Example user configuration for Operations Manager 2016
# Example assumes users named: scomadm & scomuser
# Replace usernames & corresponding /tmp/scx-\<username\> specification for your environment

# General requirements
Defaults:scomadm !requiretty

# Agent maintenance
## Certificate signing
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c cp /tmp/scx-scomadm/scx.pem /etc/opt/microsoft/scx/ssl/scx.pem; rm -rf /tmp/scx-scomadm; /opt/microsoft/scx/bin/tools/scxadmin -restart
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c cat /etc/opt/microsoft/scx/ssl/scx.pem

## Install or upgrade
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]\[0-9\]-\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --install ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --install ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --install ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]\[0-9\]-\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --upgrade --force ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --upgrade --force ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.\[5-9\].\[0-9\]-\[0-9\]\[0-9\]\[0-9\].aix.\[\[\\digit\\\]\].ppc.sh --upgrade --force ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC

## Uninstall
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c /opt/microsoft/scx/bin/uninstall

## Log file monitoring
scomuser ALL=(root) NOPASSWD: /opt/microsoft/scx/bin/scxlogfilereader -p

### Examples ###
## Custom shell command monitoring example – replace \<shell command\> with the correct command string
# scomuser ALL=(root) NOPASSWD: /bin/bash -c \<shell command\>

## Daemon diagnostic and restart recovery tasks example (using cron)
#scomuser ALL=(root) NOPASSWD: /usr/bin/sh -c ps -ef | grep cron | grep -v grep
#scomuser ALL=(root) NOPASSWD: /usr/sbin/cron & 

## End user configuration for Operations Manager agent
#-----------------------------------------------------------------------------------
```

::: moniker-end

<!-----------------

SCOM 2012 -- Decommissioned

::: moniker range="sc-om-2012"

```bash
#-----------------------------------------------------------------------------------
# User configuration for Operations Manager agent – for a user with the name: monuser

# General requirements
Defaults:monuser !requiretty

# Lower sudo password prompt timeout for the user
Defaults:monuser passwd_tries = 1, passwd_timeout = 1

# Agent maintenance (discovery, install, uninstall, upgrade, restart, cert signing)
monuser ALL=(root) NOPASSWD: /opt/microsoft/scx/bin/tools/scxadmin
monuser ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-\*/GetOSVersion.sh; EC=$?; rm -rf /tmp/scx-\*; exit $EC
monuser ALL=(root) NOPASSWD: /usr/bin/sh -c cat /etc/opt/microsoft/scx/ssl/scx.pem
monuser ALL=(root) NOPASSWD: /usr/bin/sh -c gzip -dqf /tmp/scx-\*
monuser ALL=(root) NOPASSWD: /usr/bin/sh -c echo \*
monuser ALL=(root) NOPASSWD: /usr/bin/sh -c /usr/sbin/installp -u scx

### Examples ###
## Custom shell command monitoring example ��� replace \<shell command\> with the correct command string
#monuser ALL=(root) NOPASSWD: /bin/bash -c \<shell command\>

## Daemon diagnostic and restart recovery tasks example (using cron)
#monuser ALL=(root) NOPASSWD: /bin/sh -c ps -ef | grep cron | grep -v grep
#monuser ALL=(root) NOPASSWD: /usr/sbin/cron &

# End user configuration for Operations Manager agent
#-----------------------------------------------------------------------------------
```

::: moniker-end

-------------------------->