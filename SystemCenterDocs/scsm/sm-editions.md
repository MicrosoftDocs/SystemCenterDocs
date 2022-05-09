---
title: Service Manager editions
description: Learn about Service Manager editions.
manager: evansma
ms.prod: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 01/23/2018
ms.technology: service-manager
ms.topic: article
---
# System Center - Service Manager editions

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

System Center - Service Manager is available as both a retail edition and a select edition. Both editions offer the same functionality. The retail edition is purchased separately, and it includes a product key that you enter during setup. The select edition is delivered as part of a Microsoft Volume Licensing plan, and a product key is not required.  

 During setup of the retail edition of System Center - Service Manager, you have the option of performing the installation without a product key and instead installing Service Manager as an evaluation edition. The evaluation edition times out 180 days after installation. If you start with an evaluation version of Service Manager and you rerun Setup and install the retail edition or select edition, and you decide to use the existing databases that you created originally, your installation will time out after the original expiration date.  

 The following table describes the interactions between the various editions of Service Manager.  

|If you started with&nbsp;...|And then rerun Setup to install&nbsp;...|Will the new installation time out?|  
|---------------------------|---------------------------------------|-----------------------------------------|  
|Evaluation Edition|Retail Edition|Yes|  
|Evaluation Edition|Select Edition|Yes|  
|Retail Edition|Evaluation Edition|No|  
|Retail Edition|Select Edition|No|  
|Select Edition|Retail Edition|No|

## Next steps

- Review [supported configurations](supported-configs.md), to learn about the hardware and software configurations for Service Manager. Specific considerations about the memory that servers need to support Service Manager are included.
