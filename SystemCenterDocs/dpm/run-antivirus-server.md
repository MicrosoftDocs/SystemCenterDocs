---
title:  Run antivirus software on the DPM server
description: This article provides the details about running antivirus software on the DPM server.
manager: vvithal
ms.topic: article
author: v-anesh
ms.prod: system-center
keywords:
ms.date: 04/16/2020
ms.technology: data-protection-manager
ms.assetid: c0f4201b-53f7-45c8-af16-5522d0f10c6e
ms.author: v-anesh
---

# Run antivirus software on the DPM server

DPM is compatible with most popular antivirus software products. We recommend
the following steps to avoid conflicts:

1.  **Disable real-time monitoring**— On the DPM server, disable real-time
    monitoring by the antivirus software for the following:

    -   \\XSD folder

    -   \\Temp\\MTA folder

    -   Replica and transfer logs—To do this, disable real-time monitoring of
        dpmra.exe, which is located in the folder **Program Files\\Microsoft Data Protection Manager\\DPM\\bin**. Real-time monitoring           degrades performance
        because the antivirus software scans the replicas each time DPM
        synchronizes with the protected server, and scans all affected files
        each time DPM applies changes to the replicas.

    -   Administrator console—To avoid an impact on performance disable
        real-time monitoring of the csc.exe process
        (**Windows\\Microsoft.net\\Framework\\v2.0.50727\\csc.exe**). The csc.exe
        process is the C\# compiler and real-time monitoring can degrade
        performance because the antivirus software scans files that the csc.exe
        process emits when it generates XML messages.

2.  **Configure anti-virus software to delete infected files on protected
    servers and the DPM server**— To prevent data corruption of replicas and
    recovery points, configure the antivirus software to delete infected files
    rather than automatically cleaning or quarantining them. Automatic cleaning
    and quarantining might cause the antivirus software to modify files, making
    changes that DPM cannot detect.

    You should run a manual synchronization with a consistency. Check job each time that the antivirus software deletes a file from the   replica, even though the replica is marked as inconsistent.
