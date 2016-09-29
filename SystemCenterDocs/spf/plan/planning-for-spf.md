---
title: Planning for Service Provider Foundation
description: This topic provides an overview of how to plan for a Service Provider Foundation installation.
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 617ee2c1-4dea-40e6-85b3-d87b15c0221d
author: rayne-wiselman
manager: cfreeman
ms.author: raynew
ms.date: 10/12/2016

---
# Planning for Service Provider Foundation

>Apples To: System Center 2016 - Service Provider Foundation

You will need to make several decisions before you deploy SPF. Read this topic and the topics listed under Next steps for general guidance on planning your SPF installation.

The following capacity information is to accommodate tenant usage of up to 25,000 virtual machines.

## Database storage
5 GB is sufficient storage for even large Service Provider Foundation databases.

## Hardware recommendations for servers
The following server scenarios each pertain to the recommendations listed in the following table.

-   Virtual Machine Manager \(VMM\) with or without SQL Server

-   Service Provider Foundation with or without SQL Server


|5,000 or Fewer Virtual Machines|5,000 - 12,000 Virtual Machines|12,000 - 25,000 Virtual Machines|
|-----------------------------------|-----------------------------------|------------------------------------|
|4 processor cores, 8 GB RAM|8 processor cores, 8 GB RAM.<br /><br />4 processor cores, 8 GB RAM is sufficient for computers running App Controller  with or without SQL Server.|16 processor cores, 8 GB RAM recommended only for computers running VMM with or without SQL Server.|

## Web service settings
By default, Service Provider Foundation supports up to 1000 concurrent requests for its web services. We recommend this be a lower number in a production environment. You can change this configuration by specifying the value for the **MaxRequestsPerTimeSlot** key in the **C:\\inetpub\\SPF\\web.config** file.

## Next Steps

- To learn more about security considerations for SPF see [Security Planning](/security-planning-for-service-provider-foundation.md)
- To learn more about the security requirements for the various SPF users see [Security Planning](\security-planning-for-service-provider-foundation.md)
