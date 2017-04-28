---
title: Find Appointments
description: The Find Appointments activity is used in a runbook to find an existing appointment.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 223820eb-1c24-43ce-938e-935176e2a8bf
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Find Appointments

Applies To: System Center 2016 - Orchestrator

The Find Appointments activity is used in a runbook to find an existing appointment.

The following tables list the required properties, optional properties, filters, and published data for this activity.

## Find Appointments Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Search Folder   | The ID of the folder to search   | Calendar   |
| Search Subfolders | Indicates whether subfolders will be searched | True<br>False   |
| Start Date   | The start date   | DateTime   |
| End Date   | The end date   | DateTime   |

## Find Appointments Optional Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Maximum Items | The maximum number of items to return | Integer   |

## Find Appointments Filters

| **Element**   | **Description**   | **Filters**   |
|:---|:---|:---|
| Adjacent Meeting Count   | The number of calendar entries that are adjacent to the appointment   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Allow New Time Proposal   | Indicates whether new time proposals are allowed for attendees of the meeting   | Equals<br>Does not equal   |
| Appointment Reply Time   | When the attendee replied to the meeting request   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Appointment Sequence Number | The sequence number of the appointment   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Appointment State   | The state of the appointment   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Appointment Type   | The type of the appointment   | Equals <br>Does not equal   |
| Body   | Body of the appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Conflicting Meeting Count   | The number of calendar entries that conflict with the appointment   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Date/Time Created   | Date and time the appointment was created   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Duration in Minutes   | The duration of the appointment in minutes   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Free Busy Status   | The value that indicates the free/busy status of the owner of the appointment   | Equals<br>Does not equal   |
| Has Attachments   | Indicates whether the item has an attachment   | Equals<br>Does not equal   |
| iCal DateTime Stamp   | iCalendar DateTimeStamp   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| iCal Recurrence ID   | The iCalendar RecurrenceId   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| iCal Uid   | The iCalendar Uid   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Start with   |
| ID   | ID of the appointment   | Equals<br>Does not equal   |
| Importance   | Importance of the appointment   | Equals<br>Does not equal   |
| Is All Day Event   | Indicates whether the appointment is an all-day event   | Equals<br>Does not equal   |
| Is Cancelled   | Indicates whether the appointment has been cancelled   | Equals<br>Does not equal   |
| Is Meeting   | Indicates whether the appointment is a meeting   | Equals<br>Does not equal   |
| Is Online Meeting   | Indicates whether the meeting is an online meeting   | Equals<br>Does not equal   |
| Is Recurring   | Indicates whether the appointment is recurring   | Equals<br>Does not equal   |
| Is Reminder Set   | Indicates whether there is a reminder set for this appointment   | Equals<br>Does not equal   |
| Is Response Requested   | Indicates whether responses are requested when invitations are sent   | Equals<br>Does not equal   |
| Is Submitted   | Indicates whether this message has been submitted to sent   | Equals<br>Does not equal   |
| Is Unmodified   | Indicates if the appointment has been modified since creation   | Equals<br>Does not equal   |
| Last Modified Date   | Time and date the appointment was last modified   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Last Modified Name   | Name of the user who last modified this appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Start with   |
| Location   | Location of the appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Start with   |
| Meeting Workspace URL   | The URL of the meeting workspace   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Meeting Request Was Sent   | Indicates whether the meeting request has been sent   | Equals<br>Does not equal   |
| NetShow URL   | URL of the Microsoft NetShow meeting   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Organizer   | The organizer of the meeting   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Original Start   | The original start time of the appointment   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Reminder (Minutes)   | The number of minutes before the appointment that a reminder will be triggered. | Equals<br>Does not equal<br>Is less than or equal to <br>Is greater than or equal to<br>Is less than<br>Is greater than |
| Reminder Due By   | Date and time when the reminder for this appointment will be triggered   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Sensitivity   | Sensitivity setting of the appointment   | Equals<br>Does not equal   |
| Start   | The start time of the appointment   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to   |
| Subject   | The subject of the appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Time Zone   | The specified time zone for the appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |

