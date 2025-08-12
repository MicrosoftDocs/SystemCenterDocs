---
ms.assetid: 715a0ed4-8936-4b43-ad1b-024465e0605e
title: How to Add Knowledge to a Management Pack
description: This article describes how to add custom knowledge to a workflow in a management pack.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: na
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# How to add knowledge to a management pack



System Center Operations Manager management packs include knowledge for rules, monitors, and alerts that helps you identify problems, causes, and resolutions.  

Knowledge is referred to as *product knowledge* or *company knowledge*. Product knowledge is embedded in a rule or monitor when it's authored. Company knowledge is added by management group administrators to expand the troubleshooting information and provide company-specific information for operators. Administrators can use company knowledge to document any overrides implemented for a monitor or rule, along with the explanation for the customization and any other information that might be useful.  

Operations Manager stores company knowledge in a management pack. Sealed management packs can't be modified, so Operations Manager saves customizations such as company knowledge in a custom management pack. By default, Operations Manager saves all customizations to the Default Management Pack. As a best practice, you should instead create a separate management pack for each sealed management pack you want to customize.  

> [!TIP]  
> To avoid losing your company knowledge, be sure to back up custom management packs as part of your general backup routine.  

To add or edit company knowledge, the computer must meet the following software requirements:  

-   The Operations console is installed on the computer.
-   Microsoft Word 2010 or higher.
-   [Microsoft Visual Studio 2010 Tools for Office Runtime](/visualstudio/vsto/visual-studio-tools-for-office-runtime-installation-scenarios).

To add or edit company knowledge, you must have the Author or Administrator user role.  

## To edit company knowledge  

1.  Open the Operations console with an account that is a member of the Operations Manager Author or Administrator role.  

2.  Select **Authoring**.  

3.  Locate the monitor or rule to be documented.  

4.  Select **Properties** under **Actions**, or right-click the monitor name and select **Properties** from the shortcut menu.  

5.  Select the **Company Knowledge** tab.  

6.  In the **Management pack** section, select a management pack in which to save the company knowledge.  

7.  Select **Edit** to launch Microsoft Office Word.  

8.  Add or edit text as desired.  

    The company knowledge tab displays only the sections of the Word document with custom text.  

9. On the **File** menu, select **Save** to save your changes.  

    > [!IMPORTANT]  
    > Don't close Word.  

10. Return to the company knowledge tab and select **Save**, and select **Close**. This will close both the properties dialog and Word.  

## Next steps  

- To perform common administrative tasks with management packs in your management group, see [How to Import, Export, and Remove an Operations Manager Management Pack](manage-mp-import-remove-delete.md).

- To learn how to create a custom writeable management pack to store your overrides, see [How to Create a Management Pack for Overrides](manage-mp-create-unsealed-mp.md).

- Before making changes to the monitoring settings defined in an Operations Manager management pack, review [How to Override a Rule or Monitor](manage-mp-override-rule-monitor.md) to understand how to configure the change.
