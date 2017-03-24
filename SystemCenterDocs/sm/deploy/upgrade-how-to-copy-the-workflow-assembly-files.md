---
title: Copy customized workflow assembly files
description: Before you upgrade to System Center 2016 - Service Manager, you need to copy your customized workflow assembly files.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48fa12ca-e61b-4658-8eda-f9cc3af16dfc
---

# Copy customized workflow assembly files before you upgrade

>Applies To: System Center 2016 - Service Manager

Use the following procedure to copy the workflow assembly files from the Service Manager Installation folder on the primary management server to the secondary management server that you created in the previous procedure.  

### To copy the workflow assembly files  

1.  On the computer that is running the Service Manager Primary Server role, browse to the Service Manager Installation folder for example, C:\\Program Files\\Microsoft System Center\\Service Manager copy the workflow files (workflow.dll).  

2.  On the computer that is running the Service Manager Secondary server; browse to the Service Manager Installation folder; for example, C:\\Program Files\\Microsoft System Center\\Service Manager. Paste the copied workflow files into this folder. You should overwrite any existing files.  

    > [!NOTE]  
    >  You must place the workflow assembly files in the Service Manager installation folder. This is very important step if you want to test the custom workflows that depend on workflow assembly files. Failure to copy these files would lead to failed custom workflows in the lab environment.

## Next steps

- Review [Disable connectors in the production environment before you upgrade](upgrade-how-to-disable-service-manager-connectors-in-the-production-environment.md).
