---
title: Query ConfigMgr activity
description: Describes the configurable properties for the Query ConfigMgr activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6ea8b08-b182-45dd-a680-2b06bc62ce8e
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---

# Query ConfigMgr activity for Configuration Manager Integration Pack

Applies To: System Center 2016 - Orchestrator

The Query ConfigMgr activity allows users to run an ad-hoc WQL query
against Configuration Manager, returning the query results to published
data for further action.

>[!CAUTION]
>Some pre-built queries will fail when run via the Configuration Manager WQL interface:
  -   All Audit Status Messages for a Specific User
  -   All Audit Status Messages from a Specific Site
  -   All Status Messages
  -   Remote Control Activity Initiated from a Specific System
  -   Systems by Last Logged On User
  -   All Status Messages for a Specific Collection at a Specific Site
  -   All Status Messages for a Specific Package at a Specific Site
  -   All Status Messages for a Specific Deployment at a Specific Site
  -   All Status Messages from a Specific Component at a Specific Site
  -   All Status Messages of a Specific Severity from a Specific Source at a Specific Site
  -   All Status Messages from a Specific System
  -   All Status Messages from a Specific Site
  -   All Status Messages from a Specific Component on a Specific System
  -   All Systems with Specified Software File Name and File Size
  -   All Systems with Specified Software Product Name and Version
  -   Boundaries Created, Modified, or Deleted
  -   Client Component Configuration Changes
  -   Client Components Experiencing Fatal Errors
  -   Client Configuration Requests (CCRs) Processed Unsuccessfully
  -   Clients Assigned to or Unassigned from a Specific Site
  -   Clients That Failed to Run a Specific Deployed Program Successfully
  -   Clients That Failed to Start a Specific Deployed Program
  -   Clients That Ran a Specific Deployed Program Successfully
  -   Clients That Received a Specific Deployed Program
  -   Clients That Rejected a Specific Deployed Program
  -   Clients That Reported Errors or Warnings During Inventory File Collection
  -   Clients That Reported Errors or Warnings While Creating a Hardware Inventory File
  -   Clients That Reported Errors or Warnings While Creating a Software Inventory File
  -   Clients That Started a Specific Deployed Program
  -   Collection Member Resources Manually Deleted
  -   Collections Created, Modified, or Deleted
  -   Deployments Created, Modified, or Deleted
  -   Packages Created, Modified, or Deleted
  -   Programs Created, Modified, or Deleted
  -   Queries Created, Modified, or Deleted
  -   Remote Control Activity Initiated at a Specific Site
  -   Remote Control Activity Initiated by a Specific User
  -   Remote Control Activity Targeted at a Specific System
  -   Server Component Configuration Changes
  -   Server Components Experiencing Fatal Errors
  -   Server Components Flagged with Warning or Critical Status
  -   Site Addresses Created, Modified, or Deleted
  -   Site Systems Flagged with Warning or Critical Status

The activity publishes all of the data from the required and optional
properties into published data. The following tables list the required
and optional properties and published data for this activity.

## Query ConfigMgr required properties

|Element|Description|Valid Values|
|---|---|---|
|Query|Performs a WMI query against ConfigMgr and returns the results||    
|Query Value Type|The type of query|Query Name, Query ID, or Query String|

## Query ConfigMgr published data

|Element|Description|
|---|---|
|Query results|The query results are returned as a collection of items|   
