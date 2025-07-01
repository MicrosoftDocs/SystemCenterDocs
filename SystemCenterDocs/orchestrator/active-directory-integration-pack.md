---
title: Active Directory Integration Pack for System Center - Orchestrator
description: The Integration Pack for Active Directory is an add-on for System Center - Orchestrator that enables you to automate common Active Directory management functions.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/19/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: bdb60820-2684-40c5-ae5a-b653acb7736c
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Active Directory Integration Pack for System Center - Orchestrator

The Integration Pack for Active Directory is an add-on for System Center - Orchestrator that enables you to automate common Active Directory management functions.

Microsoft is committed to protecting your privacy while delivering software that brings you the performance, power, and convenience you want. For more Orchestrator-related privacy information, see the [Privacy Statement for System Center - Orchestrator](https://www.microsoft.com/privacystatement/EnterpriseDev/default.aspx).

>[!Note]
>Azure Active Directory or Azure AD or AAD mentioned in Integration packs refers to Microsoft Entra ID. [Learn more](https://azure.microsoft.com/updates/azure-ad-is-becoming-microsoft-entra-id/).

## System Requirements

Before you can install the Integration Pack for Active Directory, you must first install and configure the following listed software. For more information on how to install and configure Orchestrator and Active Directory, see the respective product documentation.

::: moniker range="sc-orch-2025"

- System Center 2025 integration packs require System Center 2025 - Orchestrator
- Windows Server 2025 Active Directory, Windows Server 2022 Active Directory.
::: moniker-end

::: moniker range="sc-orch-2022"
- System Center 2022 integration packs require System Center 2022 - Orchestrator
- Windows Server 2022 Active Directory, Windows Server 2019 Active Directory.
::: moniker-end

::: moniker range="<=sc-orch-2019"
- System Center 2019 integration packs require System Center 2019 - Orchestrator
- System Center 2016 integration packs require System Center 2016 - Orchestrator
- Windows Server 2016 Active Directory, Windows Server 2012 R2 Active Directory, Windows Server 2012 Active Directory, Windows Server 2008 R2 Active Directory, Windows Server 2008 Active Directory, Windows Server 2003 R2 Active Directory, or Windows Server 2003 Active Directory.
::: moniker-end

## Download the Integration Pack

::: moniker range="<=sc-orch-2019"

- To download the Orchestrator 2016 integration pack, see [Active Directory Integration Pack for System Center 2016 - Orchestrator](https://www.microsoft.com/download/details.aspx?id=54098)

- To download the Orchestrator 2019 integration pack, see [Active Directory Integration Pack for System Center 2019 - Orchestrator](https://www.microsoft.com/download/details.aspx?id=58111)

::: moniker-end

::: moniker range="sc-orch-2022"

- To download the Orchestrator 2022 integration pack, see [Active Directory Integration Pack for System Center 2022 - Orchestrator](https://www.microsoft.com/download/details.aspx?id=104333)

::: moniker-end

::: moniker range="sc-orch-2025"

Active Directory Integration Pack for Orchestrator 2022 continues to work with Orchestrator 2025.

Download the Active Directory Integration Pack [here](https://www.microsoft.com/download/details.aspx?id=104333).

::: moniker-end

## Register and Deploy the Integration Pack

After you download the integration pack file, you must register it with the Orchestrator management server and then deploy it to runbook servers and Runbook Designer. For specific procedures, see [How To Install an Integration Pack](./how-to-add-an-integration-pack.md).

## Configure the Active Directory Connections

An Active Directory connection is a reusable link between Orchestrator and an Active Directory domain controller. You can specify as many connections as you require to create links to multiple domain controllers. You can also create multiple connections to the same domain controller to allow for differences in security permissions for different user accounts.

### Set up an Active Directory connection

1. In the Runbook Designer, select **Options**, and then select **Active Directory**. The **Active Directory** dialog appears.

2. On the **Configurations** tab, select **Add** to begin the connection setup. The **Add Configuration** dialog appears.

3. In the **Name** box, enter a name for the connection. This could be the name of the *Active Directory* domain or a descriptive name to distinguish the type of connection.

4. Select the ellipsis button (...) next to the **Type** box and select **Microsoft Active Directory Domain Configuration**. Select **OK**.

5. In the **Configuration User Name** and **Configuration Password** boxes, enter the credentials that Orchestrator will use to sign in to *Active Directory*. This user account must have the authority to perform the actions in any runbook where the connection is used.

6. In the **Configuration Domain Controller Name (FQDN)** box, enter the fully qualified name of the domain or domain controller for the connection.

7. In the **Configuration Default Parent Container** box, enter the default Distinguished Name for an Organizational Unit or Common Name. This default will be used when an activity such as Create User or Create Computer doesn't specify the **Container Distinguished Name**.<br>Examples of **Configuration Default Parent Container** include the following: **CN=Users, DC=mydomain, DC=com** and **OU=MyOU, DC=mydomain, DC=com**

8. Select **OK** to close the configuration dialog.

9. Add additional connections if applicable.

10. Select **Finish**.
