---
title: Define release package configuration items
description: Describes how to define release package configuration items in Service Manager.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bd274169-070c-4fa0-b00b-5170ae5308d0
---

# Define release package configuration items in Service Manager

>Applies To: System Center 2016 - Service Manager

Release packages normally contain a build and an environment that the release is tested with. The topics in this section describe how to build the configuration item parts that are contained in a release package and how they are added to the release package.  

## Create a build configuration item

The release manager can create a build configuration item that defines the software and version that a build consists of by performing the following procedure. After a build is created, it is normally added to the release package of a release record.  

### To create a build configuration item  

1.  In the Service Manager console, click **Configuration Items**.  

2.  In the **Configuration Items** pane, expand **Configuration Items**, and then click **Builds**.  

3.  In the **Tasks** pane, under **Builds**, click **Create Build**.  

4.  On the **General** tab in the form, do the following:  

    1.  In the **Title** box, type a name for the build. For example, for the build that will be used to deploy the new HRWeb software, type **HRWeb July 2016**.  

    2.  In the **Version** box, type a version number or other designation. For example, type **0.2**.  

    3.  Click **OK**.  

5.  On the **Related Items** tab, under **Configuration Items: Computers, Services and People**, click **Add** to associate a software configuration item, and then do the following for each software item that you want to add:  

    1.  In the **Select objects** dialog box under **Filter by class** list, click the drop\-down arrow, and then select **Software Items**.  

    2.  In the **Available objects** list, select the software configuration item that you want to associate with the build, click **Add**, and then click **OK** to close the **Select objects** dialog box.  

6.  Click **OK** to close the build form.  

## Create an environment configuration item

The release manager can create an environment configuration item that defines the computers, services, and people that the environment consists of by performing the following procedure. After an environment is created, it is normally added to the release package of a release record.  

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

## Add release package information to a release record

The Release Manager can add release package information for a release record using the following procedure. The release package normally contains the build and environment that the release is tested with.  

### To add release package information to a release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  

2.  Select any Release Management view that contains a release record where you want to add release package information.  

3.  In the **Tasks** pane, click **Edit**, and then in the release record form, click the **Release Package** tab.  

4.  On the **Release Package** tab, under **Configuration Items to Modify**, click **Add**.  

5.  In the **Select objects** dialog box, select the computer\-related configuration items that you want to add to the release package, click **Add**, and then click **OK** to close the **Select objects** dialog box.  

6.  Under **Affected Services**, click **Add**.  

7.  In the **Select objects** dialog box, select the business service items that you want to add to the release package and click **Add**, and then click **OK** to close the **Select objects** dialog box.  

8.  In the release record form, click **OK** to close it.  
