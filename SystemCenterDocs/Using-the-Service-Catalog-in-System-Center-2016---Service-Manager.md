---
title: Using the Service Catalog in System Center 2016 - Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37c13875-a46b-4387-b35a-5d2c8f511f56
---
# Using the Service Catalog in System Center 2016 - Service Manager
This section provides an overview of how to use the service catalog in Service Manager. This section also contains procedures that cover management configuration scenarios for the service catalog.

The service catalog is a collection of items, assistance, actions, or groupings of them that  your IT staff and infrastructure provides and makes available to end users in the [!INCLUDE[smssp](./Token/smssp_md.md)] in Service Manager. In the [!INCLUDE[smcons](./Token/smcons_md.md)], you create catalog items to describe these items in the Library workspace using the following nodes:

-   Request Offerings

-   Service Offerings

The Request Offerings node is used to create a catalog item that describes an item, assistance, or action that is available to end users. It also defines information that you want to prompt the users for and any knowledge articles that are associated with the offering.

After it is created, you can set the status of a request offering as either Draft or Published. Draft status indicates that a request offering is not published and available to the service catalog. This prevents end users from requesting the offering. When you set the request offering status to Published, it appears in the catalog where users can request it, if they have been granted access to a catalog item group that contains the request offering. It is possible to create a request offering that is not part of a service offering. In this case, the request offering appears in the [!INCLUDE[smssp](./Token/smssp_md.md)] under an uncategorized list view.

The Service Offerings node is used to create a catalog item that categorizes request offerings.


