---
title: Service Manager published data
description: The following tables list the published data elements for all of the classes in the System Center 2016 - Service Manager Integration Pack.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 20fe155e-61d1-41fa-9d74-9df80c6d4022
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Service Manager published data

> Applies To: System Center 2016 - Orchestrator

The following tables list the published data elements for all of the classes in the System Center 2016 - Service Manager Integration Pack.

## Active Directory Group Class published data

Class Category: Visible

| Element Name   | Field Type |
|---------------------|------------|
| Distinguished Name  | string   |
| SID   | string   |
| FQDN   | string   |
| UPN   | string   |
| Domain   | string   |
| User Name   | string   |
| First Name   | string   |
| Initials   | string   |
| Last Name   | string   |
| Company   | string   |
| Department   | string   |
| Office   | string   |
| Title   | string   |
| Employee Identifier | string   |
| Street Address   | string   |
| City   | string   |
| State   | string   |
| Zip   | string   |
| Country   | string   |
| Business Phone   | string   |
| Business Phone2   | string   |
| Home Phone   | string   |
| Home Phone2   | string   |
| Fax   | string   |
| Mobile   | string   |
| Pager   | string   |
| Object Status   | enum   |
| Asset Statusenum   | string   |
| Notes   | string   |
| Display Name   | string   |
| Organization unit   | string   |
| Objectguid   | string   |

## Active Directory User or Group Class published data

Class Category: Visible

| Element Name   | Field Type |
|---------------------|------------|
| Distinguished Name  | string   |
| SID   | string   |
| FQDN   | string   |
| UPN   | string   |
| Domain   | string   |
| User Name   | string   |
| First Name   | string   |
| Initials   | string   |
| Last Name   | string   |
| Company   | string   |
| Department   | string   |
| Office   | string   |
| Title   | string   |
| Employee Identifier | string   |
| Street Address   | string   |
| City   | string   |
| State   | string   |
| Zip   | string   |
| Country   | string   |
| Business Phone   | string   |
| Business Phone2   | string   |
| Home Phone   | string   |
| Home Phone2   | string   |
| Fax   | string   |
| Mobile   | string   |
| Pager   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Active Directory User Class published data

Class Category: Visible

| Element Name   | Field Type |
|---------------------|------------|
| Distinguished Name  | string   |
| SID   | string   |
| FQDN   | string   |
| UPN   | string   |
| Domain   | string   |
| User Name   | string   |
| First Name   | string   |
| Initials   | string   |
| Last Name   | string   |
| Company   | string   |
| Department   | string   |
| Office   | string   |
| Title   | string   |
| Employee Identifier | string   |
| Street Address   | string   |
| City   | string   |
| State   | string   |
| Zip   | string   |
| Country   | string   |
| Business Phone   | string   |
| Business Phone2   | string   |
| Home Phone   | string   |
| Home Phone2   | string   |
| Fax   | string   |
| Mobile   | string   |
| Pager   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Change Request Class published data

Class Type: Visible

| Element Name   | Field Type |
|---------------------|------------|
| Reason   | string   |
| Notes   | string   |
| Implementation Plan   | string   |
| Back out Plan   | string   |
| Test Plan   | string   |
| Post Implementation Review | string   |
| Template ID   | string   |
| Required By Date   | date time  |
| Status   | enum   |
| Category   | enum   |
| Priority   | enum   |
| Impact   | enum   |
| Risk   | enum   |
| Implementation Results   | enum   |
| Area   | enum   |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method   | string   |
| Created Date   | Date time  |
| Scheduled Start Date   | Date time  |
| Scheduled End Date   | Date time  |
| Actual Start Date   | Date time  |
| Actual End Date   | Date time  |
| Display Name   | string   |

## Windows Server Class published data

Class Type: Hidden

| Element Name   | Type   |
|---------------------|------------|
| Is Virtual Node   | boolean   |
| Principal Name   | string   |
| DNS Name   | string   |
| NetBIOS Computer Name   | string   |
| NetBIOS Domain Name   | string   |
| IP Address   | string   |
| Network Name   | string   |
| Active Directory SID   | string   |
| Virtual Machine   | boolean   |
| DNS Domain Name   | string   |
| Organizational Unit   | string   |
| DNS Forest Name   | string   |
| Active Directory Site   | string   |
| Logical Processors   | int32   |
| Offset In Minutes From Greenwich Time | int32   |
| Last Inventory Date   | date time |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |

