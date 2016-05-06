---
title: Improving performance with a backup network address
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78ff64ff-e0ec-4fd4-a7b7-6f9077bc04f1
---
# Improving performance with a backup network address
[!INCLUDE[dpm2012long](Token/dpm2012long_md.md)] allows you to configure a backup network address to ensure that [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] backups do not slow down your primary network. The backup network address is created when you put separate network adapters on the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server and the protected servers and connect them through a separate LAN. As a result, backup data traffic does not impact the primary network.

You can set up your backup network address using [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] Management Shell \(PowerShell\) cmdlets.

## Setting up your network
Before you can set up a backup network address, you need to:

1.  Ensure that the name resolution of the protected server on the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server can resolve the backup address of the protected server and vice versa.

2.  Configure the backup subnet and the corresponding subnet mask using Add\-DPMBackupNetworkAddress.

    > [!NOTE]
    > The subnet should cover the entire range of network addresses for the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server and the servers you intend to protect.

3.  Restart the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] agent on the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server and the protected computers. It may cause ongoing tasks to fail. Post a restart, watch out for alerts, and perform the recommended actions, if needed.

### Example
This example details the process of setting up a backup network address for a [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server protecting another server. All names and addresses are hypothetical and for illustration only.

The existing backup setup consists of dpm.x.y.com protecting ps.x.y.com. Name lookup using “nslookup” on either server returns the following IPs \(that is, each IP address is visible to each node\):

> [!NOTE]
> The name lookups must be performed on the FQDNs; for example, “nslookup ps.x.y.com”.

|Server|NIC address|
|----------|---------------|
|[!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server \(dpm.x.y.com\)|10.10.12.89|
|Protected computer \(ps.x.y.com\)|10.10.12.90|

Now, to set up a backup network, another NIC is added to each of the above servers and connected to another network such as 192.168.1.0\/24 with a corresponding subnet mask 255.255.255.0. When the network and NICs are configured, the name lookup using “nslookup” returns two addresses per server as given below.

|Server|Primary NIC address|Backup NIC address|
|----------|-----------------------|----------------------|
|[!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server|10.10.12.89|192.168.1.23|
|Protected computer|10.10.12.90|192.168.1.24|

We recommend that you verify whether the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server is able to ping the protected computer’s backup network address \(192.168.1.24\). Similarly, the protected computer should be able to ping the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server’s backup network address \(192.168.1.23\).

At this stage, backup LAN configuration information is added to the [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server as follows:

Add\-DPMBackupNetworkAddress \-DpmServername DPM \-Address 192.168.1.0\/24 \-SequenceNumber 1

> [!NOTE]
> The “Address” parameter specifies the backup network\/subnet.

The [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] agents on TestingServer and the protected server are restarted \(“net stop dpmra” followed by “net start dpmra” on each server\). 
 Finally, a backup task is triggered and the NIC used for backup data transfer verified using taskmgr\->networking. The backup task must correspond to a data source on the protected server.

> [!NOTE]
> Add\-DPMBackupNetworkAddress enables you to configure more than one backup network. You can also use the primary network as a fallback network while using the backup network. In the above example, the primary network could also have been added with SequenceNumber 2. As a result, if the primary network is removed and the name lookup of servers no longer returns 192.168.1.0\/24 addresses, [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] can automatically start using the primary network for backup data traffic.


