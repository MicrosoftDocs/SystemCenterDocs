---
title: AdtAdmin.exe SetDBAuth
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82d634f0-c8dc-4a6f-8d52-4dad1716b209
---
# AdtAdmin.exe SetDBAuth
The *\/SetDBAuth* parameter specifies the authentication method that the ACS collector uses to access the ACS database. The two available authentication methods are Windows Authentication and SQL authentication. Windows Authentication is the most secure method but can be used only if the computer that runs the ACS collector and the computer that hosts the ACS database belong to the same Active Directory domain or to domains that trust each other.

Using the *\/Name* and the *\/Pwd* subparameters automatically configures the ACS collector to use SQL authentication. To check which authentication method the ACS collector is using, run the *\/GetDBAuth* parameter.

## Syntax
To specify that the ACS collector use Windows Authentication, use the following syntax:

`AdtAdmin.exe /SetDBAuth [/Collector:<CollectorName>]`

To specify that the ACS collector use SQL authentication and identify the user name and password of the user account that can access the ACS database, use the following syntax:

`AdtAdmin.exe /SetDBAuth [/Collector:<CollectorName>] /Name:<UserAccount> /Pwd:<Password>`

|Subparameter|Description|
|----------------|---------------|
|\/Collector:CollectorName|Specifies an ACS collector whose database authentication account you want to change. If this subparameter is omitted, the local ACS collector is assumed.|
|\/Name:UserAccount|Identifies the new user account name for the ACS collector to use to connect to the ACS database. This subparameter should be used only when you want to use SQL authentication as the authentication method between the ACS collector and the ACS database.|
|\/Pwd:Password|Specifies the password for the user account identified with the *\/Name* parameter.|

## Example
Use the following example to change the user account used by the ACS collector to connect to the ACS Database to an account that has a user name of "SQLDatabase" and a password of "SQLPass\#1":

`AdtAdmin /SetDBAuth /Name:SQLDatabase /Password:SQLPass#1`

## See Also
[Audit Collection Services Administration &#40;AdtAdmin.exe&#41;](../Topic/Audit-Collection-Services-Administration--AdtAdmin.exe-.md)
[AdtAdmin.exe AddGroup](../Topic/AdtAdmin.exe-AddGroup.md)
[AdtAdmin.exe DelGroup](../Topic/AdtAdmin.exe-DelGroup.md)
[AdtAdmin.exe Disconnect](../Topic/AdtAdmin.exe-Disconnect.md)
[AdtAdmin.exe GetDBAuth](../Topic/AdtAdmin.exe-GetDBAuth.md)
[AdtAdmin.exe GetQuery](../Topic/AdtAdmin.exe-GetQuery.md)
[AdtAdmin.exe ListForwarders](../Topic/AdtAdmin.exe-ListForwarders.md)
[AdtAdmin.exe ListGroups](../Topic/AdtAdmin.exe-ListGroups.md)
[AdtAdmin.exe SetQuery](../Topic/AdtAdmin.exe-SetQuery.md)
[AdtAdmin.exe Stats](../Topic/AdtAdmin.exe-Stats.md)
[AdtAdmin.exe UpdForwarder](../Topic/AdtAdmin.exe-UpdForwarder.md)
[AdtAdmin.exe UpdGroup](../Topic/AdtAdmin.exe-UpdGroup.md)

