---
title: How to install a WSUS server for VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b60fc35-916b-4e54-a17f-7094877d09d9
---
# How to install a WSUS server for VMM
To manage updates in Virtual Machine Manager \(VMM\), you must either set up a dedicated Windows Server Update Services \(WSUS\) server or use an existing WSUS server.

> [!NOTE]
> To use an existing WSUS server that is deployed in a System Center Configuration Manager environment, see [How to integrate fabric updates with Configuration Manager](How-to-integrate-fabric-updates-with-Configuration-Manager.md).

This topic covers either a local or remote WSUS server without Secure Sockets Layer \(SSL\).

### To install the WSUS server role for VMM

1.  Decide whether to install WSUS on the VMM management server or on a remote server. The WSUS server can be running Windows Server Technical Preview or Windows Server 2012 R2.

    We recommend setting up a remote WSUS server, especially if the VMM management server is managing a large number of computers. We also recommend that you set up a remote WSUS server if you are using a highly available VMM management server.

2.  Install the WSUS server role on the chosen server. Windows automatically selects any other server roles that are required such as Internet Information Services \(IIS\).

    For more information, see[Install the WSUS Server Role](http://technet.microsoft.com/library/hh852338.aspx).

3.  If you set up WSUS on a remote server, install a WSUS Administration Console on the VMM management server and then restart the VMM service. If you have a highly available VMM management server, on each node of the cluster, install a WSUS Administration Console and then restart the VMM service.

    Update management in VMM requires a WSUS Administration Console, which includes the respective WSUS Class Library Reference.

## See Also
[Managing fabric updates in VMM](Managing-fabric-updates-in-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


