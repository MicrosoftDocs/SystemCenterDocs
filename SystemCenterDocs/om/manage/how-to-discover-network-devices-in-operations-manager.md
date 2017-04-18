---
title: How to Discover Network Devices in Operations Manager
description: This article describes how to discover network devices to be monitored by Operations Manager.   
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 01/25/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid:  b23cc152-e396-4499-bf7c-cf208bf3741f
---

# How to discover network devices in Operations Manager

>Applies To: System Center 2016 - Operations Manager

System Center Operations Manager performs network discovery by running discovery rules that you create. Each time the rule runs, it will attempt to find new devices within its definition or changes to devices that were previously discovered.

> [!NOTE]
> Discovery of a large number of devices can take several hours to complete.

Each management server or gateway server can run only one discovery rule. You specify a single management server or gateway server to run the discovery rule and a management server resource pool to perform the actual monitoring of the network devices. If you plan to monitor more than 1000 network devices, you should use two resource pools and split the number of devices evenly between the pools.

> [!NOTE]
> If you create discovery rules on multiple management servers, you should create a management pool for each and make sure that each discovery defines a different set of devices. If a single device is managed in different pools, it will not be able to be deleted.

## Prerequisites

To create a network devices discovery rule, you need the following information:

-   The IP address or FQDN of each device that you want to discover and monitor.

    > [!NOTE]
    > Operations Manager can identify connected devices in a recursive discovery that use an IPv6 address; however, the initial device that is discovered must use an IPv4 address.

-   The version of SNMP that each devices uses. This can be SNMP v1, v2, or v3.

-   The SNMP community string of each SNMP v1 or v2 device that you want to discover and monitor.

-   The user name, context, authentication protocol, authentication key, privacy protocol, and privacy key for each SNMP v3 device that you want to discover and monitor.  

-   If you are using recursive discovery and you only want to discover network devices that have interfaces whose addresses fall within a specified IP address range, you must have the IP address range.

-   The name of the management server resource pool that will monitor the discovered devices.

> [!NOTE]
> When Network Load Balancing (NLB) is used, the destination MAC address for the network adapter (cluster adapter) uses the format of 02-BF-1-2-3-4 and the cluster hosts use a format of 02-h-1-2-3-4, where h is the host's priority within the cluster (set in the Network Load Balancing Properties dialog box). Operations Manager will create a network connection between the devices using 02-h-1-2-3-4 to the destination MAC address of 02-BF-1-2-3-4.

### Firewall configuration

You must ensure the following firewall configuration before creating the network devices discovery rule:

-   All firewalls between the management server and the network devices need to allow SNMP (UDP) and ICMP bi-directionally, and ports 161 and 162 need to be open bi-directionally. This includes Windows Firewall on the management server itself.

-   If your network devices are using a port other than 161 and 162, you need to open bi-directional UDP traffic on these ports.

> [!IMPORTANT]  
> Note for customers who used EMC Solutions for Microsoft System Center Operations Manager: EMC Smarts included tools to create an isolation layer to prevent denial of service attacks. In System Center 2016 - Operations Manager, you need to protect your network against packet storms by using external tools.  

## To create a network devices discovery rule

1.  Open the Operations console with an account that is a member of Operations Manager Administrators.

2.  In the **Administration** workspace, right-click **Administration**, and then click **Discovery Wizard**.

3.  On the **What would you like to manage?** page, select **Network devices**, and then click **Next**.

4.  On the **General Properties** page, do the following:

    1.  In the Name box, type a name, such as **My Network Devices**.

    2.  In the **Available servers** drop-down list, select a management server that has access to the devices you are discovering to run the discovery rule. Servers that already run a network devices discovery rule will not be listed.

    3.  Click **Create Resource Pool** to create a management server resource pool for monitoring the devices, or in the **Select a resource pool** drop-down list, click a resource pool, and then click **Next**.

5.  On the **Discovery Method** page, select **Explicit discovery** or **Recursive discovery**, and then click **Next**.

    > [!NOTE]
    > If you know all of the network devices that you want discovered, you should use explicit discovery. Recursive discovery can discover devices that you have no business need to monitor and as a result, can increase the administrative workload of monitoring your network

6.  On the **Default Accounts** page, if you are discovering only SNMP v3 devices, click **Next**. If you are discovering any SNMP v1 or v2 devices, do the following:

    1.  If you previously created Run As accounts for SNMP v1 or v2 devices, the Run As accounts will be listed and you can select a listed account for this discovery rule. If no accounts are listed or the listed accounts are not appropriate for this discovery rule, continue to the next step.

        > [!NOTE]
        > If you are creating a recursive discovery rule, you must create a default account, which will be used to connect to and discover devices connected to the device that you specify on the **Devices** page. If you do not create and select an account on the **Default Accounts** page, the recursive discovery will discover the device that you specify but will not discover devices connected to it.

    2.  Click **Create Account**.

    3.  In the **Create Run As Account Wizard**, on the **Introduction** page, click **Next**.

    4.  In the **Display Name** text box, type a name such as **Router Credentials**.

    5.  Optionally, type a description in the **Description** box. Click **Next**.

    6.  On the **Credentials** page, type the SNMP community string for your network devices, and then click **Create**.

        > [!NOTE]
        > If the rule will discover devices that use more than one SNMP community string, you must create one Run As account for each SNMP community string.

    7.  On the **Default Accounts** page, you will see that the Run As account that you just created is listed in the **SNMPv1/v2 Run As accounts** box and is selected. Click **Next**

