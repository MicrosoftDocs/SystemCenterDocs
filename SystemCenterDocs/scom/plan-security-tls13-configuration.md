---
title: Enforce TLS 1.3 for Operations Manager 2025 UR1
description: This article describes how to configure System Center Operations Manager to utilize Transport Layer Security (TLS) 1.3.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/20/2025
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
monikerRange: sc-om-2025
---

# Enforce TLS 1.3 for Operations Manager 2025 UR1

This article describes how to allow System Center Operations Manager to utilize Transport Layer Security (TLS) 1.3.

>[!NOTE]
>TLS 1.3 is supported from System Center Operations Manager 2025 UR1.

Operations Manager adheres to the protocol configuration defined at the Operating system level. When all protocols are enabled, Operations Manager negotiates the connection using the protocols in the order of preference determined by Windows Schannel, starting from the highest to the lowest supported version.

1. TLS 1.3 (Windows Server 2022/Windows 11 and later) 
1. TLS 1.2
1. TLS 1.1
1. TLS 1.0

The [Schannel SSP](/windows-server/security/tls/tls-ssl-schannel-ssp-overview) then selects the most preferred authentication protocol that the client and server can support.

Perform the following steps to implement TLS protocol version 1.3 in Operations Manager:

1. Install the latest Microsoft OLE DB Driver (x64) on all management servers and the web console server.
1.  the latest Microsoft ODBC Driver (x64) on all management servers and the web console server.
1. Configure Windows to use TLS 1.3.  
1. Configure .NET Framework to utilize higher levels of cryptography by default.

1. Configure Audit Collection Services if installed.

