---
title: Active Directory Integration Pack for System Center 2016 - Orchestrator
description: The Integration Pack for Active Directory is an add-on for System Center 2016 - Orchestrator that enables you to automate common Active Directory management functions.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: bdb60820-2684-40c5-ae5a-b653acb7736c
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Active Directory Integration Pack for System Center 2016 - Orchestrator

Applies To: System Center 2016 - Orchestrator

The Integration Pack for Active Directory is an add-on for System Center 2016 - Orchestrator that enables you to automate common Active Directory management functions.

Microsoft is committed to protecting your privacy, while delivering software that brings you the performance, power, and convenience you want. For more Orchestrator-related privacy information, see the [Privacy Statement for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/privacystatement/EnterpriseDev/default.aspx).

## System Requirements

Before you can install the Integration Pack for Active Directory, you must first install and configure the following listed software. For more information about how to install and configure Orchestrator and Active Directory, refer to the respective product documentation.

-   System Center 2016 integration packs require System Center 2016 - Orchestrator.
-   Windows Server 2016 Active Directory, Windows Server 2012 R2 Active Directory, Windows Server 2012 Active Directory, Windows Server 2008 R2 Active Directory, Windows Server 2008 Active Directory, Windows Server 2003 R2 Active Directory, or Windows Server 2003 Active Directory.

## Downloading the Integration Pack

To download this integration pack, see [Active Directory Integration Pack for System Center 2016 - Orchestrator](https://www.microsoft.com/en-us/download/details.aspx?id=54098).

## Registering and Deploying the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designer. For specific procedures, see [How To Install an Integration Pack](https://technet.microsoft.com/system-center-docs/orch/manage/how-to-add-an-integration-pack).

## Configuring the Active Directory Connections

An Active Directory connection is a reusable link between Orchestrator and an Active Directory domain controller. You can specify as many connections as you require to create links to multiple domain controllers. You can also create multiple connections to the same domain controller to allow for differences in security permissions for different user accounts.

#### To set up an Active Directory connection

1.  In the Runbook Designer, click **Options**, and then click **Active Directory**. The **Active Directory** dialog box appears.

2.  On the **Configurations** tab, click **Add** to begin the connection setup. The **Add Configuration** dialog box appears.

3.  In the **Name** box, enter a name for the connection. This could be the name of the *Active Directory* domain, or a descriptive name to distinguish the type of connection.

4.  Click the ellipsis button (...) next to the **Type** box and select **Microsoft Active Directory Domain Configuration**. Click **OK**.

5.  In the **Configuration User Name** and **Configuration Password** boxes, type the credentials that Orchestrator will use to log on to *Active Directory*. This user account must have the authority to perform the actions in any runbook where the connection is used.

6.  In the **Configuration Domain Controller Name (FQDN)** box type the fully qualified name of the domain or domain controller for the connection.

7.  In the **Configuration Default Parent Container** box, type the default Distinguished Name for an Organizational Unit or Common Name. This default will be used when an activity such as Create User or Create Computer does not specify the **Container Distinguished Name**.<br>Examples of **Configuration Default Parent Container** include the following: **CN=Users, DC=mydomain, DC=com** and **OU=MyOU, DC=mydomain, DC=com**

8.  Click **OK** to close the configuration dialog box.

9.  Add additional connections if applicable.

10. Click **Finish**.