7.  If you are adding an SNMP v1 or v2 device, on the **Devices** page, do the following:

    > [!NOTE]
    > This procedure describes how to add devices one at a time. You can also add multiple devices by clicking the **Import** button to import a text file with a list of IPv4 addresses. This file should have a single IP address on each line. After import, the IP addresses are part of the discovery rule and the text file is no longer needed.

    1.  Click **Add** to open the **Add Device** page.

    2.  On the **Add Device** page, type the IPv4 address or FQDN of the device that you want to discover and monitor. If you are creating a recursive discovery, the discovery will access this device to locate other devices on your network.

    3.  In **Access Mode**, select **ICMP**, **SNMP**, or **ICMP and SNMP**. This specifies how the device will be discovered and how it will be monitored after discovery.

        > [!NOTE]
        > If you select **ICMP and SNMP**, the device must be accessible by both protocols or it will not be discovered. If you select **ICMP**, discovery will be limited to the specified device, and monitoring will be limited to whether the device is online or offline.

    4.  In **Port number**, retain the default port (161) or select another port number for the device.

    5.  Select **v1 or v2** from the **SNMP version** drop-down box.

    6.  In **SNMP V1 or V2 Run As account**, select **Use selected default account**. If you specify an account in this window, then only the specified account will be used for discovery.

        > [!NOTE]
        > If you are discovering devices that use more than one SNMP community string and therefore have multiple Run As accounts, you can retain the default value of **Use selected default accounts** in the **SNMP V1 or V2 Run As account** field. When you do this, the Network Devices Discovery Wizard will attempt to use the community string for every Run As account that you selected on the **Default Accounts** page against every device that you add to the discovery list until a community string succeeds.

    7.  Click **OK**. This returns you to the **Devices** page and you should see the device that you just added listed.

        > [!NOTE]
        > The **Advanced Discovery Settings** button on the **Devices** page opens a dialog box that contains a number of settings that you can use to configure discovery of network devices, such as number of retry attempts. If you know you are going to discover more than 1500 devices, you must change the **Maximum number of devices to discover** in **Advanced Discovery Settings**.

    8.  Add other SNMP v1 or v2 devices and Run As accounts as necessary, and then click **Next**.

        > [!NOTE]
        > If you add multiple devices to the rule, you can set a common Run As Account for all of them by selecting all of the devices and then clicking **Edit**.

8.  If you are adding an SNMP v3 device, on the **Devices** page, do the following:

    > [!NOTE]
    > This procedure describes how to add devices one at a time. You can also add multiple devices by clicking the **Import** button to import a text file with a list of IPv4 addresses. This file should have a single IP address on each line.  After import, the IP addresses are part of the discovery rule and the text file is no longer needed. Each device requires an SNMP v3 credential. After you import the addresses, you can edit each device to add the credential or you can select multiple devices and provide the same credential for all selected devices.

    1.  Click **Add**. This opens the **Add Device** page.

    2.  On the **Add a Device** page, type the IPv4 address or FQDN of the SNMP v3 device that you want to discovery and monitor.

    3.  In **Access Mode**, select **ICMP**, **SNMP**, or **ICMP and SNMP**. This specifies how the device will be discovered and how it will be monitored after discovery.

        > [!NOTE]
        > If you select **ICMP and SNMP**, the device must be accessible by both protocols or it will not be discovered. If you select **ICMP**, discovery will be limited to the specified device, and monitoring will be limited to whether the device is online or offline.

    4.  In **Port number**, retain the default port (161) or select another port number for the device.

    5.  Select **v3** from the **SNMP version** drop-down box.

    6.  Click **Add SNMP V3 Run As Account**.

        > [!NOTE]
        > Each SNMP v3 device requires its own Run As account.

    7.  In the **Create Run As Account Wizard**, on the **Introduction** page, click **Next**.

    8.  Type a value in the **Display name** box, optionally type a description, and then click **Next**.

    9. On the **Credentials** page, enter the values for **User name**, **Context**, **Authentication protocol**, **Authentication key**, **Privacy protocol** and **Privacy key** for the SNMP v3 device. Click **Create**.

        Click **OK**. This returns you to the **Devices** page.

    10. > [!NOTE]
        > The **Advanced Discovery Settings** button on the **Devices** page opens a dialog box that contains a number of settings that you can use to configure discovery of network devices, such as number of retry attempts. If you know you are going to discover more than 1500 devices, you must change the **Maximum number of devices to discover** in **Advanced Discovery Settings**. For more information on the available settings, see [How to configure network device discovery settings](../../scom/manage-monitor-networkdevice-discovery-settings.md).

    11. Add other SNMP v3 devices and Run As accounts as necessary, and then click **Next**.

