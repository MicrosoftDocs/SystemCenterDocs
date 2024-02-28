---
ms.assetid:
title: How to configure the Operations console cache
description: This article describes the new Type Cache feature for the System Center Operations Manager Operations console and dependent applications.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 02/08/2024
ms.custom: engagement-fy24
ms.service: system-center
monikerRange: 'sc-om-1801'
ms.subservice: operations-manager
ms.topic: article
---

# Operations console refresh optimization


[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]


In Operations Manager 1801, performance improvements have been implemented in the Operations console while a new management pack is being imported or deleted, or a configuration change to an MP is saved that previously prevented the console from responding while these operations were being performed.  

On a new install or upgrade of the Operations console, this feature is enabled by default. To provide backward compatibility, for any application other than the Operations console, this feature is disabled by default.  

## How to configure this feature

To modify this behavior for the Operations console, the following registry key enables or disables this feature - **HKLM\Software\Microsoft\System Center Operations Manager\12\Setup\Console “IsCacheUnlockedRefresh**

Setting the value to **True** enables the feature and setting it to **False** disables the feature.

> [!NOTE]
> For applications integrating with Operations Manager that require the Operations console, disabling this feature will also affect the application installed on the system.  
>

## Application support

The new refresh logic only applies to your application if it has explicitly enabled it using a new parameter that needs to be passed when doing an `EnterpriseManagementGroup` connect. Since this is a new parameter, the existing applications won't be affected and will continue to work fine.  

To enable this feature for an application that interoperates with Operations Manager outside of the Operations console, a new `ConnectionSetting` mode needs to be added:
`EnterpriseManagementConnectionSettings.CacheRefreshMode = CacheRefreshMode.Unlocked`.  