## Windows Server Operating System Class published data

Class Category: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Operating System Version   | string   |
| Operating System Version Display Name | string   |
| Product Type   | string   |
| Build Number   | string   |
| CSD Version   | string   |
| Service Pack Version   | string   |
| Serial Number   | string   |
| Install Date   | string   |
| System Drive   | string   |
| Windows Directory   | string   |
| Physical Memory (MB)   | int32   |
| Logical Processors   | int32   |
| Country Code   | string   |
| Locale   | string   |
| Description   | string   |
| Manufacturer   | string   |
| OS Language   | string   |
| Minor Version   | string   |
| Major Version   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Trouble Ticket Analyst Comments Class published data

Class Type: Hidden

| Element Name | Field Type |
|---------------------|------------|
| Is Private   | boolean   |
| Comment   | string   |
| Entered By   | string   |
| Entered Date | date time  |
| ID   | string   |
| Display Name | string   |

## Star Rating Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| ID   | string   |
| Total Rating Count | int32   |
| Total Rating Stars | int32   |
| Rating Comments   | string   |
| Display Name   | string   |

## Windows Computer Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Principal Name   | string   |
| DNS Name   | string   |
| NetBIOS Computer Name   | string   |
| NetBIOS Domain Name   | string   |
| IP Address   | string   |
| Network Name   | string   |
| Active Directory SID   | string   |
| Virtual Machine   | boolean   |
| DNS Domain Name   | string   |
| Organizational Unit   | string   |
| DNS Forest Name   | string   |
| Active Directory Site   | string   |
| Logical Processors   | int32   |
| Offset In Minutes From Greenwich Time | int32   |
| Last Inventory Date   | date time  |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Software Items Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Publisher   | string   |
| Version String   | string   |
| Product Name   | string   |
| Major Version   | string   |
| Minor Version   | string   |
| Locale ID   | int32   |
| Is Virtual Application | boolean   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |
| Test\_EX1   | string   |
| Test\_EX2   | string   |
| Domain   | string   |
| User Name   | string   |
| First Name   | string   |
| Initials   | string   |
| Last Name   | string   |
| Company   | string   |
| Department   | string   |
| Office   | string   |
| Title   | string   |
| Employee Identifier   | string   |
| Street Address   | string   |
| City   | string   |
| State   | string   |
| Zip   | string   |
| Country   | string   |
| Business Phone   | string   |
| Business Phone2   | string   |
| Home Phone   | string   |
| Home Phone2   | string   |
| Fax   | string   |
| Mobile   | string   |
| Pager   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Manual Activity Class published data

Class Type: Visible

| Element Name   | Field Type |
|---------------------|------------|
| Sequence ID   | int32   |
| Notes   | string   |
| Status   | enum   |
| Priority   | enum   |
| Area   | enum   |
| Stage   | enum   |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Windows Operating System Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Operating System Version   | string   |
| Operating System Version Display Name | string   |
| Product Type   | string   |
| Build Number   | string   |
| CSD Version   | string   |
| Service Pack Version   | string   |
| Serial Number   | string   |
| Install Date   | date time  |
| System Drive   | string   |
| Windows Directory   | string   |
| Physical Memory (MB)   | int32   |
| Logical Processors   | int32   |
| Country Code   | string   |
| Locale   | string   |
| Description   | string   |
| Manufacturer   | string   |
| OS Language   | string   |
| Minor Version   | string   |
| Major Version   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Program Class published data

Class Type: Hidden

| Element Name  | Field Type |
|---------------------|------------|
| ProgramId   | string   |
| Display name  | string   |
| Program Name  | string   |
| Description   | string   |
| Comment   | string   |
| Command   | string   |
| Msi file path | string   |
| Source Site   | string   |
| Object Status | enum   |
| Asset Status  | enum   |
| Notes   | string   |
| Display Name  | string   |

## Email Notification Log for Trouble Tickets Class published data

Class Type: Hidden

| Element Name | Field Type |
|---------------------|------------|
| Body   | string   |
| Subject   | string   |
| Priority   | int32   |
| Encoding   | string   |
| Sent To   | string   |
| Sent Date   | date time  |
| ID   | string   |
| Display Name | string   |

