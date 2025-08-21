---
title: Invoke Web Services 
description: This article describes the Invoke Web Services activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: how-to
ms.assetid: 44490141-2205-427b-a700-1e64ed61a561
caps.latest.revision: 15
author: jyothisuri
ms.author: jsuri
---
# Invoke Web Services

The Invoke Web Services activity runs a web service with the XML parameters you specify.  

## Configure the Invoke Web Services Activity

 Before you configure the Invoke Web Services activity, you need to determine the following:  

- WSDL file of the web service.

- Web service method name.

- Input SOAP message body format.

- Output SOAP message body format.

Use the following information to configure the Invoke Web Services activity.  

### Details  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**WSDL**|Enter the path of the WSDL file or use the ellipsis **(...)** to browse for the file.|  
|**Method**|Enter the name of the method that you're invoking on the web service, or select the ellipsis **(...)** and browse for it. Ensure that you match the casing of the method.|  
|**XML Request Payload**|Enter the parameters that you're sending to the web service method. Ensure that the format matches what is described in the WSDL document.|  
|**Format Hint**|Select this to receive hints on formatting the XML job payload. Replace the placeholder values with your own.|  

### Advanced  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Save**|To save the responses, select the **Save** checkbox and specify the folder where the responses will be saved.|  
|**URL**|To specify the URL location of the web service, select the **URL** checkbox and enter the URL location.|  
|**Value**|Select the SOAP protocol that the web service uses. The **Value** options include the following:<br /><br /> -   SOAP 1.1<br />-   SOAP 1.2|  

### Security  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Enable**|Select the **Enable** checkbox to enable HTTP authentication, and fill in the fields.|  
|**User name**|Enter the user name to access the secured web service.|  
|**Password**|Enter the password to access the secured web service.|  

###  <a name="BKMK_HTTPS"></a> HTTPS certificate options

 Orchestrator allows you to configure HTTPS certificate options in cases where certificate validation fails.  

 Use the following steps to configure HTTPS certificate options.  

#### Configure HTTPS certificate options

1. In the Runbook Designer, select the **Options** menu and select **Invoke Web Services** to open the **Invoke Web Services** dialog.  

2. Configure the settings on the **Details** tab. Configuration instructions are listed in the following table.  

### Details

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**HTTPS Options**|Select one of the following **HTTPS Options**:<br /><br /> -   **Accept all certificates**<br />-   **Accept certificates from trusted hosts**<br /><br /> Configuration instructions for each of the **HTTPS Options** are listed in the following tables.|  

### Accept all certificates Details

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Accept all certificates**|Accepts certificates from all hosts.<br /><br /> After you select this HTTPS option, select **Finish**.|  

### Accept certificates from trusted hosts Details

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Accept certificates from trusted hosts**|Specifies the hosts you want to accept the certificates from.<br /><br /> 1.  Select **Add** to open the **Trusted Host** dialog.<br />2.  Enter the trusted host name in the **Value** box, and select **OK**. The host is then added to the list.<br /><br /> To edit hosts, select **Edit**.<br /><br /> To remove hosts, select **Remove**.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|WSDL Path|The WSDL path.|  
|Method Name|The name of the web method.|  
|XML Job Payload|The text of the XML job payload.|  
|XML Response Payload|The text of the XML response payload.|  
|Response File|The path and filename of the response.|  
|Web Service URL|The URL of the web service.|  
|Web Service protocol|The protocol that the web service uses.|  

### Publish web services

 The Invoke Web Service object builds an assembly at **C:\ProgramData\Microsoft System Center 2012\Orchestrator\Activities\WebServices2**or **C:\Users\USERNAME\AppData\Local\Microsoft System Center 2012\Orchestrator\Activities\WebServices2**. The assembly is identified by the web service location. For example, **http://localhost/TestService/DylanService.asmx?WSDL**.  

 If you publish additional services or update an existing service, you must clean the cache, except for the **wspkey.snk** file. After cleaning the cache, the web service changes are   correctly published.
