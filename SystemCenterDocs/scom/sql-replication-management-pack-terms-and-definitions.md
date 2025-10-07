---
ms.assetid: 8229529e-f43d-4ab2-bbea-14edc1ba34ec
title: Terms and definitions in Management Pack for SQL Server Replication
description: This article explains Terms and Definitions
author: Anastas1ya
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Terms and Definitions

The following terms and definitions are mentioned throughout this guide:

- **Distributor**

  Distributor is a database instance that acts as a store for replication of specific data associated with one or more Publishers. Each Publisher is associated with a single database (known as a distribution database) at the Distributor. In many cases, a single database server instance acts as both the Publisher and Distributor. This is known as a local Distributor. When Publisher and Distributor are configured on separate database server instances, the Distributor is known as a remote Distributor.

- **Distribution database**

  Distribution database stores replication status data, metadata about the publication, and, in some cases, acts as a queue for data moving from the Publisher to Subscribers. In many cases, a single database server instance acts as both Publisher and Distributor. This is known as a local Distributor. When Publisher and Distributor are configured on separate database server instances, the Distributor is known as a remote Distributor.

- **Publisher**

  Publisher is a database instance that makes data available to other locations through replication. A Publisher can have one or more publications, each defining a logically related set of objects and data to replicate.

- **Publication**

  Publication is a collection of one or more articles from one database. Such grouping of multiple articles into a publication makes it easier to specify a logically related set of data and database objects that are replicated as a unit. A publication can contain different types of articles, including tables, views, stored procedures, and other objects. When tables are published as articles, filters can be used to restrict the columns and rows of the data sent to Subscribers.

- **Article**

  Article identifies a database object that is included in a publication.

- **Subscriber**

  Subscriber is a database instance that receives replicated data. A Subscriber can receive data from multiple Publishers and publications. Depending on the selected replication type, a Subscriber can also pass data changes back to the Publisher, or republish the data to other Subscribers.

- **Subscription**

  Subscription is a request for a copy of a publication to be delivered to a Subscriber. A subscription defines what publication will be received, where, and when. There are two types of subscriptions: push and pull.

- **Push subscription**

  Push subscription is represented by a subscription created and administered at the Publisher. The distribution agent or merge agent for this subscription runs at the Distributor. For more information about subscriptions, see [Subscribe to Publications](/sql/relational-databases/replication/subscribe-to-publications).

- **Pull Subscription**

  Pull subscription is represented by a subscription configured and maintained at each recipient. The subscribers administer the synchronization schedules and can pull changes whether they consider it necessary. For more information about subscriptions, see [Subscribe to Publications](/sql/relational-databases/replication/subscribe-to-publications).

- **Virtual Distributor**

  Virtual Distributor is a virtual entity that serves to represent a real distributor on the diagram view for a Replication Database Health.

- **Virtual Publisher**

  Virtual Publisher is a virtual entity that serves to represent a real publisher on the diagram view for a Replication Database Health.

- **Virtual Subscriber Host**

  Virtual Subscriber Host is a virtual entity that contains Virtual Subscribers.

- **Virtual Subscriber**

  Virtual Subscriber is a virtual entity that serves to represent a real Subscriber on the diagram view for a Replication Database Health.

- **Virtual Publication Host**

  Virtual Publication Host is a virtual entity that contains Publications.

- **Publication database**

  Publication database is the database on the Publisher that is the source of data and database objects to be replicated.

- **Virtual Subscription**

  Virtual Subscription is a virtual entity that serves to represent a real subscription on the diagram view for a Replication Database Health. The purpose of this entity is to hide all subscriptions when the diagram is opened for the first time.
