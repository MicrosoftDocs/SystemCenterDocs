---
title: Recommended deployment topology scenarios
description: Recommended deployment topology scenarios for Service Manager.
ms.service: system-center
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 05/16/2023
ms.subservice: service-manager
ms.topic: article
ms.custom: UpdateFrequency2, engagement-fy23
---

# Recommended deployment topologies for Service Manager


For performance and scalability planning purposes, we recommend that you plan your deployment topology for System Center - Service Manager using scenarios that we've tested. While these aren't firm guidelines, Microsoft has tested deployment topologies using these scenarios and found that each configuration achieves satisfactory performance.  

## Test and small deployment scenarios

The test and small deployment scenarios contain only two servers and support 100 to 2,000 computers. In these configurations, a single physical computer hosts a virtual server.

Select the required tab to view the Service Manager roles and hardware configuration for the Test and small deployment scenarios:

# [Test scenario](#tab/Test)

 In this scenario, we recommend the following Service Manager roles and hardware as described.  

Service Manager roles:  

- One computer with a Service Manager management server, a Service Manager database, SharePoint server\/site and web content server (WCS), and Service Manager console.  
- One data warehouse server. The Self-Service Portal should be placed on a computer other than the one hosting the data warehouse.  

Hardware configuration:  

- 8-core 2.66 GHz CPU
- 16-GB RAM (5 GB for each virtual computer and 1 GB for the host computer)
- 100 GB of available disk space

This configuration was tested with the following load.  

|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|Up to 500|  
|Number of Computers in the  Service Manager database|500|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|20|  
|Number of Concurrent Consoles|2|  
|Is the Self-Service Portal Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|  

# [Small scenario](#tab/Small)

In this scenario, we recommend the following hardware configured for roles and hardware as described.  

Service Manager roles:  

- One computer with a management server, Service Manager database, and Service Manager console.  
- One data warehouse server. The Self-Service Portal should be placed on a physical host or on a virtual computer other than the computer hosting the data warehouse.  

Hardware configuration:  

- 8-core 2.66 GHz CPU  
- 16-GB RAM (5 GB for each virtual computer and 1 GB for the host computer)  
- 100 GB of available disk space, which doesn't include the .vhd file disk space requirements on the host computer  

This configuration was tested with the following load.  

|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|501 to 2,000|  
|Number of Computers in the  Service Manager database|2,000|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|100|  
|Number of Concurrent Consoles|10|  
|Is the Self-Service Portal Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|  

---

## Medium deployment scenario

The medium deployment scenario contains two servers and supports 2,001 to 5,000 computers. In this configuration, two physical computers host the Service Manager management server and Service Manager data warehouse management server.  

We recommend the following hardware, configured for roles and hardware as described.  

Hardware configuration for the Service Manager management server:  

- 4-core 2.66 GHz CPU  
- 8-GB RAM  
- 2 disk RAID 1  

Hardware configuration for the Service Manager data warehouse management server:  

- 4-core 2.66 GHz CPU  
- 8-GB RAM  
- 2 disk RAID 1  

Hardware configuration for the Self-Service Portal with web content server with SharePoint Web Parts:  

- 8-core, 64-bit CPU  
- 16 - 32 GB RAM, depending on the size of the expected database  
- 80 GB of available hard disk space  

This configuration was tested with the following load.  

|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|2,001 to 5,000|  
|Number of Computers in the Service Manager database|3,000|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|150|  
|Number of Concurrent Consoles|15 to 30|  
|Is the Self-Service Portal Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|  

## Large deployment scenario

The large deployment scenario contains four servers and supports 5,001 to 20,000 computers. In this large configuration, four physical computers host server roles.  

In this scenario, we recommend the following hardware, configured for roles and hardware as described.  

Hardware configuration for the Service Manager management server:  

- 4-core 2.66 GHz CPU  
- 8 GB RAM  
- 2 disk RAID 1  
- 10 GB of available hard disk space  

Hardware configuration for the Service Manager data warehouse management server:  

- 4-core 2.66 GHz CPU  
- 8-GB RAM  
- 2 disk RAID 1  
- 10 GB of available hard disk space  

Hardware configuration for the Service Manager database server:  

- 8-core 2.66 GHz CPU  
- 8 - 32 GB RAM, depending on the size of the expected database  
- 4 RAID 1\+0 disk drives for data  
- 2 RAID 1 disk drives for logs  

Hardware configuration for the Service Manager data warehouse database server:  

- 8-core 2.66 GHz CPU  
- 8-GB RAM  
- 4 RAID 1\+0 disk drives for data  
- 2 RAID 1 disk drives for logs  
- 80 GB of available hard disk space  

Hardware configuration for the Self-Service Portal with web content server:  

- 4-core 2.66 GHz CPU  
- 8 \- 16 GB RAM, depending on the size of the expected database  
- 1 GB of available hard disk space  

Hardware configuration for the Self-Service Portal with SharePoint web parts:  

- 4-Core 2.66 GHz CPU  
- 8-GB RAM  
- 80 GB of available hard disk space  

This configuration was tested with the following load.  

|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|5,001 to 20,000|  
|Number of Computers in the  Service Manager database|20,000|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|2,000|  
|Number of Concurrent Consoles|40 to 60|  
|Is the Self-Service Portal Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|  

## Advanced deployment scenario

The advanced deployment scenario contains more than four servers and supports more than 20,000 computers. Each additional management server can host up to 60 Service Manager consoles.  

In this scenario, we recommend the following hardware, configured for roles and hardware as described.  

Hardware configuration for the Service Manager management server:  

- 4-core 2.66 GHz CPU  
- 8-GB RAM  
- 2 disk RAID 1  
- 10 GB of available hard disk space  

Hardware configuration for each additional Service Manager management server:  

- 4-core 2.66 GHz CPU  
- 8-GB RAM  
- 2 RAID 1 disk drives  

Hardware configuration for the Service Manager data warehouse management server:  

- 4-core 2.66 GHz CPU  
- 8-GB RAM  
- 2 RAID 1 disk drives  
- 10 GB of available hard disk space  

Hardware configuration for the Service Manager database server:  

- 8-core 2.66 GHz CPU  
- 8-GB RAM to 32-GB RAM, depending on the expected size of the database  
- 4 RAID 1\+0 disk drives for data  
- 2 RAID 1 disk drives for logs  

Hardware configuration for the Service Manager data warehouse database server:  

- 8-core 2.66 GHz CPU
- 8 - 16 GB RAM, depending on the size of the expected database  
- 4 RAID 1\+0 disk drives for data  
- 2 RAID 1 disk drives for logs  

Hardware configuration for the Self-Service Portal with web content server:  

- 4-core 2.66 GHz CPU
- 8 - 16 GB RAM, depending on the size of the expected database  
- 1 GB of available hard disk space  

Hardware configuration for the Self-Service Portal with SharePoint web parts:  

- 4-core 2.66 GHz CPU
- 8-GB RAM  
- 80 GB of available hard disk space  

Hardware configuration for each Service Manager console:  

- 2-core 2.0 GHz CPU  
- 4-GB RAM  
- 10 GB of available hard disk space  

This configuration was tested with the following load.  

|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|More than 20,000|  
|Number of Computers in the Service Manager database|20,000 to 50,000 or more|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|2,000 or more|  
|Number of Concurrent Consoles|60 to 100|  
|Is the Self-Service Portal Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|

## Next steps

To learn about deploying Service Manager in one of several different scenarios, review [Deploy System Center - Service Manager](deploy-sm.md).
