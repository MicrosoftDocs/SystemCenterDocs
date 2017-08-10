---
title: Monitor Item
description: The Monitor Item activity is used in a runbook to monitor new or modified items.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 99513133-5547-471a-b1c1-cabfad6eab0b
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Monitor Item

> Applies To: System Center 2016 - Orchestrator

The Monitor Item activity is used in a runbook to monitor new or modified items.

The following tables list the required properties, filters, and published data for this activity. The tables for filters and published data are presented according to the supported item types: appointment, contact group, email message, and task.

## Monitor Item required properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Search Folder   | Folder to search for the item   | String   |
| Search Subfolders   | Indicates whether subfolders are going to be searched as well | True<br>False   |
| Monitor New Items   | Indicates whether new items should be monitored   | True<br>False   |
| Monitor Updated Items | Indicates whether updated items should be monitored   | True<br>False   |
| Monitor Intervals   | Monitoring interval   | Integer   |

## Monitor Item filters (appointment)

| **Element**   | **Description**   | **Filters**   |
|:---|:---|:---|
| Allow New Time Proposal   | Indicates whether new time proposals are allowed for attendees of the meeting | Equals<br>Does not equal   |
| Appointment Reply Time   | When the attendee replied to the meeting request   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Appointment Sequence Number | The sequence number of the appointment   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Appointment State   | The state of the appointment   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Body   | Body of the appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Date/Time Created   | Date and time the appointment was created   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Free Busy Status   | The free/busy status of the owner of the appointment   | Equals<br>Does not equal   |
| Has Attachments   | Indicates whether the message has an attachment   | Equals<br>Does not equal   |
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
| Is Submitted   | Indicates whether this appointment has been submitted to be sent   | Equals<br>Does not equal   |
| Is Unmodified   | Indicates if the appointment has been modified since its initial creation   | Equals<br>Does not equal   |
| Last Modified Date   | Time and date the appointment was last modified   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Last Modified Name   | Name of the user who last modified the appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Start with   |
| Location   | The location of the appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Start with   |
| Meeting Workspace URL   | The URL of the meeting workspace   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Start with   |
| Meeting Request Was Sent   | Indicates whether the meeting request has been sent   | Equals<br>Does not equal   |
| NetShow Url   | URL of the Microsoft NetShow meeting   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Organizer   | The organizer of the meeting   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Reminder (Minutes)   | Number of minutes before the occurrence that a reminder should be triggered   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Sensitivity   | Sensitivity of the appointment   | Equals<br>Does not equal   |
| Start   | The start time of the appointment   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Subject   | The subject of the appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Time Zone   | The time zone that is specified for the appointment   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |

