---
title: Establish trust between Service Management Automation and Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b1ce164-f5c2-4a94-bce9-9271e3666f89
---
# Establish trust between Service Management Automation and Service Provider Foundation
For Service Provider Foundation to successfully call the Service Management Automation web service, the Service Management Automation web service certificate must be trusted by the server on which Service Provider Foundation is installed. This topic applies whether you are using a self-signed certificate or a certification authority certificate for your Service Management Automation web service.

#### To trust the Service Management Automation certificate

1.  Log on to the computer that is running Service Provider Foundation.

2.  In a web browser, connect to the Service Management Automation web service endpoint. This procedure assumes that Internet Explorer is being used and that it is being run with elevated privileges.

3.  Click **Continue to this website (not recommended)**.

4.  In the browser address bar, click **Certificate Error**, and then click **View Certificates** on the **Certificate Invalid** pop-up.

5.  In the **Certificate** dialog box, click **Install Certificate**.

6.  In the **Certificate Import** wizard, select the **Local Machine** option and click **Next**.

7.  Select the **Place all certificates in the following store** option, and then click **Browse**.

8.  In the Select Certificate Store dialog box, click **Trusted People**, and then click **OK**.

9. Click **Next**, and then review your choices and click **Finish**.

10. If the import is successful, click OK to close the **Certificate** dialog box.

Service Provider Foundation should now be able to successfully call the Service Management Automation web service.

For detailed guidance to understand, create, test, and publish runbooks, see [Authoring Automation Runbooks](Authoring-Automation-Runbooks.md).


