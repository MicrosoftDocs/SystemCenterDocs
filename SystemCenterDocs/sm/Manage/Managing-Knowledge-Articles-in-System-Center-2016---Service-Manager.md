---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Managing Knowledge Articles in System Center 2016   Service Manager
ms.technology:  service-manager
ms.assetid:  50edf3f3-fa1d-4134-8383-dfc6be73ddf0
---

# Managing Knowledge Articles in System Center 2016 - Service Manager

>Applies To: System Center 2016 Technical Preview - Service Manager

Knowledge articles in Service Manager can help service desk analysts and end users understand and solve problems. Because any employee can search for and view knowledge articles, create knowledge articles so that end users can help themselves resolve IT problems before new work items are opened. Service desk analysts also have to link work items to knowledge articles.

Use the procedures in this section to create and search for knowledge articles.

## How to Create a Knowledge Article

You can use the following procedure to create a knowledge article in Service Manger. This procedure describes how to create a new example knowledge article to help users obtain the latest service pack for Windows 10. However, you can complete these steps to create any type of knowledge article.

> [!NOTE]
> To view external content in knowledge articles, the computer on which the Service Manager console is installed must be connected to the Internet, either directly or through a proxy server.

### To create a knowledge article

1.  In the Service Manager console, click **Library**.

2.  In the **Library** pane, expand **Knowledge**, and then click **All Knowledge Articles**.

3.  In the **Tasks** pane, under **Knowledge**, click **Create Knowledge Article**.

4.  In the form that appears, on the **General** tab, in the **Knowledge article information** area, follow these steps:

    1.  In the **Title** box, type a title for the knowledge article. For example, type **How to obtain Windows 10 service packs**.

    2.  In the description box, type a description for the article. For example, type **You can use this article to help understand this problem and to correct the problem yourself.**

5.  In the **Knowledge** form, expand the **Classification** area, and then complete these steps:

    1.  In the **Keywords** box, type classification keywords that you can later search, separated by semicolons. For example, type **Windows; Service; Pack**.

    2.  In the **Knowledge Article Owner** box, browse for and then select an owner for the knowledge article. For example, select **Phil Gibbons**.

    3.  In the **Category** list, select an applicable category. For example, select **Software**.

6.  Expand the **External Content** area. In the **URL** box, type the web address if the information source of the article is known. For example, type **http://support.microsoft.com/kb/935791**.

7.  Expand **Internal Content**. In the box, type or paste information about how the user can apply information from the **External Content** box to fix a problem that is specific to your organization. For example, type **Visit the URL to read about how to download the latest service pack for Windows 10**.

8.  Click **OK** to save the new knowledge article.

### To validate that the knowledge article was created

-   Verify that the new knowledge article appears in the **All Knowledge Articles** pane.



## How to Search for a Knowledge Article
You can use the following procedures to search for a knowledge article by using the Service Manager console in Service Manager. If you want to link a knowledge article to an incident or to a change request, save the incident or change request first. You can perform full-text searches when you search for knowledge articles. When you search, Service Manager queries the following fields in the knowledge search form:

-   **Title**

-   **Description**

-   **Comments**

-   **Keywords**

-   **External URL**

-   **Internal Content**

-   **Analyst Content**

When the search is complete, Service Manager displays matches for content in the **Title**, **End-User** content, and **Analyst Content** fields. If you want to view the whole article, click **Open article to see external content**. If you type **Windows 10** in the search box, that exact string must exist in one of the knowledge article fields.

> [!NOTE]
> Partial matches are not returned by a search. Therefore, when you search for a knowledge article based on a keyword, you must type the exact word. However, you can use the asterisk (*) as a wildcard character when you perform a search.

### To search for a knowledge article using the Service Manager console

1.  In the Service Manager console, in the search box, type a keyword or term. For example, type **Windows 10**.

2.  Click the arrow to the right of the search box to view a list of the objects for which you want to search, and then click **Knowledge**.

The **Knowledge Search** form displays the knowledge articles that match the search term.

### To search for a knowledge article when an incident or change request form is open

1.  With an incident or change request form open, in the **Tasks** pane, click **Search for Knowledge Articles**.

2.  In the **Knowledge Search** form, type a search term in the **Search for** box, and then click **Go**. For example, type **Windows 10**.

### To link a knowledge article to an incident or change request

1.  In the Service Manager console, in the search box, type the keyword or term for which you want to search. For example, type **Windows 10**.

2.  Click the arrow to the right of the search box to view a list of the objects for which you want to search, and then click **Knowledge**.

3.  The **Knowledge Search** form displays the knowledge articles that match the search term.

4.  Select the article that you want to link, and then click **Link To**.

5.  In the **Select objects** dialog box, under **Filter by class**, select either **Incident** or **Change Request**.

6.  Select an incident or change request, and then click **OK**.

7.  Click **OK** to close the informational message.

8.  In the **Knowledge Search** form, click **Close**.



