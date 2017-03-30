---
title: Manage release records
description: Provides an overview and describes how to manage Service Manager release records.
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
ms.assetid: 2847c2cf-422d-4cfa-8e36-6f7eb7856afa
---

# Manage Service Manager release records

>Applies To: System Center 2016 - Service Manager

The key to understanding release management in System Center 2016 - Service Manager is realizing how objects, such as change requests and activities, interact when facilitated by release records. Release management uses parent and child release records to help automate the process of updating the status of change requests and the status propagation between parallel activities, sequential activities, and the activities within them.  

Often, there are multiple parts of a project, and there is more than one change request that can be deployed at different times that can affect a project. The overall goal of change management and release management is to protect the production environment from unnecessary changes, so that every change to it must first be approved. Release management deals only with approved changes.  

When changes are approved, it is up to release management processes to group the changes together, schedule them, and develop them. Depending on the nature of the change, sometimes development can occur in the project phase and other times it can occur in the release management phase. Regardless of when development occurs, release management ensures that changes are tested and that they are safe to deploy. Additionally, release management is used to evaluate and package various releases together to help minimize infrastructure downtime. The package of releases is tested together to verify that no technical or resource conflicts exist that could affect infrastructure availability. Multiple changes are bundled together and planned for deployment together during the next scheduled release or maintenance window. The function of release management using release records is to consolidate multiple changes and deploy them in the safest and most efficient method possible.  

After changes have been bundled together, a release manager defines the sequence of actions needed for a release with release activities. For example, different changes might have infrastructure update tasks, database modification tasks, tasks to update applications, or other individual tasks. In some cases, it might make sense to group some tasks together with infrastructure updates or perform database updates or application updates. Some tasks can be deployed simultaneously, while other tasks must be deployed sequentially or separately.  

## Managing release records

The release manager or other person responsible for the release defines the sequence of actions with a release record. The release record might depict the deployment sequence of different changes using parallel activities, sequential activities, and other activities. The release manager can delegate the responsibility for activities to others. When an activity is delegated, the person responsible for the activity can modify the activity and update its status.  

When you modify an activity, its status is not immediately updated. There is a delay after until the workflow activates and the activity status is updated. Often, 30  to 60 seconds might elapse before you see the updated status of the activity in the console after you refresh your view of an item. Other dependent activities in the release record might take longer to update. For example, assume that you have a release record containing a dozen activities. If you update an item near the top of the list, it might take 30 seconds to update in the console. Then, the next activity in the release record might automatically get updated 30 seconds later, and so on. Therefore, the update that you originally made might take some time to propagate to all affected activities in the release record.  

### Parts of release records  

Because releases are often bundled together, you can group multiple release records together by using a parent\-child relationship. Essentially, a parent release record serves as a container for multiple child release records. However, a newly created release record is not a parent release record by default. You must convert a release record to a parent release record in order to add child release records.  

Like change requests, release records contain activities for approval and manual actions. In addition, release records can contain parallel and sequential activities. Parallel and sequential activities are containers for other activities, and they define how constituent activities must be implemented-parallel activities can be implemented simultaneously, while other parallel activities are also in progress. Sequential activities must be completed in the order they are organized, one after another.  

## Sample scenario to manage Service Manager release records

This sample scenario for Service Manager helps you achieve your goal of managing release records by using multiple scenarios end to end. You can think of this sample scenario as a case study that helps put the individual scenarios and procedures in context.  

Information Technology \(IT\) managers at Woodgrove Bank administer multiple projects simultaneously. Usually, IT project teams in the organization do not have access to the controlled production environment. Additionally, the preproduction environment is limited with restricted access. The IT organization runs projects, develops financial applications, and develops infrastructure improvements. When it is necessary to modify some part the controlled environment production environment, the IT project team submits change requests asking to update infrastructure, update an application, deploy a product, or implement a set of new processes.  

