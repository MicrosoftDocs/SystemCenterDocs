---
ms.assetid: 
title: Include file
description: Include file with sudoers configuration for HP-UX operating systems.
author: sepaugh
ms.author: lornesepaugh
manager: benvan
ms.date: 03/07/2025
ms.topic: include
ms.service: system-center
ms.subservice: operations-manager
---

<!-----------------

SCOM 2019 and above does not support HP-UX

-------------------------->


<!-----------------

SCOM 2016

-------------------------->

::: moniker range="sc-om-2016"

## HP-UX

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
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9][0-9]-[0-9].hpux.11iv3.ia64.sh --install ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].hpux.11iv3.ia64.sh --install ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9][0-9][0-9].hpux.11iv3.ia64.sh --install ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9][0-9]-[0-9].hpux.11iv3.ia64.sh --upgrade --force ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9].hpux.11iv3.ia64.sh --upgrade --force ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c sh /tmp/scx-scomadm/scx-1.[5-9].[0-9]-[0-9][0-9][0-9].hpux.11iv3.ia64.sh --upgrade --force ; EC=$?; cd /tmp; rm -rf /tmp/scx-scomadm; exit $EC

## Uninstall
scomadm ALL=(root) NOPASSWD: /usr/bin/sh -c /opt/microsoft/scx/bin/uninstall

## Log file monitoring
scomuser ALL=(root) NOPASSWD: /opt/microsoft/scx/bin/scxlogfilereader -p

### Examples ###
## Custom shell command monitoring example – replace \<shell command\> with the correct command string
#scomuser ALL=(root) NOPASSWD: /bin/bash -c \<shell command\>

## Daemon diagnostic and restart recovery tasks example (using cron)
#scomuser ALL=(root) NOPASSWD: /usr/bin/sh -c ps -ef | grep cron | grep -v grep
#scomuser ALL=(root) NOPASSWD: /usr/sbin/cron & 

# End user configuration for Operations Manager agent
#-----------------------------------------------------------------------------------
```

::: moniker-end
