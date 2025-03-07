---
ms.assetid: 
title: Include file
description: Include file with sudoers configuration for operating systems that fall under Universal Linux monitoring.
author: sepaugh
ms.author: lornesepaugh
manager: benvan
ms.date: 03/07/2025
ms.topic: include
ms.service: system-center
ms.subservice: operations-manager
---

<!-----------------

SCOM 2022 and above

-------------------------->

::: moniker range="> sc-om-2022"

```bash
#----------------------------------------------------------------------------------------
# Example user configuration for Operations Manager 2022 and above
# Example assumes users named: scomadm & scomuser
# Replace usernames & corresponding /tmp/scx-\<username\> specification for your environment

# General requirements
Defaults:scomadm !requiretty

# Agent maintenance
## Certificate signing
scomadm ALL=(root) NOPASSWD: /bin/sh -c cp /tmp/scx-scomadm/scx.pem /etc/opt/microsoft/scx/ssl/scx.pem; rm -rf /tmp/scx-scomadm; /opt/microsoft/scx/bin/tools/scxadmin -restart
scomadm ALL=(root) NOPASSWD: /bin/sh -c cat /etc/opt/microsoft/scx/ssl/scx.pem
scomadm ALL=(root) NOPASSWD: /bin/sh -c if test -f /opt/microsoft/omsagent/bin/service_control; then cp /tmp/scx-scomadm/omsadmin.conf /etc/opt/microsoft/omsagent/scom/conf/omsadmin.conf; /opt/microsoft/omsagent/bin/service_control restart scom; fi

## Install or upgrade
# Compiler mitigated agent version changes
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].s.x[6-8][4-6].sh --install --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --install --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --install --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].s.x[6-8][4-6].sh --upgrade --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --upgrade --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --upgrade --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC

## Uninstall
#scomadm ALL=(root) NOPASSWD: /bin/sh -c /opt/microsoft/scx/bin/uninstall
scomadm ALL=(root) NOPASSWD: /bin/sh -c if test -f /opt/microsoft/omsagent/bin/omsadmin.sh; then if test "$(/opt/microsoft/omsagent/bin/omsadmin.sh -l | grep scom | wc -l)" \= "1" && test "$(/opt/microsoft/omsagent/bin/omsadmin.sh -l | wc -l)" \= "1" || test "$(/opt/microsoft/omsagent/bin/omsadmin.sh -l)" \= "No Workspace"; then /opt/microsoft/omsagent/bin/uninstall; else /opt/microsoft/omsagent/bin/omsadmin.sh -x scom; fi; else /opt/microsoft/scx/bin/uninstall; fi

## Log file monitoring
scomuser ALL=(root) NOPASSWD: /opt/microsoft/scx/bin/scxlogfilereader -p

### Examples ###
## Custom shell command monitoring example – replace \<shell command\> with the correct command string
#scomuser ALL=(root) NOPASSWD: /bin/sh -c echo error

## For ubuntu18
#scomuser ALL=(root) NOPASSWD: /bin/bash -c echo error

## Daemon diagnostic and restart recovery tasks example (using cron)
#scomuser ALL=(root) NOPASSWD: /bin/sh -c ps -ef | grep cron | grep -v grep
#scomuser ALL=(root) NOPASSWD: /usr/sbin/cron & 

# End user configuration for Operations Manager 
#-----------------------------------------------------------------------------------
```

::: moniker-end

<!-----------------

SCOM 2019 

-------------------------->

::: moniker range="sc-om-2019"

