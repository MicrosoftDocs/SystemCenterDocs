---
title: Get User Role Quota activity in System Center - Orchestrator
description: The Get User Role Quota activity is used in a runbook to return information about all user role quotas in a VMM management server.
ms.date: 11/01/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency3, engagement-fy23, engagement-fy24
---

# Get User Role Quota activity

The Get User Role Quota activity is used in a runbook to return information about all user role quotas in a VMM management server.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Required properties

This activity has no required properties.

## Optional properties

This activity has no optional properties.

## Filters

| Element   | Description   | Valid Values   |
|:---|:---|:---|
| Actions Permitted   | The actions that members of a Self-Service User role can perform on their virtual machines or services. | AllowLocalAdmin, Author, CanShare, CanReceive, Checkpoint,CheckpointRestoreOnly, Create, CreateFromVHDOrTemplate, PauseAndResume, RemoteConnect, Remove, Save, Shutdown, Start, Stop, Store. |
| Cloud Names in Scope   | The cloud scope of a user role.   |   |
| Host Group Names in Scope   | The host scope of a user role (not for Self-Service User Role).   |   |
| Description   | An alphanumeric description of the user role.   |   |
| Library Server Names   | The library server that the user role can use. (not for Self-Service User Role)   |   |
| Member Names   | Members of a user role.   |   |
| Profile Type   | The type of VMM user role.   | Administrator, SelfServiceUser, ReadOnlyAdmin, DelegatedAdmin   |
| User Role data Path   | The library path that each member of this user role can upload their data to   | \\\\MyLibraryServer.CONTOSO.com\\OneUserRoleVMMLibrary   |
| Most Recent   | True or False   |   |
| User Role ID   | The unique identifier (GUID) of the user role   |   |
| User Role Name   | The names of the user role   |   |
| Application Profile Resource Names   |   |   |
| Guest OS Profile Resource Names   |   |   |
| Hardware Profile Resource Names   |   |   |
| Service Configuration Resource Names |   |   |
| Service Instance Resource Names   |   |   |
| Service Template Resource Names   |   |   |
| SQL Profile Resource Names   |   |   |
| VM Instance Resource Names   |   |   |
| VM template Resource Names   |   |   |

## Published data

| Element   | Description    |
|:---|:---|
| User Role ID   | The ID of the user role   |   
| User Role Name   | The name of the user role   |   
| Profile Type   | The profile type of the user role |   
| Host Group Names in Scope   |   |   
| Cloud Names in Scope   |   |   
| Actions Permitted   | List of actions permitted   |   
| Member Names   | Members of the user role   |   
| Description   | Text description of the user role |   
| User Role Data Path   |   |   
| Library Server Names   |   |   
| VM Template Resource Names   |   |   
| Service Template Resource Names   |   |   
| Service Instance Resource Names   |   |   
| VM Instance Resource Names   |   |   
| Hardware Profile Resource Names   |   |   
| Application Profile Resource Names   |   |   
| Guest OS Profile Resource Names   |   |   
| SQL Profile Resource Names   |   |   
| Service Configuration Resource Names |   |   
