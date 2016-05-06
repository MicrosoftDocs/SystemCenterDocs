---
title: Installing Microsoft Monitoring Agent_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ef12a11-8215-4983-b92c-f59d534dc65d
---
# Installing Microsoft Monitoring Agent_1
You can obtain and install Microsoft Monitoring Agent in several ways. You can manually install it from the [!INCLUDE[omblue_1](../Token/omblue_1_md.md)] media or the Microsoft Download Center, or you can deploy it automatically by using the **Administration** pane of the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console. Additionally, you can opt in to automatically get the latest updates of the agent from Microsoft Update. Local collection is a lightweight monitoring solution that does not require any special configuration. You do not need databases or special accounts.

> [!IMPORTANT]
> Microsoft Update will not upgrade the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] agent from [!INCLUDE[sc2012sp1_long](../Token/sc2012sp1_long_md.md)] – [!INCLUDE[om12short](../Token/om12short_md.md)] to Microsoft Monitoring Agent. For more information, see [Microsoft Monitoring Agent Requirements and Compatibility](../Topic/Microsoft-Monitoring-Agent-Requirements-and-Compatibility.md) to make sure that a compatible version of the agent is running in your environment.

> [!NOTE]
> System Center versions before [!INCLUDE[omblue_1](../Token/omblue_1_md.md)] delivered the agent as the MOMAgent.msi file. You can still find the file that has the same name on the [!INCLUDE[omblue_1](../Token/omblue_1_md.md)] installation media. However, the file now installs Microsoft Monitoring Agent. If you get Microsoft Monitoring Agent from the Download Center, you can download either the 32\-bit \(MMASetup\-i386.exe\) version or the 64\-bit \(MMASetup\-AMD64.exe\) version of the agent.

To install Microsoft Monitoring Agent from the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] installation media, see [Install Agent Using the MOMAgent.msi Setup Wizard](http://go.microsoft.com/fwlink/?LinkId=323496).

To install Microsoft Monitoring Agent from the **Administration** pane in [!INCLUDE[omblue_2](../Token/omblue_2_md.md)], see [Install Agent on Windows Using the Discovery Wizard](http://go.microsoft.com/fwlink/?LinkId=323497).

### To install Microsoft Monitoring Agent from the Download Center for stand\-alone monitoring

1.  Open the Microsoft Monitoring Agent download page in the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=309771).

    > [!IMPORTANT]
    > Local collection requires Microsoft .NET Framework 3.5 and the Windows PowerShell 2.0 command\-line interface. Some features, such as downloadable Help and pre\-imported monitoring Windows PowerShell modules, are not available unless you have Windows PowerShell 3.0.

2.  Choose whether to install the 32\-bit \(MMASetup\-i386.exe\) or 64\-bit \(MMASetup\-AMD64.exe\) version of Microsoft Monitoring Agent, and follow the instructions to download the file.

3.  When the download is complete, run the file and follow the instructions.

4.  On the **Agent Setup Options** page, you can choose whether you want to connect the agent to [!INCLUDE[omblue_2](../Token/omblue_2_md.md)]. When you connect the agent with [!INCLUDE[omblue_2](../Token/omblue_2_md.md)], you can manually choose the management group that this agent will participate with in monitoring. If you do not select this option, the agent can still collect Application Performance Monitoring data locally. You can change your selection in the **Monitoring Agent** item in Control Panel.

    > [!IMPORTANT]
    > If you connected this installation of the agent to [!INCLUDE[omblue_2](../Token/omblue_2_md.md)], your System Center administrator must allow manual agent installations on the management server. This setting is controlled in the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console. Additionally, before System Center begins to accept monitoring traffic from your agent, the System Center administrator must approve the agent in the Pending Management view in the **Administration** pane of the [!INCLUDE[omblue_2](../Token/omblue_2_md.md)] console.

