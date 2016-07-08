---
title: Examples of Using Advanced Search in Operations Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b27af613-4283-4fc5-bb5a-c5af294bdd22
author:mgoedtel
manager:cfreemanwa
---
# Examples of Using Advanced Search in Operations Manager
The following table lists examples of using advanced search to find objects in [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)]:  
  
|To find|Use this object, condition, and value|  
|-----------|-----------------------------------------|  
|All alerts closed in the previous 2 hours.|-   **Object:** Alerts<br />-   **Condition\/Value:** With specific resolution state\/Closed<br />-   **Condition\/Value:** That was resolved in a specific time period\/Last 2 Hours|  
|All rules that have overrides|-   **Object:** Rules<br />-   **Condition:** the rule has been overridden for any context \(excluding category overrides\)|  
|All monitors that auto\-resolve alerts|-   **Object:** Monitors<br />-   **Condition:** auto\-resolves alerts|  
|All Unix computers in a warning or critical state|-   **Object:** Managed Objects<br />-   **Condition\/Value:** In specific health state\/warning, critical<br />-   **Condition\/Value:** Contained in a specific group\/Unix Computer Group|  
|||  
|||  
|||  
|||  
|||  
|||  
  
## See Also  
[Finding Data and Objects in the Operations Manager Consoles](../../om/manage/Finding-Data-and-Objects-in-the-Operations-Manager-Consoles.md)  
[Using Advanced Search](../../om/manage/Using-Advanced-Search.md)  
  
