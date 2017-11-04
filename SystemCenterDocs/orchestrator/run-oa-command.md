---
title: Run OA Command
description: The Run OA Command activity is used in a runbook to run a command that can be used to perform management activities such as Add User, Enable User, and Show Server Status.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: d86c35be-c407-4f65-aec2-593839e58b4f
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Run OA Command

The **Run OA Command** activity is used in a runbook to run a command that can be used to perform management activities such as **Add User**, **Enable User**, and **Show Server Status**.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Run OA Command required properties

| **Element** | **Description**   | **Valid Values**   | **Lookup** |
|:---|:---|:---|:---|
| Command   | The OA command to run   | ADD EBIPA<br>ADD LDAP GROUP<br>ADD OA DNS<br>ADD SNMP TRAPRECEIVER<br>ADD USER<br>ASSIGN<br>ASSIGN OA<br>ASSIGN OA LDAP GROUP<br>DISABLE EBIPA<br>DISABLE USER<br>DOWNLOAD CONFIG<br>DOWNLOAD LDAP CERTIFICATE<br>ENABLE ALERTMAIL<br>ENABLE EBIPA<br>ENABLE HTTPS<br>ENABLE LDAP<br>ENABLE NTP<br>ENABLE SNMP<br>ENABLE TELNET<br>ENABLE TRUSTED HOSTS<br>ENABLE USER<br>ENABLE XMLREPLY<br>FORCE TAKEOVER<br>HPONCFG<br>PING<br>POWEROFF SERVER<br>POWERON SERVER<br>REBOOT SERVER<br>REMOVE EBIPA<br>REMOVE LDAP GROUP<br>RESTART OA<br>SAVE EBIPA<br>SET ALERTMAIL MAILBOX<br>SET ALERTMAIL SENDERDOMAIN<br>SET ALERTMAIL SMTPSERVER<br>SET DATE<br>SET EBIPA<br>SET EBIPA DOMAIN<br>SET EBIPA GATEWAY<br>SET EBIPA INTERCONNECT NTP<br>SET ENCLOSURE ASSET<br>SET ENCLOSURE NAME<br>SET ENCLOSURE UID<br>SET HPSIM TRUST MODE<br>SET IPCONFIG DHCP<br>SET LDAP NAME MAP<br>SET LDAP PORT<br>SET LDAP SEARCH<br>SET LDAP SERVER<br>SET NTP POLL<br>SET NTP PRIMARY<br>SET NTP SECONDARY<br>SET OA GATEWAY<br>SET OA NAME<br>SET OA UID<br>SET POWER MODE<br>SET POWER LIMIT<br>SET POWER SAVINGS<br>SET RACK NAME<br>SET SCRIPT<br>SET SERVER BOOT FIRST<br>SET SERVER BOOT ONCE<br>SET SERVER DVD<br>SET SNMP COMMUNITY<br>SET SNMP CONTACT<br>SET SNMP LOCATION<br>SET TIMEZONE<br>SET USER ACCESS<br>SET USER PASSWORD<br>SHOW ENCLOSURE FAN<br>SHOW ENCLOSURE INFO<br>SHOW ENCLOSURE LCD<br>SHOW ENCLOSURE POWERSUPPLY<br>SHOW ENCLOSURE STATUS<br>SHOW ENCLOSURE TEMP<br>SHOW INTERCONNECT INFO<br>SHOW INTERCONNECT LIST<br>SHOW INTERCONNECT STATUS<br>SHOW INTERCONNECT PORT MAP<br>SHOW OA STATUS<br>SHOW POWER<br>SHOW RACK NAME<br>SHOW SERVER DVD<br>SHOW SERVER STATUS<br>SHOW SERVER TEMP<br>UNASSIGN<br>UNASSIGN LDAP GROUP<br>UNASSIGN OA<br>UNASSIGN OA LDAP GROUP<br>UPDATE DEVICE<br>UPDATE IMAGE<br>UPDATE IMAGE SYNC<br>UPDATE SHOW<br>UPLOAD CONFIG | Yes   |
| Fields   | Required fields for the selected command. | String   | No   |

## Run OA Command optional properties

| **Element** | **Description**   | **Valid Values** |   |
|:---|:---|:---|:---|
| Fields   | Optional fields can be added to the Fields list by clicking Select fields. | String   |   |

## Run OA Command published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Command   | Selected command   | String   |
| Command line   | Command line for command   | String   |
| Connection name | Named connection   | String   |
| Error output   | Command error output   | String   |
| Exit code   | Exit code of command   | String   |
| Private Key   | SSH private key   | String   |
| SSH Address   | IP address or network name | String   |
| SSH user   | SSH username   | String   |
| Standard output | Standard output of command | String   |

>[!NOTE]
>When testing a configured connection, you may get a popup window with the message **Microsoft System Center 2016 Orchestrator has stopped working** with the Application Name of **sshclient.exe**. You can choose the **Close the program** option to dismiss the window without affecting the result of the test. If the connection is good, you should see another message window reporting **Test connection succeeded.**.

## Other activities

The Integration Pack for HP iLO and OA contains the following additional activities:

- [Run iLO Command](run-ilo-command.md)
