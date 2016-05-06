---
title: Orchestrator_2
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c716211e-43ad-41cc-a651-3c371752b485
---
# Orchestrator_2
Welcome to [!INCLUDE[orchlong](../Token/orchlong_md.md)]. Orchestrator is a workflow management solution for the data center. Orchestrator lets you automate the creation, monitoring, and deployment of resources in your environment.   This topic is intended solely to point you to information on various [!INCLUDE[orchshort](../Token/orchshort_md.md)] features.

The following topics provide information to help you deploy and use [!INCLUDE[orchshort](../Token/orchshort_md.md)].

## In this release

-   [Release Notes for System Center 2012 - Orchestrator_1](../Topic/Release-Notes-for-System-Center-2012---Orchestrator_1.md)

## Learn [!INCLUDE[orchshort](../Token/orchshort_md.md)]

-   [Getting Started with System Center 2012 - Orchestrator](../Topic/Getting-Started-with-System-Center-2012---Orchestrator.md)

## Install and configure [!INCLUDE[orchshort](../Token/orchshort_md.md)]

-   [Upgrading System Center 2012 \- Orchestrator to System Center 2012 SP1](assetId:///b36553d2-6029-4eb0-9365-56b2cd6e16a9)

-   [Deploying System Center 2012 - Orchestrator](../Topic/Deploying-System-Center-2012---Orchestrator.md)

-   [Administering System Center 2012 - Orchestrator](../Topic/Administering-System-Center-2012---Orchestrator.md)

-   [Integration Packs for System Center 2012 \- Orchestrator &#91;Orch2012\_TechNet\_IP&#93;](assetId:///e6aff353-c364-4852-bfb7-9088407a7bd9)

## Install and configure [!INCLUDE[spfshort](../Token/spfshort_md.md)]

-   [Service Provider Foundation](../Topic/Service-Provider-Foundation.md)

## Work with runbooks

-   [Using Runbooks in System Center 2012 - Orchestrator](../Topic/Using-Runbooks-in-System-Center-2012---Orchestrator.md)

-   [Using the Orchestration Console in System Center 2012 - Orchestrator](../Topic/Using-the-Orchestration-Console-in-System-Center-2012---Orchestrator.md)

## Downloadable documentation
You can download [a copy of this technical documentation from the Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=247109). However, for the most up\-to\-date information, always use the TechNet library.

## Comparison to Other Automation Tools
The following table compares Orchestrator to the other Microsoft automation tools, Service Management Automation and Microsoft Azure Automation.

|Automation Tool|Primary Function|Access to Resources|Runbooks|
|-------------------|--------------------|-----------------------|------------|
|[Orchestrator](http://aka.ms/runbookauthor/orchestrator)|Orchestrator is intended for automation of all on\-premises resources. It uses a different runbook engine than Service Management Automation and Azure Automation.|Orchestrator runbooks can access resources that are on\-premises and in the private cloud. They can access resources in Azure using the [Windows Azure Integration Pack for Orchestrator](http://aka.ms/runbookauthor/azureip).<br /><br />Orchestrator runbooks can manage Azure Automation using the [Azure cmdlets](http://aka.ms/runbookauthor/azurecmdlets) or Service Management Automation using [Service Management Automation PowerShell module](http://aka.ms/runbookauthor/smacmdlets).|Orchestrator has a graphical interface to create runbooks without requiring any scripting. Its runbooks are composed of activities from Integration Packs that are written specifically for Orchestrator. You can also use the [Run .NET Script activity](http://aka.ms/runbookauthor/activity/runnetscript) to run PowerShell to perform any functionality that is not included in an integration pack.|
|[Service Management Automation](http://aka.ms/runbookauthor/sma)|Service Management Automation is installed locally in your data center as a component of [Windows Azure Pack](http://aka.ms/runbookauthor/wap) and is intended to automate management tasks in the private cloud.|While runbooks in SMA will typically use System Center and Windows Azure Pack cmdlets to access WAP components, they can access any resource in your data center. They can include Azure cmdlets in order to manage components in the public cloud for hybrid scenarios.<br /><br />SMA runbooks can access Orchestrator through the [Orchestrator PowerShell module](http://aka.ms/runbookauthor/orchestratormodule) and Azure Automation through the [Azure PowerShell module](http://aka.ms/runbookauthor/azurecmdlets).|Service Management Automation and Azure Automation use an identical runbook format based on Windows PowerShell Workflow. While runbooks in Azure Automation will primarily use Azure cmdlets to access public cloud resources, runbooks in SMA will typically use System Center and Windows Azure Pack cmdlets to access WAP components.|
|[Azure Automation](http://aka.ms/runbookauthor/azure)|Azure Automation runbooks run in the Azure public cloud and are intended to automate Azure\-related management tasks.|Runbooks in Azure Automation cannot access resources in your data center that are not accessible from the public cloud. They also have no way to access Orchestrator or SMA runbooks.<br /><br />Azure Automation runbooks can access any external resources that can be accessed from a Windows PowerShell Workflow.|Service Management Automation and Azure Automation use an identical runbook format based on Windows PowerShell Workflow. While runbooks in Azure Automation will primarily use Azure cmdlets to access public cloud resources, runbooks in SMA will typically use System Center and Windows Azure Pack cmdlets to access WAP components.|

## Reference information

-   [Runbook Activity Reference for System Center 2012 - Orchestrator](../Topic/Runbook-Activity-Reference-for-System-Center-2012---Orchestrator.md)

-   [System Center 2012 \- Orchestrator SDK](http://go.microsoft.com/fwlink/p/?LinkId=230570)

-   [System Center Orchestrator 2012 Beta Privacy Statement](assetId:///bab5f7fc-05bf-4c8c-ac49-53d60d3c1cd6)

-   [Glossary for System Center 2012 - Orchestrator](../Topic/Glossary-for-System-Center-2012---Orchestrator.md)

-   [Glossary for Opalis Integration Server 6.3](../Topic/Glossary-for-Opalis-Integration-Server-6.3.md)

