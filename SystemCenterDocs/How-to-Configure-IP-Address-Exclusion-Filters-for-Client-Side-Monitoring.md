---
title: How to Configure IP Address Exclusion Filters for Client-Side Monitoring
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0529d193-725b-48bf-bfcc-eb153985e298
---
# How to Configure IP Address Exclusion Filters for Client-Side Monitoring
You can use client IP filters to choose the networks that you want to monitor. By applying filters, administrators can limit the scope of the monitored computers. By default, only localhost is monitored. If the IP filter list is empty, all IP addresses are monitored. Any IP addresses that fit the filter definitions are excluded from client\-side monitoring.

The following examples show how to use IP filters to monitor IP addresses.

## Exclude a Set of IP Addresses from Monitoring

#### Example: To monitor all IP addresses except 192.168.\*.\*

1.  To monitor all IP addresses, except some \(IP addresses 192.168.\*.\* in this example\), on the **Client Side Configuration** tab, in the **Configure client IP filter** section, click **Add**.

2.  On the **Client IP address filter** page, set the **Comparison Type** to **IP is in subnet**.

    > [!NOTE]
    > Comparison type has two values: **In subnet** excludes user IP addresses that match the IP addresses in the subnet. **Not in subnet** excludes the user IP addresses that do not match the IP addresses in the subnet.

3.  In the **IP address** box, enter the IP addresses that you want to exclude from monitoring. In this example, enter **192.168.0.0**.

4.  In the **Netmask** box, enter the part of the filter IP address and user IP address that have to be compared for equality. In this example, enter **255.255.0.0**.

5.  Click **OK**.

## Monitor a Specific Set of IP Addresses

#### Example: To monitor the specific set IP addresses 192.168.\*.\*

1.  To monitor a specific set of IP addresses \(in this example, IP addresses 192.168.\*.\*\), on the **Client Side Configuration** tab, in the **Configure client IP filter** section, click **Add**.

2.  On the **Client IP address filter** page, set the **Comparison Type** to **IP is not in subnet**.

3.  In the **IP address** box, enter the IP addresses that you want to monitor. In this example, enter **192.168.0.0**.

4.  In the **Netmask** box, enter the part of the filter IP address and user IP address that have to be compared for equality. In this example, enter **255.255.0.0**.

5.  Click **OK**.

## Monitor a Specific Set of IP Addresses and Exclude Some IP Addresses from that Set

#### Example: To monitor IP addresses 192.168.\*.\* and exclude IP addresses 192.168.10.\*

1.  To monitor a specific set of IP addresses and exclude some from that set \(in this example, only IP addresses 192.168.\*.\*, except IP addresses 192.168.10.\*\), you have to configure two filters. First, create the filter to scope to only IP addresses 192.168.\*.\*, and then a filter that excludes 192.168.10.\*. To create the first filter to monitor only IP addresses 192.168.\*.\*, on the **Client Side Configuration** tab, in the **Configure client IP filter** section, click **Add**.

2.  Set the **Compare Type** to **IP is not in subnet**.

3.  In the **IP address** box, enter the IP addresses that you want to monitor. In this example, enter **192.168.0.0**.

4.  In the **Netmask** box, enter the part of the filter IP address and user IP address that have to be compared for equality. In this example, enter **255.255.0.0**.

5.  Click **OK**.

6.  Then, create the second IP filter to exclude IP addresses 192.168.10.\*. On the **Client Side Configuration** tab, in the **Configure client IP filter** section, click **Add**.

7.  Set the **Compare Type** to **IP is in subnet**.

8.  In the **IP address** box, enter the IP addresses that you want to exclude from monitoring. In this example, enter **192.168.10.0**.

9. In the **Netmask** box, enter the part of the filter IP address and user IP address that have to be compared for equality. In this example, enter **255.255.255.0**.

10. Click **OK**.

## When to Use the IPv4 and IPv6 Filters
If the IPv4 protocol is the only protocol that is enabled on the web server, leave the **Use IPv6** check box blank.

If the IPv6 protocol is enabled on the web server, select the **Use IPv6** check box to add the IPv6 filter.


