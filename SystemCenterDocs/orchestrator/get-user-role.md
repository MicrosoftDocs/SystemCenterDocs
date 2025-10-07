---
title: Get User Role
description: Returns data on all the user roles within the VMM server.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 2c0732bd-d486-48c2-ae47-b35d42b45810
author: Jeronika-MS
ms.author: v-gajeronika
---

# Get User Role

Returns data on all the user roles within the VMM server.

>[!IMPORTANT]
>When designating a computer, you must specify it using the FQDN. FQDN names are case sensitive.

## Get User Role Required Properties

None

## Get User Role Optional Properties

None

## Get User Role Filters

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
| Most Recent   | True or False.   |   |
| User Role ID   | The unique identifier (GUID) of the user role.   |   |
| User Role Name   | The names of the user role.   |   |
| Application Profile Resource Names   |   |   |
| Guest OS Profile Resource Names   |   |   |
| Hardware Profile Resource Names   |   |   |
| Service Configuration Resource Names |   |   |
| Service Instance Resource Names   |   |   |
| Service Template Resource Names   |   |   |
| SQL Profile Resource Names   |   |   |
| VM Instance Resource Names   |   |   |
| VM template Resource Names   |   |   |

## Get User RolePublished Data

| Element   | Description   |
|:---|:---|
| User Role ID   | The ID of the user role.   |   
| User Role Name   | The name of the user role.   |   
| Profile Type   | The profile type of the user role. |   
| Host Group Names in Scope   |   |   
| Cloud Names in Scope   |   |   
| Actions Permitted   | List of actions permitted.   |   
| Member Names   | Members of the user role.   |   
| Description   | Text description of the user role. |   
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