Release management starts when there are approved changes. According to company policies, the changes must be deployed through release management processes. The release manager, Garret, creates a parent release record, and then he drafts a high\-level diagram of the release and links high\-level activities to a change request. The release activity in a release record is linked to an existing deployment activity in a change request. Garret or a delegated activity designer then adds child release records and new activities as necessary to the release record that detail the steps needed to be completed to deploy the change. This process is repeated for each change request to allow any level of detail needed. Therefore, any number of change requests can be included in the release record, depending on the need of the organization. When a change request is ready for implementation, the change implementer marks corresponding activities as Completed.  

Woodgrove Bank normally deploys updates to its production environment, also called a release, once a month. Garret wants to package several releases that he defined in the June release, in the July release, and so on. He defines those releases as parent releases, and he links all network\-related and database\-related releases into the June parent release, and he links an application\-related release into the July parent release. He also adds a new "Test Network with Database Integration" activity into the June release to ensure that both subreleases function together.  

The next major release for Woodgrove Bank is a deployment of a new version of its HRWeb web application. HRWeb developers have given the Release Management team a new build of the HRWeb application. The Woodgrove Release Management team evaluates the build in its testing environment, finds a critical problem in the build, and then asks developers to fix the problem and provide a new build. The development team provides a new build, and the Release Management team successfully retests it in the test environment. The build then moves to the preproduction environment, where it is tested and used in the preproduction environment for two weeks. When testing is completed successfully, the build is deployed to the production environment. During this process, Garret creates a new build configuration item, links it to the HRWeb software configuration item, and links the build configuration item to the release record release package. When the last build is deployed into the production environment, Garret updates the version information in the HRWeb software configuration item, and he closes the release record.  

At Woodgrove Bank, Garret configures administrative settings for releases, and he creates a parent release record. He also creates templates for parallel and sequential activities. Then, Phil creates release records, based on the templates that Garret created. Phil chooses which changes to deploy, and then he updates release activities by adding, deleting, or modifying them for each release, as necessary. Garret configures notifications for release records to notify users. Garret and Phil can review the status and the progress of change requests for a release whenever they need to.

## Create a Service Manager release record


The Release Manager creates a release record in Service Manager using the following procedure.  

### To create a release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  
2.  In the **Tasks** pane, click **Create Release Record**.  
3.  In the **Select Template** dialog box, select a release record template, and then click **OK** to open it.  
4.  In the release record form on the **General** tab, enter any necessary information, and then click the **Activities** tab.  
5.  Modify the default set of release activities that are added from the release record template, if any are present. You can add, delete, or modify sets of activities to the release record, including the following actions:  
    -   Add activities from the list of existing activity templates.  
    -   Move activities up and down in the order in which they are completed.  
    -   Move activities in the process list, and place them inside container activities.  
    -   Move activities from container activities, and place them anywhere in the process list.  
    -   Delete activities.  
6.  As you add an activity, the activity form opens. Enter necessary information, and then click **OK** to save the activity.  
7.  When you have added all the activities you want, click **OK** to save the release record and close it. The release record then appears in the **Release Records: All** view.  

## Create a Service Manager release record template

A release record template is used to create new release records. A release record template can include predefined release activities. When you use a template for new release records, new release records are created faster than when you create them from scratch.  

The template author creates a template for release records by completing the following procedure.  

### To create a release record template  

1.  In the Service Manager console, open the **Library** workspace, and in the **Library** pane, select **Templates**.  
2.  In the **Templates** list, select **Default Release Record**, and then in the **Tasks** pane under **Templates**, click **Create Template**.  
3.  In the **Create Template** dialog box, type a name for the template and a description of what the template applies.  
4.  Under **Class**, click **Browse**, and in the **Select a Class** box, select **Release Record**, and then click **OK** to close the **Select a Class** box.  
5.  Click **OK** to close the **Create Template** dialog box, and the New Release Record Template form appears.  
6.  Enter information in the boxes on the **General** tab, and then click the **Activities** tab.  
7.  You can add, delete, or modify sets of activities to the release record template, including the following actions:  
    -   Add activities from the list of existing activity templates.  
    -   Move activities up and down in the order in which they are completed.  
    -   Move activities in the process list, and place them inside container activities.  
    -   Move activities from container activities, and place them anywhere in the process list.  
    -   Delete activities.  
