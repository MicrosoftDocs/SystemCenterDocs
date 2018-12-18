---
title: "Connect-Disconnect Dial-up | Microsoft Docs"
ms.custom: ""
ms.date: "2016-05-13"
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "System Center 2012 SP1 - Orchestrator"
  - "System Center 2012 - Orchestrator"
  - "System Center 2012 R2 Orchestrator"
ms.assetid: d1841bbc-7c36-4f3c-983f-db7c74a56cd5
caps.latest.revision: 5
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Connect/Disconnect Dial-up
The Connect/Disconnect Dial-up activity connects or disconnects a dial-up connection or VPN. The connection must be configured on the Runbook server before the activity can use it. For more information on creating a network connection in Windows Server 2008, see [Establish Network Connections](http://go.microsoft.com/fwlink/?LinkID=229330)  
  
## Configuring the Connect/Disconnect Dial-up Activity  
 Use the following information to configure the Connect/Disconnect Dial-up activity.  
  
### Connection Tab  
  
|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Dial-up or VPN entry**|Type the name of the entry as entered in the address book, or click the ellipsis **(…)** button and select the entry from the Remote Access Phone Book.|  
|**Connect/Disconnect**|Select whether to connect to or disconnect from the dial-up connection or VPN|  
|**Attempts**|Enter the number of times the activity should attempt to connect to the remote network before quitting.|  
|**Delay**|Enter the amount of time, in seconds, that the activity should wait between retry attempts.|  
  
### Authentication Tab  
  
|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Domain**|Enter the name of the domain for the username.|  
|**Username**|Enter the username to logon to the remote network.|  
|**Password**|Enter the password for the username.|  
  
### Published Data  
 The following table lists the published data items.  
  
|Item|Description|  
|----------|-----------------|  
|Dial-up or VPN name|The name assigned of the network connection|  
|Number of retries attempted|Indicates how many times the activity attempted to establish the connection before succeeding or failing.|  
|Domain name credential|The domain name used by the activity when establishing a connection|  
|User name credential|The user name used by the activity when establishing a connection|