9. If you are creating an explicit discovery rule, go to the next step. If you are creating a recursive discovery rule, do the following:

    1.  On the **Include Filters** page, leave the default setting to discover all devices. If you want to filter for only a particular set of devices, select **Discover only network devices within the specific IP address ranges**, and then click **Add** to configure a filter. Click **Next** when complete.

        In the **IP address range** field, you can enter addresses such as the following:

        -   **10.193.220.25** (a single IP address to include one specific device)

        -   **172.23.136<1-100>** (include any IP address from 1 to 100 in 172.23.136/255.255.255.0)

        -   **172.23.135.\*** (include any IP address in 172.23.135/255.255.255.0)

        > [!NOTE]
        > For more information on formatting an IP address range, see [How to configure network device discovery settings](../../scom/manage-monitor-networkdevice-discovery-settings.md).

    2.  On the **Exclude Filters** page, leave the default setting to not exclude any of the discovered devices. If you want to filter an IP address from being discovered, click **Add** and specify an IP address. Click **Next** when complete.

    > [!NOTE]
    > Although the dialog box states that an IP address or host name can be entered for an exclude filter, only an IP address is valid. A host name cannot be specified here.

10. On the **Schedule Discovery** page, either accept the default value of Saturday at 2 AM or specify an alternate schedule, and then click **Next**.

    > [!NOTE]
    > We recommend that you do not run network discovery more frequently than twice per week because network discovery can take hours to complete and may place an excessive load on the management server or gateway server during discovery.

11. Review your settings on the **Summary** page, and then click **Finish** when you are ready to proceed.

12. You will see a Warning popup that reads  "The following accounts need to be distributed to the health service *management server name* in order for the discovery to work: *DiscoveryName\Run As Account*. Would you like Operations Manager to distribute the accounts? Yes: Distribute the accounts and create the discovery. No: Do not distribute the accounts and do not create the discovery."  Click **Yes**.

13. The wizard completes and you see the message **The network discovery rule was successfully created**. Ensure **Run the network discovery rule after the wizard is closed** is selected if you want the rule to run immediately, and then click **Close**. The network devices discovery rule is created. If you did not select **Run the network discovery rule after the wizard is closed**, the discovery rule will run on the scheduled day and time.

    > [!NOTE]
    > It can take several minutes for the network discovery rule to appear in the Operations console and begin discovery if you select **Run the network discovery rule after the wizard is closed**.

14. To monitor the progress of network device discovery, watch the **status** column of the discovery rule. It will provide the following statuses while it is running, along with the number of devices that it has located:

    1.  **Probing**

        During the probing phase, Operations Manager attempts to contact device using the specified protocol, as follows:

        -   ICMP only: ping the device

        -   ICMP and SNMP: contact the device using both protocols

        -   SNMP only: uses the SNMP GET message

    2.  **Processing**

        After probing is complete, Operations Manager processes all of the components of the device, such as ports and interfaces, memory, processors, VLAN membership, and HSRP groups.

    3.  **Post Processing**

        Operations Manager correlates network device ports to the servers that the ports are connected to, inserts items into the operational database, and associates Run As accounts.

15. To confirm the successful discovery and management of the devices, select **Device Management**, and then select **Network Devices**. You should see your discovered devices listed in the results pane.

If a network device discovery rule fails, the device or devices will be listed in **Network Devices Pending Management**. This can be a subset of the devices specified in the discovery rule. Use one of the following methods to retry the discovery:

-   To attempt to discover that specific device only, right-click the device in **Network Devices Pending Management** and then click **Submit rediscovery**.

-   To retry a recursive discovery that begins with that device, click **Discovery Rules**, right-click the respective rule, and then click **Run**.

### To change the discovery type of a network devices discovery rule

1.  In the Operations console, in the **Administration** workspace, click **Discovery Rules**.

2.  In the results pane, right-click the discovery rule that you want to change and click **Properties**.

3.  On the **General Properties** page, click **Next**.

4.  On the **Discovery Method** page, click the type of discovery you want the rule to use.

5.  Follow the instructions for creating a discovery rule to complete the remaining wizard pages, and then click **Save**.

## Next steps

- To view information about the network devices you are monitoring, see [Viewing Network Devices and Data in Operations Manager](../../scom/manage-monitor-networkdevice-viewing-data.md).  

- To understand how to configure what to monitor and alert with your network devices, see [How to configure monitoring of network devices](../../scom/manage-monitor-networkdevice-configure-monitoring.md).  

- To understand how to stop monitoring a network device, see [How to Delete or Restore a Network Device in Operations Manager](../../scom/manage-monitor-networkdevice-delete-restore.md). 
