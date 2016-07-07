---
title: Configurations for Deployment Scenarios
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e9a7de24-e680-4a93-9d81-e8d3bf41a7ce
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Configurations for Deployment Scenarios
For performance and scalability planning purposes, we recommend that you plan your deployment topology for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] using scenarios that we have tested. While these are not firm guidelines, Microsoft has tested deployment topologies using these scenarios and found that each configuration achieves satisfactory performance.  
  
## Test and Small Deployment Scenarios  
 The test and small deployment scenarios contain only two servers and support 100 to 2,000 computers. In these configurations, a single physical computer hosts a virtual server.  
  
### Test Scenario  
 In this scenario, we recommend the following Service Manager roles and hardware as described.  
  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] roles:  
  
-   One computer with a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, SharePoint server\/site and web content server \(WCS\), and [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
-   One data warehouse server. The [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] should be placed on a computer other than the one hosting the data warehouse.  
  
 Hardware configuration:  
  
-   8\-core 2.66 GHz CPU  
  
-   16 GB RAM \(5 GB for each virtual computer and 1 GB for the host computer\)  
  
-   100 GB of available disk space  
  
 This configuration was tested with the following load.  
  
|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|Up to 500|  
|Number of Computers in the  [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database|500|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|20|  
|Number of Concurrent Consoles|2|  
|Is the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|  
  
### Small Scenario  
 In this scenario, we recommend the following hardware, configured for roles and hardware as described.  
  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] roles:  
  
-   One computer with a management server, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, and [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
-   One data warehouse server. The [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] should be placed on a physical host or on a virtual computer other than the computer hosting the data warehouse.  
  
 Hardware configuration:  
  
-   8\-core 2.66 GHz CPU  
  
-   16 GB RAM \(5 GB for each virtual computer and 1 GB for the host computer\)  
  
-   100 GB of available disk space, which does not include the .vhd file disk space requirements on the host computer  
  
 This configuration was tested with the following load.  
  
|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|501 to 2,000|  
|Number of Computers in the  [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database|2,000|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|100|  
|Number of Concurrent Consoles|10|  
|Is the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|  
  
### Medium Scenario  
 The medium deployment scenario contains two servers and supports 2,001 to 5,000 computers. In this configuration, two physical computers host the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse management server.  
  
 We recommend the following hardware, configured for roles and hardware as described.  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   2 disk RAID 1  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse management server:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   2 disk RAID 1  
  
 Hardware configuration for the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] with web content server with SharePoint Web Parts:  
  
-   8\-core, 64\-bit CPU  
  
-   16 \- 32 GB RAM, depending on the size of the expected database  
  
-   80 GB of available hard disk space  
  
 This configuration was tested with the following load.  
  
|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|2,001 to 5,000|  
|Number of Computers in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database|3,000|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|150|  
|Number of Concurrent Consoles|15 to 30|  
|Is the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|  
  
## Large Deployment Scenario  
 The large deployment scenario contains four servers and supports 5,001 to 20,000 computers. In this large configuration, four physical computers host server roles.  
  
 In this scenario, we recommend the following hardware, configured for roles and hardware as described.  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   2 disk RAID 1  
  
-   10 GB of available hard disk space  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse management server:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   2 disk RAID 1  
  
-   10 GB of available hard disk space  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database server:  
  
-   8\-core 2.66 GHz CPU  
  
-   8 \- 32 GB RAM, depending on the size of the expected database  
  
-   4 RAID 1\+0 disk drives for data  
  
-   2 RAID 1 disk drives for logs  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse database server:  
  
-   8\-core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   4 RAID 1\+0 disk drives for data  
  
-   2 RAID 1 disk drives for logs  
  
-   80 GB of available hard disk space  
  
 Hardware configuration for the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] with web content server:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 \- 16 GB RAM, depending on the size of the expected database  
  
-   1 GB of available hard disk space  
  
 Hardware configuration for the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] with SharePoint web parts:  
  
-   4\-Core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   80 GB of available hard disk space  
  
 This configuration was tested with the following load.  
  
|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|5,001 to 20,000|  
|Number of Computers in the  [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database|20,000|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|2,000|  
|Number of Concurrent Consoles|40 to 60|  
|Is the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|  
  
## Advanced Deployment Scenario  
 The advanced deployment scenario contains more than four servers and supports more than 20,000 computers. Each additional management server can host up to 60 [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]s.  
  
 In this scenario, we recommend the following hardware, configured for roles and hardware as described.  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   2 disk RAID 1  
  
-   10 GB of available hard disk space  
  
 Hardware configuration for each additional [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   2 RAID 1 disk drives  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse management server:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   2 RAID 1 disk drives  
  
-   10 GB of available hard disk space  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database server:  
  
-   8\-core 2.66 GHz CPU  
  
-   8 GB RAM to 32 GB RAM, depending on the expected size of the database  
  
-   4 RAID 1\+0 disk drives for data  
  
-   2 RAID 1 disk drives for logs  
  
 Hardware configuration for the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] data warehouse database server:  
  
-   8\-core 2.66 GHz CPU  
  
-   8 \- 16 GB RAM, depending on the size of the expected database  
  
-   4 RAID 1\+0 disk drives for data  
  
-   2 RAID 1 disk drives for logs  
  
 Hardware configuration for the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] with web content server:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 \- 16 GB RAM, depending on the size of the expected database  
  
-   1 GB of available hard disk space  
  
 Hardware configuration for the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] with SharePoint web parts:  
  
-   4\-core 2.66 GHz CPU  
  
-   8 GB RAM  
  
-   80 GB of available hard disk space  
  
 Hardware configuration for each [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] console:  
  
-   2\-core 2.0 GHz CPU  
  
-   4 GB RAM  
  
-   10 GB of available hard disk space  
  
 This configuration was tested with the following load.  
  
|Description|Value|  
|-----------------|-----------|  
|Number of Supported End Users|More than 20,000|  
|Number of Computers in the Service Manager database|20,000 to 50,000 or more|  
|Number of New Incidents per Month for each computer|2|  
|Number of New Change Requests per Month|2,000 or more|  
|Number of Concurrent Consoles|60 to 100|  
|Is the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] Installed?|Yes|  
|Is the Active Directory Connector Enabled?|Yes|  
|Is the Configuration Manager Connector Enabled?|Yes|  
|Is the Operations Manager Connector Enabled?|Yes|