## Monitor Item published data (appointment)

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Adjacent Meeting Count   | The number of calendar items that are adjacent to the appointment   | Number   |
| Allow New Time Proposal   | Indicates whether the new time proposals are allowed   | Boolean   |
| Appointment Reply Time   | The date and time when the attendee replied to the meeting request   | DateTime   |
| Appointment Sequence Number   | The sequence number of the appointment   | Number   |
| Appointment State   | The state of the appointment   | String   |
| Appointment Type   | The type of the appointment   | String   |
| Attachments   | List of attachments for the meeting   | String   |
| Body   | The body of the appointment   | String   |
| Body Type   | Body text format   | String   |
| Categories   | List of categories associated with the appointment   | String   |
| Conflicting Meeting Count   | Number of conflicting appointments   | Number   |
| Culture   | Culture associated with the appointment   | String   |
| Date/Time Created   | Date and time the appointment was created   | DateTime   |
| Domain   | Domain the Exchanges server belongs to   | String   |
| Duration In Minutes   | The duration of the appointment in minutes   | Number   |
| End   | Sets the end time of the appointment   | DateTime   |
| Exchange Server Address   | Address of the Exchange server   | String   |
| Free Busy Status   | The free/busy status of the owner of the appointment   | String   |
| Has Attachments   | Indicates whether the message has an attachment   | Boolean   |
| ID   | ID of the appointment   | String   |
| Importance   | The importance of the appointment   | String   |
| Is All Day Event   | Indicates whether the appointment is an all day event   | Boolean   |
| Is Cancelled   | Indicates whether the appointment has been cancelled   | Boolean   |
| Is Meeting   | Indicates whether the appointment is a meeting   | Boolean   |
| Is Online Meeting   | Indicates whether the meeting is an online meeting   | Boolean   |
| Is Recurring   | Indicates whether the appointment is recurring   | Boolean   |
| Is Reminder Set   | Indicates whether a reminder is set for this appointment   | Boolean   |
| Is Response Requested   | Indicates whether responses are requested   | Boolean   |
| Is Submitted   | Indicates whether this appointment has been submitted to be sent   | Boolean   |
| Is Unmodified   | Indicates if the appointment has been modified since creation   | Boolean   |
| Item Count   | Number of items found   | Number   |
| Item Type   | Type of this item   | String   |
| Last Modified Date   | The date and time that the item was last modified   | DateTime   |
| Last Modified Name   | The name of the user who last modified the item   | String   |
| Location   | The location of the appointment   | String   |
| Meeting Request Was Sent   | Indicates whether the meeting request has been sent   | Boolean   |
| Monitor Interval   | Monitor interval   | Number   |
| Monitor New Items   | Indicates whether new items are monitored   | Boolean   |
| Monitor Timestamp   | Timestamp of the last monitoring cycle   | DateTime   |
| Monitor Updated Items   | Indicates whether updated items are monitored   | Boolean   |
| Meeting Workspace URL   | The URL of the meeting workspace   | String   |
| NetShow URL   | The URL of the Microsoft NetShow online meeting   | String   |
| Optional Attendees   | Optional attendees   | String   |
| Organizer   | The organizer of the meeting   | String   |
| Original Start   | The original start time of the appointment   | DateTime   |
| Reminder (Minutes)   | The number of minutes before the start of the item that the reminder should be triggered  | Integer   |
| Reminder Due By   | The date and time when the reminder is due for this item   | DateTime   |
| Required Attendees   | List of required attendees   | String   |
| Resources   | List of resources for the meeting   | String   |
| Search Folder   | Folder to search for appointments   | String   |
| Search Subfolders   | Indicates whether subfolders are to be searched   | Boolean   |
| Sensitivity   | Sensitivity of the item   | String   |
| Start   | The start time of the appointment   | DateTime   |
| Subject   | The subject of the appointment   | String   |
| Time Zone   | The time zone that is specified for the appointment   | String   |
| Timeout (seconds)   | Connection timeout threshold   | Number   |
| Use Autodiscover   | Indicates whether or not the Autodiscover service is used   | Boolean   |
| User Name   | Username used to log on to the Exchange server   | String   |
| Web Client Edit Form Query String | Query string to append to the Exchange Web client URL to open the appointment for editing | String   |
| Web Client Read Form Query String | Query string to append to the Exchange Web client URL to open the appointment for reading | String   |
| iCal DateTime Stamp   | The iCal date/time stamp   | DateTime   |
| iCal Recurrence ID   | The iCal RecurrenceId   | DateTime   |
| iCal Uid   | The iCal UiD   | String   |

## Monitor Item filters (contact group)

| **Element**   | **Description**   | **Filters**   |
|:---|:---|:---|
| Date/Time Created  | Date and time the contact group was created   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Display Name   | Name of the contact group   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| ID   | ID of the contact group   | Equals<br>Does not equal   |
| Is Unmodified   | Indicates if the contact group has been modified since creation | Equals<br>Does not equal   |
| Last Modified Date | Time and date the contact group was last modified   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Last Modified Name | Name of the user who last modified this contact group   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Start with   |
| Members   | List of members associated with the contact group   | Comma separated list of email addresses   |

