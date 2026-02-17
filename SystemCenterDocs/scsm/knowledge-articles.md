---
title: Manage Knowledge Articles
description: Describes how to manage Service Manager knowledge articles.
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
keywords:
ms.date: 04/15/2025
ms.subservice: service-manager
ms.assetid: 50edf3f3-fa1d-4134-8383-dfc6be73ddf0
ms.update-cycle: 1095-days
ms.custom: UpdateFrequency2, engagement-fy24
---

# Manage Service Manager knowledge articles



Knowledge articles in Service Manager can help service desk analysts and end-users understand and solve problems. Any employee can search for, view, and create knowledge articles so that end-users can help themselves and resolve IT problems before new work items are opened. Service desk analysts also have to link work items to knowledge articles.

Use the procedures in this article to create and search for knowledge articles.

## Create a knowledge article

You can use the following procedure to create a knowledge article in Service Manager. This procedure describes how to create a new example knowledge article to help users obtain the latest service pack for Windows 10. However, you can complete these steps to create any type of knowledge article.

> [!NOTE]
> To view external content in knowledge articles, the computer on which the Service Manager console is installed must be connected to the Internet, either directly or through a proxy server.

To create a knowledge article, follow these steps:

1. In the Service Manager console, select **Library**.

2. In the **Library** pane, expand **Knowledge**, and select **All Knowledge Articles**.

3. In the **Tasks** pane, under **Knowledge**, select **Create Knowledge Article**.

4. In the form that appears, on the **General** tab, in the **Knowledge article information** area, follow these steps:

    1. In the **Title** box, enter a title for the knowledge article. For example, enter **How to obtain Windows 10 service packs**.

    2. In the description box, enter a description for the article. For example, enter **You can use this article to help understand this problem and to correct the problem yourself.**

5. In the **Knowledge** form, expand the **Classification** area, and then complete these steps:

    1. In the **Keywords** box, enter classification keywords that you can later search, separated by semicolons. For example, enter **Windows; Service; Pack**.

    2. In the **Knowledge Article Owner** box, browse for and select an owner for the knowledge article. For example, select **Phil Gibbons**.

    3. In the **Category** list, select an applicable category. For example, select **Software**.

6. Expand the **External Content** area. In the **URL** box, enter the web address if the information source of the article is known. For example, enter **https://support.microsoft.com/kb/935791**.

7. Expand **Internal Content**. In the box, enter or paste information about how the user can apply information from the **External Content** box to fix a problem that is specific to your organization. For example, enter **Visit the URL to read about how to download the latest service pack for Windows 10**.

8. Select **OK** to save the new knowledge article.

### Validate that the knowledge article was created

- Verify that the new knowledge article appears in the **All Knowledge Articles** pane.

## Search for a knowledge article

You can use the following procedures to search for a knowledge article by using the Service Manager console in Service Manager. If you want to link a knowledge article to an incident or to a change request, save the incident or change request first. You can perform full-text searches when you search for knowledge articles. When you search, Service Manager queries the following fields in the knowledge search form:

- **Title**

- **Description**

- **Comments**

- **Keywords**

- **External URL**

- **Internal Content**

- **Analyst Content**

When the search is complete, Service Manager displays matches for content in the **Title**, **End-User** content, and **Analyst Content** fields. If you want to view the whole article, select **Open article to see external content**. If you enter **Windows 10** in the search box, that exact string must exist in one of the knowledge article fields.

> [!NOTE]
> Partial matches aren't returned by a search. Therefore, when you search for a knowledge article based on a keyword, you must enter the exact word. However, you can use the asterisk (&#42;) as a wildcard character when you perform a search.

### Search for a knowledge article using the Service Manager console

To search for a knowledge article using the Service Manager console, follow these steps:

1. In the Service Manager console, in the search box, enter a keyword or term. For example, enter **Windows 10**.

2. Select the arrow to the right of the search box to view a list of the objects for which you want to search, and select **Knowledge**.

The **Knowledge Search** form displays the knowledge articles that match the search term.

### Search for a knowledge article when an incident or change request form is open

To search for a knowledge article when an incident or change request form is open, follow these steps:

1. With an incident or change request form open, in the **Tasks** pane, select **Search for Knowledge Articles**.

2. In the **Knowledge Search** form, enter a search term in the **Search for** box, and select **Go**. For example, enter **Windows 10**.

### Link a knowledge article to an incident or change request

To link a knowledge article to an incident or change request, follow these steps:

1. In the Service Manager console, in the search box, enter the keyword or term for which you want to search. For example, enter **Windows 10**.

2. Select the arrow to the right of the search box to view a list of the objects for which you want to search, and select **Knowledge**.

3. The **Knowledge Search** form displays the knowledge articles that match the search term.

4. Select the article that you want to link, and select **Link To**.

5. In the **Select objects** dialog, under **Filter by class**, select either **Incident** or **Change Request**.

6. Select an incident or change request, and select **OK**.

7. Select **OK** to close the informational message.

8. In the **Knowledge Search** form, select **Close**.

## Next steps

[Configure and use Service Manager cmdlets](sm-cmdlets.md).
