---
description: Provides an overview of how you can establish trust between Service Management Automation and Service Provider Foundation.
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
keywords:
ms.date: 11/01/2024
title: Establish trust between Service Management Automation and Service Provider Foundation.
ms.subservice: service-management-automation
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency2, engagement-fy24
---

# Establish trust between Service Management Automation and Service Provider Foundation

For Service Provider Foundation to successfully call the Service Management Automation web service, the Service Management Automation web service certificate must be trusted by the server on which Service Provider Foundation is installed. This article applies whether you're using a self-signed certificate or a certification authority certificate for your Service Management Automation web service.

## Trust the Service Management Automation certificate

1. Sign in to the computer that is running Service Provider Foundation.

2. In a web browser, connect to the Service Management Automation web service endpoint. This procedure assumes that Internet Explorer is being used and that it's being run with elevated privileges.

3. Select **Continue to this website (not recommended)**.

4. In the browser address bar, select **Certificate Error**, and select **View Certificates** on the **Certificate Invalid** pop-up.

5. In the **Certificate** dialog, select **Install Certificate**.

6. In the **Certificate Import** wizard, select the **Local Machine** option and select **Next**.

7. Select the **Place all certificates in the following store** option, and select **Browse**.

8. In the Select Certificate Store dialog, select **Trusted People**, and select **OK**.

9. Select **Next**, and then review your choices and select **Finish**.

10. If the import is successful, select **OK** to close the **Certificate** dialog.

Service Provider Foundation should now be able to successfully call the Service Management Automation web service.

## Next steps

- For detailed guidance to understand, create, test, and publish runbooks, see [Authoring automation runbooks](authoring-automation-runbooks.md).
