---
title: Advanced Analytical Reports Available in Service Manager
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
ms.assetid: d79b0585-58e7-483c-904a-800fa9480493
---

# Advanced Analytical Reports Available in Service Manager

>Applies To: System Center 2016 - Service Manager

The following analytical reports - which are presented as Microsoft Online Analytical Processing \(OLAP\) data cubes - are available in Service Manager. The data cubes that are included in this release of Service Manager contain measures and dimensions.  

## Dimensions  
 The following dimensions are contained in various data cubes. However - not all data cubes contain each dimension.  

 - WorkItemDim
 - ConfigItemDim
 - UserDim
 - ComputerDim  
 - ChangeRequestDim
 - ReviewerDim
 - SerivceDim
 - ConfigItemObjectStatus
 - ConfigItemAssetStatus
 - ActivityStatus
 - ActivityPriority
 - ActivityArea
 - ActivityStage
 - ChangeStatus
 -Change Category
 - ChangePriority
 - ChangeImpact
 - ChangeRisk
 - ChangeImplementationResults
 - ChangeArea
 - ReviewerDecision
 - ServiceStatus
 - ServiceClassification
 - ServicePriority
 - DateDim
 - DeletionStatusDim
 - OperatingSystemDim
 - ProcessorDim
 - NetworkAdapterDim
 - LogicalDiskDim
 - PhysicalDiskDim
 - DeployedComputerDim
 - SLAConfigurationDim
 - SLAMetricDim
 - SLADatePropertyTimeMetricDim
 - CalendarDim
 - WorkItemGroupDim
 - BillableTimeDim
 - IncidentDim
 - ProblemDim
 - ReleaseRecordDim
 - SLAInstanceStatus
 - IncidentStatus
 - IncidentSource
 - IncidentTierQueues
 - IncidentClassification
 - IncidentResolutionCategory
 - IncidentImpact
 - IncidentUrgency
 - ProblemStatus
 - ProblemSource
 - ProblemClassification
 -ProblemResolution
 - ReleaseStatus
 - ReleaseType
 - ReleaseCategory
 - ReleasePriority
 - ReleaseImpact
 - ReleaseRisk
 - ReleaseImplementionResults
 - ReleaseTemplate
 - ReviewActivityDim
 - ServiceRequestDim
 - RequestOfferingDim
 - ServiceOfferingDim
 - OfferingDim
 - ReviewActivityApproval
 - ServiceRequestStatus
 - ServiceRequestTemplate
 - ServiceRequestPriority
 - ServiceRequestUrgency
 - ServiceRequestSource
 - ServiceRequestImplementationResults
 - ServiceRequestArea
 - ServiceRequestSupportGroup
 - OfferingStatus
 - ServiceOfferingCategory
 - ConfigurationManagerCollectionDim
 - PowerActivityRecordEventType
 - SoftwareUpdateDim  

