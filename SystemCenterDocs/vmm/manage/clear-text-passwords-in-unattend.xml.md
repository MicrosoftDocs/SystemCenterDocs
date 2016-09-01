---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Clear text passwords in unattend.xml
ms.technology:  virtual-machine-manager
ms.assetid:  6edef97a-d93b-4f8f-ae01-486952c6d69b
---

# Clear text passwords in unattend.xml

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

There is a possibility that if the installation of a VMM host fails to complete successfully, the installation process might not delete some temporary files. In this situation, a file named unattend.xml might remain on your computer. It is possible that unencrypted passwords might be visible in this file. To improve security, we recommend the following:

-   Manually delete the file named unattend.xml.

-   During installation, use an account with only domain join privileges, not a full administrator"s account.



