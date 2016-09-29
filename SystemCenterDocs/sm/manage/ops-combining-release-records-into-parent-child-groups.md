---
title: Combining Release Records into Parent-Child Groups
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eaa51912-14c0-4ff5-bd4a-e7c5354e6260
---

# Combining Release Records into Parent-Child Groups

>Applies To: System Center 2016 - Service Manager

Releases are normally deployed to production environments at intervals you define. For example, you can package several releases into monthly batches. You can define each batch as a parent release, which consolidates and links other smaller project\-specific releases into a monthly package. This process can help you verify that all child releases are evaluated together.  

## How to Promote a Release Record to a Parent Release Record

The Release Manager can promote a release record to parent release record using the following procedure. A parent release record serves as a container for several releases.  

 The following procedure is performed on a release record that is neither a parent release record nor a child release record.  

### To promote a release record to a parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  

2.  Select any Release Management view, and then select a release record.  

3.  In the **Tasks** pane, click **Edit** to open the release record.  

4.  In the **Tasks** pane, click **Convert or Revert to Parent**.  

5.  In the **Comments** box, type a comment indicating that you have converted the release record to a parent release record, and then click **OK** to close the **Comments** box.  

6.  The **Child Items** tab appears in the form where you can add child release records.  

7.  In the release record form, click **OK** to close it.  

# How to Demote a Parent Release Record to a Child Release Record

The Release Manager can demote a parent release record using the following procedure. If a parent release record contains child release records, all the child release records that it contains are unlinked from the parent and are no longer child release records.  

 The following procedure is performed on a parent release record that may or may not have child release records linked to it.  

### To demote a parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  

2.  Select any Release Management view that contains a parent release that you want to demote, and then select the release record.  

3.  In the **Tasks** pane, click **Edit** to open the release record.  

4.  In the **Tasks** pane, click **Convert or Revert to Parent**.  

5.  If the release record that you are demoting contains child release records, a message appears stating that all links to child records will be removed. If so, click **OK** to unlink any child release records.  

6.  In the **Comments** box, type a comment indicating that you have reverted the release record from a parent release record, and then click **OK** to close the **Comments** box.  

7.  The **Child Items** tab no longer appears in the form.  

8.  In the release record form, click **OK** to close it.  

## How to Link a Child Release Record to the Current Release Record

The Release Manager can link a child release record while editing a parent release record using the following procedure.  

### To link a child release record to the current parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  

2.  Select any Release Management view that contains a parent release record where you want link to a child release record.  

3.  In the **Tasks** pane, click **Edit**, and then in the parent release record form, click the **Child Items** tab.  

4.  On the **Child Items** tab, click **Add**.  

5.  In the **Select objects** dialog box, select the release record that you want to link to a parent, and then click **Add**. Click **OK** to close the **Select objects** dialog box.  

6.  In the parent release record form, click **OK** to close it.  

## How to Unlink the Current Release Record from a Parent Release Record

The Release Manager can unlink a child release record using the following procedure.  

### To unlink the current release record from a parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  

2.  Select any Release Management view that contains a child release record that you want to unlink from its parent release record.  

3.  In the **Tasks** pane, click **Link or Unlink to Existing Parent Release Record**, and then in the fly\-out list, click **Unlink**.  

4.  In the **Comments** box, type a comment indicating that you have unlinked the child release record from its parent release record, and then click **OK** to close the **Comments** box.  

## How to Unlink a Child Release Record from the Current Release Record

The Release Manager can unlink a child release record while editing a parent release record using the following procedure.  

### To unlink a child release record from the current parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  

2.  Select any Release Management view that contains a parent release record where you want unlink to a child release record.  

3.  In the **Tasks** pane, click **Edit**, and then in the parent release record form, click the **Child Items** tab.  

4.  On the **Child Items** tab, select the child release records to unlink, and then click **Remove**.  

    > [!NOTE]  
    >  You can select multiple child items by pressing Shift\+Click.  

5.  In the parent release record form, click **OK** to close it.  
