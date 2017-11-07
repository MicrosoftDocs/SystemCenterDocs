---
ms.assetid: 1e144c7f-4ab3-4f06-abd9-1c45dea099f9
title: Configure SLB VIPs using VMM service templates  in System Center Preview Virtual Machine Manager preview version 1711
description: This article explains about how to configure SLB VIPs through VMM service templates using preview VMM 1711.
author: JYOTHIRMAISURI
ms.author: v-jysur
manager: riyazp
ms.date: 11/08/2017
ms.topic: article
ms.prod:  system-center-2016
ms.technology: virtual-machine-manager
monikerRange: 'sc-vmm-1711'
---
#	Configure SLB VIPs through VMM service templates (Technical Preview)

Software Defined Networking (SDN) in Windows 2016 can use Software Load Balancing (SLB) to evenly distribute network traffic among workloads managed by service provider and tenants. VMM 2016 only supports deploying SLB Virtual IPs (VIPs) using power shell.

With System Center VMM preview 1711, VMM supports configuration of SLB VIPs while deploying multi-tier application by using service templates and also supports both public and internal load balancing.


## Before you begin

Ensure the following prerequisites are met:

-  [Deployed SDN Network Controller](sdn-controller.md).
-  [Deployed SDN Software load balancer](sdn-slb.md).


## Procedure to create SLB VIPs

**Use the following steps**:

1. Specify the affinity to logical networks.
  - in VMM console click **Fabric** > **Network Service** > **Network Controller** > **Properties** > **Logical Network Affinity** page.
  - Specify the Front-end and Back-end networks available for load balancing and click **OK**.

    ![affinity](media/slb-vip/affinity.png)


2. Create a VIP template.
   - In the VMM console click **Fabric** > **Create VIP Template**.
   -  In the **Load Balancer VIP Template Wizard** > **Name**, specify the template name and description.  
    - In **Virtual IP port**, specify the port that will be used for the type of network traffic you want to balance.
    - In **Backend port**, specify the port on which the backend server is listening for requests.

        ![template properties](media/slb-vip/slb-properites.png)

   - In **Type** , specify a template type, click **Specific**. Select **Microsoft** for Manufacturer. Select **Microsoft network controller** for Model. Click **Next**.

        ![template type](media\slb-vip\template-type.png)

 - In **Protocol**, specify protocol options. Click **Next**.

    ![protocol](media/slb-vip/protocol-options.png)

  - In **Load Balancing method**, select the method  and click **Next**.

    ![load balancing method](media/slb-vip/load-balancing.png)

   - In **Health Monitors**, you can optionally specify that a verification should run against the load balancer at regular intervals. To add a health monitor, specify the protocol and the request. For example, entering the command GET makes an HTTP GET request for the home page of the load balancer and checks for a header response. You can also modify the response type, and monitoring interval, timeout, and retries. Note that the timeout should be less than the interval.

    ![load balancing method](media/slb-vip/health-monitor.png)

       - In **Summary** , confirm the Settings and click **Finish** to create the VIP template.

3. Configure SLB VIP while deploying Service
  - If the service template isn't open, click **Library** > **Templates** > **Service Templates** and open it.
  -  Click **Actions** > **Open Designer**.
  - In the **Service Template Designer**, click the **Service Template Components group** > **Add Load Balancer**.
  - Click the load balancer object. You'll identify it with the VIP template name.
  -  Click **Tool** > **Connector**. Click the Server connection associated with template and then click a NIC object to connect the load balancer to the adapter. In the **NIC properties**, check the address types and that the MAC address is static.

    > [!NOTE]

    > Server connection must be connected to the Back-End network interface of the service. The back-end network interface can be connected to either a One Connected VM Network or a network virtualized VM Network.

 - With the Connector enabled,  click the client connection associated with the load balancer and then click a logical network object.

    > [!NOTE]

    > Client connection must be connected to a Front-End network of the load balancer. This can be a Public VM network or a network virtualized VM network. A network virtualized VM Network is used for internal load balancing scenarios.

  - Save the service template in **Service Template** > **Save and Validate**.

**Example 1**: Configuring Service with ‘Public’ VM Network as front end. Here the ‘Backend’ network can be One connected or network virtualized VM network.

![slb vip example 1](media\slb-vip\example-1.png)


**Example 2**: Configuring Service with Front-end and Back-end connected to network virtualized VM Network ‘HNV VM Network’. This scenario is used for Internal load balancing.


![slb vip example 2](media\slb-vip\example-2.png)


## Set up the VIP for user access

When the service is deployed, VMM automatically selects a VIP from the reserved range in the static IP address pool, and assigns it to the load-balanced service tier. To enable users to connect to the service, after the service is deployed you need to determine the VIP and configure a DNS entry for it.

1.	After the service is deployed click **Fabric** > **Networking** > **Load Balancers**.
2.	Click **Show** > **Service** > **Load Balancer Information for Services** and expand the service to see which VIP is assigned.
3.	If users use the DNS name to access the service, request that the DNS administrator manually create a DNS entry for the VIP. The entry should be the name that users will specify to connect to the service.  For example, servicename.contosol.com.
