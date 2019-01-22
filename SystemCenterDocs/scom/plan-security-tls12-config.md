---
ms.assetid: 
title: Implement TLS 1.2 for Operations Manager
description: This article describes how to configure Transport Layer Security (TLS) 1.2 for System Center Operations Manager.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 11/28/2018
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# How to implement Transport Layer Security 1.2 
This topic describes how to enable Transport Layer Security (TLS) protocol version 1.2 for a System Center 2016 - Operations Manager and version 1801 management group.  

Perform the following steps to enable TLS protocol version 1.2:

1. Install [SQL Server 2012 Native Client 11.0](https://www.microsoft.com/download/details.aspx?id=50402&751be11f-ede8-5a0c-058c-2ee190a24fa6=True) on all management servers and the Web console server.  
2. Install [.NET Framework 4.6](https://support.microsoft.com/help/3151800/the-net-framework-4-6-2-offline-installer-for-windows) on all management servers, gateway servers, Web console server, and SQL Server hosting the Operations Manager databases and Reporting server role.  
3. Install the [Required SQL Server update](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) that supports TLS 1.2.  
4. Install [ODBC 11.0](https://www.microsoft.com/download/details.aspx?id=36434) or [ODBC 13.0](https://www.microsoft.com/download/details.aspx?id=50420) on all management servers.  
5. For System Center 2016 - Operations Manager, install [Update Rollup 4](https://support.microsoft.com/help/4024941).  
6. Configure Windows to only use TLS 1.2.  
7. Configure Operations Manager to only use TLS 1.2.  

Operations Manager generates SHA1 and SHA2 self-signed certificates.  This is required to enable TLS 1.2.  If CA-signed certificates are used, make sure that the certificates are either SHA1 or SHA2.

>[!NOTE]
>If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 management server, gateway server, Web console, and Reporting services role will fail because the setup media does not include the updates to support TLS 1.2.  The only way you can install these roles is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system.  This limitation does not apply to Operations Manager version 1801.
>

## Configure Windows to only use TLS 1.2 protocol
Use one of the following methods to configure Windows to use only the TLS 1.2 protocol.

### Method 1: Manually modify the registry
>[!IMPORTANT]
>Follow the steps in this section carefully. Serious problems might occur if you modify the registry incorrectly. Before you modify it, back up the registry for restoration in case problems occur.
>
Use the following steps to enable/disable all SCHANNEL protocols system-wide. We recommend that you enable the TLS 1.2 protocol for incoming communications; and enable the TLS 1.2, TLS 1.1, and TLS 1.0 protocols for all outgoing communications.

>[!NOTE]
> Making these registry changes does not affect the use of Kerberos or NTLM protocols.
> 

1. Log on to the server by using an account that has local administrative credentials. 
2. Start Registry Editor by right-clicking **Start**, type **regedit** in the **Run** textbox, and then click **OK**.
3. Locate the following registry subkey: **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols**.
4. Create a subkey under **Protocols** for **SSL 2.0**, **SSL 3.0**, **TLS 1.0**, **TLS 1.1**, and **TLS 1.2**.  
5. Create a **Client** and **Server** subkey under each protocol version subkey you created earlier.  For example, the sub-key for TLS 1.0 would be **HKLM\System\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client** and **HKLM\System\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server**.  
6. To disable each protocol, create the following DWORD values under **Server** and **Client**:  
   * **Enabled** [Value = 0]  
   * **DisabledByDefault** [Value = 1]  

7. To enable the TLS 1.2 protocol, create the following DWORD values under **HKLM\System\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client** and **HKLM\System\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server**:
   * **Enabled** [Value = 1]  
   * **DisabledByDefault** [Value = 0]  

8. Close the Registry Editor.

### Method 2: Automatically modify the registry
Run the following Windows PowerShell script in Administrator mode to automatically configure Windows to use only the TLS 1.2 Protocol.

```   
$ProtocolList       = @("SSL 2.0","SSL 3.0","TLS 1.0", "TLS 1.1", "TLS 1.2")  
$ProtocolSubKeyList = @("Client", "Server")  
$DisabledByDefault = "DisabledByDefault"  
$Enabled = "Enabled"  
$registryPath = "HKLM:\\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\"  
  
foreach($Protocol in $ProtocolList)  
{  
    Write-Host " In 1st For loop"  
	foreach($key in $ProtocolSubKeyList)  
	{  
		$currentRegPath = $registryPath + $Protocol + "\" + $key  
		Write-Host " Current Registry Path $currentRegPath"  
  		
		if(!(Test-Path $currentRegPath))  
		{  
		    Write-Host "creating the registry"  
			New-Item -Path $currentRegPath -Force | out-Null  		
		}  
		if($Protocol -eq "TLS 1.2")  
		{  
		    Write-Host "Working for TLS 1.2"  
			New-ItemProperty -Path $currentRegPath -Name $DisabledByDefault -Value "0" -PropertyType DWORD -Force | Out-Null  
			New-ItemProperty -Path $currentRegPath -Name $Enabled -Value "1" -PropertyType DWORD -Force | Out-Null  
  		
		}  
		else  
		{  
		    Write-Host "Working for other protocol"  
			New-ItemProperty -Path $currentRegPath -Name $DisabledByDefault -Value "1" -PropertyType DWORD -Force | Out-Null  
			New-ItemProperty -Path $currentRegPath -Name $Enabled -Value "0" -PropertyType DWORD -Force | Out-Null   
		}  	
	}  
}  

Exit 0
```
## Configure Operations Manager to use only TLS 1.2
After completing the configuration of all prerequisites for Operations Manager, perform the following steps on all management servers, the server hosting the Web console role, and on any Windows or Linux server the agent is installed on.  

>[!IMPORTANT]
>Follow the steps in this section carefully. Serious problems might occur if you modify the registry incorrectly. Before making any modifications, back up the registry for restoration in case problems occur.

### Manually modify the registry
1. Log on to the server by using an account that has local administrative credentials.  
2. Start Registry Editor by right-clicking **Start**, type **regedit** in the **Run** texbox, and then click **OK**.  
3. Locate the following registry subkey: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.30319**.  
4. Create the DWORD value **SchUseStrongCrypto** under this subkey with a value of **1**.    
5. Locate the following registry subkey: **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\\.NETFramework\v4.0.30319**.  
6. Create the DWORD value **SchUseStrongCrypto** under this subkey with a value of **1**.    
7. Restart the system for the settings to take effect.  

## Automatically modify the registry
Run the following Windows PowerShell script in Administrator mode to automatically configure Operations Manager to use only the TLS 1.2 Protocol.  

```
# Tighten up the .NET Framework
$NetRegistryPath = "HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319"
New-ItemProperty -Path $NetRegistryPath -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null

$NetRegistryPath = "HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319"
New-ItemProperty -Path $NetRegistryPath -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null
```

## Additional settings

If this is being implemented for System Center 2016 - Operations Manager, after applying Update Rollup 4, be sure to import the management pacsk that are included in this rollup located in the following directory: **\Program Files\Microsoft System Center 2016\Operations Manager\Server\Management Packs for Update Rollups**.  

If you are monitoring a supported version of Linux server with Operations Manager, follow the instructions on the appropriate website for your distro to configure TLS 1.2.  

### Audit Collection Services
For Audit Collection Services (ACS), you must make additional changes in the registry on ACS Collector server.  ACS uses the DSN to make connections to the database. You must update DSN settings to make them functional for TLS 1.2.

1. Log on to the server by using an account that has local administrative credentials.  
2. Start Registry Editor by right-clicking **Start**, type **regedit** in the **Run** texbox, and then click **OK**.  
3. Locate the following ODBC subkey for OpsMgrAC: **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC**.  
 
    >[!NOTE]
    >The default name of DSN is OpsMgrAC.

4. Under **ODBC Data Sources** subkey, select the DSN name **OpsMgrAC**. This contains the name of ODBC driver to be used for the database connection. If you have ODBC 11.0 installed, change this name to **ODBC Driver 11 for SQL Server**, or if you have ODBC 13.0 installed, change this name to **ODBC Driver 13 for SQL Server**.
5. Under the **OpsMgrAC** subkey, update the **Driver**  for the ODBS version that is installed.
   * If ODBC 11.0 is installed, change the Driver entry to %WINDIR%\system32\msodbcsql11.dll.
   * If ODBC 13.0 is installed, change the Driver entry to %WINDIR%\system32\msodbcsql13.dll.

   Alternatively, create and save the following .reg file in Notepad or another text editor. To run the saved .reg file, double-click the file.

    * For ODBC 11.0, create the following ODBC 11.0.reg file:
    
         ```
        [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources]
        "OpsMgrAC"="ODBC Driver 11 for SQL Server"

        [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC]

        [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC]
        "Driver"="%WINDIR%\\system32\\msodbcsql11.dll"
        ```

    * For ODBC 13.0, create the following ODBC 13.0.reg file:
  
        ```
        [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources]
        "OpsMgrAC"="ODBC Driver 13 for SQL Server"

        [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC]

        [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC]
        "Driver"="%WINDIR%\\system32\\msodbcsql13.dll"
        ```

## Next steps

* For a complete listing of ports used, the direction of the communication, and if the ports can be configured, see [Configuring a Firewall for Operations Manager](plan-security-config-firewall.md).

* For an overall review of how data between components in a management group is protected, see [Authentication and Data Encryption in Operations Manager](plan-security-authentication-data-encryption.md).
