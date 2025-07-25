---
title: Service Manager Editions
description: Learn about Service Manager editions.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 04/02/2025
ms.subservice: service-manager
ms.topic: article
ms.custom: UpdateFrequency5, engagement-fy24
---
# System Center - Service Manager editions



System Center - Service Manager is available as both a retail edition and a select edition. Both editions offer the same functionality. The retail edition is purchased separately, and it includes a product key that you enter during setup. The select edition is delivered as part of a Microsoft Volume Licensing plan, and a product key isn't required.  

During setup of the retail edition of System Center - Service Manager, you have the option of performing the installation without a product key and instead installing Service Manager as an evaluation edition. The evaluation edition times out 180 days after installation. If you start with an evaluation version of Service Manager and you rerun Setup and install the retail edition or select edition, and you decide to use the existing databases that you created originally, your installation will time out after the original expiration date.  

## Service Manager editions 

The following table describes the interactions between the various editions of Service Manager.  

If you started with&nbsp;...|And then rerun Setup to install&nbsp;...|Will the new installation time out?|  
|---------------------------|---------------------------------------|-----------------------------------------|  
|Evaluation Edition|Retail Edition|Yes|  
|Evaluation Edition|Select Edition|Yes|  
|Retail Edition|Evaluation Edition|No|  
|Retail Edition|Select Edition|No|  
|Select Edition|Retail Edition|No|

## Next steps

To learn about the hardware and software configurations for Service Manager, review [supported configurations](supported-configs.md). Specific considerations about the memory that servers need to support Service Manager are included.
