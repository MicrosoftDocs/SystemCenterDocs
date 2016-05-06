---
title: Set up the protection agent
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2810f7df-2eef-4b12-957f-701b13a42652
---
# Set up the protection agent
After data storage is in place, you can configure protection. The first step is to install the DPM protection agent software on each computer or server you want to protect with DPM. On the computer the agent identifies data that DPM can protect and recover, tracks changes to that data, and transfers the changes from the protected computer to the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server to synchronize the source data with the replica.

1.  [Install the DPM protection agent](assetId:///eb7c4a0f-5332-477f-8d08-53b8784fae1d)—You can install the DPM protection agent using a couple of methods. Including from the DPM console if the resource you want to protect isn’t behind a firewall, manually if it is, or using a server image.

2.  [Attach the DPM protection agent](assetId:///57b1cade-7050-4303-9be8-ac95aff1be0a)—If you install the agent on a computer or server behind a firewall, on a computer that already had the agent installed, or on a computer or server in a workgroup or untrusted domain, you’ll need to attach the agent running on the computer manually to the DPM server.

3.  [Update the DPM protection agent](assetId:///7ce0a27f-201d-4235-b9ea-7f2a6e19657f)—You can update the agent on a computer connected to the network, or one that’s unconnected.

4.  Configure firewall exceptions for the agent—If the protected computer or server is behind a firewall you’ll need to create exceptions for the DPM protection agent.

**Next steps**

After agents are installed you can create protection groups containing the servers, computers, and workloads you want to protect.