> [!NOTE]
> If utilizing SQL Server connection encryption, install these driver versions instead:
>
> - Microsoft OLE DB Driver 19: [https://aka.ms/downloadmsoledbsql](https://aka.ms/downloadmsoledbsql)
> - Microsoft ODBC Driver 18: [https://aka.ms/downloadmsodbcsql](https://aka.ms/downloadmsodbcsql)
>
> More information about configuring SQL connection encryption can be found here: [Configure SQL Server Database Engine for encrypting connections](/sql/database-engine/configure-windows/configure-sql-server-encryption).

TLS 1.3 requires the use of strong hash algorithms. Self-signed certificates must be generated using a SHA-2 or later hash algorithm. The certificate must use a SHA-2 family hash, such as SHA256, SHA384, or SHA512. 

If CA-signed certificates are used, ensure that they are issued with a SHA-2 or later hash algorithm. 

## Configure Windows Operating System to use TLS 1.3 protocol

Use one of the following methods to configure Windows using the TLS 1.3 protocol.

### Method 1: Modify the registry manually

> [!IMPORTANT]
> Follow the steps in this section carefully. Serious problems might occur if the registry is modified incorrectly. Before making changes, back up the registries in case problems occur.
>
> For more information, see: [How to back up and restore the registry in Windows](https://support.microsoft.com/topic/how-to-back-up-and-restore-the-registry-in-windows-855140ad-e318-2a13-2829-d428a2ab0692).

Use the following steps to modify SChannel protocols system-wide. We recommend explicitly enabling the TLS 1.3 protocol.

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
    - **TLS 1.3**
1. Create a **Client** and **Server** subkey under each protocol version subkey created earlier. For example, the subkey for TLS 1.0 would be
    - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client`
    - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server`
1. To *disable* a protocol, create the following DWORD values under **Server** and **Client**:  
    - **Enabled** [Value = 0]
    - **DisabledByDefault** [Value = 1]
1. To *explicitly* enable the TLS 1.3 protocol (default is enabled), create the following registry keys:
    - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.3\Client`
    - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.3\Server`
1. Then create the following DWORD values under **Server** and **Client**:
   - **Enabled** [Value = 1]  
   - **DisabledByDefault** [Value = 0]  
1. Close the Registry Editor.

### Method 2: Modify the registry with PowerShell

Run the following Windows PowerShell script as Administrator to configure the Windows Operating System to use the TLS 1.3 Protocol:

```powershell
# Define the base registry path for SCHANNEL protocols 

$SchannelProtocolsPath = "HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols" 

 

# Define the TLS 1.3 client and server paths 

$Tls13ClientPath = "$SchannelProtocolsPath\TLS 1.3\Client" 

$Tls13ServerPath = "$SchannelProtocolsPath\TLS 1.3\Server" 

 

# Create or update TLS 1.3 Client keys and values 

If (-not (Test-Path $Tls13ClientPath)) { 

    New-Item -Path $Tls13ClientPath -Force | Out-Null 

} 

Set-ItemProperty -Path $Tls13ClientPath -Name "DisabledByDefault" -Value 0 -Type DWord -Force | Out-Null 

Set-ItemProperty -Path $Tls13ClientPath -Name "Enabled" -Value 1 -Type DWord -Force | Out-Null 

 

# Create or update TLS 1.3 Server keys and values 

If (-not (Test-Path $Tls13ServerPath)) { 

    New-Item -Path $Tls13ServerPath -Force | Out-Null 

} 

Set-ItemProperty -Path $Tls13ServerPath -Name "DisabledByDefault" -Value 0 -Type DWord -Force | Out-Null 

Set-ItemProperty -Path $Tls13ServerPath -Name "Enabled" -Value 1 -Type DWord -Force | Out-Null 

 

Write-Host "TLS 1.3 registry settings have been applied." 

Write-Host "A system restart may be required for changes to take full effect."
```

## Configure .NET Framework to use higher levels of cryptography

.NET Framework typically requires the application to define what TLS protocol to use for communication. In the instance of Operations Manager however, we need to tell .NET Framework system-wide which protocol to use.

After completing the configuration of all prerequisites for Operations Manager, perform the following steps on all Operations Manager servers, and on any Windows agents.  

> [!IMPORTANT]
> Follow the steps in this section carefully. Serious problems might occur if the registry is modified incorrectly. Before making changes, back up the registries in case problems occur.
>
> For more information, see: [How to back up and restore the registry in Windows](https://support.microsoft.com/topic/how-to-back-up-and-restore-the-registry-in-windows-855140ad-e318-2a13-2829-d428a2ab0692).

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

If monitoring a supported version of Linux server with Operations Manager, follow the instructions on the appropriate website for your distro to configure TLS 1.3.  

### Audit Collection Services

For Audit Collection Services (ACS), additional changes must be made in the registry on ACS Collector server. ACS uses the ODBC Data Source Name (DSN) to make connections to the database. Ensure the DSN settings are updated to make them functional for TLS 1.3.

1. Sign in to the server by using an account that has local administrative credentials.  
1. Start Registry Editor by selecting and holding **Start**, enter **regedit** in the **Run** textbox, and select **OK**.  
1. Locate the following ODBC subkey for OpsMgrAC: `HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC`.  

    > [!NOTE]
    > The default name of DSN is **OpsMgrAC**.

1. Under **ODBC Data Sources** subkey, select the DSN name **OpsMgrAC**. This contains the name of the ODBC driver to be used for the database connection. If ODBC 17.0 is installed, change this name to **ODBC Driver 17 for SQL Server**, or if ODBC 18.0 is installed, change this name to **ODBC Driver 18 for SQL Server**.
1. Under the **OpsMgrAC** subkey, update the **Driver**  for the ODBC version that is installed.
   - For example, if ODBC 18 is installed, change the Driver entry to `%WINDIR%\system32\msodbcsql18.dll`.
   - Check the name of the DLL for the current version of the ODBC driver installed if different.

#### Registry File

Alternatively, create and save the following **.reg** file in Notepad or another text editor. To run the saved **.reg** file, double-click the file.

- For ODBC 17.x or 18.x, create the following ODBC.reg (replace ODBC with the version used) file:

  ```cmd
  Windows Registry Editor Version 5.00 

  [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources] 

  "OpsMgrAC"="ODBC Driver 18 for SQL Server" 

  [HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC] 

  "Driver"="%WINDIR%\system32\msodbcsql18.dll"
  ```

#### PowerShell

Alternatively, run the following PowerShell commands to automate the change.

- Ensure to replace the dll file path to an appropriate version if using an ODBC driver version other than 18.

  ```powershell
  New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\OpsMgrAC" -Name "Driver" -Value "%WINDIR%\system32\msodbcsql8.dll" -PropertyType STRING -Force | Out-Null 

  New-ItemProperty -Path "HKLM:\SOFTWARE\ODBC\ODBC.INI\ODBC Data Sources" -Name "OpsMgrAC" -Value "ODBC Driver 18 for SQL Server" -PropertyType STRING -Force | Out-Null 
  ```

## Next steps

- For more information about TLS 1.0 from our Security Engineering team, see [Solving the TLS 1.0 Problem](/security/engineering/solving-tls1-problem).
- For a complete listing of ports used, the direction of the communication, and if the ports can be configured, see [Configuring a Firewall for Operations Manager](plan-security-config-firewall.md).
- For an overall review of how data between components in a management group is protected, see [Authentication and Data Encryption in Operations Manager](plan-security-authentication-data-encryption.md).
