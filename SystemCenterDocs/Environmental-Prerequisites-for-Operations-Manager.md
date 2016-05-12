---
title: Environmental Prerequisites for Operations Manager
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39f027a6-039e-460c-86df-0a5cc17360f9
---
# Environmental Prerequisites for Operations Manager
This section covers the infrastructure that you need to have in place and other factors to consider before you run the Setup for [!INCLUDE[om12long](Token/om12long_md.md)] or [!INCLUDE[sc2012sp1_long](Token/sc2012sp1_long_md.md)], [!INCLUDE[om12short](Token/om12short_md.md)].

There are two sets of prerequisites that must be satisfied prior to installing any of the [!INCLUDE[om12short](Token/om12short_md.md)] features. One set consists of those items that the Prerequisite checker identifies during Setup. The Prerequisite checker is targeted at the server that Setup is running on and determines if the server has the necessary configuration to host whatever role you have chosen.

The other set consists of those items that are outside the scope of the Prerequisite checker, such as the Active Directory domain or forest functional level, or the availability of a certification authority \(CA\) to issue the certificates that are necessary for deploying agents and gateway servers across trust boundaries. This section addresses this second set of prerequisites, which are much broader in scope, because they apply to the whole environment that [!INCLUDE[om12short](Token/om12short_md.md)] will be functioning in, rather than those that are verified by the Prerequisite checker during Setup. To ensure that [!INCLUDE[om12short](Token/om12short_md.md)] deploys smoothly and functions as expected, the environment that it will run in must be properly prepared. Because environmental changes affect more than [!INCLUDE[om12short](Token/om12short_md.md)], ensure that you exercise due caution before making sweeping changes. The prerequisites are presented in a unified format with scenario\-specific items called out.

For more information about design and environmental decisions, see [Planning the Operations Manager for System Center 2012 Deployment](assetId:///d6edb9b4-5db8-40c2-be00-a32445732d50). For more information about supported configurations for [!INCLUDE[om12long](Token/om12long_md.md)], see [System Requirements for System Center 2012 – Operations Manager](http://go.microsoft.com/fwlink/p/?LinkID=219650).

## In This Section
[Supporting Infrastructure](assetId:///9c9c8c72-0fa5-46ff-8abe-67dca0b27ee5)
Describes prerequisites and issues that you need to be aware of before you install [!INCLUDE[om12long](Token/om12long_md.md)].

[Security Considerations](assetId:///9c0f4ce0-8cfc-4994-97e4-5e0e29c1b6c5)
Describes high\-level security factors that need to be addressed.

[Agent and Agentless Monitoring](assetId:///504958df-f853-49f2-b27a-795948234220)
Describes the environmental prerequisites for deploying agents to monitor devices and for deploying agentless monitoring.


