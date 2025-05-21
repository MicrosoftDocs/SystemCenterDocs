---
ms.assetid:
title: Enforce TLS 1.2 for Operations Manager
description: This article describes how to configure System Center Operations Manager to utilize Transport Layer Security (TLS) 1.2.
author: jyothisuri
ms.author: jsuri

ms.date: 02/19/2025
ms.custom: na
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Enforce TLS 1.2 for Operations Manager

This article describes how to allow System Center Operations Manager to utilize Transport Layer Security (TLS) 1.2.

::: moniker range="sc-om-2016"

> [!NOTE]
> Operations Manager uses the protocol configured at the Operating System level. For example, if all protocols are enabled, then Operations Manager selects one of the three protocols in the following order of preference:
>
> 1. TLS version 1.0
> 1. TLS version 1.1
> 1. TLS version 1.2
>
> The [Schannel SSP](/windows-server/security/tls/tls-ssl-schannel-ssp-overview) then selects the most preferred authentication protocol that the client and server can support.

Perform the following steps to implement TLS protocol version 1.2 in Operations Manager:

> [!NOTE]
> Microsoft OLE DB Driver 18 for SQL Server (recommended) is supported with Operations Manager 2016 UR9 and later.

1. Install [SQL Server 2012 Native Client 11.0](https://www.microsoft.com/download/details.aspx?id=50402&751be11f-ede8-5a0c-058c-2ee190a24fa6) or [Microsoft OLE DB Driver](/sql/connect/oledb/release-notes-for-oledb-driver-for-sql-server) (x64) on all management servers and the web console server.  
1. Install [Microsoft ODBC Driver](/sql/connect/odbc/windows/release-notes-odbc-sql-server-windows) (x64) on all management servers and the web console server.
1. Install the [Required SQL Server update](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) that supports TLS 1.2.  
1. Install a minimum of Update Rollup 4 for Operations Manager 2016 on all components.
1. Ensure all servers have a minimum .NET Framework 4.6 installed as compatible with the OS version: [.NET Framework versions and dependencies](/dotnet/framework/migration-guide/versions-and-dependencies)

   1. **Don't install .NET Framework 4.8, as there are known incompatibilities with Operations Manager 2016.**

1. Configure Windows to only use TLS 1.2.  
1. Configure .NET Framework to utilize higher levels of cryptography by default.

1. Configure Audit Collection Services if installed.

::: moniker-end

::: moniker range=">sc-om-2016"

1. Install [Microsoft OLE DB Driver for SQL](/sql/connect/oledb/release-notes-for-oledb-driver-for-sql-server?view=sql-server-ver16#1874) version 18.7.4 on all management servers and the web console server.
1. Install [Microsoft ODBC Driver for SQL](/sql/connect/odbc/windows/release-notes-odbc-sql-server-windows?view=sql-server-ver16#17106) version 17.10.6 on all management servers and the web console server.
1. Configure Windows to only use TLS 1.2.  
1. Configure .NET Framework to utilize higher levels of cryptography by default.

1. Configure Audit Collection Services if installed.

> [!NOTE]
> If utilizing SQL Server connection encryption, install these driver versions instead:
>
> - Microsoft OLE DB Driver 19: [https://aka.ms/downloadmsoledbsql](https://aka.ms/downloadmsoledbsql)
> - Microsoft ODBC Driver 18: [https://aka.ms/downloadmsodbcsql](https://aka.ms/downloadmsodbcsql)
>
> More information about configuring SQL connection encryption can be found here: [Configure SQL Server Database Engine for encrypting connections](/sql/database-engine/configure-windows/configure-sql-server-encryption)

::: moniker-end

::: moniker range="sc-om-2016"

Operations Manager generates SHA1 and SHA2 self-signed certificates, which are required to enable TLS 1.2. If CA-signed certificates are used, ensure that the certificates are either SHA1 or SHA2.

> [!NOTE]
> If security policies restrict TLS 1.0 and 1.1, installing a new Operations Manager 2016 role fails because the setup media doesn't include the updates to support TLS 1.2. To continue setting up a new role, enable TLS 1.0 on the system, apply [Update Rollup 4](https://support.microsoft.com/kb/4024941), and then redisable TLS 1.0 on the system.

::: moniker-end

## Configure Windows Operating System to only use TLS 1.2 protocol

Use one of the following methods to configure Windows to use only the TLS 1.2 protocol.

### Method 1: Modify the registry manually

> [!IMPORTANT]
> Follow the steps in this section carefully. Serious problems might occur if the registry is modified incorrectly. Before making changes, back up the registries in case problems occur.
>
> For more information, see: [How to back up and restore the registry in Windows](https://support.microsoft.com/en-us/topic/how-to-back-up-and-restore-the-registry-in-windows-855140ad-e318-2a13-2829-d428a2ab0692)

Use the following steps to modify SChannel protocols system-wide. We recommend explicitly enabling the TLS 1.2 protocol.

> [!NOTE]
> Making these registry changes doesn't affect the use of Kerberos or NTLM protocols.

1. Sign in to the server by using an account that has local administrative credentials.
1. Start Registry Editor by selecting and holding **Start**, enter **regedit** in the **Run** textbox, and select **OK**.
1. Locate the following registry subkey:

    `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols`

1. Create a subkey under **Protocols** for:
    - **SSL 2.0**
    - **SSL 3.0**
    - **TLS 1.0**
    - **TLS 1.1**
    - **TLS 1.2**
1. Create a **Client** and **Server** subkey under each protocol version subkey created earlier. For example, the subkey for TLS 1.0 would be
    - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client`
    - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server`
1. To *disable* a protocol, create the following DWORD values under **Server** and **Client**:  
    - **Enabled** [Value = 0]
    - **DisabledByDefault** [Value = 1]
1. To *explicitly* enable the TLS 1.2 protocol (default is enabled), create the following registry keys:
    - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client`
    - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server`
1. Then create the following DWORD values under **Server** and **Client**:
   - **Enabled** [Value = 1]  
   - **DisabledByDefault** [Value = 0]  
1. Close the Registry Editor.

### Method 2: Modify the registry with PowerShell

Run the following Windows PowerShell script as Administrator to configure the Windows Operating System to use the TLS 1.2 Protocol:

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
    Write-Output " Explicitly enable TLS 1.2 (default is enabled)"
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

## Configure .NET Framework to use higher levels of cryptography

.NET Framework typically requires the application to define what TLS protocol to use for communication. In the instance of Operations Manager however, we need to tell .NET Framework system-wide which protocol to use.

After completing the configuration of all prerequisites for Operations Manager, perform the following steps on all Operations Manager servers, and on any Windows agents.  

> [!IMPORTANT]
> Follow the steps in this section carefully. Serious problems might occur if the registry is modified incorrectly. Before making changes, back up the registries in case problems occur.
>
> For more information, see: [How to back up and restore the registry in Windows](https://support.microsoft.com/en-us/topic/how-to-back-up-and-restore-the-registry-in-windows-855140ad-e318-2a13-2829-d428a2ab0692)

::: moniker range="sc-om-2016"

### Prerequisites for Windows Server 2012/2012 R2

Additional changes are required on Windows Server 2012/2012 R2 to use TLS 1.2 over HTTP for UNIX/LINUX monitoring. In order to allow/enable TLS 1.2 as default security protocols in WinHTTP in Windows, the following changes need to be made as per [Update to enable TLS 1.1 and TLS 1.2 as default secure protocols in WinHTTP in Windows](https://support.microsoft.com/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392).

1. Install [KB3140245](https://support.microsoft.com/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392) on the Management Servers/Gateways Servers in the UNIX/LINUX Resource Pool.
2. Back up the registries that are modified as mentioned in the KB article.
3. Download and run the [Easy Fix](https://support.microsoft.com/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392#bkmk_easy) tool on the Management Servers/Gateways in the UNIX/LINUX Resource Pool.
4. Reboot the servers.

::: moniker-end

### Method 1: Modify the registry manually

1. Open the Registry Editor
1. Locate the following registry subkey: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727`
    1. Create the following DWORD value pairs:
        - **SchUseStrongCrypto** [Value = 1]
        - **SystemDefaultTlsVersions** [Value = 1]
1. Locate the following registry subkey: `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v2.0.50727`
    1. Create the following DWORD value pairs:
        - **SchUseStrongCrypto** [Value = 1]
        - **SystemDefaultTlsVersions** [Value = 1]
1. Locate the following registry subkey: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319`  
    1. Create the following DWORD value pairs:
        - **SchUseStrongCrypto** [Value = 1]
        - **SystemDefaultTlsVersions** [Value = 1]
1. Locate the following registry subkey: `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319`
    1. Create the following DWORD value pairs:
        - **SchUseStrongCrypto** [Value = 1]
        - **SystemDefaultTlsVersions** [Value = 1]
1. Restart the system for the settings to take effect.  

### Method 2: Modify the registry with PowerShell

Run the following Windows PowerShell script in Administrator mode to automatically configure .NET Framework to prevent framework-inherited TLS 1.0 dependencies:

```powershell
# Allow .NET Framework to use higher levels of Cryptography
$NetRegistryPath1 = "HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v2.0.50727" 
New-ItemProperty -Path $NetRegistryPath1 -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null 
New-ItemProperty -Path $NetRegistryPath1 -Name "SystemDefaultTlsVersions" -Value "1" -PropertyType DWORD -Force | Out-Null

$NetRegistryPath2 = "HKLM:\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319" 
New-ItemProperty -Path $NetRegistryPath2 -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null
New-ItemProperty -Path $NetRegistryPath2 -Name "SystemDefaultTlsVersions" -Value "1" -PropertyType DWORD -Force | Out-Null

$NetRegistryPath3 = "HKLM:\SOFTWARE\Microsoft\.NETFramework\v2.0.50727" 
New-ItemProperty -Path $NetRegistryPath3 -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null 
New-ItemProperty -Path $NetRegistryPath3 -Name "SystemDefaultTlsVersions" -Value "1" -PropertyType DWORD -Force | Out-Null

$NetRegistryPath4 = "HKLM:\SOFTWARE\Microsoft\.NETFramework\v4.0.30319" 
New-ItemProperty -Path $NetRegistryPath4 -Name "SchUseStrongCrypto" -Value "1" -PropertyType DWORD -Force | Out-Null
New-ItemProperty -Path $NetRegistryPath4 -Name "SystemDefaultTlsVersions" -Value "1" -PropertyType DWORD -Force | Out-Null
```

## Additional settings

::: moniker range="sc-om-2016"

After applying Update Rollup 4, ensure to import the management packs that are included in this rollup located in the following directory: `%ProgramFiles%\Microsoft System Center 2016\Operations Manager\Server\Management Packs for Update Rollups`.

::: moniker-end

If monitoring a supported version of Linux server with Operations Manager, follow the instructions on the appropriate website for your distro to configure TLS 1.2.  

::: moniker range="sc-om-2016"

### Audit Collection Services

For Audit Collection Services (ACS), additional changes must be made in the registry on ACS Collector server. ACS uses the ODBC Data Source Name (DSN) to make connections to the database. Ensure the DSN settings are updated to make them functional for TLS 1.2.

1. Sign in to the server by using an account that has local administrative credentials.  
1. Start Registry Editor by selecting and holding **Start**, enter **regedit** in the **Run** textbox, and select **OK**.  
1. Locate the following ODBC subkey for OpsMgrAC: `HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC`.
   1. **Note that the default DSN name is `OpsMgrAC`**.
1. Under **ODBC Data Sources** subkey, select the DSN name **OpsMgrAC**. This contains the name of the ODBC driver to be used for the database connection. If ODBC 11.0 is installed, change this name to **ODBC Driver 11 for SQL Server**, or if ODBC 13.0 is installed, change this name to **ODBC Driver 13 for SQL Server**.
1. Under the **OpsMgrAC** subkey, update the **Driver** for the ODBC version that is installed.
   - If ODBC 11.0 is installed, change the Driver entry to `%WINDIR%\system32\msodbcsql11.dll`.
   - If ODBC 13.0 is installed, change the Driver entry to `%WINDIR%\system32\msodbcsql13.dll`.
   - If ODBC 17.0 is installed, change the Driver entry to `%WINDIR%\system32\msodbcsql17.dll`.
   - If ODBC 18.0 is installed, change the Driver entry to `%WINDIR%\system32\msodbcsql18.dll`.

#### Registry File

Alternatively, create and save the following **.reg** file in Notepad or another text editor. To run the saved **.reg** file, double-click the file.

- For ODBC 11.0, 13.0, 17.x, or 18.x. Create the following file ODBC.reg and (replace with the ODBC version being used):

    ```cmd
    Windows Registry Editor Version 5.00
    
    [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources]
    "OpsMgrAC"="ODBC Driver 18 for SQL Server"
    
    [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC]
    "Driver"="%WINDIR%\system32\msodbcsql18.dll"
    ```

#### PowerShell

Alternatively, run the following PowerShell commands to automate the change.

- For ODBC 11.0, run the following PowerShell commands:

  ```powershell
  New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC" -Name "Driver" -Value "%WINDIR%\system32\msodbcsql11.dll" -PropertyType STRING -Force | Out-Null
  New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources" -Name "OpsMgrAC" -Value "ODBC Driver 11 for SQL Server" -PropertyType STRING -Force | Out-Null
  ```
  
- For ODBC 13.0, run the following PowerShell commands:

  ```powershell
  New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC" -Name "Driver" -Value "%WINDIR%\system32\msodbcsql13.dll" -PropertyType STRING -Force | Out-Null
  New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources" -Name "OpsMgrAC" -Value "ODBC Driver 13 for SQL Server" -PropertyType STRING -Force | Out-Null
  ```

::: moniker-end

::: moniker range=">sc-om-2016"

### Audit Collection Services

For Audit Collection Services (ACS), additional changes must be made in the registry on ACS Collector server. ACS uses the ODBC Data Source Name (DSN) to make connections to the database. Ensure the DSN settings are updated to make them functional for TLS 1.2.

1. Sign in to the server by using an account that has local administrative credentials.  
1. Start Registry Editor by selecting and holding **Start**, enter **regedit** in the **Run** textbox, and select **OK**.  
1. Locate the following ODBC subkey for OpsMgrAC: `HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC`.  

    > [!NOTE]
    > The default name of DSN is OpsMgrAC.

1. Under **ODBC Data Sources** subkey, select the DSN name **OpsMgrAC**. This contains the name of the ODBC driver to be used for the database connection. If ODBC 17 is installed, change this name to **ODBC Driver 17 for SQL Server**.
1. Under the **OpsMgrAC** subkey, update the **Driver**  for the ODBC version that is installed.
   - For example, if ODBC 17 is installed, change the Driver entry to `%WINDIR%\system32\msodbcsql17.dll`.
   - Check the name of the DLL for the current version of the ODBC driver installed if different.

#### Registry File

Alternatively, create and save the following **.reg** file in Notepad or another text editor. To run the saved **.reg** file, double-click the file.

- For ODBC 17, create the following ODBC 17.reg file:

  ```cmd
  Windows Registry Editor Version 5.00
  
  [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources]
  "OpsMgrAC"="ODBC Driver 17 for SQL Server"
  
  [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC]
  "Driver"="%WINDIR%\system32\msodbcsql17.dll"
  ```

#### PowerShell

Alternatively, run the following PowerShell commands to automate the change.

- Ensure to replace the dll file path to an appropriate version if using an ODBC driver version other than 17.

  ```powershell
  New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC" -Name "Driver" -Value "%WINDIR%\system32\msodbcsql7.dll" -PropertyType STRING -Force | Out-Null
  New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources" -Name "OpsMgrAC" -Value "ODBC Driver 17 for SQL Server" -PropertyType STRING -Force | Out-Null
  ```

::: moniker-end

## Next steps

- For more information about TLS 1.0 from our Security Engineering team, see [Solving the TLS 1.0 Problem](/security/engineering/solving-tls1-problem).
- For a complete listing of ports used, the direction of the communication, and if the ports can be configured, see [Configuring a Firewall for Operations Manager](plan-security-config-firewall.md).
- For an overall review of how data between components in a management group is protected, see [Authentication and Data Encryption in Operations Manager](plan-security-authentication-data-encryption.md).