## Monitor Item published data (contact group)

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Categories   | List of categories associated with the item   | String   |
| Culture   | Culture associated with the contact group   | String   |
| Date/Time Created   | Date and time the contact group was created   | DateTime   |
| Display Name   | Name of the contact group   | String   |
| Domain   | Domain the Exchange server belongs to   | String   |
| Exchange Server Address   | Address of the Exchange server   | String   |
| ID   | ID of the contact group   | String   |
| Is Unmodified   | Indicates if the contact group has been modified since creation   | Boolean   |
| Item Count   | Number of items found   | Number   |
| Item Type   | Type of this item   | String   |
| Last Modified Date   | The name of the user who last modified the item   | DateTime   |
| Last Modified Name   | The date and time that the item was last modified   | String   |
| Members   | List of members associated with the contact group   | Comma separated list of email addresses |
| Monitor Interval   | Monitor interval   | Number   |
| Monitor New Items   | Indicates whether new items are monitored   | Boolean   |
| Monitor Timestamp   | Timestamp of the last monitoring cycle   | DateTime   |
| Monitor Updated Items   | Indicates whether updated items are monitored   | Boolean   |
| Parent Folder ID   | ID of the contact group's parent folder   | String   |
| Search Folder   | The folder to search for contact groups   | String   |
| Search Subfolders   | Indicates whether subfolders should be included in the search   | String   |
| Timeout (seconds)   | Connection timeout threshold   | Number   |
| Use Autodiscover   | Indicates whether or not the Autodiscover service is used   | Boolean   |
| User Name   | Username used to log on to the Exchange server   | String   |
| Web Client Edit Form Query String | Query string to append to the Exchange Web client URL to open the contact group for editing | String   |
| Web Client Read Form Query String | Query string to append to the Exchange Web client URL to open the contact group for reading | String   |

## Monitor Item filters (e-mail message)

| **Element**   | **Description**   | **Filters**   |
|:---|:---|:---|
| Body   | The body of the item   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Conversation ID   | The ID of the conversation that this item is a part of   | Equals<br>Does not equal   |
| Conversation Topic   | The conversation topic of the email message   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Date/Time Created   | The date and time that the item was created   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Date/Time Received   | The date and time that the item was received   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Date/Time Sent   | The date and time that the item was sent   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| From   | Who the email came from   | Equals<br>Does not equal   |
| Has Attachments   | Indicates whether the item has attachments   | Equals <br>Does not equal   |
| ID   | The ID of the item   | Equals<br>Does not equal   |
| Importance   | The importance of the item   | Equals<br>Does not equal   |
| In Reply To   | The In-Reply-To reference   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Is Draft   | Indicates whether the item is a draft   | Equals <br>Does not equal   |
| Is Read   | Indicates whether the email message has been read   | Equals <br>Does not equal   |
| Is Response Requested | Indicates whether a response is requested for the email message   | Equals <br>Does not equal   |
| Is Submitted   | Indicates whether the item has been submitted to be sent   | Equals <br>Does not equal   |
| Is Unmodified   | Indicates whether the item has been modified since it was created | Equals <br>Does not equal   |
| Last Modified Name   | The name of the user who last modified the item   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Last Modified Date   | The date and time that the item was last modified   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Received By   | The delegate who received the email message   | Equals<br>Does not equal   |
| Received Representing | The principal recipient of the email message   | Equals<br>Does not equal   |
| References   | Reference of the item   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Start with   |
| Sender   | The sender of the email message   | Equals<br>Does not equal   |
| Sensitivity   | The sensitivity of the email   | Equals<br>Does not equal   |
| Subject   | The subject of the email   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |

## Monitor Item published data (e-mail message)

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Attachments   | List of attachments   | String   |
| Bcc   | List of Bcc recipients for the email message   | String   |
| Body   | The body of the item   | String   |
| Body Type   | The format of the message body (text or HTML)   | String   |
| Categories   | List of categories associated with the item   | String   |
| Cc   | List of Cc recipients for the email message   | String   |
| Conversation ID   | The ID of the conversation that this item is a part of   | String   |
| Conversation Topic   | The conversation topic of the email message   | String   |
| Culture   | The culture that is associated with the item   | String   |
| Date/Time Created   | The date and time that the item was created   | DateTime   |
| Date/Time Received   | The date and time that the item was received   | DateTime   |
| Date/Time Sent   | The date and time that the item was sent   | DateTime   |
| Domain   | Domain the Exchange server belongs to   | String   |
| Exchange Server Address   | Address of the Exchange server   | String   |
| From   | Who the email came from   | String   |
| Has Attachments   | Indicates whether the item has attachments   | Boolean   |
| ID   | The ID of the item   | String   |
| Importance   | The importance of the item   | String   |
| In Reply To   | The In-Reply-To reference   | String   |
| Is Delivery Receipt Requested   | Indicates whether a delivery receipt us requested   | Boolean   |
| Is Draft   | Indicates whether the item is a draft   | Boolean   |
| Is From Me   | Indicates whether the item was sent by the current user   | Boolean   |
| Is Read   | Indicates whether the email message has been read   | Boolean   |
| Is Read Receipt Requested   | Indicates whether a read receipt is requested for the email message   | Boolean   |
| Is Resend   | Indicates whether the email is a resend of another item   | Boolean   |
| Is Response Requested   | Indicates whether a response is requested for the email message   | Boolean   |
| Is Submitted   | Indicates whether the item has been submitted to be sent   | Boolean   |
| Is Unmodified   | Indicates whether the item has been modified since it was created   | Boolean   |
| Item Count   | The number of email messages found   | Number   |
| Item Type   | Type of the item   | String   |
| Last Modified Name   | The name of the user who last modified the item   | String   |
| Last Modified Date   | The date and time that the item was last modified   | DateTime   |
| Monitor Interval   | Monitor polling interval in seconds   | Number   |
| Monitor New Items   | Indicates whether new items should be monitored   | Boolean   |
| Monitor Timestamp   | Time of the last monitoring cycle   | DateTime   |
| Monitor Updated Items   | Indicates whether updated items should be monitored   | Boolean   |
| Parent Folder ID   | The ID of the parent folder of the item   | String   |
| Received By   | The delegate who received the email message   | String   |
| Received Representing   | The principal recipient of the email message   | String   |
| References   | References of the message   | String   |
| Reply To   | List of email addresses to which replies should be sent   | String   |
| Search Folder   | The folder to search for emails   | String   |
| Search Subfolders   | Indicates whether subfolders should be searched   | String   |
| Sender   | The sender of the email message   | String   |
| Sensitivity   | The sensitivity of the email   | String   |
| Subject   | The subject of the email   | String   |
| Timeout (seconds)   | The connection timeout threshold in seconds   | Number   |
| To   | List of To recipients of the email message   | String   |
| Use Autodiscover   | Indicates whether or not the Autodiscover service is used   | Boolean   |
| User Name   | Username used to log on to the Exchange server   | String   |
| Web Client Edit Form Query String | Query string to append to the Exchange Web client URL to open the email for editing | String   |
| Web Client Read Form Query String | Query string to append to the Exchange Web client URL to open the email for reading | String   |

## Monitor Item filters (task)

| **Element**   | **Description**   | **Filters**   |
|:---|:---|:---|
| Actual Work   | The actual amount of work spent on the task   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Assigned Time   | Date and time the task was assigned   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Billing Information | Billing information for the task   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Body   | The body of the task   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Change Count   | The number of times the task has changed since it was created   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Complete Date   | The date and time that the task was completed   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Date/Time Created   | Date and time the task was created   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Delegation State   | The current delegation state of the task   | Equals<br>Does not equal   |
| Delegator   | The name of the delegator of the task   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Due Date   | The date and time that the task is due   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| ID   | The ID of the item   | Equals<br>Does not equal   |
| Importance   | The importance of the task   | Equals<br>Does not equal   |
| Is Complete   | Indicates whether the task is complete   | Equals<br>Does not equal   |
| Is Recurring   | Indicates whether the task is recurring   | Equals<br>Does not equal   |
| Is Reminder Set   | Indicates whether a reminder is set   | Equals<br>Does not equal   |
| Is Team Task   | Indicates whether the task is a team task   | Equals<br>Does not equal   |
| Is Unmodified   | Indicates whether the item has been modified since it was created   | Equals<br>Does not equal   |
| Last Modified Name  | The name of the user who last modified the item   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Last Modified Date  | The date and time that the item was last modified   | Equals<br>Does not equal   |
| Mileage   | The mileage of the task   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Owner   | The name of the owner of the task   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Percent Complete   | The completion percentage of the task   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Reminder (Minutes)  | The number of minutes before the start of the item that the reminder should be triggered | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Sensitivity   | The sensitivity of the item   | Equals<br>Does not equal   |
| Start Date   | The date and time that the task starts   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |
| Subject   | The subject of the task   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Starts with   |
| Task Status   | The status of the task   | Equals<br>Does not equal   |
| Total Work   | The total amount of work spent on the task   | Equals<br>Does not equal<br>Less than<br>Less than or equal to<br>Greater than<br>Greater than or equal to |