## Find Appointments Published Data

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Adjacent Meeting Count   | The number of calendar items that are adjacent to the appointment   | Number   |
| Allow New Time Proposal   | Indicates whether the new time proposals are allowed   | Boolean   |
| Appointment Reply Time   | The date and time when the attendee replied to the meeting request   | DateTime   |
| Appointment Sequence Number   | The sequence number of the appointment   | Number   |
| Appointment State   | The state of the appointment   | String   |
| Appointment Type   | The type of the appointment   | String   |
| Attachments   | List of attachments for the item   | String   |
| Body   | The body of the appointment   | String   |
| Body Type   | Content type of body   | String   |
| Categories   | List of categories associated with the appointment   | String   |
| Conflicting Meeting Count   | Number of conflicting appointments   | Number   |
| Culture   | Culture associated with the appointment   | String   |
| Date/Time Created   | Date and time the message was created   | DateTime   |
| Domain   | Domain the Exchange server belongs to   | String   |
| Duration in Minutes   | The duration of the appointment in minutes   | Number   |
| End   | Sets the end time of the appointment   | DateTime   |
| Exchange Server Address   | Address of the Exchange server   | String   |
| Free Busy Status   | Value indicating the free/busy status of the owner of the appointment   | String   |
| Has Attachments   | Indicates whether the item has an attachment   | Boolean   |
| ID   | ID of the appointment   | String   |
| Importance   | Importance of the appointment   | String   |
| Is All Day Event   | Indicates whether the appointment is an all day event   | Boolean   |
| Is Cancelled   | Indicates whether the appointment has been cancelled   | Boolean   |
| Is Meeting   | Indicates whether the appointment is a meeting   | Boolean   |
| Is Online Meeting   | Indicates whether the meeting is an online meeting   | Boolean   |
| Is Recurring   | Indicates whether the appointment is recurring   | Boolean   |
| Is Reminder Set   | Indicates whether there is a reminder set for this appointment   | Boolean   |
| Is Response Requested   | Indicates whether a response is requested for this appointment invitation   | Boolean   |
| Is Submitted   | Indicates whether this message has been submitted to sent   | Boolean   |
| Is Unmodified   | Indicates if the appointment has been modified since creation   | Boolean   |
| Item Count   | Number of appointments found   | Number   |
| Last Modified Date   | Time and date the appointment was last modified   | DateTime   |
| Last Modified Name   | Name of the user who last modified this appointment   | String   |
| Location   | Location of the appointment   | String   |
| Meeting Request Was Sent   | Indicates whether a meeting request has been sent   | Boolean   |
| Meeting Workspace URL   | URL of the Meeting Workspace   | String   |
| NetShow URL   | URL of the Microsoft NetShow meeting   | String   |
| Optional Attendees   | List of optional attendees for the meeting   | String   |
| Organizer   | The organizer of the meeting   | String   |
| Original Start   | The original start time of the appointment   | String   |
| Parent Folder ID   | ID of the appointment's parent folder   | String   |
| Reminder (Minutes)   | Number of minutes before the occurrence a reminder should be triggered   | Integer   |
| Reminder Due By   | Date and time when the reminder for this appointment will be triggered   | DateTime   |
| Required Attendees   | List of required attendees   | String   |
| Resources   | List of resources for the meeting   | String   |
| Search Folder   | The name of the folder to be searched for items   | String   |
| Search Subfolders   | Indicates whether subfolders should be searched   | Boolean   |
| Sensitivity   | Sets the sensitivity of the appointment   | String   |
| Start Date   | The date and time to start searching from   | DateTime   |
| End Date   | The date and time to stop searching at   | DateTime   |
| Start   | The start time of the appointment   | DateTime   |
| Subject   | The subject of the appointment   | String   |
| Time Zone   | The time zone that is specified for the appointment   | String   |
| Timeout (seconds)   | Timeout value for the Exchange server connection   | Number   |
| Use Autodiscover   |   | Boolean   |
| User Name   | Username used to log on to the Exchange server   | String   |
| Web Client Edit From Query String | Query string to append to the Exchange Web client URL to open the appointment for editing | String   |
| Web Client Read From Query String | Query string to append to the Exchange Web client URL to open the appointment for reading | String   |
| iCal DateTime Stamp   | Contains the iCalendar DateTimeStamp   | DateTime   |
| iCal Recurrence ID   | Contains the iCalendar RecurrenceId   | DateTime   |
| iCal UID   | Contains the Uid   | String   |
