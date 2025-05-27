---
ms.assetid: 
title: Configure an HTTPS binding for a Windows Server CA
description: This article describes how to configure an HTTPS binding for a Windows Server CA.
author: jyothisuri
ms.author: jsuri

ms.date: 11/01/2024
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Configure an HTTPS binding for a Windows Server CA

If you're setting up a new certification authority (CA) for the first time for use with System Center – Operations Manager, use the following procedure to configure an HTTPS binding for the CA.

## Configure an HTTPS binding

To configure an HTTPS binding, do the following:

1. On the computer hosting your CA, on the Windows desktop, select **Start** > **Programs** > **Administrative Tools**, and  then select **Internet Information Services (IIS) Manager**.

2. In the **Internet Information Services (IIS) Manager** dialog, **Connections** pane, expand your computer name, expand **Sites**, and select **Default Web Site**.

3. On the **Actions** pane, select **Bindings**.

4. In the **Site Bindings** dialog, select **Add**.

5. In the **Add Site Binding** dialog, on the **Type** menu, select **https**.

6. In the **SSL Certificate** list, select the entry that matches the name of your computer, and select **OK**.

7. In the **Site Bindings** dialog, select **Close**.

8. On the **Connections** pane, under **Default Web Site**, select **CertSrv**.

   If the **CertServ** page is missing under Default Web Site, verify these Active Directory Certificate Services features are installed and configured on the CA server:

   - Certificate Enrollment Web Services
   - Certificate Authority Web Enrollment

9. On the **/CertSrv Home** page, right-click **SSL Settings**, and then select **Open Feature**.

10. On the **SSL Settings** pane, check the **Require SSL** box.

11. On the **Actions** pane, select **Apply**, and close Internet Information Services (IIS) Manager.

## Next steps

[Obtain a certificate for use with Windows Servers and System Center Operations Manager](obtain-certificate-windows-server-and-operations-manager.md).