```bash
#----------------------------------------------------------------------------------------
# Example user configuration for Operations Manager 2019
# Example assumes users named: scomadm & scomuser
# Replace usernames & corresponding /tmp/scx-\<username\> specification for your environment

# General requirements
Defaults:scomadm !requiretty

# Agent maintenance
## Certificate signing
scomadm ALL=(root) NOPASSWD: /bin/sh -c cp /tmp/scx-scomadm/scx.pem /etc/opt/microsoft/scx/ssl/scx.pem; rm -rf /tmp/scx-scomadm; /opt/microsoft/scx/bin/tools/scxadmin -restart
scomadm ALL=(root) NOPASSWD: /bin/sh -c cat /etc/opt/microsoft/scx/ssl/scx.pem
scomadm ALL=(root) NOPASSWD: /bin/sh -c if test -f /opt/microsoft/omsagent/bin/service_control; then cp /tmp/scx-scomadm/omsadmin.conf /etc/opt/microsoft/omsagent/scom/conf/omsadmin.conf; /opt/microsoft/omsagent/bin/service_control restart scom; fi

## Install or upgrade
# Compiler mitigated agent version changes
  
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].s.x[6-8][4-6].sh --install --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --install --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC  
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --install --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9][0-9][0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --install --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].s.x[6-8][4-6].sh --upgrade --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC  
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --upgrade --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC  
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --upgrade --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9][0-9][0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --upgrade --enable-opsmgr; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC

## Uninstall
#scomadm ALL=(root) NOPASSWD: /bin/sh -c /opt/microsoft/scx/bin/uninstall
scomadm ALL=(root) NOPASSWD: /bin/sh -c if test -f /opt/microsoft/omsagent/bin/omsadmin.sh; then if test "$(/opt/microsoft/omsagent/bin/omsadmin.sh -l | grep scom | wc -l)" \= "1" && test "$(/opt/microsoft/omsagent/bin/omsadmin.sh -l | wc -l)" \= "1" || test "$(/opt/microsoft/omsagent/bin/omsadmin.sh -l)" \= "No Workspace"; then /opt/microsoft/omsagent/bin/uninstall; else /opt/microsoft/omsagent/bin/omsadmin.sh -x scom; fi; else /opt/microsoft/scx/bin/uninstall; fi

## Log file monitoring
scomuser ALL=(root) NOPASSWD: /opt/microsoft/scx/bin/scxlogfilereader -p


### Examples ###
## Custom shell command monitoring example – replace \<shell command\> with the correct command string
#scomuser ALL=(root) NOPASSWD: /bin/sh -c echo error

## For ubuntu18
#scomuser ALL=(root) NOPASSWD: /bin/bash -c echo error

## Daemon diagnostic and restart recovery tasks example (using cron)
#scomuser ALL=(root) NOPASSWD: /bin/sh -c ps -ef | grep cron | grep -v grep
#scomuser ALL=(root) NOPASSWD: /usr/sbin/cron & 

## End user configuration for Operations Manager agent
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
scomadm ALL=(root) NOPASSWD: /bin/sh -c cp /tmp/scx-scomadm/scx.pem /etc/opt/microsoft/scx/ssl/scx.pem; rm -rf /tmp/scx-scomadm; /opt/microsoft/scx/bin/tools/scxadmin -restart
scomadm ALL=(root) NOPASSWD: /bin/sh -c cat /etc/opt/microsoft/scx/ssl/scx.pem

## Install or upgrade
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --install; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --install; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9][0-9][0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --install; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --upgrade --force; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --upgrade --force; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9][0-9][0-9].universal[[\:alpha\:]].[[\:digit\:]].x[6-8][4-6].sh --upgrade --force; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC

## Uninstall
scomadm ALL=(root) NOPASSWD: /bin/sh -c /opt/microsoft/scx/bin/uninstall

## Log file monitoring
scomuser ALL=(root) NOPASSWD: /opt/microsoft/scx/bin/scxlogfilereader -p

### Examples ###
## Custom shell command monitoring example – replace \<shell command\> with the correct command string
# scomuser ALL=(root) NOPASSWD: /bin/bash -c \<shell command\>

## Daemon diagnostic and restart recovery tasks example (using cron)
#scomuser ALL=(root) NOPASSWD: /bin/sh -c ps -ef | grep cron | grep -v grep
#scomuser ALL=(root) NOPASSWD: /usr/sbin/cron & 

# End user configuration for Operations Manager agent
#-----------------------------------------------------------------------------------
```

::: moniker-end
