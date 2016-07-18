---
title: How to Create an Environment Configuration Item
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa54faad-7fbf-4ffd-a87c-1bf5b5bc8522


















---
# How to Create an Environment Configuration Item
In System Center 2012 - Service Manager, the release manager can create an environment configuration item that defines the computers, services, and people that the environment consists of by performing the following procedure. After an environment is created, it is normally added to the release package of a release record.  
  
### To create an environment configuration item  
  
1.  In the Service Manager console, click **Configuration Items**.  
  
2.  In the **Configuration Items** pane, expand **Configuration Items**, and then click **Environments**.  
  
3.  In the **Tasks** pane, under **Environments**, click **Create Environment**.  
  
4.  On the **General** tab in the form, do the following:  
  
    1.  In the **Title** box, type a name for the environment. For example, for the pre\-environment that will be used to test the new HRWeb software, type **Environment for HRWeb July 2011**.  
  
    2.  Optionally, in other boxes on the tab, type or select information that might help you easily identify the environment that you are creating. For example, set the **Category** to **Pre Production**.  
  
    3.  Click **OK**.  
  
5.  On the **Related Items** tab, under **Configuration Items: Computers, Services and People**, you can add configuration items that are important to the environment. Examples might include the following:  
  
    -   Software  
  
    -   Users  
  
    -   Computers  
  
6.  Click **OK** to close the environment form.  
  
## See Also  
 [Defining Release Package Configuration Items](../../../sm/manage/operate/Defining-Release-Package-Configuration-Items.md)
