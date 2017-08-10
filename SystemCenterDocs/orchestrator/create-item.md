---
title: Create Item
description: The Create Item activity is used in a runbook to create new appointment, contact group, and Email Message or task items.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 5e06c804-4544-4479-a664-d4a92df0c20b
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create Item

Applies To: System Center 2016 - Orchestrator

The Create Item activity is used in a runbook to create new appointment, contact group, and Email Message or task items.

The following tables list the required properties, optional properties, and published data for Create Item activities. The required and optional properties are presented according to item type: appointment, contact group, task, and email message.

Additionally, this topic describes how to create recurring appointments and tasks.

## Create Item Required Properties (Appointment)

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Start   | The start time of the appointment | DateTime   |
| End   | The end time of the appointment   | DateTime   |
| Subject   | The subject of the appointment   | String   |
| Body   | Details about the appointment   | String   |

## Create Item Optional Properties (Appointment)

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Allow New Time Proposal | Indicates whether the new time proposals are allowed   | True<br>False   |
| Attachments   | List of attachments for the item   | Comma separated list of file paths   |
| Body Type   | Content type of body   | Text<br>HTML   |
| Categories   | List of categories that are associated with the appointment   | Comma separated list   |
| Destination Folder   | Alternative destination folder of the appointment   | String   |
| Free Busy Status   | The free/busy status of the owner of the appointment   | Free<br>Tentative<br>Busy<br>OOF<br>NoData   |
| Importance   | Sets the importance of the appointment   | Low<br>Normal<br>High   |
| Is All Day Event   | Indicates whether the appointment is an all-day event   | True<br>False   |
| Is Online Meeting   | Indicates whether the appointment is an online meeting   | True<br>False   |
| Is Reminder Set   | Indicates whether a reminder is set for the appointment   | True<br>False   |
| Is Response Requested   | Indicates whether responses are requested   | True<br>False   |
| Location   | The location of the appointment   | String   |
| NetShow URL   | The URL of the Microsoft NetShow online meeting   | String   |
| Number of Occurrences   | Number of occurrences   | Integer   |
| Optional Attendees   | Optional attendees for the meeting   | Comma separated list of e-mail addresses   |
| Recurrence   | The recurrence pattern for the meeting   | Daily<br>Weekly<br>The same day each month<br>The same week each month<br>The same day each year<br>The same week each year |
| Recurrence Ends   | The last occurrence of the meeting   | DateTime   |
| Recurrence Interval   | The recurrence interval   | Integer   |
| Recurs On These Days   | The day(s) on which the appointment recurs   | String   |
| Reminder (Minutes)   | Defines how many minutes before the occurrence a reminder is to be triggered | Integer   |
| Reminder Due By   | Sets the reminder due date and time for this appointment   | DateTime   |
| Required Attendees   | List of required attendees   | Comma separated list of email addresses   |
| Resources   | List of resources for the meeting   | Comma separated list   |
| Sensitivity   | Sets the sensitivity of the appointment   | Normal <br>Personal<br>Private<br>Confidential   |

## Create Item Required Properties (Contact Group)

| **Element**  | **Description**   | **Valid values**   |
|:---|:---|:---|
| Display Name | The name of the contact group   | String   |
| Members   | List of members associated with contact group | Comma separated list of email addresses |

## Create Item Optional Properties (Contact Group)

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Categories   | List of categories that are associated with the Contact Group | Comma separated list |
| Destination Folder | Alternative destination folder of the Contact Group   | String   |

## Create Item Required Properties (Task)

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Body   | Details about the task   | String   |
| Due Date   | The date and time that the task is due | DateTime   |
| Start Date  | The date and time that the task starts | DateTime   |
| Subject   | The subject of the task   | String   |

