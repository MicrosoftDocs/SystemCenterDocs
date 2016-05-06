---
title: How to Configure the Internet Proxy Settings for a Management Server
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14ce5bed-0294-443d-b931-e53d2a4aef7e
---
# How to Configure the Internet Proxy Settings for a Management Server
Use the following procedure to configure the Internet proxy settings for a [!INCLUDE[om12long](./Token/om12long_md.md)] management server. You must configure these settings if features of [!INCLUDE[om12short](./Token/om12short_md.md)] are enabled that require the management server to communicate over the Internet. For example, you must configure these settings if the Client Monitoring feature of [!INCLUDE[om12short](./Token/om12short_md.md)] is configured to transmit or receive data from Microsoft.

### To Configure Internet Proxy Settings for a Management Server

1.  Log on to the computer with an account that is a member of the [!INCLUDE[om12short](./Token/om12short_md.md)] Administrators role for the [!INCLUDE[om12short](./Token/om12short_md.md)] management group.

2.  In the Operations console, click the Administration button.

3.  In the Administration pane, expand **Administration**, expand **Device Management**, and then click **Management Servers**.

4.  In the results pane, right\-click the management server for which you want to view the properties, and then click **Properties**.

5.  In the **Management Server Properties** dialog box, click the **Proxy Settings** tab.

6.  On the **Proxy Settings** tab, select **Use a proxy server for communication with Microsoft** and then do the following:

7.  Select **http:\/\/** or **https:\/\/** from the drop\-down list, and type the name of the Internet proxy server in the **Address** text box.

8.  Type the **Port** number, and then click **OK**.

## See Also
[Making Changes to an Operations Manager for System Center 2012 Environment](assetId:///22675bc3-1668-44c7-bc40-484e06a01946)


