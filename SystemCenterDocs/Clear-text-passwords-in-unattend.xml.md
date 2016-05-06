---
title: Clear text passwords in unattend.xml
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6edef97a-d93b-4f8f-ae01-486952c6d69b
---
# Clear text passwords in unattend.xml
There is a possibility that if the installation of a VMM host fails to complete successfully, the installation process might not delete some temporary files. In this situation, a file named unattend.xml might remain on your computer. It is possible that unencrypted passwords might be visible in this file. To improve security, we recommend the following:

-   Manually delete the file named unattend.xml.

-   During installation, use an account with only domain join privileges, not a full administrator’s account.

