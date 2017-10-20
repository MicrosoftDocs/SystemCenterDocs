---
title: Update Remote Mailbox (Hybrid)
description: You can use the Update Remote Mailbox activity to modify the mail-related attributes of an existing user in Active Directory that is associated with a mailbox in the cloud-based service (hybrid environment).
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4931d67c-86a8-44f6-ac6d-8c4e72fd3a21
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Update Remote Mailbox (Hybrid)

Applies To: System Center 2016 - Orchestrator

You can use the Update Remote Mailbox activity to modify the mail-related attributes of an existing user in Active Directory that is associated with a mailbox in the cloud-based service (hybrid environment).

The following tables list the required properties, optional properties, and published data for this activity.

## Required properties for Update Remote Mailbox (Hybrid)

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Identity   | Specifies the mail-enabled user. You can use one of the following value types:<br>ADObjectID <br>GUID <br>Distinguished name (DN)<br>Domain\\SamAccountName<br>User principal name (UPN)<br>Legacy DN<br>E-mail address<br>User alias | String   |

## Optional properties for Update Remote Mailbox (Hybrid)

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Accept Messages Only From   | Specifies a list of mailbox users and mail-enabled users that can send email messages to a mail-enabled user. You can also specify Exchange as a valid recipient for this property. If you configure a mail-enabled user to accept messages only from the Exchange recipient, the mail-enabled user only receives system-generated messages.<br>The specified list of mailbox users be one of the following types:<br>DN<br>Canonical name <br>GUID<br>Name<br>Display name<br>Alias<br>Exchange DN<br>Primary SMTP email address<br>By default, this property is blank, which enables the mail-enabled user to accept messages from all senders.   | String   |
| Accept Messages Only From DL Members   | Specifies a list of distribution groups whose members are allowed to send e-mail messages to this mail-enabled user. The specified distribution groups can be one of the following types:<br>DN<br>Canonical name<br>GUID<br>Name<br>Display name<br>LegacyExchangeDN<br>Primary SMTP email address<br>By default, this property is blank, which enables the mail-enabled user to accept messages from all senders.   | String   |
| Accept Messages Only From Senders Or Members | Specifies a list of recipients who are allowed to send email messages to this mail-enabled user. The specified list of recipients can be one of the following types:<br>Alias<br>Canonical name<br>Display name<br>DN<br>GUID<br>Name<br>LegacyExchangeDN<br>Primary SMTP e-mail address<br>By default, this property is blank, which enables the mail-enabled user to accept messages from all senders.   | String   |
| Alias   | Specifies the alias (mail nickname) of the mail-enabled user. The alias can be a combination of characters separated by a period with no intervening spaces. Do not use special characters in the alias.   | String   |
| Archive Name   | Specifies the name of the archive mailbox. Use this property to change the name of the archive.   | String   |
| Bypass Moderation From Senders Or Members   | Specifies a list of recipients whose messages bypass moderation when are sent to this mail-enabled user. Can be one of the following types: <br>Alias<br>Canonical name<br>Display name<br>DN<br>GUID<br>Name<br>LegacyExchangeDN<br>Primary SMTP email address<br>This value makes sure that all messages are moderated when this mail-enabled user is configured for moderation. Senders that are designated as moderators for this mail-enabled user are never moderated.   | String   |
| Custom Attribute 1   | Custom attributes to store additional information.   | String   |
| Custom Attribute 10   | Custom attributes to store additional information.   | String   |
| Custom Attribute 11   | Custom attributes to store additional information.   | String   |
| Custom Attribute 12   | Custom attributes to store additional information.   | String   |
| Custom Attribute 13   | Custom attributes to store additional information.   | String   |
| Custom Attribute 14   | Custom attributes to store additional information.   | String   |
| Custom Attribute 15   | Custom attributes to store additional information.   | String   |
| Custom Attribute 2   | Custom attributes to store additional information.   | String   |
| Custom Attribute 3   | Custom attributes to store additional information.   | String   |
| Custom Attribute 4   | Custom attributes to store additional information.   | String   |
| Custom Attribute 5   | Custom attributes to store additional information.   | String   |
| Custom Attribute 6   | Custom attributes to store additional information.   | String   |
| Custom Attribute 7   | Custom attributes to store additional information.   | String   |
| Custom Attribute 8   | Custom attributes to store additional information.   | String   |
| Custom Attribute 9   | Custom attributes to store additional information.   | String   |
| Display Name   | Specifies the display name for the user account associated with this mail-enabled user.   | String   |
| Domain Controller   | Specifies the fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory.   | String   |
| Email Address Policy Enabled   | Specifies whether the email addresses for the mail-enabled user are automatically updated based on the email address policies defined. When set to value True, the Primary SMTP Address or Windows Email Address properties cannot be changed. Default value is True, when selected.   | True, False   |
| Email Addresses   | Specifies the email alias of the mail-enabled user. All valid Exchange email address types may be used. You can specify multiple values as a comma-delimited list.<br>Exchange does not validate custom addresses for proper formatting. You must ensure that the custom address that you specify complies with the format requirements for that address type. Because X.400 addresses are considered custom addresses in Exchange, they are also not validated, and you must provide the correct syntax when you specify an X.400 address.   | String   |
| Extension Custom Attribute 1   | The 1 through 5 properties for Extension Custom Attribute specify the custom attributes that store additional information. You can specify multiple values for these parameters as a comma delimited list. Each Extension Custom Attribute property can hold up to 1,300 values.   | String   |
| Extension Custom Attribute 2   | The 1 through 5 properties for Extension Custom Attribute specify the custom attributes that store additional information. You can specify multiple values for these parameters as a comma delimited list. Each Extension Custom Attribute property can hold up to 1,300 values.   | String   |
| Extension Custom Attribute 3   | The 1 through 5 properties for Extension Custom Attribute specify the custom attributes that store additional information. You can specify multiple values for these parameters as a comma delimited list. Each Extension Custom Attribute property can hold up to 1,300 values.   | String   |
| Extension Custom Attribute 4   | The 1 through 5 properties for Extension Custom Attribute specify the custom attributes that store additional information. You can specify multiple values for these parameters as a comma delimited list. Each Extension Custom Attribute property can hold up to 1,300 values.   | String   |
| Extension Custom Attribute 5   | The 1 through 5 properties for Extension Custom Attribute specify the custom attributes that store additional information. You can specify multiple values for these parameters as a comma delimited list. Each Extension Custom Attribute property can hold up to 1,300 values.   | String   |
| Grant Send On Behalf To   | Specifies the DN of recipients that can send messages on behalf of this mail-enabled user   | String   |
| Hidden From Address Lists Enabled   | Specifies whether the mail-enabled user appears in the address list. Default value is True, when selected.   | True, False   |
| Ignore Default Scope   | Instructs the command to ignore the default recipient scope setting for the Exchange Management Shell session, and use the entire forest as the scope. This allows the command to access the Active Directory objects that aren't currently in the default scope. Using this property introduces the following restrictions:<br>You can't use the Domain Controller property. The command uses an appropriate global catalog server automatically.<br>You can only use the DN for the Identity property. Other forms of identification, such as alias or GUID, aren't accepted.<br>Default value is True, when selected.   | True, False   |
| Immutable ID   | Used by Outlook Live Directory Sync (OLSync) and specifies a unique and immutable identifier in the form of an SMTP address for an Exchange mailbox that's used for federated delegation when requesting Security Assertion Markup Language (SAML) tokens. If federation is configured for this mail-enabled user and you do not set this property when you create the mailbox, Exchange creates the value for the immutable identifier based upon the mailbox's ExchangeGUID and the federated account namespace; for example, 7a78e7c8-620e-4d85-99d3-c90d90f29699@mail.contoso.com. You must set the Immutable ID property if Active Directory Federation Services (AD FS) is deployed to allow single sign-on into off-premises mailboxes, and AD FS is configured to use a different attribute than ExchangeGUID for sign-on token requests. Both, Exchange and AD FS must request the same token for the same user, to ensure proper functionality for cross-premise Exchange organizations. | String   |
| Mail Tip Translations   | Specifies additional languages when you want to provide the MailTip property information for this recipient in multiple languages. For each language, you must provide the locale, followed by a colon, and the specific MailTip property message in that language. Each MailTip property message must be less than or equal to 250 characters. Multiple languages can be separated by commas.   | String   |
| Moderated By   | Specifies the users that are responsible for moderating the messages that are sent to the mail-enabled user. To designate more than one user, separate the users with commas.<br>This property is required when the Moderation Enabled property to set to value True. If the value is not specified and there's a user already specified as the manager of this mail-enabled user, the Moderated By property is automatically set by the Managed By property of the distribution group. Otherwise, an error is returned.   | String   |
| Moderation Enabled   | Specifies whether to enable Moderation for the mail-enabled user. To enable the moderation property, set this property to True. To disable moderation, set this property to False.<br>Default value is True, when selected.   | True, False   |
| Name   | Specifies the name of the mail-enabled user.   | String   |
| Primary SMTP Address   | Specifies the primary SMTP address.   | String   |
| Reject Messages From   | Specifies a list of recipients from whom to reject messages. Can be one of the following value types:<br>Alias<br>Canonical name<br>Display name<br>DN<br>GUID<br>Name<br>LegacyExchangeDN<br>Primary SMTP email address<br>By default, this property is blank, which enables the mail-enabled user to accept messages from all senders.   | String   |
| Reject Messages From DL Members   | Specifies a list of distribution list members from which to reject messages. Can be one of the following value types:<br>DN<br>Alias<br>Canonical name<br>Display name<br>GUID<br>Name<br>LegacyExchangeDN<br>Primary SMTP email address<br>By default, this property is blank, which enables the mail-enabled user to accept messages from all senders.   | String   |
| Reject Messages From Senders Or Members   | Specifies a list of recipients who aren't allowed to send email messages to this mail-enabled user. Can be one of the following value types:<br>Alias<br>Canonical name<br>Display name<br>DN<br>GUID<br>Name<br>LegacyExchangeDN<br>Primary SMTP email address<br>By default, this property is blank, which enables the mail-enabled user to accept messages from all senders.   | String   |
| Remote Routing Address   | Specifies the SMTP address of the mailbox in the service that's associated with this mail-enabled user.<br>If the address was automatically configured by Exchange when the mail-enabled user and its associated mailbox were created, you shouldn't have to change the remote routing address..   | String   |
| Remove Picture   | Specifies whether to remove the picture that a user has added to a mailbox.<br>Default value is True, when selected.   | True, False   |
| Remove Spoken Name   | Specifies whether to remove the spoken name that a user has added to a mailbox. <br>Default value is True, when selected.   | True, False   |
| Require Sender Authentication Enabled   | Specifies whether to accept messages only from authenticated recipients. <br>Default value is True, when selected.   | True, False   |
| Reset Password On Next Logon   | Specifies whether to require the mail-enabled users to change their password the next time they sign in to the cloud-based service. When set to True, the mail-enabled users are required to change their password the next time they sign in to the cloud-based service.<br>Default value is True, when selected.   | True, False   |
| SAM Account Name   | Specifies the logon name that is used to support clients and servers that are running older versions of the operating system, such as Microsoft Windows NT 4.0, Windows 98, Windows 95, and LAN Manager. This attribute must contain less than 20 characters. An account name can contain letters, numbers, and the following punctuation marks and symbols: <br>! \# $ % ^ & - . \_ { } | ~   | String   |
| Send Moderation Notifications   | Specifies whether status notifications are sent to users when they send a message to the moderated mail-enabled user. <br>If you want notifications to be sent to all senders, set this property to Always.<br>If you want notifications to be sent only to the senders who are internal to your organization, set this property to Internal.<br>To disable all status notifications, set this property to Never.<br>The sender is always notified if the message is rejected by the moderators, regardless of the value of this property. <br>Default value is Never.   | Always<br>Internal <br>Never   |
| Single Item Recovery Enabled   | Specifies whether to prevent the Recovery Items folder from being purged. When set to True, it prevents the Recovery Items folder from being purged. It also prevents any items from being removed that have been deleted or edited.<br>Default value is True, when selected.   | True, False   |
| Type   | Specifies the type for the mailbox in the service.   | Regular<br>Room <br>Equipment<br>Shared |
| User Principal Name   | Specifies a user principal name (UPN) for the user.   | String   |
| Windows Email Address   | Specifies the Windows email address for this mail-enabled user. This address isn't used by Exchange.   | String   |

## Published data for Update Remote Mailbox (Hybrid)

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed.   | String   |
| Exchange PowerShell Application | Specifies the application name segment of the connection URI.   | String   |
| Exchange Server Host   | The connected Exchange Server.   | String   |
| Exchange Server Port   | The connected Exchange Server port.   | String   |
| Exchange User Name   | Username used to connect to Exchange Server.   | String   |
| Identity   | Identity of the mailbox or mail user.   | String   |
| Skip CA Check   | Indicates whether the client validates that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol, over Secure Socket Layer. | String   |
| Skip CN Check   | Indicates whether the client validates that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection does not validate the revocation status of the server certificate.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |

## Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
