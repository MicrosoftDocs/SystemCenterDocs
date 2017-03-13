---
title: Sample scenario to manage release records
description:
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
ms.assetid: 43437f6d-13f8-40f9-af74-3022d5e6914f
---

# Sample scenario to manage Service Manager release records

>Applies To: System Center 2016 - Service Manager

This sample scenario for Service Manager helps you achieve your goal of managing release records by using multiple scenarios end to end. You can think of this sample scenario as a case study that helps put the individual scenarios and procedures in context.  

Information Technology \(IT\) managers at Woodgrove Bank administer multiple projects simultaneously. Usually, IT project teams in the organization do not have access to the controlled production environment. Additionally, the preproduction environment is limited with restricted access. The IT organization runs projects, develops financial applications, and develops infrastructure improvements. When it is necessary to modify some part the controlled environment production environment, the IT project team submits change requests asking to update infrastructure, update an application, deploy a product, or implement a set of new processes.  

Release management starts when there are approved changes. According to company policies, the changes must be deployed through release management processes. The release manager, Garret, creates a parent release record, and then he drafts a high\-level diagram of the release and links high\-level activities to a change request. The release activity in a release record is linked to an existing deployment activity in a change request. Garret or a delegated activity designer then adds child release records and new activities as necessary to the release record that detail the steps needed to be completed to deploy the change. This process is repeated for each change request to allow any level of detail needed. Therefore, any number of change requests can be included in the release record, depending on the need of the organization. When a change request is ready for implementation, the change implementer marks corresponding activities as Completed.  

Woodgrove Bank normally deploys updates to its production environment, also called a release, once a month. Garret wants to package several releases that he defined in the June release, in the July release, and so on. He defines those releases as parent releases, and he links all network\-related and database\-related releases into the June parent release, and he links an application\-related release into the July parent release. He also adds a new "Test Network with Database Integration" activity into the June release to ensure that both subreleases function together.  

The next major release for Woodgrove Bank is a deployment of a new version of its HRWeb web application. HRWeb developers have given the Release Management team a new build of the HRWeb application. The Woodgrove Release Management team evaluates the build in its testing environment, finds a critical problem in the build, and then asks developers to fix the problem and provide a new build. The development team provides a new build, and the Release Management team successfully retests it in the test environment. The build then moves to the preproduction environment, where it is tested and used in the preproduction environment for two weeks. When testing is completed successfully, the build is deployed to the production environment. During this process, Garret creates a new build configuration item, links it to the HRWeb software configuration item, and links the build configuration item to the release record release package. When the last build is deployed into the production environment, Garret updates the version information in the HRWeb software configuration item, and he closes the release record.  

At Woodgrove Bank, Garret configures administrative settings for releases, and he creates a parent release record. He also creates templates for parallel and sequential activities. Then, Phil creates release records, based on the templates that Garret created. Phil chooses which changes to deploy, and then he updates release activities by adding, deleting, or modifying them for each release, as necessary. Garret configures notifications for release records to notify users. Garret and Phil can review the status and the progress of change requests for a release whenever they need to.