## Monitor Item published data (task)

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Actual Work   | The actual amount of work spent on the task   | Number   |
| Assigned Time   | The date and time the task was assigned   | DateTime   |
| Billing Information   | Billing information for the task   | String   |
| Body   | The body of the task   | String   |
| Body Type   | Indicates whether the body is text or HTML   | String   |
| Categories   | List of categories associated with the item   | String   |
| Change Count   | The number of times the task has changed since it was created   | Number   |
| Companies   | List of companies associated with the task   | String   |
| Complete Date   | The date and time that the task was completed   | DateTime   |
| Contacts   | List of contacts associated with the task   | String   |
| Culture   | The culture associated with the item   | String   |
| Date/Time Created   | The date and time the item was created   | DateTime   |
| Delegation State   | The current delegation state of the task   | String   |
| Delegator   | The name of the delegator of the task   | String   |
| Domain   | The Domain used to authenticate the Exchange server   | String   |
| Due Date   | The date and time that the task is due   | DateTime   |
| Exchange Server Address   | Address of the Exchange server   | String   |
| ID   | The ID of the item   | String   |
| Importance   | The importance of the task   | String   |
| Is Complete   | Indicates whether the task is complete   | Boolean   |
| Is Recurring   | Indicates whether the task is recurring   | Boolean   |
| Is Reminder Set   | Indicates whether a reminder is set   | Boolean   |
| Is Team Task   | Indicates whether the task is a team task   | Boolean   |
| Is Unmodified   | Indicates whether the item has been modified since its creation   | Boolean   |
| Item Count   | The number of tasks found   | Number   |
| Item Type   | Type of the item   | String   |
| Last Modified Date   | The date and time item was last modified   | DateTime   |
| Last Modified Name   | The name of the user who last modified the item   | String   |
| Mileage   | The mileage of the task   | String   |
| Monitor Interval   | Monitor polling interval in seconds   | Number   |
| Monitor News Items   | Indicates whether new items should be monitored   | Boolean   |
| Monitor Timestamp   | Time of the last monitoring cycle   | DateTime   |
| Monitor Updated Items   | Indicates whether updated items should be monitored   | Boolean   |
| Owner   | The name of the owner of the task   | String   |
| Parent Folder ID   | The ID of the parents   | String   |
| Percent Complete   | The completion percentage of the task   | Decimal   |
| Reminder (Minutes)   | The number of minutes before the start of the task a reminder is sent   | Integer   |
| Reminder Due By   | The date and time when the reminder is due for this task   | DateTime   |
| Search Folder   | The folder to search for tasks   | String   |
| Search Subfolders   | Indicates whether subfolders should be searched   | String   |
| Sensitivity   | The sensitivity of the item   | String   |
| Start Date   | The date and time that the task starts   | DateTime   |
| Subject   | The subject of the task   | String   |
| Task Status   | The execution status of the task   | String   |
| Timeout (seconds)   | Connection timeout threshold   | Number   |
| Total Work   | The total amount of work spent on the task   | Number   |
| Use Autodiscover   | Indicates whether or not the Autodiscover service is used   | Boolean   |
| User Name   | Username used to log on to the Exchange server   | String   |
| Web Client Edit Form Query String | Query string to append to the Exchange Web client URL to open the task for editing | String   |
| Web Client Read Form Query String | Query string to append to the Exchange Web client URL to open the task for reading | String   |
