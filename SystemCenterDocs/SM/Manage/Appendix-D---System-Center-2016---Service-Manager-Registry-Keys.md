---
title: Appendix D - System Center 2016 - Service Manager Registry Keys
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 392af14e-a6ba-4e54-b3a0-64621b30dad6
---
# Appendix D - System Center 2016 - Service Manager Registry Keys

> [!CAUTION]
> Incorrectly editing the registry can severely damage your system. Before making changes to the registry, you should back up any valued data on the computer.

Service Manager stores many settings in the registry. You seldom have to edit the registry yourself, because most of those settings are derived from entries that you make in day\-to\-day use. However, some changes to settings might occasionally be required. [!INCLUDE[smshort](../../includes/smshort_md.md)] stores most registry values in the following locations:

-   HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console

-   HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\2016

## Service Manager Console Registry Keys
The keys in this section are used to manage the [!INCLUDE[smcons](../../includes/smcons_md.md)] for the [!INCLUDE[smcons](../../includes/smcons_md.md)] user. These keys are found in the HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console directory.

|Key|Description and value|
|-------|-------------------------|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleDisplaySettings\\NavigationPaneExpanded|The navigation pane is expanded when the value is set to 1 and not expanded when the value is set to 0.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleDisplaySettings\\NavigationPaneWidth|Specifies the navigation pane width, limited to display resolution.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleDisplaySettings\\TasksPaneExpanded|The **Tasks** pane is expanded when the value is set to 1, and not expanded when the value is set to 0.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleDisplaySettings\\NaN|Specifies the **Tasks** pane width, limited to display resolution.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleDisplaySettings\\ForceHighContrast|High Contrast is enabled when the value is set to 1, and not enabled when the value is set to 0.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleWindowSettings\\IsConsoleMaximized|The [!INCLUDE[smcons](../../includes/smcons_md.md)] is maximized when the value is set to 1, and not maximized when the value is set to 0.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleWindowSettings\\ConsoleLocation\\X|Specifies the top left corner of the [!INCLUDE[smcons](../../includes/smcons_md.md)] horizontal coordinate.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleWindowSettings\\ConsoleLocation\\Y|Specifies the bottom left corner of the [!INCLUDE[smcons](../../includes/smcons_md.md)] vertical coordinate.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleWindowSettings\\ConsoleSize\\Height|Specifies the height of the [!INCLUDE[smcons](../../includes/smcons_md.md)], limited to display resolution.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ConsoleWindowSettings\\ConsoleSize\\Width|Specifies the width of the [!INCLUDE[smcons](../../includes/smcons_md.md)], limited to display resolution.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\SmConsoleDisplaySettings\\NavigationPaneVisible|The [!INCLUDE[smcons](../../includes/smcons_md.md)] navigation pane is visible when the value is set to 1 and hidden when the value is set to 0.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\SmConsoleDisplaySettings\\TasksPaneVisible|The [!INCLUDE[smcons](../../includes/smcons_md.md)]**Tasks** pane is visible when set to 1 and hidden when the value is set to 0.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\SmConsoleDisplaySettings\\ SelectedWunderBarIndex|Depending on the value, the corresponding workspace is selected in the [!INCLUDE[smcons](../../includes/smcons_md.md)]. **Administration** \= 0, **Library** \= 1, **Work Items** \= 2, **Configuration Items** \= 3, **Data Warehouse** \= 4, **Reporting** \= 5. Values higher than 5 correspond to any custom workspaces that are added to the [!INCLUDE[smcons](../../includes/smcons_md.md)].|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\SmConsoleDisplaySettings\\NavigationModelNodeLocation|The value for the key is the last view that the user selected before closing the [!INCLUDE[smcons](../../includes/smcons_md.md)], so that when the [!INCLUDE[smcons](../../includes/smcons_md.md)] reopens, it reopens in this view. **msscnav:\/\/root\/Windows\/Window\/ConsoleDisplay\/Folder.f837da16\-dc5d\-7a25\-1b48\-c62eb5965806\/Folder.8afcc5db\-910c\-35a0\-700f\-fd9a94b4169b\/View.fbf52403\-7ce7\-05c4\-0ca9\-7c61030e5f57** is an example value.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ViewDisplaySettings\\ DetailPaneHeight|Specifies the height of the details pane.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\ViewDisplaySettings\\ DetailPaneExpanded|The [!INCLUDE[smcons](../../includes/smcons_md.md)] details pane is visible when the value is set to 1 and hidden when the value is set to 0.|
|HKEY\_CURRENT\_USER\\Software\\Microsoft\\System Center\\2016\\Service Manager\\Console\\User Settings\\ SDKServiceMachine|Specifies the name of the server that the [!INCLUDE[smcons](../../includes/smcons_md.md)] is connected to.|

## Service Manager Registry Keys
Keys in this section are used to manage functions that are internal to [!INCLUDE[smshort](../../includes/smshort_md.md)].

|Key|Description and values|
|-------|--------------------------|
|HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\2016\\Common\\GroupCalcPollingIntervalMilliseconds|Specifies the group change check interval in milliseconds. |


