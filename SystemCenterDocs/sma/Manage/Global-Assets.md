---
title: Global Assets
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3544ae9-8fc7-40ce-843c-51ce7c49df6d
---
# Global Assets
Global Assets are available to all runbooks in an Automation environment.  You create and configure them using either the Automation workspace in the management portal or with the appropriate cmdlets in Windows PowerShell. From a runbook, you can retrieve and set values for global assets with activities in the **RunbookConstructs** module. The Windows PowerShell cmdlets are available to use in runbooks in Service Management Automation, but the activities are recommended as they are more efficient because they do not have to work through the Automation web service.

The following topics provide details on the different global assets, how to create and edit them using both the Management Portal and Windows PowerShell, and using them with activities in a runbook.

-   [Credentials](Credentials.md)

    An Automation Credential is either a username and password that can be used with Windows PowerShell commands or a certificate that is uploaded to the server.

-   [Connections](Connections.md)

    An Automation Connection contains the information required to connect to a service or application from a runbook.

-   [Variables](Variables.md)

    Automation variables are values that are available to all runbooks.

-   [Schedules](Schedules.md)

    Automation Schedules are used to schedule runbooks to run automatically.

## See Also
[Service Management Automation](../Service-Management-Automation.md)
[Authoring Automation Runbooks](Authoring-Automation-Runbooks.md)