## System Center Management Group Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Management Group Name   | string   |
| Management Group ID   | string   |
| Data Access Service SCP   | string   |
| Root Management Server Management Service SCP | string   |
| Join Customer Experience Improvement Program  | boolean   |
| Communication Port   | int32   |
| Send Error Reports   | int32   |
| Automatically Send Error Reports   | int32   |
| Online Product Knowledge URL   | string   |
| Send Operational Data Reports   | boolean   |
| Data Access Server Name   | string   |
| Operational Database Name   | string   |
| Operational Database SQL Server   | string   |
| Alert Auto Resolve Period   | int32   |
| Healthy Alert Auto Resolve Period   | int32   |
| Tier Time Difference Threshold   | int32   |
| Service Description   | string   |
| Business Detailed Description   | string   |
| Is Business Service   | boolean   |
| Owned By Organization   | string   |
| Priority   | enum   |
| Status   | enum   |
| Classification   | enum   |
| Availability Schedule   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## File Attachment Class published data

Class Type: Hidden

| Element Name | Field Type |
|---------------------|------------|
| Extension   | string   |
| Description  | string   |
| Content   | string   |
| Size   | int32   |
| Added Date   | date time  |
| ID   | string   |
| Display Name | string   |

## System Center Managed Computer (Client Operating System) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Install Directory   | string   |
| Principal Name   | string   |
| DNS Name   | string   |
| NetBIOS Computer Name   | string   |
| NetBIOS Domain Name   | string   |
| IP Address   | string   |
| Network Name   | string   |
| Active Directory SID   | string   |
| Virtual Machine   | boolean   |
| DNS Domain Name   | string   |
| Organizational Unit   | string   |
| DNS Forest Name   | string   |
| Active Directory Site   | string   |
| Logical Processors   | int32   |
| Offset In Minutes From Greenwich Time | int32   |
| Last Inventory Date   | date time  |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Synchronization Status Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Last Run Start Time   | date time  |
| Last Run Finish Time   | date time  |
| Status   | enum   |
| SyncPercent   | int32   |
| MaxValue   | int32   |
| MinValue   | int32   |
| Display Name   | string   |
| Greeting   | string   |
| Resolve By   | date time  |
| Escalated   | boolean   |
| Source   | enum   |
| Status   | enum   |
| Resolution Description   | string   |
| Needs Knowledge Article   | boolean   |
| Support Group   | enum   |
| Has Created Knowledge Article | boolean   |
| Last Modified Source   | enum   |
| Classification Category   | enum   |
| Resolution Category   | enum   |
| Priority   | int32   |
| Impact   | enum   |
| Urgency   | enum   |
| Closed Date   | date time  |
| Resolved Date   | date time  |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method   | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Physical Disk (Concrete) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Caption   | string   |
| Index   | int32   |
| Interface Type   | string   |
| Manufacturer   | string   |
| Model   | string   |
| SCSI Bus   | int32   |
| SCSI Logical Unit   | int32   |
| SCSI Port   | int32   |
| SCSI Target ID   | int32   |
| Size (MB)   | int32   |
| Total Cylinders   | int32   |
| Total Heads   | int32   |
| Total Sectors   | int32   |
| Total Tracks   | int32   |
| Tracks Per Cylinder   | int32   |
| Perfmon Instance   | string   |
| Media Type   | string   |
| PNP Device Identifier | string   |
| Device Identifier   | string   |
| Device Name   | string   |
| Device Description   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## System Center Managed Computer (Server Operating System) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Install Directory   | string   |
| Principal Name   | string   |
| DNS Name   | string   |
| NetBIOS Computer Name   | string   |
| NetBIOS Domain Name   | string   |
| IP Address   | string   |
| Network Name   | string   |
| Active Directory SID   | string   |
| Virtual Machine Accounts   | boolean   |
| DNS Domain Name   | string   |
| Organizational Unit   | string   |
| DNS Forest Name   | string   |
| Active Directory Site   | string   |
| Logical Processors   | int32   |
| Offset In Minutes From Greenwich Time | int32   |
| Last Inventory Date   | date time  |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Operations Manager-Generated Incident Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Management Group Name   | string   |
| Management Pack Name   | string   |
| Monitoring Rule Identifier   | string   |
| Monitoring Object Identifier  | string   |
| Alert Identifier   | string   |
| Repeat Count   | int32   |
| Alert Custom Field 1   | string   |
| Alert Custom Field 2   | string   |
| Alert Custom Field 3   | string   |
| Alert Custom Field 4   | string   |
| Alert Custom Field 5   | string   |
| Alert Custom Field 6   | string   |
| Alert Custom Field 7   | string   |
| Alert Custom Field 8   | string   |
| Alert Custom Field 9   | string   |
| Alert Custom Field 10   | string   |
| Resolve By   | date time  |
| Escalated   | boolean   |
| Source   | enum   |
| Status   | enum   |
| Resolution Description   | string   |
| Needs Knowledge Article   | boolean   |
| Support Group   | enum   |
| Has Created Knowledge Article | boolean   |
| Last Modified Source   | enum   |
| Classification Category   | enum   |
| Resolution Category   | enum   |
| Priority   | int32   |
| Impact   | enum   |
| Urgency   | enum   |
| Closed Date   | date time  |
| Resolved Date   | date time  |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method   | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Configuration Manager DCM Compliant CI Class published data

