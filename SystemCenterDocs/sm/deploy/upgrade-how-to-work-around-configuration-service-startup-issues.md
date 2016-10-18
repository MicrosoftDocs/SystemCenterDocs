---
title: How to Work Around Configuration Service Startup Issues
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3dead65-a5b9-4e16-af59-e5bd5e6f2320
---

# How to Work Around Configuration Service Startup Issues

>Applies To: System Center 2016 - Service Manager

There are two workaround procedures that you can use to try to resolve the issue in which an upgrade to System Center 2016 - Service Manager fails as a result of Configuration service Startup timing out. You can:  

-   Disable signature verification on the computer that is running Setup.  

-   Increase the service time\-out setting on the computer that is running Setup.  

### To disable signature verification  

1.  On the computer that is running Setup, edit the Microsoft.Mom.ConfigServiceHost.exe.config file, which is located in the Program Files\\Microsoft System Center 2016\\Service Manager folder.  

2.  In the `<runtime> </runtime>` section, add `<generatePublisherEvidence enabled="false">`.  

3.  Save the changes to the file.  

4.  Attempt the upgrade again.  

### To increase the service time\-out setting  

1.  On the computer that is running Setup, create the following registry value to increase the service time\-out period:  

    ```  
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control   
    ServicesPipeTimeout  
    DWORD  
    200000  

    ```  

    > [!CAUTION]  
    >  Incorrectly editing the registry may severely damage your system. Before making changes to the registry, you should back up any valued data on the computer.  

    > [!NOTE]  
    >  You may have to increase this value further if the service still fails to start. The value in this example is in milliseconds. For additional details about the registry key, see [article 922918](http://go.microsoft.com/fwlink/p/?LinkId=207191) in the Microsoft Knowledge Base.  

2.  Start the computer again.  

3.  Attempt the upgrade again.
