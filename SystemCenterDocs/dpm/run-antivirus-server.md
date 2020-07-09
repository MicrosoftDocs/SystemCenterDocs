---
title:  Run antivirus software on the DPM server
description: This article provides the details about running antivirus software on the DPM server.
manager: vvithal
ms.topic: article
author: v-anesh
ms.prod: system-center
keywords:
ms.date: 07/09/2020
ms.technology: data-protection-manager
ms.assetid: c0f4201b-53f7-45c8-af16-5522d0f10c6e
ms.author: v-anesh
---

# Run antivirus software on the DPM server

DPM is compatible with most popular antivirus software products. We recommend
the following steps to avoid conflicts:

1.  **Disable real-time monitoring**— disable real-time
    monitoring by the antivirus software for the following:

    -   C:\\Program Files\\<DPM Installation path>\XSD folder

    -  	C:\\Program Files\\<DPM Installation path>\Temp folder

    -   Drive letter of Modern Backup Storage volume

    -   Replica and transfer logs—To do this, disable real-time monitoring of
        **dpmra.exe**, which is located in the folder **Program Files\\Microsoft Data Protection Manager\DPM\bin**. Real-time monitoring degrades performance
        because the antivirus software scans the replicas each time DPM
        synchronizes with the protected server, and scans all affected files
        each time DPM applies changes to the replicas.

    -   Administrator console—To avoid an impact on performance disable
        real-time monitoring of the **csc.exe** process. The csc.exe
        process is the C\\# compiler and real-time monitoring can degrade
        performance because the antivirus software scans files that the csc.exe
        process emits when it generates XML messages.**CSC.exe** is located in the following paths:

        - \\Windows\\Microsoft.net\\Framework\\v2.0.50727\\csc.exe
        - \\Windows\\Microsoft.NET\\Framework\\v4.0.30319\\csc.exe

2.  **Disable real-time monitoring on the Protected Server** — Disable the real time monitoring of **dpmra.exe**, which is located in the folder C:\Program Files\Microsoft Data Protection Manager\DPM\bin, on the protected server.

3. **Configure anti-virus software to delete the infected files on protected servers and the DPM server**— To prevent data corruption of replicas and recovery points, configure the antivirus software to delete infected files, rather than automatically cleaning or quarantining them. Automatic cleaning and quarantining might cause the antivirus software to modify files, making changes that DPM cannot detect.

You should run a manual synchronization with a consistency. Check the job each time that the antivirus software deletes a file from the replica, even though the replica is marked as inconsistent


The default DPM installation folders for DPM are as follows:
- For DPM 2016 - C:\\Program Files\\Microsoft System Center 2016\\DPM
- For DPM 2019 - C:\\Program Files\\Microsoft System Center\\DPM

You can also run the following command to find the install folder path:

```
Reg query "HKLM\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Setup" /s /f "InstallPath"
```
