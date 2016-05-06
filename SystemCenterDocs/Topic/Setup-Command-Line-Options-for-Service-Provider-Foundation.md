---
title: Setup Command-Line Options for Service Provider Foundation
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e42b1ed8-e53e-4032-b34d-0134b0d9c453
---
# Setup Command-Line Options for Service Provider Foundation
You can use command\-line options with the [!INCLUDE[spflong](../Token/spflong_md.md)] setup to perform an unattended installation by using the **–Silent** option. All options that you want to specify must be in a response file \(text file\) whose path is specified after the **–Silent** option, except for **–Silent –Uninstall** which performs an unattended uninstallation. The options can be delineated by either one line for each option, or a single space separating each option.

This topic requires that you have located the **setup.exe** file for [!INCLUDE[spfshort](../Token/spfshort_md.md)] in the installation media for [!INCLUDE[orchshort](../Token/orchshort_md.md)].

## Setup Command\-Line Options
The **\-Silent** option must be specified followed by the name of the response file, or followed by the **\-Uninstall** option:

**setup.exe\-Silent** <*ResponseFile*>

**setup.exe\-Silent\-Uninstall**

The options that you can include in the response file are as follows. The first three options are required. The fourth option is required only if you specify the **SpecifyCertificate** option as true.

**\-SendCEIPReports** <*true*|*false*>

**\-UseMicrosoftUpdate** <*true*|*false*>

**\-SpecifyCertificate** <*true*|*false*>

**\-CertificateSerialNumber** <*CertificateSerialNumberNoSpaces*>

\[**\-CertificateStore** <*Personal*|*WebHosting*>\]

\[**\-InstallFolder** <*InstallFolder*>\]

\[**\-WebSitePortNumber** <*PortNumber*>\]

\[**\-DatabaseServer** <*ServerName*>\]

\[**\-DatabasePortNumber** <*PortNumber*>\]

\[**\-ScvmmUserName** <*ScvmmUserName*>\]

\[**\-ScvmmPassword** <*ScvmmPassword*>\]

\[**\-ScvmmDomain** <*ScvmmDomain*>\]

\[**\-ScvmmNetworkServiceSelected** <*true*|*false*>\]

\[**\-VmmSecurityGroupUsers** <*VmmSecurityGroupUsers*>\]

\[**\-ScadminUserName** <*scadminUserName*>\]

\[**\-ScadminPassword** <*scadminPassword*>\]

\[**\-ScadminDomain** <*scadminDomain*>\]

\[**\-ScadminNetworkServiceSelected** <*true*|*false*>\]

\[**\-AdminSecurityGroupUsers** <*AdminSecurityGroupUsers*>\]

\[**\-ScproviderUserName** <*scproviderUserName*>\]

\[**\-ScproviderPassword** <*scproviderPassword*>\]

\[**\-ScproviderDomain** <*scproviderDomain*>\]

\[**\-ScproviderNetworkServiceSelected** <*true*|*false*>\]

\[**\-ProviderSecurityGroupUsers** <*ProviderSecurityGroupUsers*>\]

\[**\-ScusageUserName** <*scusageUserName*>\]

\[**\-ScusagePassword** <*scpusagePassword*>\]

\[**\-ScusageDomain** <*scusageDomain*>\]

\[**\-ScusageNetworkServiceSelected** <*true*|*false*>\]

\[**\-usageSecurityGroupUsers** <*usageSecurityGroupUsers*>\]

The following table describes the command\-line options:

