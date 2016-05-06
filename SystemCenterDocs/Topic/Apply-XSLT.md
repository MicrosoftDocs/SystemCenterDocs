---
title: Apply XSLT
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07fee562-5069-45b9-b48c-a816fced7284
---
# Apply XSLT
The Apply XSLT activity enables you to transform the content of an XML file according to the rules in an XSLT file that you specify. You can use the Apply XSLT activity to transform the content of an XML file to an HTML file.

## Configuring the Apply XSLT Activity
Before you configure the Apply XSLT activity, you need to determine the following:

-   The name of the XML file that will be converted.

-   The name that you want to assign to the XML file that results from the transformation.

-   The name of the XSLT file that you will use to transform the XML file.

Use the following information to configure the Apply XSLT activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Input XML file**|Type the path and file name of the XML file that you want to transform, or click the ellipsis button **\(...\)** and browse for it.|
|**Output XML file**|Type the path, filename, and file name extension for the file that will hold the results of the transformation. Alternatively, click the ellipsis button **\(...\)** and browse for the folder where you will save the file. From the Windows **Open** dialog box, enter the file name and file name extension in the **File name** box.|
|**XSLT file**|Type the path and name of the XSLT file that you want to use to transform the input XML file, or click the ellipsis button **\(...\)** and browse for it.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Input XML|The path and file name of the XML file that will be transformed.|
|Output XML|The path and file name of the XML file that will contain the result of the transformation.|
|XSLT file|The path and file name of the XSLT file used to transform the input XML file.|

