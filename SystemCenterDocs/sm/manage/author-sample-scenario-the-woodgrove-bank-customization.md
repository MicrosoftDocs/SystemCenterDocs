---
title: Woodgrove Bank customization sample scenario
description: Provides an overview of the Woodgrove Bank customization sample scenario for the Service Manager Authoring Tool.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea9bb90e-5a00-4346-b2a2-f6076c203778
---

# Woodgrove Bank customization sample scenario for the Service Manager Authoring Tool

>Applies To: System Center 2016 - Service Manager

To provide real\-world context to the step\-by\-step procedures for the Service Manager Authoring Tool, we have created a fictitious scenario that takes place at a fictitious company, Woodgrove Bank.  

 The Woodgrove Bank customization scenario illustrates how Ken Myer, a server application developer for Woodgrove Bank, can easily extend the default change management process to support a new compliance change request process that the organization needs. The new compliance change request process will automatically add new computers to groups in Active Directory Domain Services \(AD&nbsp;DS\) so that the group software policies apply to the new computers.  

> [!NOTE]  
>  Some procedures in the Woodgrove Bank customization scenario rely on standard usage of the Service Manager console in Service Manager. This guide does not provide details for these common procedures. For more information about these procedures, see the [Administrator's Guide for System Center - Service Manager](admin-administering-system-center-2016-service-manager.md).  

 Although there are many steps in extending the change management process, Ken has to think about four main things, which are described in the following sections.  

## Create new custom activity  
 A standard change request consists of two activities, a default review activity, and a default manual activity. In the new compliance change request process, Ken will perform the default review activity first, but the second activity is customized. Ken will create a new custom change request activity that uses a Windows Workflow Foundation \(WF\) workflow to automatically add a computer to an Active&nbsp;Directory group. Automating this change request process means that after the change is approved, the change will be completed without further user interaction. The custom activity is at the core of the new compliance change request process.  

## Create additional custom objects  
 Additionally, Ken will create new custom objects, such as a template, a queue, and a view to support working with the new type of activity. If email notifications are configured in the environment, in the final steps of the scenario, Ken can configure email notifications to send confirmation email messages after the activity is complete.  

## Save custom objects in a management pack  
 Ken saves the custom objects to the Automated Activity: Add Computer to AD Group management pack so that he can transfer these objects between the Service Manager console and the Service Manager Authoring Tool.  

## Use the customized process  
 Eventually, after Ken imports the custom management pack into Service Manager and completes the creation of all the necessary custom objects, he can use the new process for compliance change requests. He creates a new compliance change request to add the ADComputer1 computer to the GP\_AUTHAPPS AD DS group. He can then monitor the process to confirm that the new computer is successfully added to the group.  
