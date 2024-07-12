---
ms.assetid:
title: Implement TLS 1.2 for Operations Manager
description: This article describes how to configure Transport Layer Security (TLS) 1.2 for System Center Operations Manager.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 06/14/2024
ms.custom: na
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Implement Transport Layer Security 1.2


This article describes how to enable Transport Layer Security (TLS) protocol version 1.2 for a System Center Operations Manager management group.  

>[!NOTE]
> Operations Manager will use the protocol configured at the Operating System Level. For example, if TLS 1.0, TLS 1.1, and TLS 1.2 are enabled at the Operating System Level, then Operations Manager will select one of the three protocols in the following order of preference:
> 1. TLS version 1.2
> 2. TLS version 1.1
> 3. TLS version 1.0
>
> The [Schannel SSP](/windows-server/security/tls/tls-ssl-schannel-ssp-overview) then selects the most preferred authentication protocol that the client and server can support.

Perform the following steps to enable TLS protocol version 1.2:

::: moniker range="sc-om-2016"

>[!NOTE]
> Microsoft OLE DB Driver 18 for SQL Server (recommended) is supported with Operations Manager 2016 UR9 and later.

1. Install [SQL Server 2012 Native Client 11.0](https://www.microsoft.com/download/details.aspx?id=50402&751be11f-ede8-5a0c-058c-2ee190a24fa6) or [Microsoft OLE DB Driver 18 for SQL Server](https://www.microsoft.com/download/details.aspx?id=56730) on all management servers and the Web console server.  
2. Install [.NET Framework 4.6](https://support.microsoft.com/help/3151800/the-net-framework-4-6-2-offline-installer-for-windows) on all management servers, gateway servers, Web console server, and SQL Server hosting the Operations Manager databases and Reporting server role.   
3. Install the [Required SQL Server update](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) that supports TLS 1.2.  
4. Install [ODBC 11.0](https://www.microsoft.com/download/details.aspx?id=36434) or [ODBC 13.0](https://www.microsoft.com/download/details.aspx?id=50420) on all management servers.
5. For System Center 2016 - Operations Manager, install Update Rollup 4 or later.  
6. Configure Windows to only use TLS 1.2.  
7. Configure Operations Manager to only use TLS 1.2.  
::: moniker-end

::: moniker range=">sc-om-2016"
1. Install [Microsoft OLE DB Driver](/sql/connect/oledb/release-notes-for-oledb-driver-for-sql-server?view=sql-server-ver16#1872) version 18.2 to 18.7.2 on all management servers and the Web console server.
2. Install [.NET Framework 4.6](https://support.microsoft.com/help/3151800/the-net-framework-4-6-2-offline-installer-for-windows) on all management servers, gateway servers, Web console server, and SQL Server hosting the Operations Manager databases and Reporting server role.
3. Install the [Required SQL Server update](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) that supports TLS 1.2.  
4. Install [ODBC Driver](/sql/connect/odbc/windows/release-notes-odbc-sql-server-windows?view=sql-server-ver16#17106) version 17.3 to 17.10.6 on all management servers.
5. Configure Windows to only use TLS 1.2.  
6. Configure Operations Manager to only use TLS 1.2.  
::: moniker-end

Operations Manager generates SHA1 and SHA2 self-signed certificates.  This is required to enable TLS 1.2. If CA-signed certificates are used, ensure that the certificates are either SHA1 or SHA2.

::: moniker range="sc-om-2016"
>[!NOTE]
>If your security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 management server, gateway server, Web console, and Reporting services role will fail because the setup media doesn't include the updates to support TLS 1.2.  The only way you can install these roles is by enabling TLS 1.0 on the system, apply Update Rollup 4, and then enable TLS 1.2 on the system.

::: moniker-end

## Configure Windows Operating System to only use TLS 1.2 protocol

Use one of the following methods to configure Windows to use only the TLS 1.2 protocol.

### Method 1: Manually modify the registry

> [!IMPORTANT]
> Follow the steps in this section carefully. Serious problems might occur if you modify the registry incorrectly. Before you modify it, back up the registry for restoration in case problems occur.
>
> Use the following steps to enable/disable all SCHANNEL protocols system-wide. We recommend that you enable the TLS 1.2 protocol for all incoming communications and outgoing communications.
>
> [!NOTE]
> Making these registry changes doesn't affect the use of Kerberos or NTLM protocols.

1. Sign in to the server by using an account that has local administrative credentials.
2. Start Registry Editor by selecting and holding **Start**, enter **regedit** in the **Run** textbox, and select **OK**.
3. Locate the following registry subkey: `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols`.
4. Create a subkey under **Protocols** for **SSL 2.0**, **SSL 3.0**, **TLS 1.0**, **TLS 1.1**, and **TLS 1.2**.  
5. Create a **Client** and **Server** subkey under each protocol version subkey you created earlier.  For example, the subkey for TLS 1.0 would be `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client` and `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server`.  
6. To disable each protocol, create the following DWORD values under **Server** and **Client**:  
   * **Enabled** [Value = 0]  
   * **DisabledByDefault** [Value = 1]  

7. To enable the TLS 1.2 protocol, create the following DWORD values under `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client` and `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server`:
   * **Enabled** [Value = 1]  
   * **DisabledByDefault** [Value = 0]  

8. Close the Registry Editor.

### Method 2: Automatically modify the registry

Run the following Windows PowerShell script as Administrator to automatically configure your Windows Operating System to use only the TLS 1.2 Protocol:

```powershell
$ProtocolList       = @("SSL 2.0", "SSL 3.0", "TLS 1.0", "TLS 1.1", "TLS 1.2")
$ProtocolSubKeyList = @("Client", "Server")
$DisabledByDefault  = "DisabledByDefault"
$registryPath       = "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\"

foreach ($Protocol in $ProtocolList)
{
	foreach ($key in $ProtocolSubKeyList)
	{
		$currentRegPath = $registryPath + $Protocol + "\" + $key
		Write-Output "Current Registry Path: `"$currentRegPath`""

		if (!(Test-Path $currentRegPath))
		{
			Write-Output " `'$key`' not found: Creating new Registry Key"
			New-Item -Path $currentRegPath -Force | out-Null
		}
		if ($Protocol -eq "TLS 1.2")
		{
			Write-Output " Enabling - TLS 1.2"
			New-ItemProperty -Path $currentRegPath -Name $DisabledByDefault -Value "0" -PropertyType DWORD -Force | Out-Null
			New-ItemProperty -Path $currentRegPath -Name 'Enabled' -Value "1" -PropertyType DWORD -Force | Out-Null
		}
		else
		{
			Write-Output " Disabling - $Protocol"
			New-ItemProperty -Path $currentRegPath -Name $DisabledByDefault -Value "1" -PropertyType DWORD -Force | Out-Null
			New-ItemProperty -Path $currentRegPath -Name 'Enabled' -Value "0" -PropertyType DWORD -Force | Out-Null
		}
		Write-Output " "
	}
}
```

## Configure Operations Manager to use only TLS 1.2

After completing the configuration of all prerequisites for Operations Manager, perform the following steps on all management servers, the server hosting the Web console role, and on any Windows computer the agent is installed on.  

>[!IMPORTANT]
>Follow the steps in this section carefully. Serious problems might occur if you modify the registry incorrectly. Before making any modifications, back up the registry for restoration in case problems occur.

::: moniker range="sc-om-2016"

> [!NOTE]
> SCOM 2012 R2 running in Windows OS 2012 needs additional changes to use TLS 1.2 over HTTP for UNIX/LINUX monitoring. In order to enable TLS 1.2 as default security protocols in WinHTTP in Windows, the following changes need to be made as per [Update to enable TLS 1.1 and TLS 1.2 as default secure protocols in WinHTTP in Windows](https://support.microsoft.com/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392).
> 1. Install [KB3140245](https://support.microsoft.com/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392) on the Management Servers/Gateways Servers in the UNIX/LINUX Resource Pool.
> 2. Back up the registries that are modified as mentioned in the KB article.
> 3. Download and run the [Easy Fix](https://support.microsoft.com/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392#bkmk_easy) tool on the Management Servers/Gateways in the UNIX/LINUX Resource Pool.
> 4. Reboot the servers.

::: moniker-end

### Manually modify the registry

1. Sign in to the server by using an account that has local administrative credentials.  
2. Start Registry Editor by selecting and holding **Start**, enter **regedit** in the **Run** textbox, and then select **OK**.  
3. Locate the following registry subkey: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319`.  
4. Create the DWORD value **SchUseStrongCrypto** under this subkey with a value of **1**.    
5. Locate the following registry subkey: `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319`.  
6. Create the DWORD value **SchUseStrongCrypto** under this subkey with a value of **1**.
7. Restart the system for the settings to take effect.  

## Automatically modify the registry

Run the following Windows PowerShell script in Administrator mode to automatically configure Operations Manager to use only the TLS 1.2 Protocol:

```powershell
# Tighten up the .NET Framework
$NetRegistryPath = "HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319"
New-ItemProperty -Path $NetRegistryPath -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null

$NetRegistryPath = "HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319"
New-ItemProperty -Path $NetRegistryPath -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null
```

## Additional settings

::: moniker range="sc-om-2016"

If this is being implemented for System Center 2016 - Operations Manager, after applying Update Rollup 4, ensure to import the management packs that are included in this rollup located in the following directory: **\Program Files\Microsoft System Center 2016\Operations Manager\Server\Management Packs for Update Rollups**.  

::: moniker-end

If you're monitoring a supported version of Linux server with Operations Manager, follow the instructions on the appropriate website for your distro to configure TLS 1.2.  

::: moniker range="sc-om-2016"

### Audit Collection Services

For Audit Collection Services (ACS), you must make additional changes in the registry on ACS Collector server.  ACS uses the DSN to make connections to the database. You must update DSN settings to make them functional for TLS 1.2.

1. Sign in to the server by using an account that has local administrative credentials.  
2. Start Registry Editor by selecting and holding **Start**, enter **regedit** in the **Run** textbox, and select **OK**.  
3. Locate the following ODBC subkey for OpsMgrAC: `HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC`.  

    >[!NOTE]
    >The default name of DSN is OpsMgrAC.

4. Under **ODBC Data Sources** subkey, select the DSN name **OpsMgrAC**. This contains the name of the ODBC driver to be used for the database connection. If you have ODBC 11.0 installed, change this name to **ODBC Driver 11 for SQL Server**, or if you have ODBC 13.0 installed, change this name to **ODBC Driver 13 for SQL Server**.
5. Under the **OpsMgrAC** subkey, update the **Driver** for the ODBC version that is installed.
   * If ODBC 11.0 is installed, change the Driver entry to `%WINDIR%\system32\msodbcsql11.dll`.
   * If ODBC 13.0 is installed, change the Driver entry to `%WINDIR%\system32\msodbcsql13.dll`.

#### Registry File

   Alternatively, create and save the following **.reg** file in Notepad or another text editor. To run the saved **.reg** file, double-click the file.

   * For ODBC 11.0, create the following ODBC 11.reg file:

      ```
      Windows Registry Editor Version 5.00
      
      [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources]
      "OpsMgrAC"="ODBC Driver 11 for SQL Server"
      
      [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC]
      "Driver"="%WINDIR%\system32\msodbcsql11.dll"
      ```

   * For ODBC 13.0, create the following ODBC 13.reg file:

      ```
      Windows Registry Editor Version 5.00
      
      [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources]
      "OpsMgrAC"="ODBC Driver 13 for SQL Server"
      
      [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC]
      "Driver"="%WINDIR%\system32\msodbcsql13.dll"
      ```

#### PowerShell

   Alternatively, you can run the following PowerShell commands to automate the change.

   * For ODBC 11.0, run the following PowerShell commands:

      ```powershell
      New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC" -Name "Driver" -Value "%WINDIR%\system32\msodbcsql11.dll" -PropertyType STRING -Force | Out-Null
      New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources" -Name "OpsMgrAC" -Value "ODBC Driver 11 for SQL Server" -PropertyType STRING -Force | Out-Null
      ```
      
   * For ODBC 13.0, run the following PowerShell commands:

      ```powershell
      New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC" -Name "Driver" -Value "%WINDIR%\system32\msodbcsql13.dll" -PropertyType STRING -Force | Out-Null
      New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources" -Name "OpsMgrAC" -Value "ODBC Driver 13 for SQL Server" -PropertyType STRING -Force | Out-Null
      ```

::: moniker-end

::: moniker range=">sc-om-2016"

### Audit Collection Services

For Audit Collection Services (ACS), you must make additional changes in the registry on ACS Collector server.  ACS uses the DSN to make connections to the database. You must update DSN settings to make them functional for TLS 1.2.

1. Sign in to the server by using an account that has local administrative credentials.  
2. Start Registry Editor by selecting and holding **Start**, enter **regedit** in the **Run** textbox, and select **OK**.  
3. Locate the following ODBC subkey for OpsMgrAC: `HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC`.  

    >[!NOTE]
    >The default name of DSN is OpsMgrAC.

4. Under **ODBC Data Sources** subkey, select the DSN name **OpsMgrAC**. This contains the name of the ODBC driver to be used for the database connection. If you have ODBC 17 installed, change this name to **ODBC Driver 17 for SQL Server**.
5. Under the **OpsMgrAC** subkey, update the **Driver**  for the ODBC version that is installed.
   * If ODBC 17 is installed, change the Driver entry to `%WINDIR%\system32\msodbcsql17.dll`.

#### Registry File

   Alternatively, create and save the following **.reg** file in Notepad or another text editor. To run the saved **.reg** file, double-click the file.

   * For ODBC 17, create the following ODBC 17.reg file:

      ```
      Windows Registry Editor Version 5.00
      
      [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources]
      "OpsMgrAC"="ODBC Driver 17 for SQL Server"
      
      [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC]
      "Driver"="%WINDIR%\system32\msodbcsql17.dll"
      ```

#### PowerShell

   Alternatively, you can run the following PowerShell commands to automate the change.

   * For ODBC 17, run the following PowerShell commands:

      ```powershell
      New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC" -Name "Driver" -Value "%WINDIR%\system32\msodbcsql17.dll" -PropertyType STRING -Force | Out-Null
      New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources" -Name "OpsMgrAC" -Value "ODBC Driver 17 for SQL Server" -PropertyType STRING -Force | Out-Null
      ```

::: moniker-end

## Next steps

* For a complete listing of ports used, the direction of the communication, and if the ports can be configured, see [Configuring a Firewall for Operations Manager](plan-security-config-firewall.md).

* For an overall review of how data between components in a management group is protected, see [Authentication and Data Encryption in Operations Manager](plan-security-authentication-data-encryption.md).
