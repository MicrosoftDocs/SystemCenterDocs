---
title: Orchestration Console Browser Requirements
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bce67b9a-a621-4496-bfea-83f049963843
---
# Orchestration Console Browser Requirements
The Orchestration console can be accessed from any browser that supports Microsoft Silverlight 4. To access the system requirements for Silverlight, see [Get Microsoft Silverlight](http://go.microsoft.com/fwlink/p/?LinkId=128111).

## Authentication
The Orchestration console requires authentication by using your domain credentials so that it can identify the runbooks and folders that you should have permission to access. If your browser is configured for automatic logon, you are not prompted for a name and password. Your browser supplies this information automatically each time you connect to the Orchestration console. If you are using a browser that does not support automatic logon or if your browser is configured to not perform automatic logon, you are prompted for a name and password each time that you connect to the Orchestration console. You can continue to type your name and password each time, or you can configure your browser to perform automatic logon.

#### To configure Internet Explorer for automatic logon

1.  In Internet Explorer, click **Tools**, and then click **Internet Options**. The **Internet Options** dialog box opens.

2.  On the **Security** tab, select **Local intranet**, and then click **Custom Level**.

3.  Scroll down to **User Authentication**, and under **Logon**, select **Automatic logon only in Intranet zone**. Click **OK**.

4.  In the **Internet Options** dialog box on the **Security Settings** tab, with  **Local intranet** still selected, click **Sites**.

5.  Click **Advanced**.

6.  Type the URL of the Orchestration console server \(for example, http:\/\/OrchSrv.contoso.com\) in the **Add this Web site to the zone** box, and then click **Add**.

    > [!NOTE]
    > If the **Require server verification \(https:\) for all sites in this zone** is selected, you have to specify https for the address, and your web server has to be configured to support Secure Sockets Layer \(SSL\).

7.  Click **OK** for this and the remaining dialog boxes.

## See Also
[Overview of Orchestration Console](Overview-of-Orchestration-Console.md)
[How to Start the Orchestration Console](How-to-Start-the-Orchestration-Console.md)
[How to Work With Runbooks in the Orchestration Console](How-to-Work-With-Runbooks-in-the-Orchestration-Console.md)


