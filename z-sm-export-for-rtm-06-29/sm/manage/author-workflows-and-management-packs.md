---
title: Workflows and Management Packs
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec884a69-178b-48ee-872c-4e306fee776e
---

# Workflows and Management Packs

System Center 2012 - Service Manager runs a Windows Workflow Foundation \(WF\) workflow using trigger condition information stored in the management pack. For each workflow, the management pack contains one data source module and one write action module. The data source module defines the condition that triggers the workflow to run, and the write action module defines the workflow actions. The management pack also stores any script information that the workflow uses.  

## Files and Formats  
 In addition to the management pack file, WF workflows require several supporting files:  

-   **Authoring environment files**. When you create or edit a workflow, these files store the raw workflow information, such as property values and workflow logic.  

-   **Compiled workflow assembly file** \(*workflowname*.dll\). When you save a management pack in the System Center 2016 - Service Manager Authoring Tool, the tool also compiles any raw workflow files \(the XOML and CS files\) into a workflow assembly \(DLL\) file.  

-   **Activity assembly files** \(*activityname*.dll\). These files contain definitions of the available workflow activities. The Authoring Tool cannot modify the activity assembly files.  

 To implement a management pack with workflows in your Service Manager console environment, make sure that Service Manager has access to the workflow assembly file and the activity assembly files, as well as the management pack itself. The following illustration shows how the various files interact when a workflow runs.  

 ![Management Pack and Workflow Files](../media/author-mpandworkflowcomponents_production.png)  

## Trigger Conditions for Workflows  
 A workflow's data source module defines the workflow trigger condition. A workflow can have one of two types of trigger condition:  

-   **Timer.** This option \(also referred to as a *schedule*\) triggers the workflow on designated days of the week or at another specified interval.  

-   **Database query**. This option \(also referred to as a *subscription*\) triggers the workflow when a specific type of change occurs to a specific class of object. You can select the class from any of the installed management packs, and you can choose from three types of changes:  

    -   When a new instance of the class is created  

    -   When an instance of the class is updated  

    -   When an instance of the class is deleted  

## See Also

- [Managing Workflows](../../../sm/manage/author/Managing-Workflows.md)   
- [How to Deploy a Workflow to Service Manager](../../../sm/manage/author/How-to-Deploy-a-Workflow-to-Service-Manager.md)   
- [Automating IT Processes with Workflows](../../../sm/manage/author/Automating-IT-Processes-with-Workflows.md)
