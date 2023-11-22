---
ms.assetid: e598989d-0aa8-4eb4-b5f7-db27d2beb8a0
title: How to Manage Resource Pools
description: This article describes how to manage and configure resource pools in Operations Manager.
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 04/24/2023
ms.custom: UpdateFrequency2, engagement-fy23
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# How to manage resource pools

::: moniker range=">= sc-om-1801 <= sc-om-1807"

[!INCLUDE [eos-notes-operations-manager.md](../includes/eos-notes-operations-manager.md)]

::: moniker-end

A Resource Pool is a collection of management servers and/or gateway servers used to distribute work among themselves and take over work from a failed member.  In this article, we'll cover how to create and modify resource pools and their membership, and configure a resource pool dedicated to monitor UNIX and Linux computers.


## To create a resource pool

1.  Sign in to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Select **Administration**.

3.  In the navigation pane, select **Resource Pools**.

4.  In the **Tasks** pane, select **Create Resource Pool**.

5.  In the **Create Resource Pool** wizard, on the **General Properties** page, enter a name and, optionally, a description for the resource pool, and select **Next**.

6.  On the **Pool Membership** page, select **Add**.

7.  In the **Member Selection** window, enter text to filter the search results if desired, and select **Search**. If you select **Search** without entering anything in the filter field, all available management servers will be displayed.

8.  In **Available items**, select the servers that you want in the resource pool, select **Add**, and select **OK**.

9. Select **Next**.

10. On the **Summary** page, review the settings and select **Create**.

11. When the wizard completes, select **Close**.

## Modifying resource pool membership

When you view the resource pools in the **Administration** workspace, you'll see that resource pools that you create have a manual membership type, and resource pools created when Operations Manager was installed have an automatic membership type, as shown in the following image.

![Screenshot showing Resource Pool Membership Type.](./media/manage-resource-pools-manage/om2016-resource-pool-membership-type.png)

By default, all management servers are members of the resource pools created when Operations Manager is installed, and any management servers added to the management group are automatically added to the resource pools that have an automatic membership type. You can remove individual management servers from those resource pools; however, that will change the membership type to manual. If you add a management server to a management group after the membership type of the resource pools created when Operations Manager was installed is changed to manual, you must add the management server to the resource pool manually.

> [!NOTE]
> The membership of the All Management Servers Resource Pool is read-only. To change its membership from automatic to manual, run the following PowerShell code in the Operations Manager Command Shell:
>  
> ```powershell
> Get-SCOMResourcePool -DisplayName "All Management Servers Resource Pool" | Set-SCOMResourcePool -EnableAutomaticMembership 0
> ```

#### To remove a member from an automatic resource pool

1.  Sign in to the Operations console with an account that is a member of the Operations Manager Administrators role.

2.  Select **Administration**.

3.  In the navigation pane, select **Resource Pools**.

4.  In the results pane, select the resource pool that you want to modify.

5.  In the **Tasks** pane, select **Manual Membership**, and select **Yes** in the **Manual Membership** message.

    > [!IMPORTANT]
    > When you select **Yes**, the membership type of the selected resource pool changes to manual. Even if you make no changes to the resource pool membership and cancel the properties dialog, the membership type will remain manual after this step.

6.  On the **General Properties** page for the resource pool, select **Next**.

7.  On the **Pool Membership** page, select the management servers that you want to remove from the resource pool, select **Remove**, and select **Next**.

8.  On the **Summary** page, select **Save**.


## Configure certificates for UNIX and Linux dedicated resource pools

An additional task must be performed in order to configure management servers that are members of a resource pool dedicated for managing UNIX and Linux computers. Operations Manager uses certificates to authenticate access to the computers it's managing. When the Discovery Wizard deploys an agent, it retrieves the certificate from the agent, signs the certificate, deploys the certificate back to the agent, and then restarts the agent.

To configure high availability, each management server in the resource pool must have all the root certificates that are used to sign the certificates that are deployed to the agents on the UNIX and Linux computers. Otherwise, if a management server becomes unavailable, the other management servers wouldn't be able to trust the certificates that were signed by the server that failed. The process for this task is as follows:

1.  Export the root certificates from each management server in the resource pool to a file.

2.  Import all the exported certificate files into each management server (except for the file that was exported by that same server).

#### To configure certificates for high availability

1.  Sign in to a management server to start the process of exporting certificates.

2.  At the command prompt, change the directory to %ProgramFiles%\System Center Operations Manager\Server.

3.  Run the following command, specifying a file name of your choosing such as **Server3.cert**:

    `scxcertconfig.exe -export <filename>`

4.  Copy the exported file to a shared directory that is accessible by all the management servers in the resource pool.

5.  Repeat the previous four steps until the shared directory contains all the exported certificate files from each management server in the resource pool.

6.  Sign in to a management server to start the process of importing certificates.

7.  At the command prompt, change the directory to %ProgramFiles%\System Center Operations Manager\Server.

8.  Run the following command for each exported certificate file (except for the file that was exported by the current management server):

    `scxcertconfig.exe -import <filename>`

    > [!NOTE]
    > If you attempt to import the certificate file that was exported by that same management server, the process will fail with an error message that the object or property already exists.

9. Repeat the previous three steps until all the certificate files have been imported to the applicable management servers in the resource pool.

10. Delete the certificate files from the shared directory. Although the file contains only the public key of the certificate, you should still treat it as a security-sensitive file.

Perform this procedure whenever you add a new management server to the resource pool so that high availability is maintained.

## Next steps

For information about deployment considerations for resource pools, see [Planning Resource Pool Design](plan-resource-pool-design.md).
