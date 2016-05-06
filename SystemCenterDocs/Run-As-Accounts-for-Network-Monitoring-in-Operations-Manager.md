---
title: Run As Accounts for Network Monitoring in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3631fac-5b64-4903-8343-8254b107db15
---
# Run As Accounts for Network Monitoring in Operations Manager
[!INCLUDE[om12long](./Token/om12long_md.md)] uses Run As accounts to discover and monitor network devices. The credentials in the Run As account enable management servers to communicate with the network devices. You can monitor devices that use SNMP v1, v2, and v3.

Network devices that use SNMP v1 or v2 require a Run As account that specifies a community string, which acts like a password to provide read\-only access to the device.

Each network device that uses SNMP v3 requires a unique Run As account that provides the following credentials:

-   User name: Obtained from device configuration.

-   Context: Name that together with the user name determines the access permissions of a request sent to the SNMPv3 agent.

-   Authentication protocol: MD5 for Message Digest 5, SHA for Secure Hash Algorithm, or NONE

-   Authentication key: String consisting of 1 to 64 characters; required if the authentication protocol is MD5 or SHA

-   Privacy protocol: DES for Data Encryption Standard, AES for Advanced Encryption Standard, or NONE

-   Privacy key: String consisting of 1 to 64 characters; required if the privacy protocol is DES or AES

    > [!NOTE]
    > The authentication key and privacy key are masked as you enter them.

You can create the required Run As accounts when you create a network devices discovery rule, or you can create the Run As accounts beforehand and then select the appropriate account when you create the discovery rule.

Two Run As profiles are created when you install [!INCLUDE[om12short](./Token/om12short_md.md)]: SNMP Monitoring Account and SNMPv3 Monitoring Account. When you create a discovery rule, the Run As accounts you create for network device discovery are automatically associated with the appropriate Run As profile.

## See Also
[Monitoring Networks by Using Operations Manager](./Monitoring-Networks-by-Using-Operations-Manager.md)
[How to Discover Network Devices in Operations Manager](./How-to-Discover-Network-Devices-in-Operations-Manager.md)
[Network Device Discovery Settings](./Network-Device-Discovery-Settings.md)
[Tuning Network Monitoring](./Tuning-Network-Monitoring.md)
[How to Delete or Restore a Network Device in Operations Manager](./How-to-Delete-or-Restore-a-Network-Device-in-Operations-Manager.md)
[Viewing Network Devices and Data in Operations Manager](./Viewing-Network-Devices-and-Data-in-Operations-Manager.md)
[Security for Servers Performing Network Discovery](./Security-for-Servers-Performing-Network-Discovery.md)
[Network Devices Supported for Discovery by Operations Manager](./Network-Devices-Supported-for-Discovery-by-Operations-Manager.md)
[Reports for Network Monitoring in Operations Manager](./Reports-for-Network-Monitoring-in-Operations-Manager.md)


