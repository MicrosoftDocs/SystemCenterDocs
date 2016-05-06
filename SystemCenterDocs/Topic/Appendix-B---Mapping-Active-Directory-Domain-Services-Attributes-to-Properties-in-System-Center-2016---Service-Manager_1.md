---
title: Appendix B - Mapping Active Directory Domain Services Attributes to Properties in System Center 2016 - Service Manager_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3da308fc-76e0-40e5-af1d-0d0161623ed7
robots: noindex,nofollow
---
# Appendix B - Mapping Active Directory Domain Services Attributes to Properties in System Center 2016 - Service Manager_1
Using an Active Directory connector, [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] synchronizes data with the User, Group, Computer, and Printer Active Directory Domain Services \(AD DS\) objects. The following tables describe the mapping between the attributes of the Active Directory objects and the corresponding [!INCLUDE[smshort12](../Token/smshort12_md.md)] class properties.

## User\/Microsoft.AD.User
The following table describes the mapping between the attributes of the Active Directory User object and the  [!INCLUDE[smshort12](../Token/smshort12_md.md)]**Microsoft.AD.User** class properties.

|Active Directory user attribute|Microsoft.AD.User property|
|-----------------------------------|------------------------------|
|physicaldeliveryofficename|Office|
|displayname|displayname|
|company|Company|
|employeeid|Employeeid|
|department|Department|
|telephonenumber|BusinessPhone|
|homePhone|HomePhone|
|facsimileTelephoneNumber|Fax|
|mobile|Mobile|
|pager|Pager|
|mail|Email|
|givenname|FirstName|
|initials|Initials|
|sn|LastName|
|distinguishedname|Distinguishedname|
|title|Title|
|manager|manager|
|samaccountname|UserName|
|l|City|
|StreetAddress|StreetAddress|
|st|State|
|postalCode|Zip|
|co|Country|
|localeID|Locale|
|msRTCSIP\-PrimaryUserAddress|SipAddress|
|objectSid|SID|
|Domain|Domain|

## Group\/Microsoft.AD.UserBase
The following table describes the mapping between the attributes of the Active Directory Group object and the [!INCLUDE[smshort12](../Token/smshort12_md.md)]**Microsoft.AD.UserBase** class properties.

|Active Directory group attribute|Microsoft.AD.UserBase property|
|------------------------------------|----------------------------------|
|displayname|displayname|
|mail|Email|
|distinguishedname|Distinguishedname|
|samaccountname|samaccountname|
|objectSid|SID|
|Domain|Domain|

## Printer\/Microsoft.AD.Printer
The following table describes the mapping between the attributes of the Active Directory PrintQueue object and the [!INCLUDE[smshort12](../Token/smshort12_md.md)]**Microsoft.AD.Printer** class properties.

|Active Directory printer attribute|Microsoft.AD.Printer property|
|--------------------------------------|---------------------------------|
|uNCName|uNCName|
|serverName|serverName|
|shortServerName|shortServerName|
|printerName|printerName|
|printNetworkAddress|printNetworkAddress|
|printShareName|printShareName|
|isDeleted|isDeleted|
|driverName|driverName|
|driverVersion|driverVersion|
|printMemory|printMemory|
|printCollate|printCollate|
|printOwner|printOwner|
|assetNumber|assetNumber|
|managedBy|managedBy|
|printDuplexSupported|printDuplexSupported|
|printColor|printColor|
|printStaplingSupported|printStaplingSupported|
|versionNumber|versionNumber|
|url|url|
|printMediaSupported|printMediaSupported|
|printRateUnit|printRateUnit|
|printMaxXExtent|printMaxXExtent|
|printKeepPrintedJobs|printKeepPrintedJobs|
|printRate|printRate|
|printMediaReady|printMediaReady|
|printPagesPerMinute|printPagesPerMinute|
|printMaxResolutionSupported|printMaxResolutionSupported|
|printMACAddress|printBinNames|
|printMACAddress|printMACAddress|
|portName|portName|
|physicalLocationObject|physicalLocationObject|
|keywords|keywords|
|printNotify|printNotify|
|wWWHomePage|wWWHomePage|
|whenChanged|whenChanged|
|modifyTimeStamp|modifyTimeStamp|
|location|location|
|canonicalName|canonicalName|
|displayname|displayname|
|cn|Fullname|
|distinguishedname|Distinguishedname|
|description|description|

## Computer\/Microsoft.Windows.Computer
The following table describes the mapping between the attributes of the Active Directory Computer object and the  [!INCLUDE[smshort12](../Token/smshort12_md.md)]**Microsoft.Windows.Computer** class properties.

|Active Directory computer attribute|Microsoft.Windows.Computer property|
|---------------------------------------|---------------------------------------|
|msDS\-SiteName|ActiveDirectorySite|
|dNSHostName|DNSName|
|ipHostNumber|IPAddress|
|networkAddress|NetworkName|
|msDS\-PrincipalName|PrincipalName|
|displayname|displayname|
|samaccountname|NetbiosComputerName|
|objectSid|ActiveDirectoryObjectSid|
|ou|OrganizationalUnit|
|Domain|NetbiosDomainName|