Class Type: Hidden

| Element Name   | Field Type |
|--------------------|------------|
| Description   | string   |
| Unique ID   | string   |
| SDM Package Digest | string   |
| Is Baseline   | boolean   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Domain User or Group Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Domain   | string   |
| User Name   | string   |
| First Name   | string   |
| Initials   | string   |
| Last Name   | string   |
| Company   | string   |
| Department   | string   |
| Office   | string   |
| Title   | string   |
| Employee Identifier | string   |
| Street Address   | string   |
| City   | string   |
| State   | string   |
| Zip   | string   |
| Country   | string   |
| Business Phone   | string   |
| Business Phone2   | string   |
| Home Phone   | string   |
| Home Phone2   | string   |
| Fax   | string   |
| Mobile   | string   |
| Pager   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Trouble Ticket Action Log Class published data

Class Type: Hidden

| Element Name | Field Type |
|--------------|------------|
| Action Type  | enum   |
| Title   | string   |
| Description  | string   |
| Entered By   | string   |
| Entered Date | date time  |
| ID   | string   |
| Display Name | string   |

## End-user Portal Contact IT Settings Class published data

Class Type: Hidden

| Element Name   | Field Type |
|----------------------|------------|
| E-mail address   | string   |
| E-mail response time | string   |
| Support phone   | string   |
| Fax number   | string   |
| Chat URL   | string   |
| Chat URL name   | string   |
| Chat response time   | string   |
| Display Name   | string   |

## Desired Configuration Management Incident Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Site Identifier   | string   |
| CI ID   | string   |
| Baseline Identifier   | string   |
| Computer Name   | string   |
| Compliance Status Details   | string   |
| Last Compliance Scan Time   | date time  |
| Max Noncompliance Criticality | int32   |
| Resolve By   | date time  |
| Escalated   | boolean   |
| Source   | enum   |
| Status   | enum   |
| Resolution Description   | string   |
| Needs Knowledge Article   | boolean   |
| Support Group   | enum   |
| Has Created Knowledge Article | boolean   |
| Last Modified Source   | enum   |
| Classification Category   | enum   |
| Resolution Category   | enum   |
| Priority   | int32   |
| Impact   | enum   |
| Urgency   | enum   |
| Closed Date   | date time  |
| Resolved Date   | date time  |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method   | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Site Management Server Class published data

Class Type: Hidden

| Element Name   | Field Type |
|----------------------------------------|------------|
| Site ID   | string   |
| Site Name   | string   |
| Management Server SCP   | string   |
| Auto Approve Manually Installed Agents | boolean   |
| Number of Missing Heartbeats Allowed   | int32   |
| Proxy Address   | string   |
| Proxy Port   | int32   |
| Reject Manually Installed Agents   | boolean   |
| Use Proxy Server   | boolean   |
| Authentication Name   | string   |
| Maximum Queue Size   | int32   |
| Maximum Size Of All Transferred Files  | int32   |
| Request Compression   | boolean   |
| Create Listener   | boolean   |
| Port   | int32   |
| Is Root Management Service   | boolean   |
| Is Management Server   | boolean   |
| Is Agent   | boolean   |
| Is Gateway   | boolean   |
| Is Manually Installed   | boolean   |
| Installed By   | string   |
| Install Time   | date time  |
| Version   | string   |
| Action Account Identity   | string   |
| Send Heartbeats to Management Servers  | boolean   |
| Heartbeat Interval (seconds)   | int32   |
| Managed Through Active Directory   | boolean   |
| Proxying Enabled   | boolean   |
| Patch List   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Processor (Concrete) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|--------------------|------------|
| Manufacturer   | string   |
| Speed   | int32   |
| Data Width   | int32   |
| Revision   | int32   |
| Version   | string   |
| Perfmon Instance   | string   |
| Family   | string   |
| Max Clock Speed   | string   |
| Type   | string   |
| Brand Identifier   | string   |
| Processor Cache   | string   |
| CPU Key   | string   |
| Is Mobile   | boolean   |
| Is Multicore   | boolean   |
| Device Identifier  | string   |
| Device Name   | string   |
| Device Description | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Active Directory Printer Class published data