## Create Item Optional Properties (Task)

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Actual Work   | The actual amount of work spent on the task   | Number   |
| Billing Information   | Billing information for the task   | String   |
| Body Type   | Indicates whether the body is text or HTML   | Text<br>HTML   |
| Categories   | List of categories associated with the task   | Comma separated list   |
| Companies   | List of companies associated with the task   | Comma separated list   |
| Complete Date   | The date and time that the task was completed   | DateTime   |
| Contacts   | List of contacts associated with the task   | Comma separated list   |
| Destination Folder   | Alternative destination folder of the task   | String   |
| Importance   | The importance of the item.   | Low<br>Normal<br>High   |
| Is Reminder Set   | Indicates whether a reminder is set for the task   | True<br>False   |
| Mileage   | The mileage of the task   | String   |
| Number of Occurrences | Number of occurrences for a recurring task   | Integer   |
| Percent Complete   | The completion percentage of the task   | Number   |
| Recurrence   | The recurrence pattern for the meeting   | Daily<br>Weekly<br>The same day each month<br>The same week each month<br>The same day each year<br>The same week each year |
| Recurrence Ends   | The last occurrence of the task   | DateTime   |
| Recurrence Interval   | The recurrence interval   | Integer   |
| Recurs On These Days  | The day(s) on which the task recurs   | String   |
| Reminder (Minutes)   | Defines how many minutes before the occurrence a reminder is to be triggered | Integer   |
| Reminder Due By   | The date and time when the reminder is due   | DateTime   |
| Sensitivity   | Sensitivity of the task   | Confidential<br>Normal<br>Personal<br>Private   |
| Task Status   | The status of the task   | NotStarted<br>InProgress<br>Completed<br>WaitingOnOthers<br>Deferred   |
| Total Work   | The total amount of work spent on the task   | Integer   |

## Create Item Required Properties (E-Mail Message)

| **Element** | **Description**   | **Valid values**   |
|:---|:---|:---|
| To   | List of recipients of the email | Comma separated list of email addresses |
| Subject   | Subject of the email   | String   |
| Body   | Body of the email   | String   |

## Create Item Optional Properties (E-Mail Message)

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Attachments   | List of attachments   | Comma separated list of file paths   |
| Bcc   | List of Bcc recipients for this email   | Comma separated list of email addresses   |
| Body Type   | Indicates whether the body is text or HTML   | Text<br>HTML   |
| Categories   | List of categories associated with the email   | Comma separated list   |
| Cc   | List of Cc recipients for this email   | Comma separated list of email addresses   |
| Destination Folder   | Alternative destination folder for the sent message | String   |
| From   | Who the email came from   | String   |
| Importance   | The importance of the email   | Low<br>Normal<br>High   |
| In Reply To   | The In-Reply-To reference   | String   |
| Is Delivery Receipt Requested | Indicates whether a delivery receipt is requested   | True<br>False   |
| Is Read Receipt Requested   | Indicates whether a read receipt is requested   | True<br>False   |
| Is Response Requested   | Indicates whether a response is requested   | True<br>False   |
| References   | References of the email   | String   |
| Sender   | The sender of the email message   | String   |
| Sensitivity   | The sensitivity of the email   | Normal<br>Personal<br>Private<br>Confidential |

## Create Item Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| ID   | The ID of the item that was created   | String   |
| Item Type   | The type of the item that was created.   | String   |
| Destination Folder   | The folder where the item is stored   | String   |
| Domain   | Domain the Exchange Server belongs to   | String   |
| Exchange Server Address | Address of the Exchange Server   | String   |
| Timeout (seconds)   | Timeout value for the Exchange Server connection   | Number   |
| Use Autodiscover   | Whether or not to use Autodiscover to check for changes | Boolean   |
| User Name   | User name used to log on to the Exchange Server   | String   |

## Recurring Appointments and Tasks

The integration pack provides the ability to create recurring appointments and tasks. To setup a recurring appointment or task, perform the following steps:

1.  Add the optional **Recurrence** property. <br><br>
2.  Select the desired recurrence pattern from one of the available options.<br><br>
3.  To use a pattern other than the Daily pattern, add the optional **Recurs On These Days** property.<br><br>
4.  Specify a value for the **Recurs On These Days** property according to the rules that are presented in the following table.<br><br>

| **Element**   | **Description**   |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Recurrence   | Recurs On These Days   |
| Daily   | Not required.   |
| Weekly   | Specify a comma separated list of day names. Full or abbreviated day names are acceptable. <br>For example: Saturday, Sunday or Sat, Sun.   |
| The same day each month  | Not required. The day is determined by the start date.   |
| The same week each month | Specify a relative index followed by a day of the week. Valid indexes include First, Second, Third, Fourth, and Last. Days of the week include Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday, Weekday, and WeekendDay.<br>For example: First Monday.   |
| The same day each year   | Not required. The day is determined by the start date.   |
| The same week each year  | Specify a relative index followed by a day of the week. Valid indexes include First, Second, Third, Fourth, and Last. Days of the week include Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday, Weekday, and WeekendDay. The month is determined by the start date.<br>For example: First Monday |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/)