|Option|Description|
|----------|---------------|
|**\-Silent**|Performs an unattended installation.<br /><br />You must include the name of response file after the **–Silent** option that contains the other options. The options can be delineated by either one line for each option, or a single space separating each option.<br /><br />The following options are required to be specified in the response file:<br /><br />-   **SendCEIPReports**<br />-   **UseMicrosoftUpdate**<br />-   **SpecifyCertificate**<br />-   **CertificateSerialNumber** \(but only if SpecifyCertificate is true\)|
|**\-Silent\-Uninstall**|Performs an unattended uninstallation.|
|**\-SendCEIPReports**|Send anonymous reports to the Customer Experience Improvement Program.|
|**\-UseMicrosoftUpdate**|Use Microsoft Update to check for updates.|
|**\-SpecifyCertificate**|Specify true to use an existing certificate or false to automatically generate a self\-signed certificate. If you specify true, you must also specify a value for the **CertificateSerialNumber** option.|
|**\-CertificateSerialNumber**|The serial number of the certificate used by IIS for HTTPS authentication. Must not contain any spaces. You can omit this option if you specified the  **SpecifyCertificate** option as false.|
|\[**\-DatabaseServer** <*ServerName*>\]|The name of the server that contains the [!INCLUDE[spfshort](../Token/spfshort_md.md)] database. Use localhost if the database is on the same computer on which you are installing [!INCLUDE[spfshort](../Token/spfshort_md.md)].|
|\[**\-CertificationStore**\]|The store location of the certificate.|
|\[**\-InstallFolder** <*InstallFolder*>\]|The path to the directory to install the product. The path must not contain any spaces.|
|\[**\-WebSitePortNumber** <*PortNumber*>\]|The port number for the web service.|
|\[**\-DatabasePortNumber** <*PortNumber*>\]|The port number of the database. The default is 1433.|
|\[**\-ScvmmUserName** <*ScvmmUserName*>\]<br /><br />\[**\-ScadminUserName** <*scadminUserName*>\]<br /><br />\[**\-ScproviderUserName** <*scproviderUserName*>\]<br /><br />\[**\-ScusageUserName** <*scusageUserName*>\]|The username credential for the Internet Information Services \(IIS\) setting for the VMM, Admin, Provider, or Usage web service.<br /><br />Omit this option if you are specifying true for the Network Service option.|
|\[**\-ScvmmPassword** <*ScvmmPassword*>\]<br /><br />\[**\-ScadminPassword** <*scadminPassword*>\]<br /><br />\[**\-ScproviderPassword** <*scproviderPassword*>\]<br /><br />\[**\-ScusagePassword** <*scusagePassword*>\]|The password credential for the IIS setting for the VMM, Admin, Provider, or Usage web service.<br /><br />Omit this option if you are specifying true for the Network Service option.|
|\[**\-ScvmmDomain** <*ScvmmDomain*>\]<br /><br />\[**\-ScadminDomain** <*scadminDomain*>\]<br /><br />\[**\-ScproviderDomain** <*scproviderDomain*>\]<br /><br />\[**\-ScusageDomain** <*scusageDomain*>\]|The domain credential for the IIS setting for the VMM, Admin, Provider, or Usage web service.<br /><br />Omit this option if you are specifying true for the Network Service option.|
|\[**\-ScvmmNetworkServiceSelected** <*true*&#124;*false*>\]<br /><br />\[**\-ScadminNetworkServiceSelected** <*true*&#124;*false*>\]<br /><br />\[**\-ScproviderNetworkServiceSelected** <*true*&#124;*false*>\]<br /><br />\[**\-ScusageNetworkServiceSelected** <*true*&#124;*false*>\]|Specifies that Network Service is to be used for application pool credentials for the VMM, Admin, Provider, or Usage web service.<br /><br />Specify false if you are specifying the username, password, or domain credential options.|
|\[**\-VmmSecurityGroupUsers** <*VmmSecurityGroupUsers*>\]<br /><br />\[**\-AdminSecurityGroupUsers** <*AdminSecurityGroupUsers*>\]<br /><br />\[**\-ProviderSecurityGroupUsers** <*ProviderSecurityGroupUsers*>\]<br /><br />\[**\-usageSecurityGroupUsers** <*usageSecurityGroupUsers*>\]|Specifies one or more security groups or users \(separated with a semicolon\) for the VMM, Admin, Provider, or Usage web service.|

## Troubleshooting

-   If you get the following error:

    **Error 0x80070003: Failed to write state to file: C:\\ProgramData\\Package Cache\\{97585be5\-93f3\-41eb\-8b19\-34f5fe52879d}\\state.rsm**

    Create a directory named "{97585be5\-93f3\-41eb\-8b19\-34f5fe52879d}" in the **C:\\ProgramData\\Package Cache\\** directory and run the setup command again.

## See Also
[How to Install Service Provider Foundation for System Center 2012 R2](../Topic/How-to-Install-Service-Provider-Foundation-for-System-Center-2012-R2.md)
[How to Uninstall Service Provider Foundation](../Topic/How-to-Uninstall-Service-Provider-Foundation.md)
[Deploying Service Provider Foundation](../Topic/Deploying-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](../Topic/Administering-Service-Provider-Foundation.md)
[Architecture Overview of Service Provider Foundation](../Topic/Architecture-Overview-of-Service-Provider-Foundation.md)

