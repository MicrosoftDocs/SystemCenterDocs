---
title: Write Web Page 
description: This article describes the Write Web Page activity that will create or add information to an HTML file.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 43f5cfc6-df95-4c03-80b4-c2157bc7f88f
caps.latest.revision: 13
author: jyothisuri
ms.author: jsuri
---
# Write Web Page

The Write Web Page activity will create or add information to an HTML file. When creating new web pages with the Write Web Page activity, you can use templates that can contain any of the formattings that you require. When using the Write Web Page activity to create web pages, all occurrences of the tags \<DOC-TITLE> and \<DOC-TEXT> will be replaced by the title and text that you specify, respectively.  

 When using the Write Web Page activity to append to an existing web page, you'll specify an HTML tag that will mark the position where the page will be appended. The Write Web Page activity will append the text above the HTML tag that you've specified.  

 The Write Web Page activity can be used to output the entire audit log of a runbook that was run to correct a problem on the network. You can also use the Write Web Page activity to keep a constant update of what maintenance runbooks are running and their status.  

## Configure the Write Web Page Activity

 Use the following information to configure the Write Web Page activity.  

### General Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Name**|Enter a descriptive name for the activity.|  
|**Description**|Enter a detailed description of the actions of the activity.|  
|**Type**|Select the **Type** from the dropdown list that matches the server you want to monitor. The options include the following:<br /><br /> -   Create Web Page<br />-   Append to Web Page<br /><br /> Configuration instructions for each **Details** tab **Type** are listed in the following tables.|  

### Details Tab Create Web Page

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Title**|Enter the title of the web page. If you're using a template, this value will replace \<DOC-TITLE> anywhere it appears in the template file. If you aren't using a template, this value will be used within the \<TITLE> tag in the header of the HTML file.|  
|**Text**|Enter the text of the web page. If you're using a template, this value will replace \<DOC-TEXT> anywhere it appears in the template file. If you aren't using a template, this value will be used within the \<BODY> tag in the header of the HTML file.|  
|**Template**|Enter the path and file name of the template file that you're using. You can also use the ellipsis **(...)** button to browse for the file.|  
|**Folder**|Enter the path of the folder where you want the web page to be created.|  
|**File name**|Select to specify the file name of the web page that will be created.|  
|**Create a file with a unique name**|Select to automatically generate a unique name for the web page when it's created. This file will have the extension .html.|  

### Details Tab Append to Web Page

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Tag**|Enter the tag that will mark the point where the page will be appended. It's recommended to use the default tag \<OP-TAG-APPEND-WEB>.|  
|**Text**|Enter the text that will be appended to the web page.|  
|**Web page**|Enter the path and file name of the web page file that you're appending. You can also use the ellipsis **(...)** button to browse for the file.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Full path and name of Web Page|The full path of the HTML file that was created or appended.|  
|Source text of the web page created|The text contained within the HTML file.|  
|Title to add to the created web page|The title that was added to the web page. This published data is only available when **Create Web Page** is selected on the **General** tab.|  
|Text to add to the web page|The text that was added to the web page. This value is determined by the **Text** field in both the **Create Web Page** and **Append to Web Page** modes.|
