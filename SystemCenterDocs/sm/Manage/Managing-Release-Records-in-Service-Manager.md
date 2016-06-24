---
title: Managing Release Records in Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68d973c3-4c17-41cb-8584-9e6e25fe2962
---
# Managing Release Records in Service Manager
The key to understanding release management in Service Manager is realizing how objects, such as change requests and activities, interact—facilitated by release records. Release management uses parent and child release records to help automate the process of updating the status of change requests and the status propagation between parallel activities, sequential activities, and the activities within them.

Often, there are multiple parts of a project, and there is more than one change request that can be deployed at different times that can affect a project. The overall goal of change management and release management is to protect the production environment from unnecessary changes, so that every change to it must first be approved. Release management deals only with approved changes.

When changes are approved, it is up to release management processes to group the changes together, schedule them, and develop them. Depending on the nature of the change, sometimes development can occur in the project phase and other times it can occur in the release management phase. Regardless of when development occurs, release management ensures that changes are tested and that they are safe to deploy. Additionally, release management is used to evaluate and package various releases together to help minimize infrastructure downtime. The package of releases is tested together to verify that no technical or resource conflicts exist that could affect infrastructure availability. Multiple changes are bundled together and planned for deployment together during the next scheduled release or maintenance window. The function of release management using release records is to consolidate multiple changes and deploy them in the safest and most efficient method possible.

After changes have been bundled together, a release manager defines the sequence of actions needed for a release with release activities. For example, different changes might have infrastructure update tasks, database modification tasks, tasks to update applications, or other individual tasks. In some cases, it might make sense to group some tasks together with infrastructure updates or perform database updates or application updates. Some tasks can be deployed simultaneously, while other tasks must be deployed sequentially or separately.

## Managing Release Records in Service Manager
The release manager or other person responsible for the release defines the sequence of actions with a release record. The release record might depict the deployment sequence of different changes using parallel activities, sequential activities, and other activities. The release manager can delegate the responsibility for activities to others. When an activity is delegated, the person responsible for the activity can modify the activity and update its status.

When you modify an activity, its status is not immediately updated. There is a delay after until the workflow activates and the activity status is updated. Often, 30  to 60 seconds might elapse before you see the updated status of the activity in the console after you refresh your view of an item. Other dependent activities in the release record might take longer to update. For example, assume that you have a release record containing a dozen activities. If you update an item near the top of the list, it might take 30 seconds to update in the console. Then, the next activity in the release record might automatically get updated 30 seconds later, and so on. Therefore, the update that you originally made might take some time to propagate to all affected activities in the release record.

### Parts of Release Records
Because releases are often bundled together, you can group multiple release records together by using a parent-child relationship. Essentially, a parent release record serves as a container for multiple child release records. However, a newly created release record is not a parent release record by default. You must convert a release record to a parent release record in order to add child release records.

Like change requests, release records contain activities for approval and manual actions. In addition, release records can contain parallel and sequential activities. Parallel and sequential activities are containers for other activities, and they define how constituent activities must be implemented—parallel activities can be implemented simultaneously, while other parallel activities are also in progress. Sequential activities must be completed in the order they are organized, one after another.

## To Manage Release Records

1.  Create a release record

2.  Create a release record template

3.  Combine release records into parent-child groups.

    1.  Promote or demote a release record to a parent release record.

    2.  Link or unlink a child release record to a selected release record.

    3.  Link or unlink a selected release record from a parent release record.

4.  Define release package configuration items.

    -   Create a build configuration item.

    -   Create an environment configuration item.

    -   Add release package information to a release record.

5.  Create a template for parallel and sequential activities that are used in release records.

6.  Review and choose changes to deploy.

7.  Plan release activities.

8.  Skip a failed activity, if necessary.

9. Determine the status and progress for a change request that is contained in a release record.