## Work Item Data Cube  
 The work item data cube contains the following measures:  

 - SLAInstanceInformationCount
 - SLAInstanceStatusCount
 - SLAConfigurationHasMetricCount
 - SLAConfigurationHasCalendarCount
 - WorkItemGroupContainsWorkItemCount
 - WorkItemIsAboutConfigItemCount
 - WorkItemCreatedByUserCount
 - WorkItemAssignedToUserCount
 - WorkItemAffectedByUserCount
 - WorkItemRelatesToConfigItemCount
 - WorkItemRelatesToWorkItemCount
 - WorkItemHasBillableTimeCount
 - BillableTimeBilledByUserCount
 - TotalTimeMeasure
 - IncidentStatusDurationCount
 - IncidentStatusCount
 - IncidentResolutionByUserCount
 - IncidentPrimaryUserCount
 - IncidentIsAboutConfigItemCount
 - IncidentCreatedByUserCount
 - IncidentAssignedToUserCount
 - IncidentAffectedByUserCount
 - IncidentRelatesToConfigItemCount
 - IncidentRelatesToWorkItemCount
 - IncidentHasBillableTimeCount
 - IncidentRelatesToProblemCount
 - IncidentSLAInstanceInformationCount
 - WorkItemGroupContainsIncidentCount
 - ProblemResolutionByUserCount
 - ProblemIsAboutConfigItemCount
 - ProblemCreatedByUserCount
 - ProblemAssignedToUserCount
 - ProblemAffectedByUserCount
 - ProblemRelatesToConfigItemCount
 - ProblemRelatesToWorkItemCount
 - ProblemHasBillableTimeCount
 - ProblemSLAInstanceInformationCount
 - ReleaseIsAboutConfigItemCount
 - ReleaseCreatedByUserCount
 - ReleaseAssignedToUserCount
 - ReleaseSLAInstanceInformationCount
 - WorkItemIsAboutComputerCount
 - WorkItemIsAboutServiceCount
 - ServiceContainsConfigItemCount
 - ServiceContainsComputerCount
 - WorkItemDimCount
 - SLAConfigurationDimCount
 - SLAMetricDimCount
 - SLADatePropertyTimeMetricDimCount
 - CalendarDimCount
 - WorkItemGroupDimCount
 - ConfigItemDimCount
 - UserDimCount
 - BillableTimeDimCount
 - TimeWorkedSum
 - IncidentDimCount
 - IncidentsResolvedCount
 - IncidentsResolvedWithinTargetResolutionTimeCount
 -IncidentsResolutionTimeInHoursSum
 - IncidentsPastTargetResolutionTimeCount
 - ProblemDimCount
 - ReleaseRecordDimCount
 - ReleasesImplementedOnScheduleCount
 - ComputerDimCount
 - ServiceDimCount  

## Power Management Data Cube  
 The power management data cube contains the following measures:  

 - ComputerHostsOperatingSystemCount
 - DeployedComputerRunsWindowsComputerCount
 - ConfigManagerCollectionHasComputerCount
 - Hour0
 - Hour1
 - Hour2
 - Hour3
 - Hour4
 - Hour5
 - Hour6
 - Hour7
 - Hour8
 - Hour9
 - Hour10
 - Hour11
 - Hour12
 - Hour13
 - Hour14
 - Hour15
 - Hour16
 - Hour17
 - Hour18
 - Hour19
 - Hour20
 - Hour21
 - Hour22
 - Hour23
 - PowerActivityDayCount
 - PowerActivityRecordEventTypeCount
 - ServiceContainsConfigItemCount
 - ServiceContainsComputerCount
 - ComputerDimCount
 - OperatingSystemDimCount
 - DeployedComputerDimCount
 - ConfigurationManagerCollectionDimCount
 - ServiceDimCount
 - ConfigItemDimCount  

## Software Updates Data Cube  
 The software updates data cube contains the following measures:  

 ComputerHostsOperatingSystemCount
 - DeployedComputerRunsWindowsComputerCount
 - ConfigurationManagerCollectionHasComputerCount
 - IsInstalled
 - IsMissing
 - IsUnknown
 - ComputerHasSoftwareUpdateCount
 - ServiceContainsConfigItemCount
 - ServiceContainsComputerCount
 - ComputerDimCount
 - OperatingSystemDimCount
 - DeployedComputerDimCount
 - ConfigurationManagerCollectionDimCount
 - SoftwareUpdateDimCount
 - ServiceDimCount
 - ConfigItemDimCount  

