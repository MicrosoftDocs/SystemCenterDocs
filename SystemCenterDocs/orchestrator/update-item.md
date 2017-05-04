---
title: Update Item
description: The Update Item activity is used in a runbook to update an existing item.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 87f2a757-d513-44fb-b1c5-bcf2feeec0bf
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Update Item

Applies To: System Center 2016 - Orchestrator

The Update Item activity is used in a runbook to update an existing item.

The following tables list the required properties, optional properties, and published data for this activity. Optional properties are presented in separate tables according to item type: appointment, contact group, task, and email message.

## Update Item Required Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| ID   | The ID of the item to be updated | String   |

## Update Item Optional Properties (Appointment)

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Allow New Time Proposal | Indicates whether new time proposals are allowed   | Boolean   |
| Attachments   | List of attachments for the appointment   | Comma separated list of file paths   |
| Body   | The message body of the appointment   | String   |
| Body Type   | Message body content type   | String   |
| Categories   | List of categories associated with the appointment   | Comma separated list   |
| End   | End time of the appointment   | DateTime   |
| Free Busy Status   | Indicates the free/busy status of the owner of the appointment   | String   |
| Importance   | The importance of the appointment   | String   |
| Is Online Meeting   | Indicates whether the appointment is an online meeting   | Boolean   |
| Is All Day Event   | Indicates whether the appointment is an all-day event   | Boolean   |
| Is Reminder Set   | Indicates whether a reminder is set for this appointment   | Boolean   |
| Is Response Requested   | Indicates whether responses are requested   | Boolean   |
| Location   | The location of the appointment   | String   |
| NetShow URL   | The URL of the Microsoft NetShow online meeting   | String   |
| Number of Occurrences   | Number of occurrences for a recurring appointment   | Number   |
| Optional Attendees   | List of optional attendees for the meeting   | Comma separated list of email addresses   |
| Recurrence   | The recurrence pattern for a recurring appointment   | Daily<br>Weekly<br>The same day each month<br>The same week each month<br>The same day each year<br>The same week each year |
| Recurrence Ends   | End of the recurrence period   | DateTime   |
| Recurrence Interval   | Recurrence interval   | Number   |
| Recurs On These Days   | The day(s) on which the appointment recurs   | String   |
| Reminder (Minutes)   | The number of minutes before the start of the item that the reminder is to be triggered | Integer   |
| Reminder Due By   | The date and time when the reminder is due for this item   | DateTime   |
| Required Attendees   | List of required attendees   | Comma separated list of email addresses   |
| Resources   | List of resources for the meeting   | Comma separated list   |
| Sensitivity   | The sensitivity of the item   | Normal <br>Personal<br>Private<br>Confidential   |
| Start   | The start time of the appointment   | DateTime   |
| Subject   | The subject of the appointment   | String   |

## Update Item Optional Properties (Contact Group)

| **Element**  | **Description**   | **Valid values**   |
|:---|:---|:---|
| Display Name | Name of the contact group   | String   |
| Members   | Members a contact group   | Comma separated list of email addresses |
| Categories   | Lists of categories associated with the contact group | Comma separated list   |

## Update Item Optional Properties (Task)

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Actual Work   | The actual amount of work spent on the task   | Number   |
| Billing Information   | Billing information for the task   | String   |
| Body   | The body of the item   | String   |
| Body Type   | Indicates whether the body is text or HTML   | String   |
| Categories   | List of categories associated with the task   | Comma separated list   |
| Companies   | List of companies associated with the task   | Comma separated list   |
| Complete Date   | The date and time that the task was completed   | DateTime   |
| Contacts   | List of contacts associated with the task   | Comma separated list   |
| Due Date   | The date and time that the task is due   | DateTime   |
| Importance   | The importance of the task   | String   |
| Is Reminder Set   | Indicates whether a reminder is set for the task   | Boolean   |
| Mileage   | The mileage of the task   | String   |
| Number of Occurrences | Number of occurrences for a recurring task   | Integer   |
| Percent Complete   | The completion percentage of the task   | Number   |
| Recurrence   | The recurrence pattern for a recurring task   | Daily<br>Weekly<br>The same day each month<br>The same week each month<br>The same day each year<br>The same week each year |
| Recurrence Ends   | Timing of the last occurrence of the task   | DateTime   |
| Recurrence Interval   | The recurrence interval   | Integer   |
| Recurs On These Days  | The day(s) on which the task recurs   | String   |
| Reminder (Minutes)   | Number of minutes before the occurrence that a reminder is to be triggered | Integer   |
| Reminder Due By   | The reminder due date and time for this task   | DateTime   |
| Sensitivity   | Sensitivity of the task   | Normal <br>Personal<br>Private<br>Confidential   |
| Start Date   | The date and time that the task starts   | DateTime   |
| Subject   | The subject of the task   | String   |
| Task Status   | The status of the task   | NotStarted<br>InProgress<br>Completed<br>WaitingOnOthers<br>DeferredString   |
| Total Work   | The total amount of work spent on the task   | Integer   |

## Update Item Optional Properties (E-Mail Message)

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Attachments   | List of attachments   | String   |
| Bcc   | List of Bcc recipients for this email   | Comma separated list of email addresses   |
| Body   | The body of the email message   | String   |
| Body Type   | Format of the email message body   | Text<br>HTML   |
| Categories   | List of categories associated with the email   | Comma separated list   |
| Cc   | List of recipients for the email message   | Comma separated list of email addresses   |
| From   | Who the email came from   | String   |
| Importance   | The importance of the email   | Low<br>Normal<br>High   |
| In Reply To   | The In-Reply-To reference   | String   |
| Is Delivery Receipt Requested | Indicates whether a delivery receipt is requested   | True<br>False   |
| Is Read   | Indicates whether the email message has been read   | True<br>False   |
| Is Read Receipt Requested   | Indicates whether a read receipt is requested for the email message | True<br>False   |
| Is Response Requested   | Indicates whether a response is requested for the email message   | True<br>False   |
| References   | Sets the reference of the email message.   | String   |
| Sender   | The sender of the email message   | String   |
| Sensitivity   | The sensitivity of the email   | Normal<br>Personal<br>Private<br>Confidential |
| Subject   | The subject of the e-mail   | String   |
| To   | List of recipients of the email message   | String   |

## Update Item Published Data

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Domain   | Domain to which the computer that runs Exchange server belongs  | String   |
| Exchange Server Address | Address of the computer that runs Exchange server   | String   |
| ID   | ID of the item to be sent   | String   |
| Item Type   | The type of item being sent   | String   |
| Timeout (seconds)   | Connection timeout threshold   | Number   |
| Use Autodiscover   | Indicates whether or not the Autodiscover service is being used | Boolean   |
| User Name   | Username to used to log on to the Exchange server   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
