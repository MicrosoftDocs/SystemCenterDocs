---
ms.assetid: accc6f3d-396c-43bc-91a6-7e723d57bfa1
title: Security Considerations for Microsoft Azure and Microsoft 365
description: This article provides design guidance on how to authenticate and securely monitor Microsoft Azure and Microsoft 365 with Operations Manager 2016.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Security Considerations for Microsoft Azure and Microsoft 365

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

## Integration with Azure

The Azure monitoring pack runs on a specified agent and uses various Windows Azure APIs to remotely discover and collect instrumentation information about a specified Windows Azure application. Secure communication and authentication with Azure is performed by certificate authentication, which is required in order to successfully monitor workloads hosted in Azure with Operations Manager.  

If you don’t have a management certificate already, begin here by reviewing [Certificates overview for Azure Cloud Services](/previous-versions/azure/gg551722(v=azure.100)).

For more information on the Windows Azure team blog, see [Introducing the Windows Azure Service Management API](https://azure.microsoft.com/blog/introducing-the-windows-azure-service-management-api/).

The Monitoring Pack for Windows Azure Applications creates three Run As profiles:

- Windows Azure Run As Profile Blob
- Windows Azure Run As Profile Password
- Windows Azure Run As Profile Proxy

You must create Run As accounts for Windows Azure Run As Profile Blob and Windows Azure Run As Profile Password. The account for Windows Azure Run As Profile Blob stores the certificate with the private key for the Windows Azure application. The account for Windows Azure Run As Profile Password stores the password for the private key.

Creating an account for Windows Azure Run As Profile Proxy is optional. The account for Windows Azure Run As Profile Proxy stores credentials for access to the HTTP proxy server that is used to make API calls to Windows Azure.

You must associate the Run As Account with an appropriate Run As profile. The Add Monitoring Wizard will associate the Windows Azure Run As Profile Blob and Windows Azure Run As Profile Password profiles with the accounts that you specify. If you create a Run As account for Windows Azure Run As Profile Proxy, you must manually associate the Windows Azure Run As Profile Proxy profile with the account that you create.

## Integration with Microsoft 365

Microsoft 365 management pack uses the agentless monitoring approach. All monitoring workflows that communicate with Microsoft 365 Monitoring API are being executed on management servers only. A user account with Global Administrator permissions for the subscription is required for monitoring of a Microsoft 365 subscription. It's highly recommended to add a new dedicated user account to each subscription you want to monitor.
To create a new user with Global Administrator permissions using Microsoft 365 admin center:
1. Go to https://portal.office.com/Adminportal/ to open the admin center. Sign in as Subscription Global Administrator.
2. On Users and Groups tab: select Add button
3. Enter First name, Last name, Display name, and User name and select a domain linked to the subscription.
Note that First and Last names are required for account with Global Administrator role.<br>![Screenshot of the New User Details page.](./media/plan-security-microsoft-cloud/om2016-o365-new-user-details.png)  
4. On setting tab, select Global administrator role to be assigned to account. Specify alternate email address and user location.<br>![Screenshot of the New User Settings page.](./media/plan-security-microsoft-cloud/om2016-o365-new-user-settings.png)  
5. You aren't required to assign Microsoft 365 services licenses to the monitoring account.
6. Specify an email address to receive a temporary password. Sign out from Microsoft 365 admin center, and sign in again using the new credentials received in the email.
7. Sign in to the Microsoft 365 management portal using the newly created credentials and set the password for the account. Remember to use a strong complex password because this account has Global administrator permissions.
   > [!NOTE]
   > Management Pack workflows are unable to obtain monitoring data, Connection State monitor sets Subscription health to “Critical” state and generates “(401) Unauthorized” Alert until new Global Administrator account is used to sign in to the Microsoft 365 management portal at least once.

### Configure Run As profiles

The Microsoft 365 management pack creates two Run As Profiles:

- Microsoft 365 Subscription Password secure reference

    Microsoft 365 Subscription Password secure reference Run As Profile is used to store subscription credentials and shouldn’t be edited manually

- Microsoft 365 Subscription Proxy secure reference

    Microsoft 365 Subscription Proxy secure reference Run As Profile should be configured manually. This profile is used by all rules and monitors defined in this Management Pack. All Run As Accounts mapped to this profile should have the following permissions:
     - Be a member of “Operations Manager Operators” System Center Operations Manager user role.
     - Be able to establish an HTTPS connection from the Management Server to the Microsoft 365 portal endpoint. Check firewall and proxy settings within your environment to ensure that the aforementioned connection is allowed.
