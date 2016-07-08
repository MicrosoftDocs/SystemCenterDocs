---
title: Get Internet Application Status
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 83143603-d47b-4162-8932-f91eb9cac53b
author:bwren
manager:cfreemanwa
---
# Get Internet Application Status
The Get Internet Application Status activity checks the availability of an internet application server. You can check the availability of a Web \(HTTP\), Email \(SMTP\), Email \(POP3\), FTP, DNS, or custom server.  You can also configure a server so it is available after a power outage or a restart.  
  
## Configuring the Get Internet Application Status Activity  
Use the following information to configure the Get Internet Application Status activity.  
  
> [!NOTE]  
> You cannot set individual security credentials for this activity. It will run under the service account configured for the Runbook Service on the Runbook server where the instance of the activity is running. This account must have the authority to access the resources and perform the actions required by this activity.  
  
### General Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Name**|Type a descriptive name for the activity.|  
|**Description**|Type a detailed description of the actions of the activity.|  
|**Type**|Select the **Type** that matches the server that you want to monitor. The options include the following:<br /><br />-   Web \(HTTP\)<br />-   E\-mail \(SMTP\)<br />-   E\-mail \(POP3\)<br />-   FTP<br />-   DNS<br />-   Custom<br /><br />Configuration instructions for each **Details** tab **Type** are listed in the following tables.|  
  
### Web \(HTTP\) Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**URL**|Type the URL that will be used to contact the web server.|  
|**Port**|Select to specify a port to use to connect to the web server. The default port is 80.|  
|**Timeout**|Type the number of seconds to wait for a response from the web server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Check that the page contains this string**|Select and type a string to search for when the page is retrieved from the web server. When this option is selected, the server is only considered available if the string can be found on the page that is specified by the **URL**.|  
|**Search is case sensitive**|Select to make the string search case sensitive.|  
  
### Email \(SMTP\) Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Computer**|Type the name of the computer where the SMTP server is located. You can also browse for the computer using the ellipsis **\(...\)** button.|  
|**Port**|Select to specify a port to use to connect to the SMTP server. The default port is 25.|  
|**Timeout**|Type the number of seconds to wait for a response from the server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Send test email**|Select to send a test email using the SMTP server. When this option is selected, the server is only considered available if the email can be sent to the server.|  
|**To**|Type the address to send the email to.|  
|**From**|Type the address that the email is being sent from.|  
  
### Email \(POP3\) Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Computer**|Type the name of the computer where the POP3 server is located. You can also browse for the computer using the ellipsis **\(...\)** button.|  
|**Port**|Select to specify a port to use to connect to the POP3 server. The default port is 110.|  
|**Timeout**|Type the number of seconds to wait for a response from the server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Test connection**|Select to use a username and password to test the connection to the POP3 server. When this option is selected, the server is only considered available if the credentials are successfully used to log into the server.|  
|**Username**|Type the username to use to log into the POP3 server.|  
|**Password**|Type the password that is associated with the **Username** that you have specified.|  
  
### FTP Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Computer**|Type the name of the computer where the FTP server is located. You can also browse for the computer using the ellipsis **\(...\)** button.|  
|**Port**|Select to specify a port to use to connect to the FTP server. The default port is 21.|  
|**Timeout**|Type the number of seconds to wait for a response from the server. If the timeout expires without a response, the server will be considered unavailable.|  
|**Test connection**|Select to use a username and password to test the connection to the FTP server. When this option is selected, the server is only considered available if the credentials are successfully used to log into the server.|  
|**Username**|Type the username to use to log into the FTP server.|  
|**Password**|Type the password that is associated with the **Username** that you have specified.|  
  
### DNS Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Computer**|Type the name of the computer where the DNS server is located. You can also browse for the computer using the ellipsis **\(...\)** button. This field is not required to test the availability of a DNS server.|  
|**Port**|Use the default port of 53 to connect to the DNS server.|  
|**Port**|Select to specify the port to use to connect to the DNS server.|  
|**Test DNS table IP address**|Select to specify a computer name and the IP address that should be associated with that IP address. When this option is selected, the server is only considered available if the IP address is assigned to the computer that you specify.|  
  
### Custom Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Actions**|Click **Add** or **Insert** to open the **Action Properties** dialog box. Configure the rest of the settings described in this table. **Tip:** Click the **Up** or **Down** buttons to change the order of the actions. Click **Remove** to remove an action. Click **Edit** to edit an action.|  
|**Open port**|Type the port number and the computer where the Internet application resides.|  
|**Send data**|Type the data that you will send to the Internet application. To specify a file that contains the data you want to send, click **Send data from file**.|  
|**Receive data**|Click **Publish as execution data** and click the name of the variable where the received data will be saved. Click **Save data**, specify the **File** where you want to save the data received from the Internet application. Click the action you want to specify in the **If the Destination File Exists** box.  You can select **Create a file with a unique name**, **Append data to the existing file**, or **Overwrite the existing file**.|  
|**Close port**|You must configure the **Open port** action before you can select this action.|  
  
You can use a sequence of actions to test a custom Internet application that is not part of the predefined list. You can perform actions such as opening and closing a port as well as communicating with the Internet application by sending and receiving information.  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|Computer|The name of the computer where the Internet application resides.|  
|Port|The port used to communicate with the Internet application.|  
|Protocol|The protocol of the Internet application. For example, HTTP or FTP.|  
|Server Greeting|The greeting message received from the Internet application. This published data is only available in FTP, Email \(POP3\), and Email \(SMTP\).|  
|Web page|The HTML of the web page that was retrieved when in Web \(HTTP\) mode.|  
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
  
