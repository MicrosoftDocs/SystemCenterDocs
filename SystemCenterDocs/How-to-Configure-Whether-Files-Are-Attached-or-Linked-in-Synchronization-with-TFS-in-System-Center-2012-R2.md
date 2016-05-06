---
title: How to Configure Whether Files Are Attached or Linked in Synchronization with TFS in System Center 2012 R2
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29198cb0-688f-4b1a-a3b3-0d622a4ab887
---
# How to Configure Whether Files Are Attached or Linked in Synchronization with TFS in System Center 2012 R2
Creating work items in Team Foundation Server \(TFS\) with large attachments can take a lot of database space. This is why you might want to save the attachments on a network file share and link to these files from the TFS work items rather than physically attaching them to the work items. By default files are saved as links rather than attachments, however, this creates additional requirements for maintaining the files and controlling permissions. If you want to keep attachments in the database, you can override this default and configure TFS integration to physically attach files and remove them from the network file share. You can also choose to attach the files and keep the files on the network share.

### To configure alert attachments to be saved as files that are physically attached to work items in the TFS database

1.  In TFS, configure the maximum attachment size for work items to accommodate your business needs. For more information, see [How to: Set the Maximum Attachment Size for Work Items](http://go.microsoft.com/fwlink/p/?LinkId=272016).

2.  In the [!INCLUDE[om12short](./Token/om12short_md.md)] console, click **Authoring**, expand **Management Pack Objects**, and then click **Rules**.

3.  To set the scope of displayed rules, click **Scope**, and then click **View all targets**. Locate and select **TFS Collection**. Click **OK**.

4.  In the list of scoped rules, right\-click **Attachments Synchronization Rule**, click **Overrides**, click **Override the Rule**, and then click **For all objects of class: TFS Collection**.

5.  Add an override for the parameter **Link as attachments**, and set its value to **True**.

    > [!IMPORTANT]
    > Some alert attachments can be very large. For example, a typical production IntelliTrace Historical Profiling snapshot might be several hundred megabytes \(MB\). When this override is configured, the attachments are stored permanently in the TFS team project database. Make sure you allocate enough storage space for attachments in your database.

6.  Save the settings to a management pack.

### To configure alert attachments to be saved on the network file share and linked to TFS work items

1.  Share access to the alert attachment network file share with developers who need to open these attachments.

    > [!NOTE]
    > By default, alert attachments that are synchronized with TFS work items are added as links that point to the alert attachment network file share.

2.  In the [!INCLUDE[om12short](./Token/om12short_md.md)] console, click **Authoring**, expand **Management Pack Objects**, and then click **Rules**.

3.  To set the scope of displayed rules, click **Scope**, and then click **View all targets**. Locate and select **TFS Collection**. Click **OK**.

4.  In the list of scoped rules, right\-click **Attachments Synchronization Rule**, click **Overrides**, click **Override the Rule**, and then click **For all objects of class: TFS Collection**.

5.  Add an override for parameter **Link as URL**, and set its value to **True**.

    > [!IMPORTANT]
    > Some alert attachments can be very large. For example, a typical production IntelliTrace Historical Profiling snapshot might be several hundred megabytes. Make sure you allocate enough storage space on the network file share to meet your business needs.

6.  Save the settings to a management pack.

## See Also
[How to Configure File Attachments for Operations Manager Alerts in System Center 2012 R2](./How-to-Configure-File-Attachments-for-Operations-Manager-Alerts-in-System-Center-2012-R2.md)


