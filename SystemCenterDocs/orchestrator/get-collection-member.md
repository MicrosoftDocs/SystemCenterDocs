---
title: Get Collection Member activity
description: Describes the configurable properties for the Get Collection Member activity for Configuration Manager Integration Pack.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: ee86105b-c786-4aee-b2ec-8cfcd88f8fc5
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Get Collection Member activity for Configuration Manager Integration Pack

Applies To: System Center 2016 - Orchestrator

The Get Collection Member activity is used in a runbook that queries an
existing Configuration Manager collection for its member computers. This
lets you specify computers individually to obtain status or perform
other activities.

This activity returns the properties associated with the
SMS\_FullCollectionMembership WMI class scoped to the collection
specified.

## Get Collection Member properties

- Collection Name: The display name or ID of an existing collection
    >[!NOTE]
    >When you use the browse feature to look up a collection name, or enter a collection name manually or from published data, you must set the **Collection Value Type** property to **Name** or the activity will fail.
- Collection Value Type   Specifies whether the value in the **Collection** property is a name or a collection ID. Options are:
    - **ID** (default): the value is a collection ID
    - **Name**: the value is a collection name

## Get Collection Member published data

The following values are published in addition to the input values
above:

| Name | Description |
|:---|:---|
| Connection | Specifies the name of the connection to the Configuration Manager server |
|  Collection ID | Provides the Collection ID value for the collection targeted for this activity (in case the collection name was specified for the input property). |
|  AMTFullVersion | Provides the Intel Active Management Technology (Intel AMT) firmware version of this computer. The format is: MAJOR.MINOR.MICRO |
|  AMTStatus | Status of the Intel AMT component of this computer. Possible values are:<br><br>NULL: Unknown<br>0: Computer is not supported<br>1: Computer is detected<br>2: Computer is not provisioned<br>3: Computer is provisioned |
|  ClientCertType | Type of certificate used by the client. Possible values are:<br><br>1.  Self-signed<br>2.  Issued by CA |
|  ClientType | Type of client. Possible values are:<br><br>1.  Client<br>2.  Device | 
|  ClientVersion | he version ID of the client |
|  Domain | Domain to which the resource belongs. |
| Is Always Internet | True or False. True if this is an Internet-facing client. |
| Is Approved | True or False. True if the client is approved. |
| Is Assigned | True or False. True if the client is assigned to any site. |
| Is Blocked | rue or False. True if the client is blocked. |
|  Is Client | True or False. True if this is a client. |
| Is Decommissioned | True or False. True if the record is deleted. |
| Is Direct | True or False. True if the client is a member through a direct rule, represented by SMS\_CollectionRuleDirect Server WMI Class; otherwise false or null. |
|  Is Internet Enabled | True or False. True if the client can be Internet-enabled. |
| Is Obsolete | True or False. True if this is an obsolete record. |
|  Is Virtual Machine | True or False. True if this is a virtual machine. |
| Member Name | Name of the resource. |
|  Member Resource Type | Type of resource. Possible values are:<br><br>System<br>User group<br>User |
| Resource ID  | Unique ID supplied by Configuration Manager for the resource. This ID is not unique across sites. |
| Site Code | Site code of the site that created the collection.
| SMSID | Configuration Manager unique ID |
|  Suppress Auto Provision | True or False. When set to true and when this resource belongs to a collection configured for automatic provisioning, prevents the resource from being automatically provisioned by an Out of Band service point. |

## Configuring the Get Collection Member activity

1.  From the **Activities** pane, drag a **Get Collection Member**
    activity to the active runbook.

2.  Double-click the **Get Collection Member** activity icon. The
    **Properties** dialog box opens.

3.  Configuring the **Details** tab:

    1.  In the **Connection** section, click the ellipsis button
        **(...)**, and then select the Configuration Manager server
        connection that you want to use for this activity. Click **OK**.

    2.  In the **Fields** section, enter a value for each of the
        required properties. If the property is Lookup-enabled, you can
        click the ellipsis **(â€¦)** button next to the text box to browse
        for a value.

        You can also use published data to automatically populate the
        value of the property from the data output by a previous
        activity in the runbook.

4.  Click **Finish**.
