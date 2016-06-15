---
title: How to Configure Notification Channels
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: edb5786f-8032-4705-8b17-8ae50f7edf17
---
# How to Configure Notification Channels
You can use the following procedures to configure notification channels and validate the configuration. Notification channels are the method by which notification messages are sent to users. You use the **Configure E\-Mail Notification Channel** dialog box to configure and enable email notifications that [!INCLUDE[smshort](../../includes/smshort_md.md)] sends to a Simple Mail Transfer Protocol \(SMTP\) server.

> [!NOTE]
> In this release of [!INCLUDE[smshort](../../includes/smshort_md.md)], only email notification is supported.

### To configure email notifications

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Notifications**, and then click **Channels**.

3.  In the **Channels** pane, click **E\-Mail Notification Channel**.

4.  In the **Tasks** pane, under **E\-Mail Notification Channel**, click **Properties** to open the **Configure E\-Mail Notification Channel** dialog box.

5.  Select the **Enable e\-mail notifications** check box.

6.  Click **Add**. In the **Add SMTP Server** dialog box, type the fully qualified domain name \(FQDN\) of the SMTP server that you want to use. For example, type **Exchange01.Woodgrove.Com**.

7.  In the **Port number** box, type or select the SMTP port number that you want to use. For example, select **25**.

8.  In the **Authentication method** box, select either **Anonymous** or **Windows Integrated**. For example, select **Anonymous**. Then, click **OK**.

9. In the **Return e\-mail address** box, type the email address of the service account that is used during setup. For example, type **smadmin@woodgrove.com**.

10. In the **Retry primary after** box, type or select the number of seconds that you want [!INCLUDE[smshort](../../includes/smshort_md.md)] to wait before it tries to resend outgoing email notifications. For example, select **25**.

11. Click **OK** to close the dialog box.

### To validate email notification configuration

1.  In the **Channels** pane, click **E\-Mail Notification Channel**.

2.  In the **Tasks** pane, under **E\-Mail Notification Channel**, click **Properties** to open the **Configure E\-Mail Notification Channel** dialog box.

3.  Verify that the configuration you entered is correct.

![](../../media/PSSymbol.gif)You can use a Windows PowerShell command to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to set the properties of an email notification channel in [!INCLUDE[smshort](../../includes/smshort_md.md)], see [Set\-SCSMChannel](http://go.microsoft.com/fwlink/p/?LinkId=225375).

-   For information about how to use Windows PowerShell to retrieve the Email Notification channels that are defined in [!INCLUDE[smshort](../../includes/smshort_md.md)], see [Get\-SCSMChannel](http://go.microsoft.com/fwlink/p/?LinkId=225319).


