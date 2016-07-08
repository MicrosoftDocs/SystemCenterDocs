---
title: How to Create a Build Configuration Item
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ecf42c85-bd58-4cd3-8697-d692a2d4c4f7


















---
# How to Create a Build Configuration Item
In System Center 2012 - Service Manager, the release manager can create a build configuration item that defines the software and version that a build consists of by performing the following procedure. After a build is created, it is normally added to the release package of a release record.  
  
### To create a build configuration item  
  
1.  In the Service Manager console, click **Configuration Items**.  
  
2.  In the **Configuration Items** pane, expand **Configuration Items**, and then click **Builds**.  
  
3.  In the **Tasks** pane, under **Builds**, click **Create Build**.  
  
4.  On the **General** tab in the form, do the following:  
  
    1.  In the **Title** box, type a name for the build. For example, for the build that will be used to deploy the new HRWeb software, type **HRWeb July 2011**.  
  
    2.  In the **Version** box, type a version number or other designation. For example, type **0.2**.  
  
    3.  Click **OK**.  
  
5.  On the **Related Items** tab, under **Configuration Items: Computers, Services and People**, click **Add** to associate a software configuration item, and then do the following for each software item that you want to add:  
  
    1.  In the **Select objects** dialog box under **Filter by class** list, click the drop\-down arrow, and then select **Software Items**.  
  
    2.  In the **Available objects** list, select the software configuration item that you want to associate with the build, click **Add**, and then click **OK** to close the **Select objects** dialog box.  
  
6.  Click **OK** to close the build form.  
  
## See Also  
 [Defining Release Package Configuration Items](../../../sm/manage/operate/Defining-Release-Package-Configuration-Items.md)
