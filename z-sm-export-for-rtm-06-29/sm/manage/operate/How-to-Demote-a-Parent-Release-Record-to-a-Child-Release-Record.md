---
title: How to Demote a Parent Release Record to a Child Release Record
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb21111f-13bd-4381-88aa-12c8e52ec5d3
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Demote a Parent Release Record to a Child Release Record
In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], the Release Manager XE "Release Manager"  can demote a parent release record using the following procedure. If a parent release record contains child release records, all the child release records that it contains are unlinked from the parent and are no longer child release records.  
  
 The following procedure is performed on a parent release record that may or may not have child release records linked to it.  
  
### To demote a parent release record  
  
1.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  
  
2.  Select any Release Management view that contains a parent release that you want to demote, and then select the release record.  
  
3.  In the **Tasks** pane, click **Edit** to open the release record.  
  
4.  In the **Tasks** pane, click **Convert or Revert to Parent**.  
  
5.  If the release record that you are demoting contains child release records, a message appears stating that all links to child records will be removed. If so, click **OK** to unlink any child release records.  
  
6.  In the **Comments** box, type a comment indicating that you have reverted the release record from a parent release record, and then click **OK** to close the **Comments** box.  
  
7.  The **Child Items** tab no longer appears in the form.  
  
8.  In the release record form, click **OK** to close it.  
  
## See Also  
 [Combining Release Records into Parent\-Child Groups](../../../sm/manage/operate/Combining-Release-Records-into-Parent-Child-Groups.md)