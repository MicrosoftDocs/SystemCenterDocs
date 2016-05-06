---
title: How to Install the Runbook Designer for System Center 2012 - Orchestrator
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d282490-cb50-4011-a6eb-47faf10bb12a
---
# How to Install the Runbook Designer for System Center 2012 - Orchestrator
Use the following steps to install the [!INCLUDE[orchlong](../Token/orchlong_md.md)] Runbook Designer on a single computer.

### To install the [!INCLUDE[orchshort](../Token/orchshort_md.md)] Runbook Designer on a single computer

1.  On the server where you want to install the [!INCLUDE[orchshort](../Token/orchshort_md.md)] Runbook Designer, start the **[!INCLUDE[orchlong](../Token/orchlong_md.md)] Setup Wizard**.

    To start the **[!INCLUDE[orchlong](../Token/orchlong_md.md)] Setup Wizard**, on your product media or network share, double\-click **SetupOrchestrator.exe**.

    > [!NOTE]
    > Before you begin the install of the Runbook Designer, close any open programs and ensure that there are no pending restarts on the computer. For example, if you have installed a server role by using [!INCLUDE[smshort](../Token/smshort_md.md)] or have applied a security update, you might have to restart the computer, and then log on to the computer with the same user account to finish the installation of the server role or the security update.

2.  On the main **[!INCLUDE[orchlong](../Token/orchlong_md.md)] Setup Wizard** page, click **Runbook Designer**.

    > [!WARNING]
    > If Microsoft .NET Framework 3.5 Service Pack 1 is not installed on your computer, a dialog box appears asking if you want to install .NET Framework 3.5 SP1. Click **Yes** to proceed with the installation.

3.  Your computer is checked for required hardware and software. If your computer meets all of the requirements, proceed to the next step.

    If a prerequisite is not met, a page displays information about the prerequisite that has not been met and how to resolve the issue. Use the following steps to resolve the failed prerequisite check:

    1.  Review the items that did not pass the prerequisite check. For some requirements, such as Microsoft .NET Framework 4, you can use the link provided in the Setup Wizard to install the missing requirement. The Setup Wizard can install or configure other prerequisites, such as the Internet Information Services \(IIS\) role.

    2.  After you resolve the missing prerequisites, click **Verify prerequisites again**.

    3.  Click **Next** to continue.

4.  On the **Select the installation location** page, verify the installation location for [!INCLUDE[orchshort](../Token/orchshort_md.md)], and then click **Next**.

5.  Review the **Installation summary** page, and then click **Install**.

    The **Installing features** page appears and displays the installation progress.

6.  On the **Setup completed successfully** page, optionally indicate whether you want to start the Runbook Designer, and then click **Close** to complete the installation.

### To connect a Runbook Designer to a management server

1.  In the Runbook Designer, select the **Connect to a server** icon in the navigation pane under the **Connections** pane.

    > [!NOTE]
    > If the Runbook Designer is connected to another management server, the **Connect to a server** icon is disabled. Click the **Disconnect** icon before you connect to a different management server.

2.  In the **System Center Orchestrator 2012 Connection** dialog box, enter the name of the server that hosts your [!INCLUDE[orchshort](../Token/orchshort_md.md)] management server, and then click **OK**.

### To enable network discovery

1.  On the desktop of your computer running Windows server, click **Start**, click **Control Panel**, click **Network and Internet**, click **Network and Sharing Center**, click **Choose Home group and Sharing Options**, and then click **Change advanced sharing settings**.

2.  To change the **Domain** profile, if needed, click the **Arrow** icon to expand the section options and make any necessary changes.

3.  Select **Turn on network discovery**, and then click **Save changes**.

    If you are prompted for an administrator password or confirmation, type the password or provide confirmation.

## See Also
[Install Individual Orchestrator Features](../Topic/Install-Individual-Orchestrator-Features.md)

