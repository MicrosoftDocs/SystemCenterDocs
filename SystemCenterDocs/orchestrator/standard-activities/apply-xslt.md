---
title: Apply XSLT
description: This article describes the functionality of Apply XSLT activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 07fee562-5069-45b9-b48c-a816fced7284
caps.latest.revision: 11
author: jyothisuri
ms.author: jsuri
---
# Apply XSLT

The Apply XSLT activity enables you to transform the content of an XML file according to the rules in an XSLT file that you specify. You can use the Apply XSLT activity to transform the content of an XML file to an HTML file.  

## Configure the Apply XSLT Activity

 Before you configure the Apply XSLT activity, you need to determine the following:  

- The name of the XML file that will be converted.  

- The name that you want to assign to the XML file that results from the transformation.  

- The name of the XSLT file that you'll use to transform the XML file.  

Use the following information to configure the Apply XSLT activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Input XML file**|Enter the path and file name of the XML file that you want to transform, or select the ellipsis button **(...)** and browse for it.|  
|**Output XML file**|Enter the path, file name, and file name extension for the file that will hold the results of the transformation. Alternatively, select the ellipsis button **(...)** and browse for the folder where you'll save the file. From the Windows **Open** dialog, enter the file name and file name extension in the **File name** box.|  
|**XSLT file**|Enter the path and name of the XSLT file that you want to use to transform the input XML file, or select the ellipsis button **(...)** and browse for it.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Input XML|The path and file name of the XML file that will be transformed.|  
|Output XML|The path and file name of the XML file that will contain the result of the transformation.|  
|XSLT file|The path and file name of the XSLT file used to transform the input XML file.|
