---
title: Network Device Discovery Settings
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30f03c58-9851-4e8a-9c57-3aeb40d968d3
author:mgoedtel
manager:cfreemanwa
---
# Network Device Discovery Settings
[!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] offers a number of settings that you can use to configure discovery of network devices. The following table explains the available settings and how to configure them in the Network Devices Discovery Wizard.  
  
|Setting|Location|Notes|  
|-----------|------------|---------|  
|**Name or IP address**|**Devices** page, **Add** button|Enter either a fully qualified domain name \(FQDN\) or an IPv4 address. [!INCLUDE[om12short](../../om/manage/includes/om12short_md.md)] can identify connected devices in a recursive discovery that use an IPv6 address; however, the initial device that is discovered must use an IPv4 address.|  
|**Access mode**|**Devices** page, **Add** button|Select either **ICMP and SNMP**, **ICMP**, or **SNMP**. This specifies the protocol that will be used for both discovery and monitoring. If you select **ICMP and SNMP**, the device must be accessible by both protocols, or discovery will fail.|  
|**SNMP version**|**Devices** page, **Add** button|Select either **v1 or v2** or **v3**. SNMP v1 and v2 devices can use the same Run As account. SNMP v3 devices require a different format Run As account.|  
|**Port number**|**Devices** page, **Add** button|The default port is 161. You can change this value if you are discovering a network device that uses another port.|  
|**Run As account**|**Devices** page, **Add** button|The available accounts in the menu are populated based on your selection in the **SNMP version** box. You can create the appropriate Run As account by clicking **Add SNMP***version***Run As Account**.|  
|**Number of retry attempts**|**Devices** page, **Advanced Discovery Settings** button|This setting specifies how many times the management server should attempt to contact the network device before reporting that discovery failed.|  
|**ICMP time\-out \(in milliseconds\)**|**Devices** page, **Advanced Discovery Settings** button|If you specify **ICMP and SNMP** or **ICMP** for **Access mode**, the management server attempts to contact the network device by using **ping**. The default setting is 1500 milliseconds \(1.5 seconds\).|  
|**SNMP time\-out \(in milliseconds\)**|**Devices** page, **Advanced Discovery Settings** button|If you specify **ICMP and SNMP** or **SNMP** for **Access mode**, the management server attempts to contact the network device by using SNMP. The default setting is 1500 milliseconds \(1.5 seconds\).|  
|**Maximum number of devices to discover**|**Devices** page, **Advanced Discovery Settings** button|This setting applies during recursive discovery and sets a limit on the number of devices to discover. The default is 1500. If you know you are going to discovery more than 1500 devices, you must change this setting.|  
|**IP address range**|**Include Filters** page, **Add** button, when configuring a recursive discovery rule|Use this field to limit the recursive discovery to IP addresses that meet the specified criteria. This field uses a wildcard format.<br /><br />For example, if you enter **192.168.1.\***, the discovery rule discovers devices that use any IP address between 192.168.1.1 and 192.168.1.255.<br /><br />If you enter **192.168.1.<1\-140>**, the discovery rule discovers devices that use any IP address between 192.168.1 and 192.168.140.<br /><br />For more options, see [IP Address Range for Network Device Filtering](assetId:///a817c0cc-fc9a-4945-82c9-13dd439dd3b0).|  
|**Included device types**|**Include Filters** page, **Add** button, when configuring a recursive discovery rule|Any devices that you select are included in the recursive discovery. Clear the selection for any type of device that you do not want discovered.|  
|**Include only network devices with the following system attributes \(OIDs\) \- Name**|**Include Filters** page, **Add** button, when configuring a recursive discovery rule|If you enter a value here, only devices with a matching name are discovered. This field allows a wildcard format. For more options, see [IP Address Range for Network Device Filtering](assetId:///a817c0cc-fc9a-4945-82c9-13dd439dd3b0).|  
|**Include only network devices with the following system attributes \(OIDs\) – Object ID \(OID\)**|**Include Filters** page, **Add** button, when configuring a recursive discovery rule|If you enter a value here, only devices with a matching OID are discovered. This field allows a wildcard format. For more options, see [IP Address Range for Network Device Filtering](assetId:///a817c0cc-fc9a-4945-82c9-13dd439dd3b0).|  
|**Include only network devices with the following system attributes \(OIDs\) – Description**|**Include Filters** page, **Add** button, when configuring a recursive discovery rule|If you enter a value here, only devices with a matching description are discovered. This field allows a wildcard format. For more options, see [IP Address Range for Network Device Filtering](assetId:///a817c0cc-fc9a-4945-82c9-13dd439dd3b0).|  
|**IP Address or Host Name**|**Exclude Filters** page, **Add** button, when configuring a recursive discovery rule|Enter either a fully qualified domain name \(FQDN\), an IPv4 address, or an IPv6 address to exclude from discovery. You can add multiple IP address individually.|  
  
## <a name="bkmk_wildcardmatchingforipaddressrange"></a>Wildcard Matching for IP Address Range  
Wildcard pattern matching is done from left to right, one character or basic wildcard pattern at a time. The pattern and the incoming string must match exactly, so for example, the pattern *abc* does not match the string *abcd*. Compound patterns consist of basic patterns separated by an ampersand \(&\) or a tilde \(~\). If the first character of a compound pattern is an ampersand or tilde, it is interpreted as if there were an asterisk at the beginning. For example, the pattern ~\*\[0\-9\] matches any string that does not contain a digit. A trailing ampersand can only match an empty string, and a trailing tilde indicates “except for an empty string.”  
  
Spaces are significant characters, and are subject to matching.  
  
The wildcard patterns consist of the following.  
  
|Character|Description|Example|  
|-------------|---------------|-----------|  
|?|Matches any single character|Example?.com matches Example1.com andExample2.com, but not Example01.com|  
|\*|Matches zero or more characters|Example\*.com matches example.com, example1.com, and examplereallylong.com|  
|\[set\]|Matches any single character in set, or if the first character ^, it matches any character not in set.<br /><br />A hyphen indicates a range. A caret \(^\) not in the first position, and a hyphen in the first or last position has no special meaning.|Ex\[abc\]mple matches Example, Exbmple, and Excmple.<br /><br />Ex\[^abc\]mple does not match Example, Exbmple, and Excmple, but does match ExZmple<br /><br />Ex\[0\-9\] matches Ex followed by a single digit.|  
|<n1\-n2>|Matches any integer greater than or equal to the non\-negative n1 and less than or equal to the non\-negative n2. Omitting n1 or n2 indicates no bound|10.193.220.<1\-25> matches all IP addresses between 10.193.220.1 and 10.193.220.25 inclusive.<br /><br /><10\-> matches any string of digits greater than or equal to 10.<br /><br /><1\-10>\* Matches any number between 1 and 10 with an option following character such as 1, 20x, 5z, but it does not match 11 since that is not a number between 1 and 10.|  
|&#124;|Alternative matches|AB&#124;DC matches either AB or DC<br /><br />ABC&#124; matches either ABC or an empty string|  
|\\|Escape character||  
|\\\\|Escape character for \(,\), \[,\], <, and >|\\\\\(A\\\\\) matches \(A\)|  
|&|And also|\*NY\*ROUTER matches all strings containing NY and ROUTER<br /><br /><1\-100>&\*\[02468\] matches all even numbers between 1 and 100.<br /><br />\*A\*&#124;\*B\*&\*C\* matches strings that contain either an A or a B, and also a C.|  
|~|Except|10.20.30.\*~10.20.30.50 matches all hosts on 10.20.30 except for 10.20.30.50.<br /><br />\*Router\*~\*Cisco\*&\*10.20.30.<5\-10> matches routers except Cisco routers with the addresses between 10.20.30.5 and 10.20.30.10.|  
  
## Configuring a VLAN Tag  
To differentiate between VLANs, you can configure a tag for a virtual local area network \(VLAN\) by editing the vlan\-tag\-settings.conf file on each management server that runs a network discovery rule. Vlan\-tag\-settings.conf is located in the Operations Manager installation directory in **\\Server\\NetworkMonitoring\\conf\\discovery**.  
  
#### To configure a VLAN tag  
  
1.  On each management server that runs a network discovery rule, open vlan\-tag\-settings.conf in a text editor.  
  
2.  Add the following text to the file. You can use wildcard matching.  
  
    ```  
    config name  
    match Type type  
    match Description text to match  
    settings VLAN_Provisioning_Setting  
    param Tag tag name  
    ```  
  
3.  Save vlan\-tag\-settings.conf.  
  
The following is an example of the configuration of a VLAN tag “LDSwitch” to be used for all switches that have a description that starts with “Cisco”:  
  
```  
config LanceSwitch  
match Type SWITCH  
match Description Cisco*  
settings VLAN_Provisioning_Setting  
param Tag LDSwitch  
```  
  
## See Also  
[Monitoring Networks by Using Operations Manager](../../om/manage/Monitoring-Networks-by-Using-Operations-Manager.md)  
[How to Discover Network Devices in Operations Manager](../../om/manage/How-to-Discover-Network-Devices-in-Operations-Manager.md)  
[Tuning Network Monitoring](../../om/manage/Tuning-Network-Monitoring.md)  
[Run As Accounts for Network Monitoring in Operations Manager](../../om/manage/Run-As-Accounts-for-Network-Monitoring-in-Operations-Manager.md)  
[How to Delete or Restore a Network Device in Operations Manager](../../om/manage/How-to-Delete-or-Restore-a-Network-Device-in-Operations-Manager.md)  
[Viewing Network Devices and Data in Operations Manager](../../om/manage/Viewing-Network-Devices-and-Data-in-Operations-Manager.md)  
[Security for Servers Performing Network Discovery](../../om/manage/Security-for-Servers-Performing-Network-Discovery.md)  
[Network Devices Supported for Discovery by Operations Manager](../../om/manage/Network-Devices-Supported-for-Discovery-by-Operations-Manager.md)  
[Reports for Network Monitoring in Operations Manager](../../om/manage/Reports-for-Network-Monitoring-in-Operations-Manager.md)  
  