Class Type: Hidden

| Element Name   | Field Type |
|--------------------------------|------------|
| UNC Name   | string   |
| Server Name   | string   |
| Short Server Name   | string   |
| Printer Name   | string   |
| Print Network Address   | string   |
| Print Share Name   | string   |
| Is Deleted   | boolean   |
| Driver Name   | string   |
| Driver Version   | string   |
| Print Memory   | string   |
| Print Collate   | string   |
| Print Owner   | string   |
| Asset Number   | string   |
| Managed By   | string   |
| Print Duplex Supported   | string   |
| Print Color   | string   |
| Print Stapling Supported   | string   |
| Version Number   | string   |
| URL   | string   |
| Print Media Supported   | string   |
| Print Rate Unit   | string   |
| Print Max XExtent   | int32   |
| Print Keep Printed Jobs   | string   |
| Print Rate   | int32   |
| Print Media Ready   | string   |
| Print Pages Per Minute   | int32   |
| Print Max Resolution Supported | int32   |
| Print Bin Names   | string   |
| Print MAC Address   | string   |
| Port Name   | string   |
| Physical Location Object   | string   |
| Keywords   | string   |
| Print Notify   | string   |
| Web Page   | string   |
| When Changed   | date time  |
| Modify Time Stamp   | date time  |
| Location   | string   |
| Canonical Name   | string   |
| Full Name   | string   |
| Distinguished Name   | string   |
| Description   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Microsoft Software Update Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Article Identifier  | string   |
| Bulletin Identifier | string   |
| Parent   | string   |
| Parent Version   | string   |
| Support String   | string   |
| Classification   | string   |
| Vendor   | string   |
| Title   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Incident Class published data

Class Type: Visible

| Element Name   | Field Type |
|---------------------|------------|
| Resolve By   | date time  |
| Escalated   | boolean   |
| Source   | enum   |
| Status   | enum   |
| Resolution Description   | string   |
| Needs Knowledge Article   | boolean   |
| Support Group   | enum   |
| Has Created Knowledge Article | boolean   |
| Last Modified Source   | enum   |
| Classification Category   | enum   |
| Resolution Category   | enum   |
| Priority   | int32   |
| Impact   | enum   |
| Urgency   | enum   |
| Closed Date   | date time  |
| Resolved Date   | date time  |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method   | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Billable Time Class published data

Class Type: Hidden

| Element Name   | Field Type |
|-----------------|------------|
| Time In Minutes | int32   |
| Last Updated   | date time  |
| ID   | string   |
| Display Name   | string   |

## Review Activity Class published data

Class Type: Visible

