---
title: Get Internet Application Status
description: This article describes the functionality of Get Internet Application Status activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 08/21/2025
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 83143603-d47b-4162-8932-f91eb9cac53b
caps.latest.revision: 18
author: Jeronika-MS
ms.author: v-gajeronika
---
# Get Internet Application Status

This article describes the functionality of Get Internet Application Status activity. The Get Internet Application Status activity checks the availability of an internet application server. You can check the availability of a Web (HTTP), Email (SMTP), Email (POP3), FTP, DNS, or custom server. You can also configure a server so that it's available after a power outage or a restart.  

## Configure the Get Internet Application Status Activity

Use the following information to configure the Get Internet Application Status activity.  

> [!NOTE]
> You can't set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.  

### [General Tab](#tab/general-tab)  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Name**|Enter a descriptive name for the activity.|  
|**Description**|Enter a detailed description of the actions of the activity.|  
|**Type**|Select the **Type** that matches the server that you want to monitor. The options include the following:<br /><br /> -   Web (HTTP)<br />-   E-mail (SMTP)<br />-   E-mail (POP3)<br />-   FTP<br />-   DNS<br />-   Custom<br /><br /> Configuration instructions for each **Details** tab **Type** are listed in the following tables.|  

### [Web (HTTP) Details Tab](#tab/web-http-details-tab)

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**URL**|Enter the URL that will be used to contact the web server.|  
|**Port**|Select to specify a port to use to connect to the web server. The default port is 80.|  
|**Timeout**|Enter the number of seconds to wait for a response from the web server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Check that the page contains this string**|Select and enter a string to search for when the page is retrieved from the web server. When this option is selected, the server is only considered available if the string can be found on the page that's specified by the **URL**.|  
|**Search is case sensitive**|Select to make the string search case sensitive.|  

### [Email (SMTP) Details Tab](#tab/email-smtp-details-tab)

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer where the SMTP server is located. You can also browse for the computer using the ellipsis **(...)** button.|  
|**Port**|Select to specify a port to use to connect to the SMTP server. The default port is 25.|  
|**Timeout**|Enter the number of seconds to wait for a response from the server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Send test email**|Select to send a test email using the SMTP server. When this option is selected, the server is only considered available if the email can be sent to the server.|  
|**To**|Enter the address to send the email to.|  
|**From**|Enter the address that the email is being sent from.|  

### [Email (POP3) Details Tab](#tab/email-pop3-details-tab)

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer where the POP3 server is located. You can also browse for the computer using the ellipsis **(...)** button.|  
|**Port**|Select to specify a port to use to connect to the POP3 server. The default port is 110.|  
|**Timeout**|Enter the number of seconds to wait for a response from the server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Test connection**|Select to use a username and password to test the connection to the POP3 server. When this option is selected, the server is only considered available if the credentials are successfully used to sign in to the server.|  
|**Username**|Enter the username to use to sign in to the POP3 server.|  
|**Password**|Enter the password that is associated with the **Username** that you've specified.|  

### [FTP Details Tab](#tab/ftp-details-tab)

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer where the FTP server is located. You can also browse for the computer using the ellipsis **(...)** button.|  
|**Port**|Select to specify a port to use to connect to the FTP server. The default port is 21.|  
|**Timeout**|Enter the number of seconds to wait for a response from the server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Test connection**|Select to use a username and password to test the connection to the FTP server. When this option is selected, the server is only considered available if the credentials are successfully used to sign in to the server.|  
|**Username**|Enter the username to use to sign in to the FTP server.|  
|**Password**|Enter the password that's associated with the **Username** that you've specified.|  

### [DNS Details Tab](#tab/dns-details-tab)

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Computer**|Enter the name of the computer where the DNS server is located. You can also browse for the computer using the ellipsis **(...)** button. This field isn't required to test the availability of a DNS server.|  
|**Port**|Use the default port of 53 to connect to the DNS server.|  
|**Port**|Select to specify the port to use to connect to the DNS server.|  
|**Test DNS table IP address**|Select to specify a computer name and the IP address that should be associated with that IP address. When this option is selected, the server is only considered available if the IP address is assigned to the computer that you specify.|  

### [Custom Details Tab](#tab/custom-details-tab)

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Actions**|Select **Add** or **Insert** to open the **Action Properties** dialog. Configure the rest of the settings described in this table. **Tip:** Select the **Up** or **Down** buttons to change the order of the actions. Select **Remove** to remove an action. Select **Edit** to edit an action.|  
|**Open port**|Enter the port number and the computer where the Internet application resides.|  
|**Send data**|Enter the data that you'll send to the Internet application. To specify a file that contains the data you want to send, select **Send data from file**.|  
|**Receive data**|Select **Publish as execution data** and select the name of the variable where the received data will be saved. Select **Save data**, specify the **File** where you want to save the data received from the Internet application. Select the action you want to specify in the **If the Destination File Exists** box. You can select **Create a file with a unique name**, **Append data to the existing file**, or **Overwrite the existing file**.|  
|**Close port**|You must configure the **Open port** action before you can select this action.|  

 You can use a sequence of actions to test a custom Internet application that isn't part of the predefined list. You can perform actions such as opening and closing a port and communicating with the Internet application by sending and receiving information.  

### [Published Data](#tab/published-data)

 The following table lists the published data items:  

|Item|Description|  
|----------|-----------------|  
|Computer|The name of the computer where the Internet application resides.|  
|Port|The port used to communicate with the Internet application.|  
|Protocol|The protocol of the Internet application. For example, HTTP or FTP.|  
|Server Greeting|The greeting message received from the Internet application. This published data is only available in FTP, Email (POP3), and Email (SMTP).|  
|Web page|The HTML of the web page that was retrieved when in Web (HTTP) mode.|  
|Receive variable 1|The first variable retrieved when in Custom mode.|  
|Receive variable 2|The second variable retrieved when in Custom mode.|  
|Receive variable 3|The third variable retrieved when in Custom mode.|  
|Receive variable 4|The fourth variable retrieved when in Custom mode.|  
|Receive variable 5|The fifth variable retrieved when in Custom mode.|  
|Receive variable 6|The sixth variable retrieved when in Custom mode.|  
|Receive variable 7|The seventh variable retrieved when in Custom mode.|  
|Receive variable 8|The eighth variable retrieved when in Custom mode.|  
|Receive variable 9|The ninth variable retrieved when in Custom mode.|  
|Receive variable 10|The tenth variable retrieved when in Custom mode.|

---