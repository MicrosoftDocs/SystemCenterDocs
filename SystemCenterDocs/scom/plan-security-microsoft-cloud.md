---
ms.assetid: accc6f3d-396c-43bc-91a6-7e723d57bfa1
title: Security Considerations for Microsoft Azure and Microsoft 365
description: This article provides design guidance on how to authenticate and securely monitor Microsoft Azure and Microsoft 365 with Operations Manager.
author: jyothisuri
ms.author: jsuri

ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Security Considerations for Microsoft Azure and Microsoft 365



## Integration with Azure

The Azure monitoring pack runs on a specified agent and uses various Windows Azure APIs to remotely discover and collect instrumentation information about a specified Windows Azure application. Secure communication and authentication with Azure is performed by certificate authentication, which is required in order to successfully monitor workloads hosted in Azure with Operations Manager.  

If you don’t have a management certificate already, begin here by reviewing [Certificates overview for Azure Cloud Services](/previous-versions/azure/gg551722(v=azure.100)).

The Monitoring Pack for Windows Azure Applications creates three Run As profiles:

- Windows Azure Run As Profile Blob
- Windows Azure Run As Profile Password
- Windows Azure Run As Profile Proxy

You must create Run As accounts for Windows Azure Run As Profile Blob and Windows Azure Run As Profile Password. The account for Windows Azure Run As Profile Blob stores the certificate with the private key for the Windows Azure application. The account for Windows Azure Run As Profile Password stores the password for the private key.

Creating an account for Windows Azure Run As Profile Proxy is optional. The account for Windows Azure Run As Profile Proxy stores credentials for access to the HTTP proxy server that is used to make API calls to Windows Azure.

You must associate the Run As Account with an appropriate Run As profile. The Add Monitoring Wizard will associate the Windows Azure Run As Profile Blob and Windows Azure Run As Profile Password profiles with the accounts that you specify. If you create a Run As account for Windows Azure Run As Profile Proxy, you must manually associate the Windows Azure Run As Profile Proxy profile with the account that you create.

## Integration with Microsoft 365

Microsoft 365 management pack uses the agentless monitoring approach. All monitoring workflows that communicate with Microsoft 365 Monitoring API are being executed on management servers only.

### Configure Run As profiles

The Microsoft 365 management pack creates two Run As Profiles:

- Microsoft 365 Subscription Password secure reference

    Microsoft 365 Subscription Password secure reference Run As Profile is used to store subscription credentials and shouldn’t be edited manually

- Microsoft 365 Subscription Proxy secure reference

    Microsoft 365 Subscription Proxy secure reference Run As Profile should be configured manually. This profile is used by all rules and monitors defined in this Management Pack. All Run As Accounts mapped to this profile should have the following permissions:
     - Be a member of “Operations Manager Operators” System Center Operations Manager user role.
     - Be able to establish an HTTPS connection from the Management Server to the Microsoft 365 portal endpoint. Check firewall and proxy settings within your environment to ensure that the aforementioned connection is allowed.