## Service Catalog Data Cube  
 The service catalog data cube contains the following measures:  

 - SLAConfigurationHasMetricCount
 - SLAConfigurationHasCalendarCount
 - ActivityIsAboutConfigItemCount
 - ActivityCreatedByUserCount
 - ActivityAssignedToUserCount
 - ActivityRelatesToConfigItemCount
 - ActivityRelatesToWorkItemCount
 - ActivityTotalTimeMeasure
 - ActivityStatusDurationCount
 - ActivityStatusCount
 - ReviewActivityHasReviewerCount
 - ReviewerIsReviewerUserCount
 - ReviewerVotedByUserCount
 - ReviewActivityRelatesToConfigItemCount
 - ReviewActivityAssignedToUserCount
 - ReviewActivityCreatedByUserCount
 - WorkItemGroupContainsServiceRequestCount
 - ServiceRequestIsAboutConfigItemCount
 - ServiceRequestCreatedByUserCount
 - ServiceRequestAssignedToUserCount
 - ServiceRequestRelatesToConfigItemCount
 - ServiceRequestRelatesToWorkItemCount
 - ServiceRequestAffectedUserCount
 - ServiceRequestContainsActivityCount
 - ServiceRequestTotalTimeMeasure
 - ServiceRequestStatusDurationCount
 - ServiceRequestStatusCount
 - ServiceRequestSLAInstanceInformationCount
 - SLAInstanceStatusCount
 - ServiceRequestRelatesToRequestOfferingCount
 - ServiceOfferingRelatesToRequestOfferingCount
 - ServiceOfferingPublishedByUserCount
 - RequestOfferingPublishedByUserCount
 - ServiceOfferingOwnerCount
 - RequestOfferingOwnerCount
 - ServiceRelatesToServiceOfferingCount
 - SLAConfigurationDimCount
 - SLAMetricDimCount
 - SLADatePropertyTimeMetricDimCount
 - CalendarDimCount
 - WorkItemDimCount
 - ConfigItemDimCount
 - ActivityDimCount
 - UserDimCount
 - ReviewerDimCount
 - ReviewActivityDimCount
 - WorkItemGroupDimCount
 - ServiceRequestDimCount
 - RequestOfferingDimCount
 - ServiceOfferingDimCount
 -OfferingDimCount
 - ServiceDimCount  

## Configuration Item Data Cube  
 The configuration item data cube contains the following measures:  

 - ConfigItemRelatesToConfigItemCount
 - ComputerPrimaryUserCount
 - ComputerHostsOperatingSystemCount
 - ComputerHostsProcessorCount
 - ComputerHostsNetworkAdapterCount
 - ComputerHostsLogicalDiskCount
 - ComputerHostsPhysicalDiskCount
 - ServiceImpactsUserCount
 - ConfigItemOwnedByUserCount
 - ConfigItemServicedByUserCount
 - ConfigItemImpactsCustomersCount
 - DeployedComputerRunsWindowsComputerCount
 - ServiceContainsConfigItemCount
 - ServiceContainsComputerCount
 - ConfigItemDimCount
 - ComputerDimCount
 - UserDimCount
 - OperatingSystemDimCount
 - TotalRAMInMB
 - ProcessorDimCount
 - TotalProcessorSpeed
 - NetworkAdapterDimCount
 - LogicalDiskDimCount
 - TotalDiskSpace
 - PhysicalDiskDimCount
 - ServiceDimCount
 - DeployedComputerDimCount  

## Change and Activity Management Data Cube  
 The change and activity management data cube contains the following measures:  

 - WorkItemIsAboutConfigItemCount
 - WorkItemCreatedByUserCount
 - WorkItemAssignedToUserCount
 - WorkItemRelatesToWorkItemCount
 - ActivityIsAboutConfigItemCount
 - ActivityCreatedByUserCount
 - ActivityAssignedToUserCount
 - ActivityRelatesToWorkItemCount
 - ActivityIsAboutComputerCount
 - ChangeRequestIsAboutConfigItemCount
 - ChangeRequestCreatedByUserCount
 - ChangeRequestAssignedToUserCount
 - ChangeRequestRelatesToWorkItemCount
 - ChangeRequestContainsActivityCount
 - ChangeRequestIsAboutComputerCount
 - ReviewActivityHasReviewerCount
 - ReviewerIsReviewerUserCount
 - ReviewerVotedByUserCount
 - ReviewActivityRelatesToConfigItemCount
 - ReviewActivityAssignedToUserCount
 - ReviewActivityCreatedByUserCount
 - WorkItemIsAboutComputerCount
 - ActivityRelatesToChangeRequestCount
 - ServiceContainsConfigItemCount
 - ServiceContainsComputerCount
 - WorkItemDimCount
 - ConfigItemDimCount
 - UserDimCount
 - ActivityDimCount
 - ActivitiesImplementedCount
 - ActivitiesImplementedOnScheduleCount
 - ComputerDimCount
 - ChangeRequestDimCount
 - ChangeRequestsImplementedCount
 - ChangeRequestsImplementedOnScheduleCount
 - EmergencyChangeRequestsCount
 - ProcessTimePerChangeInDaysSum
 - ReviewerDimCount
 - ServiceDimCount  
