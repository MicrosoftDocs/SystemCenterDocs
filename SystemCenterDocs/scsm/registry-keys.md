---
title: Service Manager registry keys
description: Learn about registry keys used by Service Manager.
manager: carmonm
ms.topic: reference
author: JYOTHIRMAISURI
ms.author: v-jysur
ms.prod: system-center
ms.date: 01/23/2018
ms.technology: service-manager
---

# Registry keys used by Service Manager

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

> [!CAUTION]
> Incorrectly editing the registry can severely damage your system. Before making changes to the registry, you should back up any valued data on the computer.

Service Manager stores many settings in the registry. You seldom have to edit the registry yourself, because most of those settings are derived from entries that you make in day-to-day use. However, some changes to settings might occasionally be required. Service Manager stores most registry values in the following locations:

-   HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console

-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\System Center\<version>

## Service Manager console registry keys
The keys in this section are used to manage the Service Manager console for the Service Manager console user. These keys are found in the HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console directory.

|Key|Description and value|
|-------|-------------------------|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleDisplaySettings\NavigationPaneExpanded|The navigation pane is expanded when the value is set to 1 and not expanded when the value is set to 0.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleDisplaySettings\NavigationPaneWidth|Specifies the navigation pane width, limited to display resolution.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleDisplaySettings\TasksPaneExpanded|The **Tasks** pane is expanded when the value is set to 1, and not expanded when the value is set to 0.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleDisplaySettings\NaN|Specifies the **Tasks** pane width, limited to display resolution.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleDisplaySettings\ForceHighContrast|High Contrast is enabled when the value is set to 1, and not enabled when the value is set to 0.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleWindowSettings\IsConsoleMaximized|The Service Manager console is maximized when the value is set to 1, and not maximized when the value is set to 0.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleWindowSettings\ConsoleLocation\X|Specifies the top left corner of the Service Manager console horizontal coordinate.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleWindowSettings\ConsoleLocation\Y|Specifies the bottom left corner of the Service Manager console vertical coordinate.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleWindowSettings\ConsoleSize\Height|Specifies the height of the Service Manager console, limited to display resolution.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ConsoleWindowSettings\ConsoleSize\Width|Specifies the width of the Service Manager console, limited to display resolution.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\SmConsoleDisplaySettings\NavigationPaneVisible|The Service Manager console navigation pane is visible when the value is set to 1 and hidden when the value is set to 0.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\SmConsoleDisplaySettings\TasksPaneVisible|The Service Manager console**Tasks** pane is visible when set to 1 and hidden when the value is set to 0.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\SmConsoleDisplaySettings\ SelectedWunderBarIndex|Depending on the value, the corresponding workspace is selected in the Service Manager console. **Administration** = 0, **Library** = 1, **Work Items** = 2, **Configuration Items** = 3, **Data Warehouse** = 4, **Reporting** = 5. Values higher than 5 correspond to any custom workspaces that are added to the Service Manager console.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\SmConsoleDisplaySettings\NavigationModelNodeLocation|The value for the key is the last view that the user selected before closing the Service Manager console, so that when the Service Manager console reopens, it reopens in this view. **msscnav://root/Windows/Window/ConsoleDisplay/Folder.f837da16-dc5d-7a25-1b48-c62eb5965806/Folder.8afcc5db-910c-35a0-700f-fd9a94b4169b/View.fbf52403-7ce7-05c4-0ca9-7c61030e5f57** is an example value.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ViewDisplaySettings\ DetailPaneHeight|Specifies the height of the details pane.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\ViewDisplaySettings\ DetailPaneExpanded|The Service Manager console details pane is visible when the value is set to 1 and hidden when the value is set to 0.|
|HKEY_CURRENT_USER\Software\Microsoft\System Center\<version>\Service Manager\Console\User Settings\ SDKServiceMachine|Specifies the name of the server that the Service Manager console is connected to.|

## Service Manager registry keys
Keys in this section are used to manage functions that are internal to Service Manager.

|Key|Description and values|
|-------|--------------------------|
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\System Center\<version>\Common\GroupCalcPollingIntervalMilliseconds|Specifies the group change check interval in milliseconds. |
