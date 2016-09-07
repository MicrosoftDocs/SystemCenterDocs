---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-08-18
title:  Authoring Automation Runbooks
ms.technology:  service-management-automation
ms.assetid:  a8b7e82f-e3fc-4286-8570-8d5ded944b27
---

# Authoring Automation Runbooks

>Applies To: Windows Azure Pack for Windows Server, System Center 2016

Runbooks in Service Management Automation and Microsoft Azure Automation are Windows PowerShell workflows or PowerShell scripts. They provide the ability to automate administrative processes for managing and deploying cloud servers or any other function that a Windows PowerShell script can perform.

There is no difference in the runbooks between the two systems, and the same runbook can run on either with identical functionality. When the term *Automation* is used in this guide, it refers to both Service Management Automation and Microsoft Azure Automation.

The additional services provided by Automation for working with Windows PowerShell Workflows include the following:

-   Centralized storage and management of runbooks.

-   Scalable architecture for scheduling and running runbooks.

-   Global resources that are centrally managed and available to all runbooks.

-   User interface for authoring and testing runbooks.

-   Set of cmdlets for managing and starting runbooks.

## Runbook Authoring Topics
The following topics provide information on creating and working with Automation runbooks.

-   [Runbook Types in Service Management Automation](../Service-Management-Automation.md)

    Describes the different types of runbooks supported by Service Management Automation.

-   [Windows PowerShell Workflow Concepts](Windows-PowerShell-Workflow-Concepts.md)

    Describes the concepts of Windows PowerShell Workflows as they relate to runbooks.

-   [Creating or Importing a Runbook](Creating-or-Importing-a-Runbook.md)

    Different methods for creating a new runbook or importing an existing runbook.

-   [Editing a Runbook](Editing-a-Runbook.md)

    Details on how to edit a runbook once it"s created.

-   [Publishing a Runbook](Publishing-a-Runbook.md)

    How to publish the draft version of a runbook to make it available to be executed.

-   [Testing a Runbook](Testing-a-Runbook.md)

    How to test a runbook before you publish it.

-   [Global Assets](Global-Assets.md)

    Assets such as connections and variables that are available to all runbooks.

-   [Runbook Output and Messages](Runbook-Output-and-Messages.md)

    Details on the different methods for sending output and user messages from a runbook.

-   [Child Runbooks](../Service-Management-Automation.md)

    Guidance on the different methods for calling one runbook from another runbook.

-   [Building an Integration Module](Building-an-Integration-Module.md)

    Details on how to build an integration module with activities that can be used by runbook.

## See Also
[Service Management Automation](../Service-Management-Automation.md)
[Runbook Operations](Runbook-Operations.md)
