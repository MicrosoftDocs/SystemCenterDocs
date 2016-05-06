---
title: Inventory of Operations Manager Infrastructure
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7067cf2d-8eb5-426d-a491-d0d116fef325
---
# Inventory of Operations Manager Infrastructure
Both maintaining and troubleshooting [!INCLUDE[om12long](./Token/om12long_md.md)] can be easier when you have a comprehensive inventory of the Operations Manager infrastructure. Ideally, the inventory is started when you first install Operations Manager, and updated as you add features and extend monitoring. If you have an existing infrastructure and no inventory, we recommend that you invest the time to document a complete inventory. [Recommendations for Daily, Weekly, and Monthly Operations Manager Tasks](./Recommendations-for-Daily,-Weekly,-and-Monthly-Operations-Manager-Tasks.md) includes a monthly task to review and update the inventory.

The following is a list of information you will find useful to include in your inventory.

-   Management group information:

    -   Name of the management group

    -   How many agents are being used \(or, how many servers\/clients are being monitored\)

    -   Agentless exception monitoring \(AEM\) setting

    -   Operational data reporting \(ODR\) setting

    -   Customer Experience Improvement Program \(CEIP\) setting

    -   Database grooming aetting

    -   Number of allowed missed heartbeats

    -   Manually installed agents

        -   Are they allowed

        -   Are they approved automatically

    -   Connectors, per connector:

        -   Name

        -   Functionality

        -   Active Directory accounts with passwords \(encrypted\)

        -   Used FQDNs and IP addresses

        -   Configured settings

    -   Whether non\-Microsoft software is being used

    -   History:

        -   When was the management group installed

        -   Which version of Operations Manager was originally used

        -   Whether it has ever been migrated to other hardware, or from physical to virtual or vice versa

        -   Any major issues such outages and other major downtimes

    -   Installed language

    -   Reporting feature:

        -   What is the SSRS url

        -   What SQL server is hosting is the Data Warehouse

    -   Web console:

        -   What is the url

        -   Is SSL used

        -   Is it published to the internet

-   Placement:

    -   Fully qualified domain name \(FQDN\) of forest

    -   LAN segment

    -   Environment, such as production, testing, or anything else

-   Version of Operations Manager, including any cumulative updates

-   Management servers:

    -   FQDN

    -   IP address

    -   LAN segment

    -   Physical location \(even when it is virtualized\)

    -   Physical or virtual computer

    -   Amount of CPU, RAM, disks

    -   Operating system and patch level

    -   Disk configuration, RAID settings, and sizes

    -   Whether it is clustered or not

    -   Any SMS\-enabled devices attached to it

    -   Accounts and passwords \(encrypted\)

        -   Operations Manager SDK Account

        -   Operations Manager Action Account

        -   Operations Manager Data Warehouse Read Account

        -   Operations Manager Data Warehouse Write Account

        -   Operations Manager Health Account

        -   Any third party software account

        -   Run\-As\-Profile accounts \(such as accounts used for the SQL Server and Active Directory management packs\)

    -   Backup of encryption key and its location

-   The total amount of gateway servers and per gateway server:

    -   FQDN

    -   IP address

    -   LAN segment

    -   Physical location \(even when it is virtualized\)

    -   Physical or virtual computer

    -   Amount of CPU, RAM, disks

    -   Operating system and patch level

    -   Disk configuration, RAID settings, and sizes

    -   Functions of gateway server: what is being monitored and how many

    -   Whether the gateway server is configured in a fail\-over configuration

    -   FQDN of PKI which is used

    -   Operations Manager Action Account for the forest \(and its password\) where the gateway server resides

-   SQL Server and Operations Manager databases

    -   FQDN

    -   IP address

    -   LAN segment

    -   Physical location \(even when it is virtualized\)

    -   Physical or virtual computer

    -   Amount of CPU, RAM, disks

    -   Operating system and patch level

    -   SQL Server:

        -   Version

        -   Edition

        -   Architecture

        -   Patch level \(service packs, cumulative updates, and so forth\)

        -   Installed features

    -   Disk configuration, RAID settings, and sizes

    -   Whether it is clustered or not

    -   If the SQL server also hosts other databases or SQL instances

    -   Operations Manager database sizes and locations

-   Management packs:

    -   Which Microsoft management packs are imported and configured, including version information

    -   Which management packs are custom\-made, including version information

    -   Which non\-Microsoft management packs are imported and configured, including version information

-   Backups:

    -   Are the Operations Manager databases backed up on a regular basis

        -   What tooling is used

        -   Where are the backups stored

        -   What retention policy is used

    -   Are the Operations Manager servers backed up on a regular basis

        -   What tooling is used

        -   Where are the backups stored

        -   What retention policy is used

    -   Are the unsealed management packs backed up on a regular basis

    -   Are the backups tested on their validity on a regular basis

## See Also
[Maintenance of Operations Manager](./Maintenance-of-Operations-Manager.md)
[Monitoring the Health of the Management Group](./Monitoring-the-Health-of-the-Management-Group.md)
[How to Configure Grooming Settings for the Reporting Data Warehouse Database](./How-to-Configure-Grooming-Settings-for-the-Reporting-Data-Warehouse-Database.md)
[Scheduling Maintenance in Operations Manager](./Scheduling-Maintenance-in-Operations-Manager.md)
[How and When to Clear the Cache](./How-and-When-to-Clear-the-Cache.md)
[How to Restart a Management Server](./How-to-Restart-a-Management-Server.md)
[How to Configure Grooming Settings for the Operations Manager Database](./How-to-Configure-Grooming-Settings-for-the-Operations-Manager-Database.md)
[Recommendations for Daily, Weekly, and Monthly Operations Manager Tasks](./Recommendations-for-Daily,-Weekly,-and-Monthly-Operations-Manager-Tasks.md)