| Element Name   | Field Type |
|--------------------------------------------|------------|
| Approval Condition   | enum   |
| Approval Percentage   | int32   |
| Comments   | string   |
| Line Manager Should Review   | boolean   |
| Owners Of Configuration Item Should Review | boolean   |
| Sequence ID   | int32   |
| Notes   | string   |
| Status   | enum   |
| Priority   | enum   |
| Area   | enum   |
| Stage   | enum   |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method   | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Management Service Watcher (Collection Management Server) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|-------------------------|------------|
| Management Service ID   | string   |
| Management Service Name | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Computer (Deployed) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|----------------------|------------|
| Hardware Identifier  | string   |
| SMBIOS UUID   | string   |
| MAC Addresses   | string   |
| System Type   | string   |
| Chassis Type   | string   |
| Serial Number   | string   |
| ISA   | string   |
| Platform Type   | string   |
| SMBIOS Asset Tag   | string   |
| Model   | string   |
| Manufacturer   | string   |
| Number Of Processors | int32   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Windows Client Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------------------------|------------|
| Principal Name   | string   |
| DNS Name   | string   |
| NetBIOS Computer Name   | string   |
| NetBIOS Domain Name   | string   |
| IP Address   | string   |
| Network Name   | string   |
| Active Directory SID   | string   |
| Virtual Machine   | boolean   |
| DNS Domain Name   | string   |
| Organizational Unit   | string   |
| DNS Forest Name   | string   |
| Active Directory Site   | string   |
| Logical Processors   | int32   |
| Offset In Minutes From Greenwich Time | int32   |
| Last Inventory Date   | date time  |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Network Adapter (Concrete) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|--------------------|------------|
| Adapter Type   | string   |
| Index   | int32   |
| Manufacturer   | string   |
| MAC Address   | string   |
| Service Name   | string   |
| Perfmon Instance   | string   |
| DHCP Enabled   | string   |
| DHCP Server   | string   |
| DNS Domain   | string   |
| IP Address   | string   |
| IP Subnet   | string   |
| Bandwidth   | int32   |
| Max Speed   | int32   |
| Product Name   | string   |
| Default IP Gateway | string   |
| DHCP Hostname   | string   |
| IP Enabled   | boolean   |
| Device Identifier  | string   |
| Device Name   | string   |
| Device Description | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Inbound Email Rule Class published data

Class Type: Hidden

| Element Name | Field Type |
|--------------|------------|
| IsEnabled   | boolean   |
| SMTPDomain   | string   |
| Service   | string   |
| Display Name | string   |

## Localization Class published data

Class Type: Hidden

| Element Name | Field Type |
|--------------|------------|
| ID   | string   |
| Time zone   | string   |
| Locale ID   | int32   |
| Display Name | string   |

## Management Service Watcher Group (Collection Management Server) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------------------------|------------|
| Watcher Group Name   | string   |
| Root Management Server Principal Name | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Management Service Watcher Group (Gateway Management Server) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------------------------|------------|
| Watcher Group Name   | string   |
| Root Management Server Principal Name | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Text Message Notification Log for Trouble Tickets Class published data

Class Type: Hidden

| Element Name | Field Type |
|--------------|------------|
| Message   | string   |
| Encoding   | string   |
| Sent To   | string   |
| Sent Date   | date time  |
| ID   | string   |
| Display Name | string   |

## Portal Software Deployment Activity Class published data

Class Type: Hidden

| Element Name   | Field Type |
|--------------------------|------------|
| Package ID   | string   |
| Machine Name   | string   |
| Error Message   | string   |
| Status   | enum   |
| Sequence ID   | int32   |
| Notes   | string   |
| Status   | enum   |
| Priority   | enum   |
| Area   | enum   |
| Stage   | enum   |
| ID   | string   |
| Title,   | string   |
| Description   | string   |
| Alternate Contact Method | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Logical Disk (Concrete) Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------------------|------------|
| File System   | string   |
| Compressed   | string   |
| Size (MB)   | int32   |
| Free Space   | int32   |
| Drive Type   | int32   |
| Supports Disk Quota   | string   |
| Quotas Disabled   | string   |
| Supports File Based Compression | string   |
| Volume Name   | string   |
| Device Identifier   | string   |
| Device Name   | string   |
| Device Description   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |
| SC\_L3\_String   | string   |
| SC\_L3\_date time   | date time  |
| SC\_L3\_Enum   | enum   |
| EX\_L4\_String   | string   |
| EX\_L4\_date time   | date time  |
| EX\_L4\_Enum   | enum   |
| SC\_L2\_String   | string   |
| SC\_L2\_date time   | date time  |
| SC\_L2\_Enum   | enum   |
| SC\_L1\_String   | string   |
| SC\_L1\_date time   | date time  |
| SC\_L1\_Enum   | enum   |
| Resolve By   | date time  |
| Escalated   | boolean   |
| Source   | enum   |
| Status   | enum   |
| Resolution Description   | string   |
| Needs Knowledge Article   | boolean   |
| Support Group   | enum   |
| Has Created Knowledge Article   | boolean   |
| Last Modified Source   | enum   |
| Classification Category   | enum   |
| Resolution Category   | enum   |
| Priority   | int32   |
| Impact   | enum   |
| Urgency   | enum   |
| Closed Date   | date time  |
| Resolved Date   | date time  |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method   | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Operations Manager Connector Synchronization Class published data

