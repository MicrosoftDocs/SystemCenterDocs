---
ms.assetid: 379bdfe5-f9d7-495b-9c89-68a3ffc26202
title:  Managing Access in Operations Manager
description: This article highlights the section titles contained within this section of the Operations Manager 2016 documentation.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Managing access in Operations Manager

>Applies To: System Center 2016 - Operations Manager

## Managing access topics

- [Implementing user roles](../../scom/manage-security-overview.md)

    To enable individuals to access monitoring data and perform actions, you assign them to user roles. This section explains how to use user roles to manage access in Operations Manager.

- [How to create a New Action Account in Operations Manager](../../scom/manage-security-create-runas-actionaccount.md)

    The action account is used to gather information about, and run responses on, the managed computer. This procedure explains how to create a new action account that Operations Manager uses to run processes and scripts .

- [How to manage the report server unattended execution account](../../scom/how-to-manage-the-report-server-unattended-execution-account.md)

    The Operations Manager Report Server unattended execution account is used to query data from the Reporting Data Warehouse and is configured through Microsoft SQL Server. This procedure explains how to manage this account.

- [Controlling access using the Health Service Lockdown tool](../../scom/manage-security-overview-hslockdown.md)

    On computers requiring high security, such as a domain controller, you may need to deny certain identities access to rules, tasks, and monitors that might jeopardize the security of your server. The Health Service lockdown tool (HSLockdown.exe) enables you to use various command-line options to control and limit the identities used to run a rule, task, or monitor.

- [Accessing UNIX and Linux computers](../../scom/manage-security-authenticate-crossplat.md)

    This section explains how to configure and manage access to computers running UNIX and Linux operating systems.

- [Managing Run As accounts and profiles](../../scom/manage-security-maintain-runas-profiles.md)

    Operations Manager workflows, such as rules, tasks, monitors, and discoveries, require credentials to run on a targeted agent or computer. These credentials are configured by using Run As profiles and Run As accounts. This section explains how to create, configure, and manage Run As profiles and accounts.


