---
title: Monitor Internet Application
description: This article provides the details about Monitor Internet Application activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 2cebdeb0-09dd-47b7-ae13-0b478fc77a6d
caps.latest.revision: 17
author: jyothisuri
ms.author: jsuri
---
# Monitor Internet Application

The Monitor Internet Application activity will invoke a runbook when an internet application server becomes unavailable or becomes available. You can monitor a Web, Email (POP3 or SMTP), FTP, or DNS server.  You can also configure your external FTP or Web servers to be reachable through the internet and then automatically restart the server if it's found to be unavailable.  

## Configure the Monitor Internet Application Activity

 Use the following information to configure the Monitor Internet Application activity.  

> [!NOTE]
>  You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.  

### General Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Name**|Enter a descriptive name for the activity.|  
|**Description**|Enter a detailed description of the actions of the activity.|  
|**Type**|Select the **Type** that matches the server that you want to monitor. The options include the following:<br /><br /> -   Web (HTTP)<br />-   E-mail (SMTP)<br />-   E-mail (POP3)<br />-   FTP<br />-   DNS<br /><br /> Configuration instructions for each **Details** tab **Type** are listed in the following tables.|  

### Web (HTTP) Details Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**URL**|Enter the URL that will be used to contact the web server.|  
|**Port**|Select to specify a port to use to connect to the web server. The default port is 80.|  
|**Timeout**|Enter the number of seconds to wait for a response from the web server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Test frequency**|Specify the amount of time to wait between each connection test to the server.|  
|**Check that the page contains this string**|Select and enter a string to search for when the page is retrieved from the web server. When this option is selected, the server is only considered available if the string can be found on the page that is specified by the **URL**.|  
|**Search is case sensitive**|Select to make the string search case sensitive.|  

### Email (SMTP) Details Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer where the SMTP server is located. You can also browse for the computer using the ellipsis **(...)** button.|  
|**Port**|Select to specify a port to use to connect to the SMTP server. The default port is 25.|  
|**Timeout**|Enter the number of seconds to wait for a response from the server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Test frequency**|Specify the amount of time to wait between each connection test to the server.|  
|**Send test email**|Select to send a test email using the SMTP server. When this option is selected, the server is only considered available if the email can be sent to the server.|  
|**To**|Enter the address to send the email to.|  
|**From**|Enter the address that the email is being sent from.|  

### Email (POP3) Details Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer where the POP3 server is located. You can also browse for the computer using the ellipsis **(...)** button.|  
|**Port**|Select to specify a port to use to connect to the POP3 server. The default port is 110.|  
|**Timeout**|Enter the number of seconds to wait for a response from the server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Test frequency**|Specify the amount of time to wait between each connection test to the server.|  
|**Test connection**|Select to use a username and password to test the connection to the POP3 server. When this option is selected, the server is only considered available if the credentials are successfully used to sign in to the server.|  
|**Username**|Enter the username to use to sign in to the POP3 server.|  
|**Password**|Enter the password that is associated with the **Username** that you've specified.|  

### FTP Details Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer where the FTP server is located. You can also browse for the computer using the ellipsis **(...)** button.|  
|**Port**|Select to specify a port to use to connect to the FTP server. The default port is 21.|  
|**Timeout**|Enter the number of seconds to wait for a response from the server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Test frequency**|Specify the amount of time to wait between each connection test to the server.|  
|**Test connection**|Select to use a username and password to test the connection to the FTP server. When this option is selected, the server is only considered available if the credentials are successfully used to sign in to the server.|  
|**Username**|Enter the username to use to sign in to the FTP server.|  
|**Password**|Enter the password that's associated with the **Username** that you've specified.|  

### DNS Details Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer where the DNS server is located. You can also browse for the computer using the ellipsis **(...)** button. This field isn't required to test the availability of a DNS server.|  
|**Port**|Select to use the default port of 53 to connect to the DNS server.|  
|**Port**|Select to specify the port to use to connect to the DNS server.|  
|**Test DNS table IP Address**|Select to specify a computer name and the IP address that should be associated with that IP address. When this option is selected, the server is only considered available if the IP address is assigned to the computer that you specify.|  
|**Test frequency**|Specify the amount of time to wait between each connection test to the server.|  

### Advanced Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Trigger if test succeeds**|Select to invoke the Monitor Internet Application activity when the server that you're checking becomes available.|  
|**Trigger if test fails**|Select to invoke the Monitor Internet Application activity when the server that you're checking becomes unavailable.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Computer|The name of the computer where the Internet application resides.|  
|Port|The port used to communicate with the Internet application.|  
|Protocol|The protocol of the Internet application. For example, HTTP or FTP.|  
|Server Greeting|The greeting message received from the Internet application.|  
|Web page|The HTML of the web page that was retrieved when in Web (HTTP) mode.|