Class Type: Hidden

| Element Name  | Field Type |
|---------------|------------|
| Data   | string   |
| SyncMetadata  | string   |
| Object Status | enum   |
| Asset Status  | enum   |
| Notes   | string   |
| Display Name  | string   |

## System Center Managed Windows Computer Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------------------------|------------|
| Install Directory   | string   |
| Principal Name   | string   |
| DNS Name   | string   |
| NetBIOS Computer Name   | string   |
| NetBIOS Domain Name   | string   |
| IP Address   | string   |
| Network Name   | string   |
| Active Directory SID   | string   |
| Virtual Machine   | boolean   |
| DNS Domain Name   | string   |
| Organizational Unit   | string   |
| DNS Forest Name   | string   |
| Active Directory Site   | string   |
| Logical Processors   | int32   |
| Offset In Minutes From Greenwich Time | int32   |
| Last Inventory Date   | date time  |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## System Center Operations Manager Connector Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------------|------------|
| SolutionName   | string   |
| DataProviderName   | string   |
| DataProviderDisplayName   | string   |
| ReaderProfileName   | string   |
| DatawarehouseProfileName  | string   |
| Reserved   | string   |
| ImpersonationEnabled   | boolean   |
| SyncType   | enum   |
| SyncInterval   | int32   |
| SyncTime   | date time  |
| SyncNow   | boolean   |
| Enabled   | boolean   |
| Connector ID   | string   |
| Connector Name   | string   |
| Connector Description   | string   |
| Is Discovery Data Managed | boolean   |
| Is Discovery Data Shared  | boolean   |
| Display Name   | string   |

## Disk Partition Class published data

Class Type: Hidden

| Element Name   | Field Type |
|--------------------|------------|
| Disk Index   | int32   |
| Block Size   | int32   |
| Primary Partition  | string   |
| Bootable   | string   |
| Size (MB)   | int32   |
| Type   | string   |
| Device Identifier  | string   |
| Device Name   | string   |
| Device Description | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Windows Domain Controller Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------------------------|------------|
| Is Virtual Node   | boolean   |
| Principal Name   | string   |
| DNS Name   | string   |
| NetBIOS Computer Name   | string   |
| NetBIOS Domain Name   | string   |
| IP Address   | string   |
| Network Name   | string   |
| Active Directory SID   | string   |
| Virtual Machine   | boolean   |
| DNS Domain Name   | string   |
| Organizational Unit   | string   |
| DNS Forest Name   | string   |
| Active Directory Site   | string   |
| Logical Processors   | int32   |
| Offset In Minutes From Greenwich Time | int32   |
| Last Inventory Date   | date time  |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Package Class published data

Class Type: Hidden

| Element Name  | Field Type |
|---------------|------------|
| Package ID   | string   |
| Name   | string   |
| Version   | string   |
| Language   | string   |
| Manufacturer  | string   |
| Description   | string   |
| Source Site   | string   |
| Publish   | boolean   |
| Object Status | enum   |
| Asset Status  | enum   |
| Notes   | string   |
| Display Name  | string   |

## Reviewer Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Reviewer Identifier | string   |
| Decision   | enum   |
| Decision Date   | date time  |
| Comments   | string   |
| Veto   | boolean   |
| Must Vote   | boolean   |
| Display Name   | string   |

## Business Service Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Service ID   | string   |
| Service Description   | string   |
| Business Detailed Description | string   |
| Is Business Service   | boolean   |
| Owned By Organization   | string   |
| Priority   | enum   |
| Status   | enum   |
| Classification   | enum   |
| Availability Schedule   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Announcement Class published data

Class Type: Hidden

| Element Name   | Field Type |
|-----------------|------------|
| ID   | string   |
| Title   | string   |
| Body   | string   |
| Expiration Date | date time  |
| Priority   | enum   |
| Display Name   | string   |

## Knowledge Article Class published data

Class Type: Visible

| Element Name   | Field Type |
|----------------------------|------------|
| Knowledge Article Type   | enum   |
| Knowledge Article Template | string   |
| Knowledge Article Owner   | string   |
| Category   | enum   |
| Comments   | string   |
| Created On   | date time  |
| Created By   | string   |
| Primary Locale ID   | string   |
| Status   | enum   |
| Tag   | enum   |
| Vendor Article Identifier  | string   |
| Title   | string   |
| Abstract   | string   |
| Keywords   | string   |
| Knowledge Article ID   | string   |
| End User Content   | string   |
| Analyst Content   | string   |
| External URL Source   | string   |
| External URL   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## System Center Operations Manager Enterprise License Class published data