8.  As you add an activity, the activity form opens. Enter necessary information, and then click **OK** to save the activity.  
9. When you have added all the activities you want, click **OK** to save the release record template and close it. The release record template then appears in **Templates** list.  

## Combine Service Manager release records into parent-child groups

Releases are normally deployed to production environments at intervals you define. For example, you can package several releases into monthly batches. You can define each batch as a parent release, which consolidates and links other smaller project\-specific releases into a monthly package. This process can help you verify that all child releases are evaluated together.  

### Promote a release record to a parent release record

The Release Manager can promote a release record to parent release record using the following procedure. A parent release record serves as a container for several releases.  

The following procedure is performed on a release record that is neither a parent release record nor a child release record.  

#### To promote a release record to a parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  
2.  Select any Release Management view, and then select a release record.  
3.  In the **Tasks** pane, click **Edit** to open the release record.  
4.  In the **Tasks** pane, click **Convert or Revert to Parent**.  
5.  In the **Comments** box, type a comment indicating that you have converted the release record to a parent release record, and then click **OK** to close the **Comments** box.  
6.  The **Child Items** tab appears in the form where you can add child release records.  
7.  In the release record form, click **OK** to close it.  

### Demote a parent release record to a child release record

The Release Manager can demote a parent release record using the following procedure. If a parent release record contains child release records, all the child release records that it contains are unlinked from the parent and are no longer child release records.  

The following procedure is performed on a parent release record that may or may not have child release records linked to it.  

#### To demote a parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  
2.  Select any Release Management view that contains a parent release that you want to demote, and then select the release record.  
3.  In the **Tasks** pane, click **Edit** to open the release record.  
4.  In the **Tasks** pane, click **Convert or Revert to Parent**.  
5.  If the release record that you are demoting contains child release records, a message appears stating that all links to child records will be removed. If so, click **OK** to unlink any child release records.  
6.  In the **Comments** box, type a comment indicating that you have reverted the release record from a parent release record, and then click **OK** to close the **Comments** box.  
7.  The **Child Items** tab no longer appears in the form.  
8.  In the release record form, click **OK** to close it.  

### Link a child release record to the current release record

The Release Manager can link a child release record while editing a parent release record using the following procedure.  

#### To link a child release record to the current parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  
2.  Select any Release Management view that contains a parent release record where you want link to a child release record.  
3.  In the **Tasks** pane, click **Edit**, and then in the parent release record form, click the **Child Items** tab.  
4.  On the **Child Items** tab, click **Add**.  
5.  In the **Select objects** dialog box, select the release record that you want to link to a parent, and then click **Add**. Click **OK** to close the **Select objects** dialog box.  
6.  In the parent release record form, click **OK** to close it.  

### Unlink the current release record from a parent release record

The Release Manager can unlink a child release record using the following procedure.  

#### To unlink the current release record from a parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  
2.  Select any Release Management view that contains a child release record that you want to unlink from its parent release record.  
3.  In the **Tasks** pane, click **Link or Unlink to Existing Parent Release Record**, and then in the fly\-out list, click **Unlink**.  
4.  In the **Comments** box, type a comment indicating that you have unlinked the child release record from its parent release record, and then click **OK** to close the **Comments** box.  

### Unlink a child release record from the current release record

The Release Manager can unlink a child release record while editing a parent release record using the following procedure.  

#### To unlink a child release record from the current parent release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  
2.  Select any Release Management view that contains a parent release record where you want unlink to a child release record.  
3.  In the **Tasks** pane, click **Edit**, and then in the parent release record form, click the **Child Items** tab.  
4.  On the **Child Items** tab, select the child release records to unlink, and then click **Remove**.  
    > [!NOTE]  
    >  You can select multiple child items by pressing Shift\+Click.  

5.  In the parent release record form, click **OK** to close it.  

## Define release package configuration items in Service Manager

