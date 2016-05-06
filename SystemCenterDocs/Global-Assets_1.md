---
title: Global Assets_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 327f3d7f-83d1-4361-a640-4d12bfd4e091
---
# Global Assets_1
Global Assets are available to all runbooks in an [!INCLUDE[sma_2](./Token/sma_2_md.md)] environment.  You create and configure them using either the Automation workspace in the management portal or with the appropriate cmdlets in Windows PowerShell. From a runbook, you can retrieve and set values for global assets with activities in the **RunbookConstructs** module. The Windows PowerShell cmdlets are available to use in runbooks in [!INCLUDE[sma_1](./Token/sma_1_md.md)], but the activities are recommended as they are more efficient because they do not have to work through the [!INCLUDE[sma_2](./Token/sma_2_md.md)] web service.

The following topics provide details on the different global assets, how to create and edit them using both the Management Portal and Windows PowerShell, and using them with activities in a runbook.

-   [Credentials](./Credentials.md)

    An Automation Credential is either a username and password that can be used with Windows PowerShell commands or a certificate that is uploaded to the server.

-   [Connections](./Connections.md)

    An Automation Connection contains the information required to connect to a service or application from a runbook.

-   [Variables](./Variables.md)

    Automation variables are values that are available to all runbooks.

-   [Schedules](./Schedules.md)

    Automation Schedules are used to schedule runbooks to run automatically.

## See Also
[Service Management Automation](./Service-Management-Automation.md)
[Authoring Automation Runbooks](./Authoring-Automation-Runbooks.md)


