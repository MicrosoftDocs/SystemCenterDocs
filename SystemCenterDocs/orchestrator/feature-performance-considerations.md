---
title: Feature performance considerations
description: Provides performance guidance for System Center - Orchestrator
author: jyothisuri
manager: mkluck
ms.date: 04/25/2023
ms.prod: system-center
ms.technology: orchestrator
ms.topic: article
ms.author: jsuri
ms.custom: UpdateFrequency3, engagement-fy23
---


# Feature performance considerations

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

Despite the great deal of variance in their design and visual complexity, runbooks are simple. Runbooks essentially do three things: Run activities, manage published data, and branch.  

## Orchestrator Feature Functions  
Additionally, runbook activities can be thought of as having two distinct types of code: Platform code and domain code. The term *domain code* is used to identify code called within a runbook activity typically not associated with the Orchestrator product itself. For example, the **Invoke Web Service** standard activity would contain Orchestrator platform code (the **plumbing** of the activity) and domain code unique to invoking a web service. The platform code will be unique but similar for most activities, since it's built from a common framework. However, there will potentially be great variation in domain code for different activities.  

Essentially, Orchestrator runbooks are designed to pass data between discrete elements of domain code.  

While technically not mandatory, every activity generally consumes published data created by prior runbook activities. What a given activity does with published data it subscribes to is entirely up to the domain code.  

All runbook activities create published data, which is referred to as *Common Published Data*. Domain code will generally create published data, generally referred to as *Activity Specific Published Data*. This data will be as unique to a given activity as the domain code itself. Also, it's not required that domain code produce published data.  

The data produced by a given activity can contain data elements that are single or multi\-valued. For example, every activity produces a single record of single\-value data referred to as common published data. Domain code can produce multiple records of multi\-value data.  

Branching is a fundamental concept for Orchestrator. A given runbook activity will create a branch if it's the origin of two or more links whose filter conditions indicate there's data to pass to the activity at the end of the link. When a runbook is first invoked, it consists of a single thread. When this thread encounters a runbook activity whose links require a branch, additional threads are created, one for each branch. Each thread takes as input the published data from the activity that created the branch. This data is correlated back to the prior activities in the runbook \(hence, the ability to subscribe to published data from prior activities\).  

::: moniker range="< sc-orch-2019"

The operator experience is based on two components: The Orchestration Console and the Web Service. The Orchestration Console is a Silverlight application that depends on the Web Service for its connection to the Orchestrator database. The Web Service is an IIS application that connects to the database. Hence, the Web Service and Orchestration Console are dependent on the performance of the Orchestrator database.

Parts of the Orchestrator database are new to the product and directly support the Web Service. However, parts of the Web Service depend on the legacy Opalis 6.3 database structure.  

Additionally, while the Orchestration Console is dependent on the Web Service, it also has logic unique to its function as a user interface that will have its own performance characteristics.  

::: moniker-end

::: moniker range=">= sc-orch-2019"

The operator experience is based on two components: The (new) Orchestration Console and Web API. The Orchestration Console is an Angular application that depends on the Web API for its connection to the Orchestrator database. The Web API is an IIS application that connects to the database. Hence, the Web API and Orchestration Console are dependent on the performance of the Orchestrator database.

Parts of the Orchestrator database are new to the product and directly support the Web API. However, parts of the Web Service depend on the legacy Opalis 6.3 database structure.  

Additionally, while the Orchestration Console is dependent on the Web API, it also has logic unique to its function as a user interface that will have its own performance characteristics.  

::: moniker-end
