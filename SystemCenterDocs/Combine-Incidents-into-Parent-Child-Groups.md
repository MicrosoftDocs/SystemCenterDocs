---
title: Combine Incidents into Parent-Child Groups
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d548b0a-e1b4-4b9b-9597-4056a832f1da
---
# Combine Incidents into Parent-Child Groups
Incidents in [!INCLUDE[smshort](../Token/smshort_md.md)] are usually short\-lived while help desk analysts investigate and then restore operations. Often, incidents are related and it is useful to group incidents together. You can create a parent incident to group other existing incidents together, which can help provide visibility into them and their relationship to one another.

A  [!INCLUDE[smshort](../Token/smshort_md.md)] administrator can define automatic incident resolution settings so that when a parent incident is resolved, all its child incidents resolve automatically, do not resolve automatically, or to let the analyst decide whether to resolve or not. Similarly, an administrator can also define automatic incident reactivation settings so that when a parent incident is reactivated, all its child incidents reactivate automatically, do not reactivate automatically, or to let the analyst decide whether to reactivate the child incidents. Both processes can help you verify that all child incidents are resolved or activated together as a group.

## Manage incidents with parent\-child groups

1.  Create a parent incident from an incident form that is already opened

2.  Or, you can link an open incident to an existing parent incident

3.  Resolve a parent incident and its child incidents

4.  Link an active incident to a resolved parent incident

5.  Reactivate a resolved parent incident and automatically reactivate its child incidents

6.  Create a parent incident template that new incidents are created from

7.  Open a parent incident from a child incident

8.  Create a new child incident and link it to a related parent incident

