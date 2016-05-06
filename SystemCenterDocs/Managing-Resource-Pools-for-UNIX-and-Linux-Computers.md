---
title: Managing Resource Pools for UNIX and Linux Computers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b77acb7a-d380-4d4d-9e3e-de86e5c80cfc
---
# Managing Resource Pools for UNIX and Linux Computers
You can specify the resource pool that manages a particular UNIX or Linux computer. This capability allows you to create a resource pool dedicated to managing only UNIX and Linux computers.

The following procedures show how to change a resource pool for a managed UNIX or Linux computer, and how to configure certificates for a resource pool. Configuring certificates is required to maintain high availability in resource pools and must be performed whenever a resource pool is created and when a management server is added to a resource pool.

## Changing Resource Pools
Changing a resource pool for a UNIX or Linux computer is different than modifying the set of management servers that are members of resource pool, as described in [How to Create a Resource Pool](./How-to-Create-a-Resource-Pool.md). The following procedure does not modify the members of a resource pool, only what the resource pool manages.

#### To change resource pools

1.  Click **Administration**.

2.  In the navigation pane, click **Resource Pools**.

3.  In the **Tasks** pane, click **Change Resource Pool**.

4.  In the upper list, select the computers that you want to change to be managed by a different resource pool.

5.  In the lower list, select the resource pool to manage computers selected in the upper list.

6.  Click **Change**.

## Configure Certificates for Resource Pools
An additional task must be performed in order to configure UNIX and Linux computers for resource pools. Operations Manager uses certificates to authenticate access to the computers it is managing. When the Discovery Wizard deploys an agent, it retrieves the certificate from the agent, signs the certificate, deploys the certificate back to the agent, and then restarts the agent.

To configure high availability, each management server in the resource pool must have all the root certificates that are used to sign the certificates that are deployed to the agents on the UNIX and Linux computers. Otherwise, if a management server becomes unavailable, the other management servers would not be able to trust the certificates that were signed by the server that failed. The process for this task is as follows:

1.  Export the root certificates from each management server in the resource pool to a file.

2.  Import all the exported certificate files into each management server \(except for the file that was exported by that same server\).

#### To configure certificates for high availability

1.  Log on to a management server to start the process of exporting certificates.

2.  At the command prompt, change the directory to %ProgramFiles%\\System Center Operations Manager 2012\\Server.

3.  Run the following command, specifying a file name of your choosing such as **Server3.cert**:

    `scxcertconfig.exe – export <filename>`

4.  Copy the exported file to a shared directory that is accessible by all the management servers in the resource pool.

5.  Repeat the previous four steps until the shared directory contains all the exported certificate files from each management server in the resource pool.

6.  Log on to a management server to start the process of importing certificates.

7.  At the command prompt, change the directory to %ProgramFiles%\\System Center Operations Manager 2012\\Server.

8.  Run the following command for each exported certificate file \(except for the file that was exported by the current management server\):

    `scxcertconfig.exe –import <filename>`

    > [!NOTE]
    > If you attempt to import the certificate file that was exported by that same management server, the process will fail with an error message that the object or property already exists.

9. Repeat the previous three steps until all the certificate files have been imported to the applicable management servers in the resource pool.

10. Delete the certificate files from the shared directory. Although the file contains only the public key of the certificate, you should still treat it as a security\-sensitive file.

Perform this procedure whenever you add a new management server to the resource pool so that high availability is maintained.

## See Also
[General Tasks in Operations Manager_1](./General-Tasks-in-Operations-Manager_1.md)
[Managing Alerts](./Managing-Alerts.md)
[How to Suspend Monitoring Temporarily by Using Maintenance Mode](./How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md)
[Creating and Managing Groups](./Creating-and-Managing-Groups.md)
[Running Tasks in Operations Manager](./Running-Tasks-in-Operations-Manager.md)
[How to Create a Resource Pool](./How-to-Create-a-Resource-Pool.md)
[Using Operations Manager Shell](./Using-Operations-Manager-Shell.md)