Class Type: Hidden

| Element Name  | Field Type |
|---------------|------------|
| Object Status | enum   |
| Asset Status  | enum   |
| Notes   | string   |
| Display Name  | string   |

## Trouble Ticket User Comments Class published data

Class Type: Hidden

| Element Name | Field Type |
|--------------|------------|
| Comment   | string   |
| Entered By   | string   |
| Entered Date | date time  |
| ID   | string   |
| Display Name | string   |

## Software Deployment Process Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------------|------------|
| ProcessId   | string   |
| ChangeRequestTemplateId   | string   |
| ChangeRequestTemplateName | string   |
| Description   | string   |
| Display Name   | string   |

## Problem Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Status   | enum   |
| Source   | enum   |
| Classification   | enum   |
| Known Error   | boolean   |
| Error Description   | string   |
| Workarounds   | string   |
| Requires Major Problem Review | boolean   |
| Review Notes   | string   |
| Auto Resolve Incidents   | boolean   |
| Resolution   | enum   |
| Resolution Description   | string   |
| Priority   | int32   |
| Impact   | enum   |
| Urgency   | enum   |
| Closed Date   | date time  |
| Resolved Date   | date time  |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method   | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Software Updates Class published data

Class Type: Hidden

| Element Name  | Field Type |
|---------------|------------|
| Vendor   | string   |
| Title   | string   |
| Object Status | enum   |
| Asset Status  | enum   |
| Notes   | string   |
| Display Name  | string   |

## Management Service Watcher (Site Management Server) Class published data

Class Type:

| Element Name   | Field Type |
|-------------------------|------------|
| Management Service ID   | string   |
| Management Service Name | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Site Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Site Name   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |
| CustomerStringField   | string   |
| CustomerEnumField   | enum   |
| Resolve By   | date time  |
| Escalated   | boolean   |
| Source   | enum   |
| Status   | enum   |
| Resolution Description   | string   |
| Needs Knowledge Article   | boolean   |
| Support Group   | enum   |
| Has Created Knowledge Article | boolean   |
| Last Modified Source   | enum   |
| Classification Category   | enum   |
| Resolution Category   | enum   |
| Priority   | int32   |
| Impact   | enum   |
| Urgency   | enum   |
| Closed Date   | date time  |
| Resolved Date   | date time  |
| ID   | string   |
| Title   | string   |
| Description   | string   |
| Alternate Contact Method   | string   |
| Created Date   | date time  |
| Scheduled Start Date   | date time  |
| Scheduled End Date   | date time  |
| Actual Start Date   | date time  |
| Actual End Date   | date time  |
| Display Name   | string   |

## Trouble Ticket Audit Log Class published data

Class Type: Hidden

| Element Name | Field Type |
|--------------|------------|
| Comment   | string   |
| Entered By   | string   |
| Entered Date | date time  |
| ID   | string   |
| Display Name | string   |

## Configuration Manager DCM Noncompliant CI Class published data

Class Type: Hidden

| Element Name   | Field Type |
|---------------------|------------|
| Max Noncompliance Criticality | int32   |
| Baseline Unique ID   | string   |
| CI Unique ID   | string   |
| Computer Name   | string   |
| Compliance Status Details   | string   |
| Last Compliance Scan Time   | date time  |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |

## Windows Client Operating System Class published data

| Element Name   | Field Type |
|---------------------------------------|------------|
| Operating System Version   | string   |
| Operating System Version Display Name | string   |
| Product Type   | string   |
| Build Number   | string   |
| CSD Version   | string   |
| Service Pack Version   | string   |
| Serial Number   | string   |
| Install Date   | string   |
| System Drive   | string   |
| Windows Directory   | string   |
| Physical Memory (MB)   | int32   |
| Logical Processors   | int32   |
| Country Code   | string   |
| Locale   | string   |
| Description   | string   |
| Manufacturer   | string   |
| OS Language   | string   |
| Minor Version   | string   |
| Major Version   | string   |
| Object Status   | enum   |
| Asset Status   | enum   |
| Notes   | string   |
| Display Name   | string   |
