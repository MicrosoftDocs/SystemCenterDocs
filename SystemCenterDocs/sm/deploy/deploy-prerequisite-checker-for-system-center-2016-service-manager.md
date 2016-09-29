---
title: Prerequisite Checker for System Center - Service Manager
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84bd6b90-52d0-4aa0-8f2f-27ee402e3e13
---

# Prerequisite Checker for System Center - Service Manager

>Applies To: System Center 2016 - Service Manager

During installation, System Center - Service Manager Setup performs prerequisite checks for software and hardware requirements and returns one of the three following states:  

-   **Success**: Setup finds that all software and hardware requirements are met, and installation proceeds.  

-   **Warning**: Setup finds that all software requirements are met, but the computer does not meet minimum hardware requirements. Or, the requirements for optional software are missing. Installation proceeds.  

-   **Failure**: At least one software or hardware requirement is not met, and installation cannot proceed. An **Installation cannot continue** message appears.  

> [!NOTE]  
>  On the **Installation cannot continue** screen, there is no option to restart the prerequisite checker. You must click **Cancel** to restart the installation process. Make sure that the computer meets all hardware and software requirements before you run Setup again.
