---
title: Watcher Nodes
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 63abfb68-9449-4922-940c-0f4b80f8c4b1
---
# Watcher Nodes
A *watcher node* is an agent that runs monitors and rules that test an application or feature on another computer. The following management pack templates use watcher nodes:

-   **OLE DB Data Source**

-   **TCP Port**

-   **Web Application Transaction Monitoring**

When you use one of these templates, you must specify one or more watcher nodes to run the monitor.

**Conceptual view of watcher nodes**

![](/Image/OM12Author_WatcherNode.gif)

A watcher node can either be the agent with the application or feature installed, or it can be a separate agent. If the watcher node is a separate computer, in addition to ensuring that the application or feature is healthy, the watcher node can validate that clients can connect to it and  test such additional features as security, network availability, and firewalls.

You can best ensure availability of an application or feature by specifying watcher nodes in different network segments. For example, a database might be accessed from application servers in each of two different network segments. While the database might be available to one set of servers, an issue such a problem with a network device could make it inaccessible to servers on the other segment. If you use the **OLE DB Data Source** template to create a monitor for the database with a watcher node in each segment, you are assured that any problem accessing the database is detected.

You can also specify the computer with the application or feature itself as a watcher node. This watcher node performs the test without relying on any external features.

## See Also
[TCP Port Template](./TCP-Port-Template.md)
[OLE DB Data Source Template](./OLE-DB-Data-Source-Template.md)
[Web Application Transaction Monitoring Template](./Web-Application-Transaction-Monitoring-Template.md)