Release packages normally contain a build and an environment that the release is tested with. The topics in this section describe how to build the configuration item parts that are contained in a release package and how they are added to the release package.  

### Create a build configuration item

The release manager can create a build configuration item that defines the software and version that a build consists of by performing the following procedure. After a build is created, it is normally added to the release package of a release record.  

#### To create a build configuration item  

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

### Create an environment configuration item

The release manager can create an environment configuration item that defines the computers, services, and people that the environment consists of by performing the following procedure. After an environment is created, it is normally added to the release package of a release record.  

#### To create an environment configuration item  

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

### Add release package information to a release record

The Release Manager can add release package information for a release record using the following procedure. The release package normally contains the build and environment that the release is tested with.  

#### To add release package information to a release record  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**.  
2.  Select any Release Management view that contains a release record where you want to add release package information.  
3.  In the **Tasks** pane, click **Edit**, and then in the release record form, click the **Release Package** tab.  
4.  On the **Release Package** tab, under **Configuration Items to Modify**, click **Add**.  
5.  In the **Select objects** dialog box, select the computer\-related configuration items that you want to add to the release package, click **Add**, and then click **OK** to close the **Select objects** dialog box.  
6.  Under **Affected Services**, click **Add**.  
7.  In the **Select objects** dialog box, select the business service items that you want to add to the release package and click **Add**, and then click **OK** to close the **Select objects** dialog box.  
8.  In the release record form, click **OK** to close it.  

## Create a template for parallel and sequential activities in Service Manager

Release record templates for parallel and sequential activities are used to create new activities that contain a collection of predefined activities that should be grouped together to form some kind of process. You can think of parallel and sequential activities as container activities because their primary function is to contain individual activities.  

The template author creates a template for a parallel activity by performing the following procedure. Afterward, the same steps are followed to create a template for a sequential activity.  

### To create a template for a parallel activity  

1.  In the Service Manager console, open the **Library** workspace, and in the **Library** pane, select **Templates**.  
2.  In the **Templates** list, select **Default Parallel Activity**, and then in the **Tasks** pane under **Templates**, click **Create Template**.  
3.  In the **Create Template** dialog box, type a name for the template and a description of what the template applies.  
4.  Under **Class**, click **Browse**, in the **Select a Class** box, select **Parallel Activity**, and then click **OK** to close the **Select a Class** box.  
5.  Click **OK** to close the **Create Template** dialog box, and the New Container Activity Template form appears.  
6.  Enter information in the boxes on the **General** tab, and then click the **Activities** tab.  
7.  You can add, delete, or modify sets of activities to the parallel activity template, including the following actions:  
    1.  Add activities from the list of existing activity templates.  
    2.  Add parallel or sequential activities from the list of existing activity templates.  
    3.  Move activities up and down in the order in which they are completed.  
    4.  Move activities in the process list.  
    5.  Delete activities.  
8.  As you add an activity, the activity form opens. Enter necessary information, and then click **OK** to save the activity.  
9. When you have added all the activities you want, click **OK** to save the parallel activity template and close it. The parallel activity template then appears in **Templates** list.  
10. Repeat this procedure for a sequential activity, replacing instances of "parallel activity" with "sequential activity."  

## Choose changes to deploy in Service Manager

The release manager selects approved changes for release by performing the following procedure. Using this process, the release manager links a manual activity in the release record to a dependent activity in a change request and then completes the manual activity in the release record. As a result, this process marks the dependent activity in the change request as completed.  

The procedure to create a dependent activity to add it to a change request should already be completed before you proceed.

### To choose changes to deploy  

1.  In the Service Manager console, open the **Work Items** workspace, in the **Work Items** pane, expand **Release Management**, and then select **Release Management**.  
2.  In the **Work Items** pane, select a view under **Release Management** that displays a release record that comprises changes that are ready for deployment, and then double\-click the release record.  
3.  Click the **Activities** tab.  
4.  In the list that appears, right\-click a manual activity to link a change request dependent activity to, and then select **Link to Change Request Activity**.  
5.  In the **Select Change Request Activity** dialog box, select the change request to link to, expand it, and then select one or more dependent activities, and then click **OK** twice.  
    > [!TIP]  
    >  When you have linked the activity, the selected activity shows a linking indicator that resembles a chain icon. The tooltip for the selected activity shows IDs for the linked change request dependent activities.  

6.  Navigate to **Activity Management**, expand **Manual Activities**, and then select **In\-Progress Activities**.  
7.  Select the manual activity and then in the **Tasks** list click **Mark as Completed**.  
8.  Navigate to **Change Management**, expand **All Change Requests**, and then open the change request that is linked to the release record.  
9. Click the **Activities** tab and notice that the dependent activity is now marked **Completed**.  

## Plan release activities in Service Manager

The Release Manager creates and modifies the structure of release activities by performing the following procedure.  

### To plan release activities  

1.  In the Service Manager console, open the **Work Items** workspace, and in the **Work Items** pane, expand **Release Management**, and then select **Release Management**.  
2.  In the **Work Items** pane, select a view under **Release Management** that displays a release record that includes release activities that you want to add or modify activities for, and then double\-click the record to open it.  
3.  Click the **Activities** tab to view the list of proposed changes and dependent activities they contain.  
4.  Optionally, you can change the activities view by clicking either **Diagram View** or **List View**.  
5.  Select a dependent change management activity, and then move it to the top of release management activity list or diagram. A dependent indicator appears on release management activities, which resembles the link in a chain.  

## Skip a failed activity in Service Manager

The release manager skips a failed activity by performing the following procedure.  

### To skip a failed activity  

1.  In the Service Manager console, open the **Work Items** workspace, in the **Work Items** pane, expand **Release Management**, and then select **Release Management**.  
2.  In the **Work Items** pane, select a view under **Release Management** that displays a release record that includes a failed release activity or an activity in progress that you want to skip, and then double\-click the record to open it.  
3.  Click the **Activities** tab to view the list of proposed changes and dependent activities they contain. Optionally, you can change the activities view by clicking either **Diagram View** or **List View**.  
4.  Right\-click the failed activity or the activity in progress that you want to skip, and then click **Skip Activity**.  
5.  In the **Comments** box, enter the reason why you are skipping the activity, and then click **OK** to close the box. The activity that you skipped displays an icon resembling a blue down\-pointing arrow to indicate that the activity is marked as skipped.  

## Determine status and progress for a Service Manager change request in the release record

The change manager reviews the status and progress of a change request in the currently opened release record. He knows the ID of the change request and its title, or at least a few of the keywords of the title. He can review the status of the change request by performing the following procedure.  

### To determine status and progress for a change request in a release record  

1.  In the Service Manager console, open the **Work Items** workspace, in the **Work Items** pane, expand **Release Management**, and then select **Release Management**.  
2.  In the **Work Items** pane, under **Release Management**, select the **Release Records: In Progress**.  
3.  In the **Release Records: In Progress** view, double\-click the record of interest to open it.  
4.  Click the **Activities** tab to view the list of proposed changes and dependent activities they contain. Optionally, you change the activities view by clicking either **Diagram View** or **List View**.  
5.  You can view records by using any of the following methods:  
    -   Mouse scrolling:  
        -   You can find the release management activity showing that it is linked to the specific change request by looking for an indicator icon and viewing its properties while in either diagram view or list view.  
        -   The following information is shown for all activities:  
            -   Activity IDs  
            -   Activity titles  
            -   Activity status indicator icons, which vary based on the state of the activity  
    -   Using the diagram view:  
        -   When you are using the diagram view, you can use **Zoom** to choose different for activities.  
    -   Using search anywhere in the Service Manager console:  
        -   You can search for and view an activity by searching with any of the following information:  
            -   Change request ID  
            -   Keywords from the linked change request's title  
            -   Change activity's ID  
            -   Keywords from the dependent activity's title  
        -   Filtering:  
            -   You can filter any returned search results by keywords and also by criteria such as class, last modified dates, and name.  
6.  You can double\-click an activity to view its status and the details of its progress.  
